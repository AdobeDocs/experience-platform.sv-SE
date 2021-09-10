---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/render` för att återge exporterade data för ditt mål, baserat på din meddelandeomvandlingsmall.
title: API-åtgärder för återgivningsmall
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# API-åtgärder för återgivningsmall {#render-template-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/render` för att återge exporterade data för ditt mål, baserat på din [meddelandeomformningsmall](./message-format.md#using-templating). En beskrivning av de funktioner som stöds av den här slutpunkten finns i [skapa mall](./create-template.md).

## Komma igång med åtgärder för återgivningsmall-API {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Återge exporterade data baserat på mall {#render-exported-data}

Du kan återge exporterade data genom att göra en POST-förfrågan till `authoring/testing/template/render`-slutpunkten och ange mål-ID för målkonfigurationen och den mall du skapade med [API-slutpunkten för exempelmallen](./sample-template-api.md).

>[!TIP]
>
>* Det mål-ID som du bör använda här är det `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Se [API-referens för målkonfiguration](./destination-configuration-api.md#retrieve-list).



**API-format**


```http
POST authoring/testing/template/render
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `destinationId` | ID:t för målkonfigurationen som du återger exporterade data för. |
| `template` | Den teckenescape-version av mallen som du återger exporterade data utifrån. |
| `profiles` | Om du vill lägga till profiler i brödtexten av samtalet kan du generera några med hjälp av [API:t för generering av exempelprofiler](./sample-profile-generation-api.md). |

{style=&quot;table-layout:auto&quot;}


Du kan återge exporterade data enligt exemplen nedan:

* [Återge en mall utan profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-no-body)
* [Återge en mall med profiler som skickats i brödtexten](./render-template-api.md#multiple-profiles-with-body)

<!--

### Render a template for single profile, no profiles sent in body {#single-profile-no-body}

**Request**

The following request renders sample profiles that match the format expected by your destination.

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}"
}'

```

**Response**

The response returns the result of rendering the template, or any errors encountered.
A successful response returns HTTP status 200 with details of the exported data.
An unsuccessful response returns HTTP status 500 along with descriptions of the encountered errors.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

### Render a template for single profile, with profiles sent in body {#single-profile-with-body}

**Request**

The following request renders a profile that matches the format expected by your destination. You can generate profiles to send on the call by using the [sample profile generation API](./sample-profile-generation-api.md).

```shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "a9fb4f0f-3983-4756-b756-00cf25fe5a35",
    "template": "{# THIS is an example template for a single profile #}\r\n{\r\n    \"identities\": [\r\n        {% for email in input.profile.identityMap.email %}\r\n            {\r\n                \"type\": \"email\",\r\n                \"id\": \"{{ email.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n\r\n        {# Add a comma only if we have both emails and external_ids. #}\r\n        {% if input.profile.identityMap.email is not empty and input.profile.identityMap.external_id is not empty %}\r\n            ,\r\n        {% endif %}\r\n\r\n        {% for external in input.profile.identityMap.external_id %}\r\n            {\r\n                \"type\": \"external_id\",\r\n                \"id\": \"{{ external.id }}\"\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            {% for segment in input.profile.segmentMembership.ups | added %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n            {# Alternative syntax for filtering segments by status: #}\r\n            {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n                \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n            {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626238Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-17T11:49:06.626240Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-c3fjU"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-VNq0z"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-HATAl"
                }
            ],
            "external_id": [
                {
                    "id": "extern_id-cP732"
                }
            ],
            "email": [
                {
                    "id": "email_lc_sha256-cBltJ"
                }
            ]
        }
    }
    ]
}'

```

**Response**

A successful response returns HTTP status 200 with details of the exported data.

```json

{
    "identities": [
        {
            "type": "email",
            "id": "email_lc_sha256-cBltJ"
        },
        {
            "type": "external_id",
            "id": "extern_id-cP732"
        }
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
            "segmentid1",
            "segmentid2"
        ],
        "remove": [
            "segmentid3"
        ]
    }
}

```

-->

### Återge en mall utan profiler som skickats i brödtexten {#multiple-profiles-no-body}

**Begäran**

Följande begäran återger flera exempelprofiler som matchar det format som förväntas av ditt mål.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**Svar**

Svaret returnerar resultatet av återgivningen av mallen eller eventuella fel som påträffats.
Ett lyckat svar returnerar HTTP-status 200 med information om exporterade data.
Ett misslyckat svar returnerar HTTP-statusen 500 tillsammans med beskrivningar av de fel som påträffats.

```json
{
   "profiles":[
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      },
      {
         "identities":[
            
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}       
```

### Återge en mall med profiler som skickats i brödtexten {#multiple-profiles-with-body}

**Begäran**

Följande begäran återger exempelprofiler som matchar det format som förväntas av ditt mål. Du kan generera profiler som ska skickas vid samtalet med hjälp av [API:t för generering av exempelprofiler](./sample-profile-generation-api.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
   "destinationId":"{DESTINATION_ID}",
   "template":"{# THIS is an example template for multiple profiles #}\r\n{\r\n    \"profiles\": [\r\n        {% for profile in input.profiles %}\r\n            {\r\n                \"identities\": [\r\n                    {% for email in profile.identityMap.email %}\r\n                        {\r\n                            \"type\": \"email\",\r\n                            \"id\": \"{{ email.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n\r\n                    {# Add a comma only if we have both emails and external_ids. #}\r\n                    {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}\r\n                        ,\r\n                    {% endif %}\r\n\r\n                    {% for external in profile.identityMap.external_id %}\r\n                        {\r\n                            \"type\": \"external_id\",\r\n                            \"id\": \"{{ external.id }}\"\r\n                        }{% if not loop.last %},{% endif %}\r\n                    {% endfor %}\r\n                ],\r\n                \"AdobeExperiencePlatformSegments\": {\r\n                    \"add\": [\r\n                        {% for segment in profile.segmentMembership.ups | added %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ],\r\n                    \"remove\": [\r\n                        {# Alternative syntax for filtering segments by status: #}\r\n                        {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                            \"{{ segment.key }}\"{% if not loop.last %},{% endif %}\r\n                        {% endfor %}\r\n                    ]\r\n                }\r\n            }{% if not loop.last %},{% endif %}\r\n        {% endfor %}\r\n    ]\r\n}",
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "segmentid1":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870859Z",
                  "status":"existing"
               },
               "segmentid3":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"exited"
               },
               "segmentid2":{
                  "lastQualificationTime":"2021-06-17T12:08:07.870860Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "email":[
               {
                  "id":"Email-gq3zZ"
               }
            ],
            "external_id":[
               {
                  "id":"external_id"
               }
            ]
         }
      }
   ]
}'
```

**Svar**

Svaret returnerar resultatet av återgivningen av mallen eller eventuella fel som påträffats.
Ett lyckat svar returnerar HTTP-status 200 med information om exporterade data.
Ett misslyckat svar returnerar HTTP-statusen 500 tillsammans med beskrivningar av de fel som påträffats.

```json
{
   "profiles":[
      {
         "identities":[
            {
               "type":"email",
               "id":"Email-gq3zZ"
            },
            {
               "type":"external_id",
               "id":"external_id"
            }
         ],
         "AdobeExperiencePlatformSegments":{
            "add":[
               "segmentid1",
               "segmentid2"
            ],
            "remove":[
               "segmentid3"
            ]
         }
      }
   ]
}
```

## API-felhantering {#api-error-handling}

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du använder meddelandeomformningsmallen för att generera exporterade profiler som matchar målets förväntade dataformat. Läs [hur du använder mål-SDK för att konfigurera ditt mål](./configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
