---
description: På den här sidan beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten "/authoring/audition-templates".
title: API-åtgärder för målgruppsmetadata
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# API-åtgärder för målgruppsmetadata

>[!IMPORTANT]
>
>**API-slutpunkt**:  `platform.adobe.io/data/core/activation/authoring/audience-templates`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/audience-templates`. En beskrivning av när den här slutpunkten ska användas finns i [hantering av målgruppsmetadata](./audience-metadata-management.md).

## Komma igång med API-åtgärder för målgruppsmallar {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa en ny målgruppsmall {#create}

Du kan skapa en ny målgruppsmall genom att göra en POST-förfrågan till `/authoring/audience-templates`-slutpunkten.

**API-format**


```http
POST /authoring/audience-templates
```

**Begäran**

I följande begäran skapas en ny metadatamall för målgruppen, som konfigureras med parametrarna i nyttolasten. Nyttolasten nedan innehåller alla parametrar som accepteras av slutpunkten `/authoring/audience-templates`. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Egenskap | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `name` | Sträng | Namnet på målets metadatamall för målgruppen. Det här namnet visas i alla partnerspecifika felmeddelanden i användargränssnittet i Experience Platform, följt av felmeddelandet som tolkas från `metadataTemplate.create.errorSchemaMap`. |
| `url` | Sträng | URL:en och slutpunkten för ditt API, som används för att skapa, uppdatera, ta bort eller validera målgrupper/segment på din plattform. Två branschexempel: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` och `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Sträng | Den metod som används i slutpunkten för att skapa, uppdatera, ta bort eller validera segmentet/målgruppen i ditt mål programmatiskt. Exempel: `POST`, `PUT`, `DELETE` |
| `headers.header` | Sträng | Anger alla HTTP-huvuden som ska läggas till i anropet till ditt API. Exempel: `"Content-Type"` |
| `headers.value` | Sträng | Anger värdet för HTTP-huvuden som ska läggas till i anropet till ditt API. Exempel: `"application/x-www-form-urlencoded"` |
| `requestBody` | Sträng | Anger innehållet i meddelandetexten som ska skickas till din API. Vilka parametrar som ska läggas till i `requestBody`-objektet beror på vilka fält ditt API accepterar. Se till exempel det första mallexemplet [i funktionsdokumentet för målets metadata.](./audience-metadata-management.md#example-1) |
| `responseFields.name` | Sträng | Ange eventuella svarsfält som API:t returnerar när det anropas. Se till exempel [mallexemplen](./audience-metadata-management.md#examples) i funktionsdokumentet för målets metadata. |
| `responseFields.value` | Sträng | Ange värdet för eventuella svarsfält som API:t returnerar när det anropas. |
| `responseErrorFields.name` | Sträng | Ange eventuella svarsfält som API:t returnerar när det anropas. Se till exempel mallexemplen [](./audience-metadata-management.md#examples) i funktionsdokumentet för målets metadata. |
| `responseErrorFields.value` | Sträng | Tolkar felmeddelanden som returneras på API-anropssvar från ditt mål. Dessa felmeddelanden kommer att visas för användare i användargränssnittet i Experience Platform. |
| `validations.field` | Sträng | Anger om valideringar ska köras för fält innan API-anrop görs till målet. Du kan till exempel använda `{{validations.accountId}}` för att validera användarens konto-ID. |
| `validations.regex` | Sträng | Anger hur fältet ska struktureras för att valideringen ska gå igenom. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nya målgruppsmall.

## Uppdatera målgruppsmall {#update}

Du kan uppdatera en befintlig målgruppsmall genom att göra en PUT-begäran till `/authoring/audience-templates`-slutpunkten och ange instans-ID för den målgruppsmall som du vill uppdatera. Ange den uppdaterade mallen i anropets brödtext.

**API-format**


```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för den målgruppsmetadatamall som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar en befintlig målgruppsmetadatamall som konfigurerats med parametrarna i nyttolasten.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```


## Hämta en lista med målgruppsmallar {#retrieve-list}

Du kan hämta en lista över alla målgruppsmallar för din IMS-organisation genom att göra en GET-förfrågan till `/authoring/audience-templates`-slutpunkten.

**API-format**


```http
GET /authoring/audience-templates
```

**Begäran**

Följande begäran hämtar listan med målgruppsmallar som du har tillgång till, baserat på konfigurationen för IMS-organisationen och sandlådan.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över målgruppsmetadatamallar som du har tillgång till, baserat på det IMS-organisations-ID och sandlådenamn som du använde. Ett `instanceId` motsvarar mallen för ett mål. Svaret kortas av för att vara kortfattat.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Hämta en specifik målgruppsmall {#get}

Du kan hämta detaljerad information om en viss målgruppsmall genom att göra en GET-förfrågan till `/authoring/audience-templates`-slutpunkten och ange instans-ID:t för den målgruppsmall som du vill hämta.

**API-format**


```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målgruppens metadatamall som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna målgruppsmallen.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Ta bort en specifik målgruppsmall {#delete}

Du kan ta bort den angivna målgruppsmallen genom att göra en DELETE-begäran till `/authoring/audience-templates`-slutpunkten och ange ID:t för målgruppsmallen som du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` för målgruppsmallen som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu när du ska använda metadatamallar för målgrupper och hur du konfigurerar en metadatamall för målgrupper med hjälp av API-slutpunkten `/authoring/audience-templates`. Läs [hur du använder mål-SDK för att konfigurera ditt mål](./configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
