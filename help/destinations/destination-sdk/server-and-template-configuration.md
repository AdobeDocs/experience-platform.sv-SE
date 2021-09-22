---
description: Server- och mallspecifikationerna kan konfigureras i Adobe Experience Platform mål-SDK via den gemensamma slutpunkten `/authoring/destination-servers`.
title: Konfigurationsalternativ för server- och mallspecifikationer i mål-SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 5%

---

# Konfigurationsalternativ för server- och mallspecifikationer

## Översikt {#overview}

Server- och mallspecifikationerna kan konfigureras i Adobe Experience Platform mål-SDK via den gemensamma slutpunkten `/authoring/destination-servers`. Läs [Slutpunktsåtgärder för mål-API](./destination-server-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Exempelkonfiguration {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Serverspecifikationer {#server-specs}

![Serverkonfigurationen är markerad](./assets/server-configuration.png)

Kunderna kan aktivera data från Adobe Experience Platform till er destination via HTTP-exporter. Serverkonfigurationen innehåller information om servern som tar emot meddelandena (servern på din sida).

Den här processen levererar användardata som en serie HTTP-meddelanden till målplattformen. Parametrarna nedan utgör mallen för specifikationer för HTTP-servern.

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | *Obligatoriskt.* Representerar ett eget namn på servern som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Obligatoriskt.* `URL_BASED` är för närvarande det enda tillgängliga alternativet. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omforma URL:en i fältet `value` nedan. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Använd `NONE` om ingen omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Mallspecifikationer {#template-specs}

![Mallkonfigurationen är markerad](./assets/template-configuration.png)

I mallspecifikationen kan du konfigurera hur det exporterade meddelandet ska formateras till ditt mål. Adobe använder ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) för att omforma fälten från XDM-schemat till ett format som stöds av ditt mål. Mer information om omvandlingen finns på länkarna nedan:

* [Meddelandeformat](./message-format.md)
* [Använda ett mallspråk för identitet, attribut och segmentmedlemskapsomvandlingar ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe erbjuder ett [utvecklarverktyg](./create-template.md) som hjälper dig att skapa och testa en meddelandeomvandlingsmall.

| Parameter | Typ | Beskrivning |
|---|---|---|
| `httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. Alternativen är `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `value` | Sträng | *Obligatoriskt.* Strängen är den teckenescape-konverterade version som transformerar plattformskundernas data till det format som tjänsten förväntar sig. <br> Mer information om hur du skriver mallen finns i avsnittet [ ](./message-format.md#using-templating)Använda mall. <br> Mer information om teckenigenkänning finns i  [RFC JSON-standarden, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). <br> Ett exempel på en enkel omformning finns i  [Profile ](./message-format.md#attributes) Attributomformning. |
| `contentType` | Sträng | *Obligatoriskt.* Den innehållstyp som servern accepterar. Detta värde är troligen `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
