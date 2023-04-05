---
description: På den här sidan beskrivs hur du använder API-slutpunkten /sample-profiles från Destinationen SDK för att generera exempelprofiler baserat på ett källschema. Du kan använda de här exempelprofilerna för att testa din filbaserade målkonfiguration.
title: Generera exempelprofiler baserat på ett källschema
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Generera exempelprofiler baserat på ett källschema

## Översikt {#overview}

Det första steget för att testa det filbaserade målet är att använda `/sample-profiles` slutpunkt för att generera en exempelprofil baserat på ditt befintliga källschema.

Exempelprofiler kan hjälpa dig att förstå JSON-strukturen för en profil. Dessutom får du ett standardvärde som du kan anpassa med dina egna profildata för ytterligare destinationstestning.

## Komma igång {#getting-started}

Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Förutsättningar {#prerequisites}

Innan du kan använda `/sample-profiles` måste du se till att följande villkor uppfylls:

* Du har ett befintligt filbaserat mål som skapas via Destinationen SDK och du kan se det i [målkatalog](../ui/destinations-workspace.md).
* Du har skapat minst ett aktiveringsflöde för destinationen i användargränssnittet i Experience Platform. The `/sample-profiles` slutpunkten skapar profilerna baserat på det källschema som du definierade i aktiveringsflödet. Se [självstudiekurs om aktivering](../ui/activate-batch-profile-destinations.md) om du vill veta hur du skapar ett aktiveringsflöde.
* För att kunna utföra API-begäran behöver du det målinstans-ID som motsvarar den målinstans som du ska testa. Hämta det målinstans-ID som du bör använda i API-anropet från webbadressen när du bläddrar i en anslutning till målet i plattformsgränssnittet.

   ![Användargränssnittsbild som visar hur du hämtar målinstans-ID från URL:en.](assets/get-destination-instance-id.png)

## Generera exempelprofiler för måltestning {#generate-sample-profiles}

Du kan generera exempelprofiler baserat på ditt källschema genom att göra en GET-förfrågan till `/sample-profiles` slutpunkten med målinstans-ID:t för målet som du vill testa.

**API-format**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Frågeparametrar | Beskrivning |
| -------- | ----------- |
| `destinationInstanceId` | ID:t för målinstansen som du genererar exempelprofiler för. Se [krav](#prerequisites) om du vill ha mer information om hur du får detta ID. |
| `count` | *Valfritt*. Antalet exempelprofiler som du vill generera. Parametern kan ha värden mellan `1 - 1000`. Om den här egenskapen inte definieras genererar API:t en enda exempelprofil. |

**Begäran**

Följande begäran genererar en exempelprofil baserad på det källschema som definierats i målinstansen med motsvarande `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med segmentmedlemskap, identiteter och profilattribut som motsvarar XDM-källschemat.

>[!NOTE]
>
> Svaret returnerar endast segmentmedlemskap, identiteter och profilattribut som används i målinstansen. Även om källschemat innehåller andra fält ignoreras dessa.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![Bild som visar mappningen från användargränssnittet till fälten från API-svaret.](assets/sample-api-response-mapping.png)

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentMembership` | Ett kartobjekt som beskriver personens segmentmedlemskap. Mer information om `segmentMembership`, läsa [Information om segmentmedlemskap](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `status` | Ett strängfält som anger om segmentmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`realized`: Profilen är en del av segmentet.</li><li>`exited`: Profilen avslutar segmentet som en del av den aktuella begäran.</li></ul> |
| `identityMap` | Ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Mer information om `identityMap`, se [grund för schemakomposition](../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du genererar exempelprofiler baserat på källschemat som du konfigurerade i målet [aktiveringsflöde](../ui/activate-batch-profile-destinations.md).

Du kan nu anpassa de här profilerna eller använda dem som de returneras av API:t för att [testa din filbaserade destinationskonfiguration](file-based-destination-testing-api.md).
