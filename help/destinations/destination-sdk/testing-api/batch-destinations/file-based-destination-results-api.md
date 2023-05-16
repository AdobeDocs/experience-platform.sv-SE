---
description: På den här sidan beskrivs hur du använder API-slutpunkten /testing/destinationInstance för att visa fullständig information om testresultaten. Denna API-slutpunkt returnerar samma resultat som du skulle få när du använde API:t för Flow Service för att övervaka dataflöden.
title: Visa detaljerade aktiveringsresultat
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# Visa detaljerade aktiveringsresultat {#view-test-results}

## Översikt {#overview}

På den här sidan beskrivs hur du använder `/testing/destinationInstance` API-slutpunkt för att visa fullständig information om filbaserade testresultat för mål.

Om du redan har [testade destinationen](file-based-destination-testing-api.md) och har fått ett giltigt API-svar fungerar målet korrekt.

Om du vill ha mer detaljerad information om aktiveringsflödet kan du använda `results` -egenskapen från [destinationstest](file-based-destination-testing-api.md) endpoint response (endpoint response) enligt beskrivningen nedan.

>[!NOTE]
>
>API-slutpunkten returnerar samma resultat som när du använder [API för flödestjänst](../../../api/update-destination-dataflows.md) för att övervaka dataflöden.

## Komma igång {#getting-started}

Läs igenom [komma igång-guide](../../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Förutsättningar {#prerequisites}

Innan du kan använda `/testing/destinationInstance` måste du se till att följande villkor uppfylls:

* Du har ett befintligt filbaserat mål som skapas via Destinationen SDK och du kan se det i [målkatalog](../../../ui/destinations-workspace.md).
* Du har skapat minst ett aktiveringsflöde för destinationen i användargränssnittet i Experience Platform.
* För att kunna utföra API-begäran behöver du det målinstans-ID som motsvarar den målinstans som du ska testa. Hämta det målinstans-ID som du bör använda i API-anropet från webbadressen när du bläddrar i en anslutning till målet i plattformsgränssnittet.

   ![Användargränssnittsbild som visar hur du hämtar målinstans-ID från URL:en.](../../assets/testing-api/get-destination-instance-id.png)
* Du har tidigare [testade målkonfigurationen](file-based-destination-testing-api.md)och fick ett giltigt API-svar, som innehåller `results` -egenskap. Du kommer att använda den här `results` för att ytterligare testa destinationen.

## Visa detaljerade testresultat för destinationer {#test-activation-results}

När du har [har verifierat målkonfigurationen](file-based-destination-testing-api.md)kan du se de detaljerade aktiveringsresultaten genom att skicka en GET till `authoring/testing/destinationInstance/` slutpunkt och ange målinstans-ID för det mål som du testar, samt ID:n för flödeskörning för de aktiverade segmenten.

Du hittar den fullständiga API-URL som du behöver i `results` egenskapen som returneras i [svar på destinationstestningsanropet](file-based-destination-testing-api.md).

**API-format**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Sökvägsparametrar | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID:t för målinstansen som du genererar exempelprofiler för. Se [krav](#prerequisites) om du vill ha mer information om hur du får detta ID. |

| Frågesträngsparametrar | Beskrivning |
| -------- | ----------- |
| `flowRunIds` | ID för flödeskörning som motsvarar de aktiverade segmenten. Du hittar ID:n för flödeskörning i dialogrutan `results` egenskapen som returneras i [svar på destinationstestningsanropet](file-based-destination-testing-api.md). |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en fullständig beskrivning av aktiveringsflödet. Du kan få samma svar genom att ringa [API för flödestjänst](../../../api/update-destination-dataflows.md) för att övervaka dataflöden.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du testar din filbaserade destinationskonfiguration och ser alla detaljer om aktiveringsresultaten.

Om du skapar ett offentligt mål kan du nu [skicka in målkonfigurationen](../../guides/submit-destination.md) till Adobe för granskning.
