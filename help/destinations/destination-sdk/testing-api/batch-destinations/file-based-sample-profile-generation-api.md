---
description: På den här sidan beskrivs hur du använder API-slutpunkten /sample-profiles från Destinationen SDK för att generera exempelprofiler baserat på ett källschema. Du kan använda de här exempelprofilerna för att testa din filbaserade målkonfiguration.
title: Generera exempelprofiler baserat på ett källschema
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Generera exempelprofiler baserat på ett källschema

Det första steget i testningen av ditt filbaserade mål är att använda slutpunkten `/sample-profiles` för att generera en exempelprofil baserat på ditt befintliga källschema.

Exempelprofiler kan hjälpa dig att förstå JSON-strukturen för en profil. Dessutom får du ett standardvärde som du kan anpassa med dina egna profildata för ytterligare destinationstestning.

## Komma igång {#getting-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Förhandskrav {#prerequisites}

Innan du kan använda slutpunkten `/sample-profiles` måste du kontrollera att följande villkor uppfylls:

* Du har ett befintligt filbaserat mål som skapats via Destinationen SDK och du kan se det i din [målkatalog](../../../ui/destinations-workspace.md).
* Du har skapat minst ett aktiveringsflöde för destinationen i användargränssnittet i Experience Platform. Slutpunkten `/sample-profiles` skapar profilerna baserat på det källschema som du definierade i ditt aktiveringsflöde. Se självstudiekursen [aktivering](../../../ui/activate-batch-profile-destinations.md) om du vill veta mer om hur du skapar ett aktiveringsflöde.
* För att kunna utföra API-begäran behöver du det målinstans-ID som motsvarar den målinstans som du ska testa. Hämta det målinstans-ID som du bör använda i API-anropet från webbadressen när du bläddrar i en anslutning till målet i plattformsgränssnittet.

  ![Gränssnittsbild som visar hur du hämtar målinstans-ID från URL:en.](../../assets/testing-api/get-destination-instance-id.png)

## Generera exempelprofiler för måltestning {#generate-sample-profiles}

Du kan generera exempelprofiler baserat på ditt källschema genom att göra en GET-förfrågan till `/sample-profiles`-slutpunkten med målförekomstens ID för det mål som du vill testa.

**API-format**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Frågeparametrar | Beskrivning |
| -------- | ----------- |
| `destinationInstanceId` | ID:t för målinstansen som du genererar exempelprofiler för. I avsnittet [Krav](#prerequisites) finns mer information om hur du får detta ID. |
| `count` | *Valfritt*. Antalet exempelprofiler som du vill generera. Parametern kan ha värden mellan `1 - 1000`. Om den här egenskapen inte definieras genererar API:t en enda exempelprofil. |

**Begäran**

Följande begäran genererar en exempelprofil baserat på det källschema som definierats i målinstansen med motsvarande `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med målgruppsmedlemskap, identiteter och profilattribut som motsvarar XDM-källschemat.

>[!NOTE]
>
> Svaret returnerar endast målgruppsmedlemskap, identiteter och profilattribut som används i målinstansen. Även om källschemat innehåller andra fält ignoreras dessa.

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

![Bild som visar mappningen från användargränssnittet till fälten från API-svaret.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentMembership` | Ett kartobjekt som beskriver personens målgruppsmedlemskap. Mer information om `segmentMembership` finns i [Information om målgruppsmedlemskap](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `status` | Ett strängfält som anger om målgruppsmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`realized`: Profilen ingår i segmentet.</li><li>`exited`: Profilen avslutar målgruppen som en del av den aktuella begäran.</li></ul> |
| `identityMap` | Ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Mer information om `identityMap` finns i [Bas för schemakomposition](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du genererar exempelprofiler baserat på källschemat som du konfigurerade i [aktiveringsflödet](../../../ui/activate-batch-profile-destinations.md) för ditt mål.

Du kan nu anpassa de här profilerna eller använda dem när de returneras av API:t för att [testa din filbaserade målkonfiguration](file-based-destination-testing-api.md).
