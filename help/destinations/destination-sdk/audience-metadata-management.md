---
description: Använd metadatamallar för att programmässigt skapa, uppdatera eller ta bort målgrupper i er målgrupp. Adobe tillhandahåller en utbyggbar metadatamall för målgrupper, som du kan konfigurera baserat på specifikationerna för ditt marknadsförings-API. När du har definierat, testat och skickat in mallen används den av Adobe för att strukturera API-anropen till ditt mål.
title: Hantering av målgruppsmetadata
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Hantering av målgruppsmetadata {#audience-metadata-management}

## Översikt {#overview}

Använd metadatamallar för att programmässigt skapa, uppdatera eller ta bort målgrupper i er målgrupp. Adobe tillhandahåller en utbyggbar metadatamall för målgrupper, som du kan konfigurera baserat på specifikationerna för ditt marknadsförings-API. När du har definierat, testat och skickat konfigurationen används den av Adobe för att strukturera API-anropen till ditt mål.

Du kan konfigurera de funktioner som beskrivs i det här dokumentet med API-slutpunkten `/authoring/audience-templates`. Läs [API-åtgärder för målets metadata-slutpunkt](./audience-metadata-api.md) om du vill se en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Använda slutpunkten för hantering av målgruppsmetadata {#when-to-use}

Beroende på din API-konfiguration kan du behöva använda slutpunkten för hantering av målgruppsmetadata när du konfigurerar målet i Experience Platform. Använd beslutsträdsdiagrammet nedan om du vill veta när målgruppsmetadatans slutpunkt ska användas och hur du konfigurerar en målgruppsmetadatamall för ditt mål.

![Beslutsträdsdiagram](./assets/audience-metadata-decision-tree.png)

## Användningsfall som stöds av hantering av målgruppsmetadata {#use-cases}

Med stöd för målgruppsmetadata i mål-SDK kan du, när du konfigurerar Experience Platform, ge plattformsanvändare ett av flera alternativ när de mappar och aktiverar segment till ditt mål. Du kan styra vilka alternativ som är tillgängliga för användaren via parametrarna i segmentmappningsavsnittet i [målkonfigurationen](./destination-configuration.md#segment-mapping).

### Använd fall 1 - Du har ett API från tredje part och användarna behöver inte ange ID för indatamappning

Om du har en API-slutpunkt för att skapa/uppdatera/ta bort segment eller målgrupper kan du använda målgruppsmetadatamallar för att konfigurera mål-SDK så att det matchar specifikationerna för segmentets skapa/uppdatera/ta bort-slutpunkt. Experience Platform kan programmatiskt skapa/uppdatera/ta bort segment och synkronisera metadata tillbaka till Experience Platform.

När man aktiverar segment i användargränssnittet i Experience Platform behöver man inte fylla i ett ID-fält för segmentmappning manuellt i aktiveringsarbetsflödet.

### Använd fall 2 - Användare måste skapa ett segment i målet först och måste ange ett manuellt mappnings-ID

Om segment och andra metadata måste skapas manuellt av partners eller användare i målet, måste användarna manuellt fylla i ID-fältet för segmentmappning i aktiveringsarbetsflödet för att synkronisera segmentmetadata mellan målet och Experience Platform.

![ID för indatamappning](./assets/input-mapping-id.png)

### Använd fall 3 - Målet godkänner Experience Platform segment-ID, användarna behöver inte manuellt ange mappnings-ID

Om målsystemet godkänner Experience Platform segment-ID:t kan du konfigurera det i målgruppens metadatamall. Användarna behöver inte fylla i ett segmentmappnings-ID när de aktiverar ett segment.

## Allmän och utbyggbar målgruppsmall {#generic-and-extensible}

För att stödja de användningsfall som listas ovan tillhandahåller Adobe en allmän mall som kan anpassas efter dina API-specifikationer.

Du kan använda den generiska mallen för att [skapa en ny målgruppsmall](./audience-metadata-api.md#create) om ditt API stöder:

* HTTP-metoderna: POST, GET, PUT, DELETE, PATCH
* Autentiseringstyper: OAuth 1, OAuth 2 med uppdateringstoken, OAuth 2 med bearer-token
* Funktionerna: skapa en målgrupp, uppdatera en målgrupp, få en målgrupp, ta bort en målgrupp, validera inloggningsuppgifterna

Teknikteamet på Adobe kan samarbeta med dig för att utöka den generiska mallen med anpassade fält om det behövs för dina användningsfall.

## Exempel på mallar {#template-examples}

Det här avsnittet innehåller tre exempel på allmänna konfigurationer av målgruppsmetadata, tillsammans med beskrivningar av huvudavsnitten i konfigurationen. Lägg märke till hur brödtexten för URL, rubriker, begäran och svar skiljer sig mellan de tre exempelkonfigurationerna. Detta beror på de olika specifikationerna för de tre exempelplattformarnas marknadsförings-API.

Observera att i vissa exempel används makrofält som `{{authData.accessToken}}` eller `{{segment.name}}` i URL:en, och i andra exempel används de i rubrikerna eller begärandetexten. Det beror på era specifikationer för marknadsförings-API.

| Mallavsnitt | Beskrivning |
|--- |--- |
| `create` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att programmässigt skapa segment/målgrupper på din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `update` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att programmässigt uppdatera segment/målgrupper på din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `delete` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, rubriker, begärande och svarstext) för att göra ett HTTP-anrop till ditt API, för att programmässigt ta bort segment/målgrupper på din plattform. |
| `validations` | Kör valideringar för fält i mallkonfigurationen innan du anropar partner-API:t. Du kan till exempel validera att användarens konto-ID är korrekt angivet. |

{style=&quot;table-layout:auto&quot;}

### Första exemplet {#example-1}

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

### Andra exemplet {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### Tredje exemplet {#example-3}

```json
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
```

Hitta beskrivningar av alla parametrar i mallen i referensdokumentationen [API-åtgärder för målets metadata](./audience-metadata-api.md).

## Makron som används i mallar för målgruppsmetadata

För att skicka information som segment-ID, åtkomsttoken, felmeddelanden med mera mellan Experience Platform och ditt API innehåller målgruppsmallarna makron som du kan använda. Läs nedan en beskrivning av makrona som används i de tre konfigurationsexemplen på den här sidan:

| Makro | Beskrivning |
|--- |--- |
| `{{segment.alias}}` | Gör att du kan komma åt segmentaliaset i Experience Platform. |
| `{{segment.name}}` | Gör att du kan komma åt segmentnamnet i Experience Platform. |
| `{{segment.id}}` | Gör att du kan komma åt segment-ID:t i Experience Platform. |
| `{{customerData.accountId}}` | Gör att du kan komma åt det konto-ID-fält som du har konfigurerat i målkonfigurationen. |
| `{{oauth2ServiceAccessToken}}` | Gör att du dynamiskt kan generera en åtkomsttoken baserat på din OAuth 2-konfiguration. |
| `{{authData.accessToken}}` | Gör att du kan skicka åtkomsttoken till API-slutpunkten. Använd `{{authData.accessToken}}` om Experience Platform ska använda token som inte upphör att gälla för att ansluta till ditt mål, annars använder du `{{oauth2ServiceAccessToken}}` för att generera en åtkomsttoken. |
| `{{body.segments[0].segment.id}}` | Returnerar den skapade målgruppens unika identifierare som värdet för nyckeln `externalAudienceId`. |
| `{{error.message}}` | Returnerar ett felmeddelande som kommer att visas för användare i användargränssnittet i Experience Platform. |

{style=&quot;table-layout:auto&quot;}
