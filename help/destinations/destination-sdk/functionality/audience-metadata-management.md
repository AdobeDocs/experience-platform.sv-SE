---
description: Använd metadatamallar för att programmässigt skapa, uppdatera eller ta bort målgrupper i er målgrupp. Adobe tillhandahåller en utbyggbar metadatamall för målgrupper, som du kan konfigurera baserat på specifikationerna för ditt marknadsförings-API. När du har definierat, testat och skickat in mallen används den av Adobe för att strukturera API-anropen till ditt mål.
title: Hantering av målgruppsmetadata
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 2%

---

# Hantering av målgruppsmetadata

Använd metadatamallar för att programmässigt skapa, uppdatera eller ta bort målgrupper i er målgrupp. Adobe tillhandahåller en utbyggbar metadatamall för målgrupper, som du kan konfigurera baserat på specifikationerna för ditt marknadsförings-API. När du har definierat, testat och skickat in konfigurationen används den av Adobe för att strukturera API-anropen till ditt mål.

Du kan konfigurera de funktioner som beskrivs i det här dokumentet med API-slutpunkten `/authoring/audience-templates`. Läs [skapa en metadatamall](../metadata-api/create-audience-template.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Använda slutpunkten för hantering av målgruppsmetadata {#when-to-use}

Beroende på din API-konfiguration kan du behöva använda slutpunkten för hantering av målgruppsmetadata när du konfigurerar målet i Experience Platform. Använd beslutsträdsdiagrammet nedan om du vill veta när målgruppsmetadatans slutpunkt ska användas och hur du konfigurerar en målgruppsmetadatamall för ditt mål.

![Beslutsträdsdiagram](../assets/functionality/audience-metadata-decision-tree.png)

## Användningsfall som stöds av hantering av målgruppsmetadata {#use-cases}

Med stöd för målgruppsmetadata i Destination SDK kan du när du konfigurerar ditt Experience Platform-mål ge Experience Platform-användare ett av flera alternativ när de mappar och aktiverar målgrupper till ditt mål. Du kan styra vilka alternativ som är tillgängliga för användaren via parametrarna i avsnittet [konfiguration av målmetadata](../functionality/destination-configuration/audience-metadata-configuration.md) i målkonfigurationen.

### Använd fall 1 - Du har ett API från tredje part och användarna behöver inte ange ID för indatamappning

Om du har en API-slutpunkt för att skapa/uppdatera/ta bort målgrupper eller målgrupper kan du använda metadatamallar för målgrupper för att konfigurera Destination SDK så att det matchar specifikationerna för målgruppen när du skapar/uppdaterar/tar bort slutpunkter. Experience Platform kan programmatiskt skapa/uppdatera/ta bort målgrupper och synkronisera metadata tillbaka till Experience Platform.

När du aktiverar målgrupper till ditt mål i Experience Platform användargränssnitt behöver användarna inte fylla i ett fält för målgruppsmappning i aktiveringsarbetsflödet manuellt.

### Användningsfall 2 - Användarna måste skapa en målgrupp i ditt mål först och måste ange ett manuellt ID för inmatningsmappning

Om målgrupper och andra metadata måste skapas manuellt av partners eller användare i målgruppen måste användarna manuellt fylla i ID-fältet för målgruppsmappning i aktiveringsarbetsflödet för att synkronisera målgruppsmetadata mellan målplatsen och Experience Platform.

![ID för indatamappning](../assets/functionality/input-mapping-id.png)

### Använd fall 3 - Målet godkänner Experience Platform målgrupps-ID, användarna behöver inte ange något manuellt ID för inmatningsmappning

Om målsystemet godkänner Experience Platform målgrupps-ID kan du konfigurera detta i din målgruppsmetadatamall. Användarna behöver inte fylla i ett målgruppsmappnings-ID när de aktiverar ett segment.

## Allmän och utbyggbar målgruppsmall {#generic-and-extensible}

För att stödja de användningsfall som listas ovan tillhandahåller Adobe en allmän mall som kan anpassas efter dina API-specifikationer.

Du kan använda den generiska mallen för att [skapa en ny målgruppsmall](../metadata-api/create-audience-template.md) om ditt API har stöd för:

* HTTP-metoderna POST, GET, PUT, DELETE, PATCH
* Autentiseringstyperna: OAuth 1, OAuth 2 med uppdateringstoken, OAuth 2 med bearer-token
* Funktionerna: skapa en målgrupp, uppdatera en målgrupp, hämta en målgrupp, ta bort en målgrupp, validera inloggningsuppgifterna

Adobe tekniker kan samarbeta med dig för att utöka den generiska mallen med anpassade fält om det behövs.


## Mallhändelser som stöds {#supported-events}

Tabellen nedan beskriver de händelser som stöds av metadatamallar för målgrupper.

| Mallavsnitt | Beskrivning |
|--- |--- |
| `create` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att programmässigt skapa segment/målgrupper på din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `update` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att programmässigt uppdatera segment/målgrupper på din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `delete` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, rubriker, begärande och svarstext) för att göra ett HTTP-anrop till ditt API, för att programmässigt ta bort segment/målgrupper på din plattform. |
| `validate` | Kör valideringar för fält i mallkonfigurationen innan du anropar partner-API:t. Du kan till exempel validera att användarens konto-ID är korrekt angivet. |
| `notify` | Gäller endast för filbaserade mål. Inkluderar alla nödvändiga komponenter (URL, HTTP-metod, rubriker, begärande och svarstext) för att göra ett HTTP-anrop till ditt API, för att meddela dig om filexporter lyckades. |
| `createDestination` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att skapa ett programmatiskt dataflöde på din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `updateDestination` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, headers, request och response body) för att göra ett HTTP-anrop till ditt API, för att uppdatera ett dataflöde i din plattform och synkronisera informationen tillbaka till Adobe Experience Platform. |
| `deleteDestination` | Innehåller alla nödvändiga komponenter (URL, HTTP-metod, rubriker, begärande och svarstext) för att göra ett HTTP-anrop till ditt API, för att programmässigt ta bort ett dataflöde från din plattform. |

