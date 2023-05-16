---
description: Lär dig hur du formaterar HTTP-begäranden som skickas till slutpunkten. Använd slutpunkten /authoring/destination-servers för att konfigurera målserverns mallspecifikationer i Adobe Experience Platform Destination SDK.
title: Mallspecifikationer för mål som skapats med Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---


# Mallspecifikationer för mål som skapats med Destination SDK

Använd mallens specifika del av målserverkonfigurationen för att konfigurera hur HTTP-begäranden som skickas till målet ska formateras.

I en mallspecifikation kan du definiera hur profilattributfält ska omformas mellan XDM-schemat och det format som stöds på plattformen.

Mallspecifikationer är en del av målserverkonfigurationen för mål för realtidsströmning.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Du kan konfigurera mallspecifikationerna för ditt mål via `/authoring/destination-servers` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Uppdatera en målserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Nej |

## Konfigurera en mallspecifikation {#configure-template-spec}

Adobe använder ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) för att omvandla fälten från XDM-schemat till ett format som stöds av ditt mål.

![Mallkonfigurationen är markerad](../../assets/functionality/destination-server/template-configuration.png)

Mer information om omvandlingen finns på länkarna nedan:

* [Meddelandeformat](message-format.md)
* [Använda ett mallspråk för identitet, attribut och segmentmedlemskapsomvandlingar ](message-format.md#using-templating)

>[!TIP]
>
>Adobe erbjuder [utvecklarverktyg](../../testing-api/streaming-destinations/create-template.md) som hjälper dig att skapa och testa en meddelandeomformningsmall.

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
| `httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. Metoder som stöds: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `value` | Sträng | *Obligatoriskt.* Strängen är den teckenescape-konverterade versionen av mallen som formaterar HTTP-begäranden som skickas av Platform till det format som förväntas av målet. <br> Mer information om hur du skriver mallen finns i avsnittet om [använda mall](message-format.md#using-templating). <br> Mer information om teckenigenkänning finns i [RFC JSON-standard, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). <br> Ett exempel på en enkel omformning finns i [profilattribut](message-format.md#attributes) omformning. |
| `contentType` | Sträng | *Obligatoriskt.* Den innehållstyp som servern accepterar. Beroende på vilken typ av utdata som din omformningsmall skapar kan detta vara någon av de utdata som stöds [Innehållstyper för HTTP-program](https://www.iana.org/assignments/media-types/media-types.xhtml#application). I de flesta fall bör det här värdet anges till `application/json`. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vad en mallspecifikation är och hur du kan konfigurera den.

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](server-specs.md)
* [Meddelandeformat](message-format.md)
* [Filformateringskonfiguration](file-formatting.md)