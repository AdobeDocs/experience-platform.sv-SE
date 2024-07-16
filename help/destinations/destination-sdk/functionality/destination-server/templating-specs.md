---
description: Lär dig hur du formaterar HTTP-begäranden som skickas till slutpunkten. Använd slutpunkten /authoring/destination-servers för att konfigurera målserverns mallspecifikationer i Adobe Experience Platform Destination SDK.
title: Mallspecifikationer för mål som skapats med Destination SDK
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Mallspecifikationer för mål som skapats med Destination SDK

Använd mallens specifika del av målserverkonfigurationen för att konfigurera hur HTTP-begäranden som skickas till målet ska formateras.

I en mallspecifikation kan du definiera hur profilattributfält ska omformas mellan XDM-schemat och det format som stöds på plattformen.

Mallspecifikationer är en del av målserverkonfigurationen för mål för realtidsströmning.

Mer information om var den här komponenten passar in i en integrering som skapats med Destination SDK finns i diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller i guiden om hur du [använder Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Du kan konfigurera mallspecifikationerna för ditt mål via slutpunkten `/authoring/destination-servers`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Uppdatera en målserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Nej |

## Konfigurera en mallspecifikation {#configure-template-spec}

Adobe använder ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) för att omvandla fälten från XDM-schemat till ett format som stöds av ditt mål.

![Mallkonfigurationen är markerad](../../assets/functionality/destination-server/template-configuration.png)

Mer information om omvandlingen finns på länkarna nedan:

* [Meddelandeformat](message-format.md)
* [Använda ett mallspråk för omvandlingar av identitet, attribut och målgruppsmedlemskap](message-format.md#using-templating)

>[!TIP]
>
>Adobe har ett [utvecklarverktyg](../../testing-api/streaming-destinations/create-template.md) som hjälper dig att skapa och testa en meddelandeomvandlingsmall.

Nedan finns ett exempel på en mall för en HTTP-begäran, tillsammans med beskrivningar av varje enskild parameter.

```json
{
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
| `httpMethod` | Sträng | *Krävs.* Den metod som Adobe ska använda i anrop till servern. Metoder som stöds: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `value` | Sträng | *Krävs.* Den här strängen är den version av mallen som innehåller tecken som formaterar HTTP-begäranden som skickas av Platform till det format som förväntas av målet. <br> Mer information om hur du skriver mallen finns i avsnittet [med mallar](message-format.md#using-templating). <br> Mer information om teckenflytning finns i [RFC JSON-standarden, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). <br> Ett exempel på en enkel omformning finns i omformningen [profile attributes](message-format.md#attributes) . |
| `contentType` | Sträng | *Krävs.* Innehållstypen som servern accepterar. Beroende på vilken typ av utdata som din omformningsmall skapar kan detta vara någon av de [HTTP-programinnehållstyper som stöds](https://www.iana.org/assignments/media-types/media-types.xhtml#application). I de flesta fall bör värdet anges till `application/json`. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vad en mallspecifikation är och hur du kan konfigurera den.

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](server-specs.md)
* [Meddelandeformat](message-format.md)
* [Filformateringskonfiguration](file-formatting.md)
