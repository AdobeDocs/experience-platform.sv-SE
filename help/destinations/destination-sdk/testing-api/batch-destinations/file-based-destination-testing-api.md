---
description: På den här sidan beskrivs hur du använder API-slutpunkten /testing/destinationInstance för att testa om ditt filbaserade mål är korrekt konfigurerat och för att verifiera dataflödenas integritet till det konfigurerade målet.
title: Testa ditt filbaserade mål med exempelprofiler
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Testa ditt filbaserade mål med exempelprofiler

## Översikt {#overview}

På den här sidan beskrivs hur du använder `/testing/destinationInstance` API-slutpunkt för att testa om ditt filbaserade mål är korrekt konfigurerat och för att verifiera dataflödenas integritet till det konfigurerade målet.

Du kan göra förfrågningar till testslutpunkten med eller utan att lägga till [exempelprofiler](file-based-sample-profile-generation-api.md) till samtalet. Om du inte skickar några profiler på begäran genererar API:t en exempelprofil automatiskt och lägger till den i begäran.

De automatiskt genererade exempelprofilerna innehåller generiska data. Om du vill testa målet med anpassade, mer intuitiva profildata använder du [API för generering av exempelprofiler](file-based-sample-profile-generation-api.md) för att generera en exempelprofil, anpassa sedan svaret och inkludera det i begäran till `/testing/destinationInstance` slutpunkt.

## Komma igång {#getting-started}

Läs igenom [komma igång-guide](../../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Förutsättningar {#prerequisites}

Innan du kan använda `/testing/destinationInstance` måste du se till att följande villkor uppfylls:

* Du har ett befintligt filbaserat mål som skapas via Destinationen SDK och du kan se det i [målkatalog](../../../ui/destinations-workspace.md).
* Du har skapat minst ett aktiveringsflöde för destinationen i användargränssnittet i Experience Platform.
* För att kunna utföra API-begäran behöver du det målinstans-ID som motsvarar den målinstans som du ska testa. Hämta det målinstans-ID som du bör använda i API-anropet från webbadressen när du bläddrar i en anslutning till målet i plattformsgränssnittet.

  ![Användargränssnittsbild som visar hur du hämtar målinstans-ID från URL:en.](../../assets/testing-api/get-destination-instance-id.png)
* *Valfritt*: Om du vill testa målkonfigurationen med en exempelprofil som lagts till i API-anropet använder du [/sample-profiles](file-based-sample-profile-generation-api.md) slutpunkt för att generera en exempelprofil baserat på ditt befintliga källschema. Om du inte anger någon exempelprofil genererar API:t en och returnerar den i svaret.

## Testa målkonfigurationen utan att lägga till profiler till samtalet {#test-without-adding-profiles}

**API-format**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Begäran**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Sökvägsparametrar | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID:t för målinstansen som du genererar exempelprofiler för. Se [krav](#prerequisites) om du vill ha mer information om hur du får detta ID. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med svarsnyttolasten.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `activations` | Returnerar målgrupps-ID och flödeskörnings-ID för varje aktiverad målgrupp. Antalet aktiveringsposter (och associerade genererade filer) är lika med antalet målgrupper som mappas på målinstansen. <br><br> Exempel: Om du har mappat två målgrupper till målinstansen visas `activations` -arrayen innehåller två poster. Varje aktiverad målgrupp motsvarar en exporterad fil. |
| `results` | Returnerar destinationsinstansens ID och de flödes-ID som du kan använda för att anropa [Resultat-API](file-based-destination-results-api.md)för att ytterligare testa integreringen. |
| `inputProfiles` | Returnerar de exempelprofiler som har genererats automatiskt av API:t. |

{style="table-layout:auto"}

## Testa målkonfigurationen med profiler som lagts till i samtalet {#test-with-added-profiles}

Om du vill testa målet med anpassade, mer intuitiva profildata kan du anpassa svaret från [/sample-profiles](file-based-sample-profile-generation-api.md) slutpunkt med valfria värden och inkludera den anpassade profilen i begäran till `/testing/destinationInstance` slutpunkt.

**API-format**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Begäran**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Målinstans-ID:t för målet som du testar.  ID:t för målinstansen som du genererar exempelprofiler för. Se [krav](#prerequisites) om du vill ha mer information om hur du får detta ID. |
| `profiles` | Array som kan innehålla en eller flera profiler. Använd [API-slutpunkt för exempelprofil](file-based-sample-profile-generation-api.md) för att generera profiler som ska användas i detta API-anrop. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med svarsnyttolasten.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `activations` | Returnerar målgrupps-ID och flödeskörnings-ID för varje aktiverad målgrupp. Antalet aktiveringsposter (och associerade genererade filer) är lika med antalet målgrupper som mappas på målinstansen. <br><br> Exempel: Om du har mappat två målgrupper till målinstansen visas `activations` -arrayen innehåller två poster. Varje aktiverad målgrupp motsvarar en exporterad fil. |
| `results` | Returnerar destinationsinstansens ID och de flödes-ID som du kan använda för att anropa [Resultat-API](file-based-destination-results-api.md)för att ytterligare testa integreringen. |
| `inputProfiles` | Returnerar de anpassade exempelprofilerna som du skickade i API-begäran. |

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du testar din filbaserade målkonfiguration.

Om du har fått ett giltigt API-svar fungerar målet korrekt. Om du vill ha mer detaljerad information om aktiveringsflödet kan du använda `results` egenskap från svaret på [visa detaljerade aktiveringsresultat](file-based-destination-results-api.md).

Om du skapar ett offentligt mål kan du nu [skicka in målkonfigurationen](../../guides/submit-destination.md) till Adobe för granskning.
