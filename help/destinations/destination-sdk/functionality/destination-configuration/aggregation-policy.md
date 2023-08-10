---
description: Lär dig hur du ställer in en aggregeringsprincip för att bestämma hur HTTP-begäranden till ditt mål ska grupperas och grupperas.
title: Samlingsprincip
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---


# Samlingsprincip

För att vara så effektiv som möjligt när du exporterar data till API-slutpunkten kan du använda olika inställningar för att samla exporterade profiler i större eller mindre grupper, gruppera dem efter identitet och andra användningsfall. På så sätt kan du skräddarsy dataexport till eventuella efterföljande begränsningar för API-slutpunkten (hastighetsbegränsning, antal identiteter per API-anrop osv.).

Använd konfigurerbar aggregering för att fördjupa dig i inställningarna som tillhandahålls av Destinationen SDK eller använd bästa möjliga ansträngningsaggregering för att ange för Destinationen SDK att batchköra API-anropen så mycket som möjligt.

När du skapar ett mål för direktuppspelning i realtid med Destination SDK kan du konfigurera hur de exporterade profilerna ska kombineras i den resulterande exporten. Det här beteendet avgörs av inställningarna för aggregeringsprincipen.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-destination-configuration).

Du kan konfigurera inställningar för sammanställningsprofiler via `/authoring/destinations` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla aggregeringsprincipinställningar som stöds och som du kan använda för ditt mål.

När du har läst igenom det här dokumentet, se dokumentationen för [använda mall](../../functionality/destination-server/message-format.md#using-templating) och [exempel på aggregeringsnyckel](../../functionality/destination-server/message-format.md#template-aggregation-key) om du vill veta hur du inkluderar aggregeringsprincipen i din meddelandetransformeringsmall baserat på din valda aggregeringsprincip.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Nej |

## Bästa ansträngningsaggregering {#best-effort-aggregation}

Bästa ansträngningsaggregering fungerar bäst för mål som föredrar färre profiler per begäran och som hellre vill ta in fler förfrågningar med mindre data än färre förfrågningar med mer data.

I exempelkonfigurationen nedan visas en aggregeringskonfiguration för bästa insats. Ett exempel på konfigurerbar aggregering finns i [konfigurerbar aggregering](#configurable-aggregation) -avsnitt. De parametrar som är tillämpliga på bästa möjliga ansträngningsaggregering beskrivs i tabellen nedan.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `aggregationType` | Sträng | Anger vilken typ av aggregeringsprincip som ditt mål ska använda. Aggregeringstyper som stöds: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Heltal | Experience Platform kan samla flera exporterade profiler i ett enda HTTP-anrop. <br><br>Det här värdet anger det maximala antalet profiler som slutpunkten ska ta emot i ett enda HTTP-anrop. Observera att detta är en bästa ansträngningsaggregering. Om du till exempel anger värdet 100 kan Platform skicka valfritt antal profiler som är mindre än 100 på ett samtal. <br><br> Om servern inte accepterar flera användare per begäran anger du det här värdet till `1`. |
| `bestEffortAggregation.splitUserById` | Boolean | Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop, för ett givet identitetsnamnutrymme. |

{style="table-layout:auto"}

>[!TIP]
>
>Använd aggregering av bästa möjliga ansträngning om API-slutpunkten accepterar färre än 100 profiler per API-anrop.

## Konfigurerbar aggregering {#configurable-aggregation}

Konfigurerbar aggregering fungerar bäst om du hellre vill ta med stora grupper, med tusentals profiler på samma samtal. Med det här alternativet kan du också sammanfoga de exporterade profilerna baserat på komplexa sammanställningsregler.

I exempelkonfigurationen nedan visas en konfigurerbar aggregeringskonfiguration. Ett exempel på bästa möjliga ansträngningsaggregering finns i [bästa ansträngningsaggregering](#best-effort-aggregation) -avsnitt. De parametrar som är tillämpliga på konfigurerbar aggregering beskrivs i tabellen nedan.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `aggregationType` | Sträng | Anger vilken typ av aggregeringsprincip som ditt mål ska använda. Aggregeringstyper som stöds: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Boolean | Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop, för ett givet identitetsnamnutrymme. |
| `configurableAggregation.maxBatchAgeInSecs` | Heltal | Används i konjugering med `maxNumEventsInBatch`anger den här parametern hur länge Experience Platform ska vänta tills ett API-anrop skickas till slutpunkten. <ul><li>Minsta värde (sekunder): 1 800</li><li>Högsta värde (sekunder): 3 600</li></ul> Om du till exempel använder maxvärdet för båda parametrarna väntar Experience Platform antingen 3600 sekunder ELLER tills det finns 1000 kvalificerade profiler innan API-anropet görs, beroende på vilket som inträffar först. |
| `configurableAggregation.maxNumEventsInBatch` | Heltal | Används tillsammans med `maxBatchAgeInSecs`anger den här parametern hur många kvalificerade profiler som ska aggregeras i ett API-anrop. <ul><li>Minsta värde: 1000</li><li>Högsta värde: 10000</li></ul> Om du till exempel använder maxvärdet för båda parametrarna väntar Experience Platform antingen 3600 sekunder ELLER tills det finns 1000 kvalificerade profiler innan API-anropet görs, beroende på vilket som inträffar först. |
| `configurableAggregation.aggregationKey` | – | Gör att du kan sammanställa de exporterade profilerna som är mappade till målet baserat på parametrarna som beskrivs nedan. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Ställ in den här parametern på `true` om du vill gruppera profiler som exporterats till ditt mål efter målgrupps-ID. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Ange både den här parametern och `includeSegmentId` till `true`om du vill gruppera profiler som exporterats till ditt mål efter målgrupps-ID och målgruppsstatus. |
| `configurableAggregation.aggregationKey.includeIdentity` | Boolean | Ställ in den här parametern på `true` om du vill gruppera profiler som exporterats till ditt mål efter identitetsnamnutrymme. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Ange den här parametern till `true` om du vill att de exporterade profilerna ska samlas i grupper baserat på en enda identitet (GAID, IDFA, telefonnummer, e-post osv.). |
| `configurableAggregation.aggregationKey.groups` | Array | Skapa listor med identitetsgrupper om du vill gruppera profiler som exporterats till ditt mål med grupper av identitetsnamnutrymmen. Du kan t.ex. kombinera profiler som innehåller IDFA- och GAID-mobilidentifierare i ett anrop till ditt mål och e-postmeddelanden i ett annat genom att använda konfigurationen som visas i exemplet ovan. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur du kan konfigurera aggregeringsregler för ditt mål.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Konfiguration av kundautentisering](customer-authentication.md)
* [OAuth2-autentisering](oauth2-authentication.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)