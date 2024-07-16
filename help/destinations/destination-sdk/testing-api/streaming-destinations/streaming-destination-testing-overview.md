---
description: Lär dig hur du använder API:t för måltestning för att testa målkonfigurationen för direktuppspelning innan du publicerar den.
title: API-översikt för testning av direktuppspelningsmål
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# API-översikt för testning av direktuppspelningsmål

Som en del av Destinationen SDK har Adobe utvecklarverktyg som hjälper dig att konfigurera och testa destinationen. På den här sidan beskrivs hur du testar målkonfigurationen. Mer information om hur du skapar en meddelandeomformningsmall finns i [Skapa och testa en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md).

Om du vill **testa om målet är korrekt konfigurerat och verifiera dataflödenas integritet till det konfigurerade målet** använder du *måltestningsverktyget*. Med det här verktyget kan du testa målkonfigurationen genom att skicka meddelanden till REST API-slutpunkten.

Nedan visas hur testning av ditt mål passar in i arbetsflödet för [målkonfiguration](../../guides/configure-destination-instructions.md) i Destinationen SDK:

![Bild av var målteststeget passar in i målkonfigurationsarbetsflödet](../../assets/testing-api/test-destination-step.png)

## Måltestningsverktyg - Syfte och krav {#destination-testing-tool}

Använd måttestningsverktyget för att testa målkonfigurationen genom att skicka meddelanden till partnerslutpunkten som du angav i [serverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md).

Innan du använder verktyget bör du kontrollera att:
* Konfigurera ditt mål genom att följa de steg som beskrivs i [arbetsflödet för målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md) och
* Upprätta en anslutning till ditt mål, vilket beskrivs i [Hämta målinstans-ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Med det här verktyget kan du göra följande när du har konfigurerat målet:
* Testa om målet är korrekt konfigurerat;
* Verifiera dataflödenas integritet till det konfigurerade målet.

### Så här använder du {#how-to-use}

>[!NOTE]
>
>Fullständig API-referensdokumentation finns i [API-åtgärder för måltestning](../../testing-api/streaming-destinations/destination-testing-api.md).

Du kan anropa API-slutpunkten för måltestning med eller utan att lägga till profiler på begäran.

Om du inte lägger till några profiler i begäran, genererar Adobe dessa internt åt dig och lägger till dem i begäran. Om du vill generera profiler som ska användas i den här begäran, se [API-referens för generering av exempelprofiler](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Du måste generera profiler baserade på XDM-källschemat, vilket visas i [API-referensen](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Observera att källschemat är [unionsschemat](../../../../profile/ui/union-schema.md) för sandlådan som du använder.

Svaret innehåller resultatet av bearbetningen av målbegäran. Begäran innehåller tre huvudavsnitt:
* Begäran som genererats av Adobe för destinationen.
* Svaret som togs emot från ditt mål.
* Listan över profiler som skickats i begäran, oavsett om profilerna [lades till av dig i begäran](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles) eller genererades av Adobe om [innehållet i måltestningsbegäran var tomt](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe kan generera flera par med begäran och svar. Om du till exempel skickar 10 profiler till ett mål som har värdet `maxUsersPerRequest` 7, kommer det att finnas en begäran med 7 profiler och en annan begäran med 3 profiler.

**Exempelbegäran med profilparametern i brödtexten**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Exempelbegäran utan profilparameter i brödtexten**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Exempelsvar**

Observera att innehållet i parametern `results.httpCalls` är specifikt för ditt REST API.

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

Beskrivningar av parametrarna för begäran och svar finns i [API-åtgärder för måltestning](../../testing-api/streaming-destinations/destination-testing-api.md).

## Nästa steg

När du har testat destinationen och bekräftat att den är korrekt konfigurerad kan du använda [API:t för målpublicering](../../publishing-api/create-publishing-request.md) för att skicka konfigurationen till Adobe för granskning.
