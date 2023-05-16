---
description: Den här sidan innehåller exempel på API-anropet som används för att skapa en målgruppsmall via Adobe Experience Platform Destination SDK.
title: Skapa en målgruppsmall
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# Skapa en målgruppsmall

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

För vissa mål som skapats med Destination SDK måste du skapa en målgruppsmetadatakonfiguration för att programmässigt skapa, uppdatera eller ta bort segmentmetadata i målet. På den här sidan visas hur du använder `/authoring/audience-templates` API-slutpunkt för att skapa konfigurationen.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i [hantering av målgruppsmetadata](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målgruppsmallar {#get-started}

Läs igenom [komma igång-guide](../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa en målgruppsmall {#create}

Du kan skapa en ny målgruppsmall genom att skapa en `POST` begäran till `/authoring/audience-templates` slutpunkt.

**API-format**

```http
POST /authoring/audience-templates
```

+++Begäran

Följande begäran skapar en ny målgruppsmall som konfigureras med parametrarna som anges i nyttolasten. Nedan finns alla parametrar som accepteras av `/authoring/audience-templates` slutpunkt. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      },
      "notify":{
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
| `requestBody` | Sträng | Anger innehållet i meddelandetexten som ska skickas till din API. Parametrarna som ska läggas till i `requestBody` -objektet beror på vilka fält som API:t godkänner. Se till exempel [första mallexemplet](../functionality/audience-metadata-management.md#example-1) i funktionsdokumentet för målgruppsmetadata. |
| `responseFields.name` | Sträng | Ange eventuella svarsfält som API:t returnerar när det anropas. Se till exempel [mallexempel](../functionality/audience-metadata-management.md#examples) i funktionsdokumentet för målgruppsmetadata. |
| `responseFields.value` | Sträng | Ange värdet för eventuella svarsfält som API:t returnerar när det anropas. |
| `responseErrorFields.name` | Sträng | Ange eventuella svarsfält som API:t returnerar när det anropas. Se till exempel [ mallexempel](../functionality/audience-metadata-management.md#examples) i funktionsdokumentet för målgruppsmetadata. |
| `responseErrorFields.value` | Sträng | Tolkar felmeddelanden som returneras på API-anropssvar från ditt mål. Dessa felmeddelanden kommer att visas för användare i användargränssnittet i Experience Platform. |
| `validations.field` | Sträng | Anger om valideringar ska köras för fält innan API-anrop görs till målet. Du kan till exempel använda `{{validations.accountId}}` för att validera användarens konto-ID. |
| `validations.regex` | Sträng | Anger hur fältet ska struktureras för att valideringen ska gå igenom. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om din nya målgruppsmall.

+++

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu när du ska använda målgruppsmallar och hur du konfigurerar en målgruppsmall med `/authoring/audience-templates` API-slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
