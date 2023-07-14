---
description: Lär dig hur du använder API:t för måltestning för att testa om ditt mål för direktuppspelning är korrekt konfigurerat och för att verifiera dataflödenas integritet till det konfigurerade målet.
title: Testa strömningsmålet med exempelprofiler
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Testa strömningsmålet med exempelprofiler {#template-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med `/authoring/testing/destinationInstance/` API-slutpunkt, för att testa om målet är korrekt konfigurerat och för att verifiera dataflödenas integritet till det konfigurerade målet. En beskrivning av de funktioner som stöds av den här slutpunkten finns i [Testa målkonfigurationen](streaming-destination-testing-overview.md).

Du gör förfrågningar till testslutpunkten med eller utan att lägga till profiler till anropet. Om du inte skickar några profiler på begäran, genererar Adobe dessa internt åt dig och lägger till dem i begäran.

Du kan använda [API för generering av exempelprofiler](sample-profile-generation-api.md) för att skapa profiler som ska användas i begäranden till API:t för måltestning.

## Hämta målinstans-ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Om du vill använda detta API måste du ha en befintlig anslutning till målet i användargränssnittet i Experience Platform. Läs [ansluta till mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) och [aktivera profiler och målgrupper till ett mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) för mer information.
> * När du har upprättat anslutningen till målet, hämta det målinstans-ID som du bör använda i API-anrop till den här slutpunkten när [bläddra genom en anslutning till destinationen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
>![Användargränssnittsbild för att hämta målinstans-ID](../../assets/testing-api/get-destination-instance-id.png)

## Komma igång med API-åtgärder för måltestning {#get-started}

Läs igenom [komma igång-guide](../../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Testa målkonfigurationen utan att lägga till profiler till samtalet {#test-without-adding-profiles}

Du kan testa målkonfigurationen genom att göra en POST-förfrågan till `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` slutpunkt och ange målinstans-ID för målet som du testar.

**API-format**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Målinstans-ID:t för målet som du testar. |

**Begäran**

Följande begäran anropar målets REST API-slutpunkt. Begäran har konfigurerats av `{DESTINATION_INSTANCE_ID}` frågeparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med API-svaret från målets REST API-slutpunkt.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `aggregationKey` | Innehåller information om den aggregeringsprincip som har konfigurerats för målet. Mer information finns i [Samlingsprincip](../../functionality/destination-configuration/aggregation-policy.md) dokumentation. |
| `traceId` | En unik identifierare för åtgärden. När du får problem kan du dela detta ID med Adobe-teamet för felsökning. |
| `results.httpCalls.request` | Inkluderar den begäran som skickades av Adobe till ditt mål. |
| `results.httpCalls.response` | Inkluderar det svar som togs emot av Adobe från ditt mål. |
| `inputProfiles` | Inkluderar de profiler som exporterades i samtalet till målet. Profilerna matchar ditt källschema. |

{style="table-layout:auto"}

## Testa målkonfigurationen med profiler som lagts till i samtalet {#test-with-added-profiles}

Du kan testa målkonfigurationen genom att göra en POST-förfrågan till `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` slutpunkt och ange målinstans-ID för målet som du testar.

**API-format**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Målinstans-ID:t för målet som du testar. |

**Begäran**

Följande begäran anropar målets REST API-slutpunkt. Begäran konfigureras av parametrarna som anges i nyttolasten och `{DESTINATION_INSTANCE_ID}` frågeparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med API-svaret från målets REST API-slutpunkt.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du testar målet. Nu kan du använda Adobe [självbetjäningsdokumentationsprocess](../../docs-framework/documentation-instructions.md) för att skapa en dokumentationssida för destinationen.
