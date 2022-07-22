---
description: Server- och mallspecifikationerna kan konfigureras i Adobe Experience Platform Destination SDK via den gemensamma slutpunkten "/authoring/destination-servers".
title: Konfigurationsalternativ för server- och mallspecifikationer i Destinationen SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Konfigurationsalternativ för direktuppspelning av server- och mallspecifikationer

## Översikt {#overview}

Server- och mallspecifikationerna kan konfigureras i Adobe Experience Platform Destination SDK via den gemensamma slutpunkten `/authoring/destination-servers`. Läs [Slutpunktsåtgärder för mål-API](./destination-server-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Serverspecifikationer {#server-specs}

![Serverkonfigurationen är markerad](./assets/server-configuration.png)

Kunderna kan aktivera data från Adobe Experience Platform till er destination via HTTP-exporter. Serverkonfigurationen innehåller information om servern som tar emot meddelandena (servern på din sida).

Den här processen levererar användardata som en serie HTTP-meddelanden till målplattformen. Parametrarna nedan utgör mallen för specifikationer för HTTP-servern.

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | *Obligatoriskt.* Representerar ett eget namn på servern som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Obligatoriskt.* Ange till `URL_BASED` för direktuppspelningsmål. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om du använder ett makro i stället för ett fast värde i `value` fält. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Använd `NONE` om ingen omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |

{style=&quot;table-layout:auto&quot;}

## Mallspecifikationer {#template-specs}

![Mallkonfigurationen är markerad](./assets/template-configuration.png)

I mallspecifikationen kan du konfigurera hur det exporterade meddelandet ska formateras till ditt mål. Adobe använder ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) för att omvandla fälten från XDM-schemat till ett format som stöds av ditt mål. Mer information om omvandlingen finns på länkarna nedan:

* [Meddelandeformat](./message-format.md)
* [Använda ett mallspråk för identitet, attribut och segmentmedlemskapsomvandlingar ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe erbjuder [utvecklarverktyg](./create-template.md) som hjälper dig att skapa och testa en meddelandeomformningsmall.

## Exempelkonfiguration för direktuppspelningsmål  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. Alternativen är `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `value` | Sträng | *Obligatoriskt.* Strängen är den teckenescape-konverterade version som transformerar plattformskundernas data till det format som tjänsten förväntar sig. <br> Mer information om hur du skriver mallen finns i [Använda mallavsnitt](./message-format.md#using-templating). <br> Mer information om teckenigenkänning finns i [RFC JSON-standard, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). <br> Ett exempel på en enkel omformning finns i [Profilattribut](./message-format.md#attributes) omformning. |
| `contentType` | Sträng | *Obligatoriskt.* Den innehållstyp som servern accepterar. Detta värde är mest sannolikt `application/json`. |

{style=&quot;table-layout:auto&quot;}