{style="table-layout:auto"}

## Konfigurationsexempel {#configuration-examples}

I det här avsnittet finns exempel på allmänna konfigurationer av målgruppsmetadata, som du kan använda som referens.

Lägg märke till hur URL:en, rubrikerna och förfrågantexterna skiljer sig åt mellan de tre exempelkonfigurationerna. Detta beror på de olika specifikationerna för de tre exempelplattformarnas marknadsförings-API.

Observera att i vissa exempel används makrofält som `{{authData.accessToken}}` eller `{{segment.name}}` i URL:en, och i andra exempel används de i rubrikerna eller i begärandetexten. Hur de används beror på era API-specifikationer för marknadsföring.

+++Exempel på strömning 1

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

+++

+++Exempel på strömning 2

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

+++

+++Exempel på direktuppspelning 3

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

+++

+++Filbaserat exempel

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

+++

Hitta beskrivningar av alla parametrar i mallen i API-referensen för [Skapa en målgruppsmall](../metadata-api/create-audience-template.md).

## Makron som används i mallar för målgruppsmetadata {#macros}

För att skicka information som målgrupps-ID:n, åtkomsttoken, felmeddelanden med mera mellan Experience Platform och ditt API innehåller målgruppsmallarna makron som du kan använda. Läs nedan en beskrivning av makrona som används i de tre konfigurationsexemplen på den här sidan:

| Makro | Beskrivning |
|--- |--- |
| `{{segment.alias}}` | Ger åtkomst till målgruppsalias i Experience Platform. |
| `{{segment.name}}` | Gör att du kan komma åt målgruppens namn i Experience Platform. |
| `{{segment.id}}` | Ger åtkomst till målgrupps-ID i Experience Platform. |
| `{{customerData.accountId}}` | Gör att du kan komma åt det konto-ID-fält som du har konfigurerat i målkonfigurationen. |
| `{{oauth2ServiceAccessToken}}` | Gör att du dynamiskt kan generera en åtkomsttoken baserat på din OAuth 2-konfiguration. |
| `{{authData.accessToken}}` | Gör att du kan skicka åtkomsttoken till API-slutpunkten. Använd `{{authData.accessToken}}` om Experience Platform ska använda token som inte upphör att gälla för att ansluta till ditt mål. Annars använder du `{{oauth2ServiceAccessToken}}` för att generera en åtkomsttoken. |
| `{{body.segments[0].segment.id}}` | Returnerar den unika identifieraren för den skapade målgruppen som värdet för nyckeln `externalAudienceId`. |
| `{{error.message}}` | Returnerar ett felmeddelande som kommer att visas för användare i Experience Platform-gränssnittet. |
| `{{{segmentEnrichmentAttributes}}}` | Gör att du kan komma åt alla anrikningsattribut för en viss målgrupp.  Det här makrot stöds av händelserna `create`, `update` och `delete`. Berikningsattribut är bara tillgängliga för [anpassade uppladdade målgrupper](destination-configuration/schema-configuration.md#external-audiences). Se [aktiveringsguiden för gruppmålare](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) för att se hur markering av anrikningsattribut fungerar. |
| `{{destination.name}}` | Returnerar namnet på målet. |
| `{{destination.sandboxName}}` | Returnerar namnet på den Experience Platform-sandlåda där målet är konfigurerat. |
| `{{destination.id}}` | Returnerar ID:t för målkonfigurationen. |
| `{{destination.imsOrgId}}` | Returnerar det IMS-Org-ID där målet är konfigurerat. |
| `{{destination.enrichmentAttributes}}` | Gör att du kan komma åt alla anrikningsattribut för alla målgrupper som mappas till ett mål. Det här makrot stöds av händelserna `createDestination`, `updateDestination` och `deleteDestination`. Berikningsattribut är bara tillgängliga för [anpassade uppladdade målgrupper](destination-configuration/schema-configuration.md#external-audiences). Se [aktiveringsguiden för gruppmålare](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) för att se hur markering av anrikningsattribut fungerar. |
| `{{destination.enrichmentAttributes.<namespace>.<segmentId>}}` | Gör att du kan komma åt anrikningsattribut för specifika externa målgrupper mappade till ett mål. Berikningsattribut är bara tillgängliga för [anpassade uppladdade målgrupper](destination-configuration/schema-configuration.md#external-audiences). Se [aktiveringsguiden för gruppmålare](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) för att se hur markering av anrikningsattribut fungerar. |

{style="table-layout:auto"}
