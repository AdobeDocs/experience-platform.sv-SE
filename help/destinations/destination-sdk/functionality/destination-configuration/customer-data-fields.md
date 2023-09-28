---
description: Lär dig hur du skapar indatafält i användargränssnittet i Experience Platform som gör att dina användare kan ange olika typer av information som är relevant för att ansluta och exportera data till ditt mål.
title: Kunddatafält
source-git-commit: cadffd60093eef9fb2dcf4562b1fd7611e61da94
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 1%

---


# Konfigurera användarindata via kunddatafält

När du ansluter till ditt mål i användargränssnittet i Experience Platform kan du behöva ange specifik konfigurationsinformation eller välja specifika alternativ som du gör tillgängliga för dem. I Destination SDK kallas dessa alternativ för kunddatafält.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se följande sidor med översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Användningsexempel för kunddatafält {#use-cases}

Använd kunddatafält för en mängd olika användningsområden där du vill att användare ska kunna mata in data i användargränssnittet i Experience Platform. Använd t.ex. kunddatafält när användare måste ange:

* Lagringsbucket-namn och sökvägar för molnet, för filbaserade mål.
* Det format som accepteras av kunddatafälten.
* Tillgängliga filkomprimeringstyper som användarna kan välja mellan.
* Listor över tillgängliga slutpunkter för realtidsintegreringar (direktuppspelning).

Du kan konfigurera kunddatafält via `/authoring/destinations` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla konfigurationstyper för kunddatafält som stöds och som du kan använda för ditt mål. Artikeln innehåller även information om vad kunderna kommer att se i användargränssnittet för Experience Platform.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## parametrar som stöds {#supported-parameters}

När du skapar egna kunddatafält kan du använda de parametrar som beskrivs i tabellen nedan för att konfigurera deras beteende.

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---------|----------|------|---|
| `name` | Sträng | Obligatoriskt | Ange ett namn för det anpassade fält som du introducerar. Det här namnet visas inte i plattformens användargränssnitt, såvida inte `title` fältet är tomt eller saknas. |
| `type` | Sträng | Obligatoriskt | Anger typen av anpassat fält som du introducerar. Godkända värden: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | Sträng | Valfritt | Anger fältets namn, så som det visas av kunderna i plattformsgränssnittet. Om fältet är tomt eller saknas ärver gränssnittet fältnamnet från `name` värde. |
| `description` | Sträng | Valfritt | Ange en beskrivning för det anpassade fältet. Den här beskrivningen visas inte i plattformsgränssnittet. |
| `isRequired` | Boolean | Valfritt | Anger om användare måste ange ett värde för det här fältet i arbetsflödet för målkonfiguration. |
| `pattern` | Sträng | Valfritt | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID:n inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i detta fält. |
| `enum` | Sträng | Valfritt | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `default` | Sträng | Valfritt | Definierar standardvärdet från ett `enum` lista. |
| `hidden` | Boolean | Valfritt | Anger om kunddatafältet visas i användargränssnittet eller inte. |
| `unique` | Boolean | Valfritt | Använd den här parametern när du behöver skapa ett kunddatafält vars värde måste vara unikt för alla måldataflöden som har konfigurerats av en användares organisation. Till exempel **[!UICONTROL Integration alias]** fältet i [Anpassad personalisering](../../../catalog/personalization/custom-personalization.md) målet måste vara unikt, vilket innebär att två separata dataflöden till det här målet inte kan ha samma värde för det här fältet. |
| `readOnly` | Boolean | Valfritt | Anger om kunden kan ändra fältets värde eller inte. |

{style="table-layout:auto"}

I exemplet nedan är `customerDataFields` -avsnittet definierar två fält som användare måste ange i plattformens användargränssnitt när de ansluter till målet:

* `Account ID`: Ett användarkonto-ID för målplattformen.
* `Endpoint region`: Den regionala slutpunkten för det API som de ansluter till. The `enum` skapar en rullgardinsmeny med de värden som är definierade i som är tillgängliga för användarna att välja.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![En gränssnittsbild som visar ett exempel på kunddatafält.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Namn och beskrivningar för målanslutning {#names-description}

När ett nytt mål skapas läggs Destinationen SDK automatiskt till **[!UICONTROL Name]** och **[!UICONTROL Description]** fält till målanslutningsskärmen i plattformsgränssnittet. Som du kan se i exemplet ovan **[!UICONTROL Name]** och **[!UICONTROL Description]** fält återges i användargränssnittet utan att inkluderas i konfigurationen för kunddatafält.

>[!IMPORTANT]
>
>Om du lägger till **[!UICONTROL Name]** och **[!UICONTROL Description]** fält i konfigurationen av kunddatafält, användarna ser dem duplicerade i användargränssnittet.

## Beställa kunddatafält {#ordering}

Den ordning i vilken du lägger till kunddatafälten i målkonfigurationen återspeglas i plattformens användargränssnitt.

Konfigurationen nedan återspeglas till exempel i användargränssnittet, där alternativen visas i ordningen **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL Bucket name]**, **[!UICONTROL Folder path]**, **[!UICONTROL File Type]**, **[!UICONTROL Compression format]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![Bild som visar ordningen för filformateringsalternativ i användargränssnittet för Experience Platform.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Gruppera kunddatafält {#grouping}

Du kan gruppera flera kunddatafält i ett avsnitt. När du konfigurerar anslutningen till målet i användargränssnittet kan användarna se och dra nytta av en visuell gruppering av liknande fält.

Om du vill göra det använder du `"type": "object"` för att skapa gruppen och samla in önskade kunddatafält inom en `properties` objekt, som visas i bilden nedan, där grupperingen **[!UICONTROL CSV Options]** är markerat.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Bild som visar gruppering av kunddatafält i användargränssnittet.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Skapa nedrullningsbara väljare för kunddatafält {#dropdown-selectors}

I situationer där du vill att användarna ska kunna välja mellan flera alternativ, t.ex. vilket tecken som ska användas för att avgränsa fälten i CSV-filer, kan du lägga till nedrullningsbara fält i användargränssnittet.

Använd `namedEnum` enligt nedan och konfigurera ett `default` värdet för de alternativ som användaren kan välja.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Skärminspelning som visar ett exempel på listruteväljare som har skapats med den konfiguration som visas ovan.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Skapa dynamiska listruteväljare för kunddatafält {#dynamic-dropdown-selectors}

I situationer där du vill anropa ett API dynamiskt och använda svaret för att dynamiskt fylla i alternativen i en listruta kan du använda en dynamisk listruteväljare.

De dynamiska listruteväljarna ser likadana ut som [vanliga listruteväljare](#dropdown-selectors) i användargränssnittet. Den enda skillnaden är att värdena hämtas dynamiskt från ett API.

Om du vill skapa en dynamisk nedrullningsbar väljare måste du konfigurera två komponenter:

**Steg 1.** [Skapa en målserver](../../authoring-api/destination-server/create-destination-server.md#dynamic-dropdown-servers) med `responseFields` mall för det dynamiska API-anropet enligt nedan.

```json
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":" <--YOUR-API-ENDPOINT-PATH--> "
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

**Steg 2.** Använd `dynamicEnum` som visas nedan. I exemplet nedan är `User` listrutan hämtas med den dynamiska servern.


```json {line-numbers="true" highlight="13-21"}
"customerDataFields": [
  {
    "name": "integrationId",
    "title": "Integration ID",
    "type": "string",
    "isRequired": true
  },
  {
    "name": "userId",
    "title": "User",
    "type": "string",
    "isRequired": true,
    "dynamicEnum": {
      "queryParams": [
        "integrationId"
      ],
      "destinationServerId": "<~dynamic-field-server-id~>",
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "value": "$.list",
      "responseFormat": "NAME_VALUE"
    }
  }
]
```

Ange `destinationServerId` parameter till ID:t för målservern som du skapade i steg 1. Du kan se målserverns ID i svaret från [hämta en målserverkonfiguration](../../authoring-api/destination-server/retrieve-destination-server.md) API-anrop.

## Skapa villkorliga kunddatafält {#conditional-options}

Du kan skapa villkorsstyrda kunddatafält, som bara visas i aktiveringsarbetsflödet när användarna väljer ett visst alternativ.

Du kan till exempel skapa alternativ för villkorsstyrd filformatering som bara visas när användarna väljer en viss filexporttyp.

I konfigurationen nedan skapas en villkorsstyrd gruppering för CSV-filformateringsalternativ. CSV-filalternativen visas bara när användaren väljer CSV som önskad filtyp för export.

Om du vill ange ett fält som villkorligt använder du `conditional` enligt nedan:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

I ett större sammanhang kan du se `conditional` fält som används i målkonfigurationen nedan, tillsammans med `fileType` strängen och `csvOptions` det objekt som det är definierat i.

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

Nedan visas den resulterande gränssnittsskärmen baserat på konfigurationen ovan. När användaren väljer filtypen CSV visas ytterligare filformateringsalternativ som refererar till CSV-filtypen i användargränssnittet.

![Skärminspelning som visar alternativet för villkorsstyrd filformatering för CSV-filer.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Åtkomst till mallsidiga kunddatafält {#accessing-templatized-fields}

När målet kräver användarindata måste du tillhandahålla ett urval av kunddatafält till dina användare, som de kan fylla i via plattformsgränssnittet. Sedan måste du konfigurera målservern så att den läser användarindata från kunddatafälten korrekt. Detta görs genom mallsidiga fält.

Mallade fält använder formatet `{{customerData.fieldName}}`, där `fieldName` är namnet på kunddatafältet som du läser information från. Alla mallsidiga kunddatafält föregås av `customerData.` och innesluten inom dubbla klammerparenteser `{{ }}`.

Låt oss titta på följande Amazon S3-destinationskonfiguration:

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Den här konfigurationen uppmanar dina användare att ange sina [!DNL Amazon S3] bucket name and folder path into their respective customer data fields.

För att Experience Platform ska kunna ansluta till [!DNL Amazon S3]måste målservern vara konfigurerad att läsa värdena från dessa två kunddatafält, vilket visas nedan:

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

De mallsidiga värdena `{{customerData.bucketName}}` och `{{customerData.path}}` läsa de värden som användaren anger så att Experience Platform kan ansluta till målplattformen.

Mer information om hur du konfigurerar målservern för att läsa mallsidiga fält finns i dokumentationen om [hårdkodade jämfört med mallsidesfält](../destination-server/server-specs.md#templatized-fields).

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur du kan låta dina användare mata in information i användargränssnittet i Experience Platform via kunddatafält. Du vet nu också hur du väljer rätt kunddatafält för ditt användningsfall och konfigurerar, beställer och grupperar kunddatafält i plattformsgränssnittet.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-autentisering](oauth2-authentication.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)