---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa e-postmarknadsföringsmål
topic: tutorial
translation-type: tm+mt
source-git-commit: bde86cc835c2bd579404480ece8e850fbef8a9b2
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 0%

---


# Skapa e-postmarknadsföringsmål och aktivera data med API-anrop i Adobe [!DNL Real-time Customer Data Platform]

I den här självstudiekursen visas hur du använder API-anrop för att ansluta till dina Adobe Experience Platform-data, skapa ett [e-postmarknadsföringsmål](../../rtcdp/destinations/email-marketing-destinations.md), skapa ett dataflöde till det nya målet som du skapat och aktivera data till det nya målet som du skapat.

I den här självstudien används Adobe Campaign-destinationen i alla exempel, men stegen är identiska för alla e-postmarknadsföringsmål.

![Översikt - stegen för att skapa ett mål och aktivera segment](/help/rtcdp/destinations/assets/flow-api-destinations-steps-overview.png)

Om du föredrar att använda användargränssnittet i Adobe CDP i realtid för att ansluta ett mål och aktivera data, se [Koppla ett mål](../../rtcdp/destinations/connect-destination.md) och [Aktivera profiler och segment till en målsjälvstudiekurs](../../rtcdp/destinations/activate-destinations.md) .

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] är systemet för registrering av dataplatser och datalinje inom [!DNL Experience Platform].
* [[!DNL-sandlådor]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna aktivera data till e-postmarknadsföringsmål i CDP i realtid i Adobe.

### Samla in nödvändiga inloggningsuppgifter

Om du vill slutföra stegen i den här självstudiekursen bör du ha följande autentiseringsuppgifter tillgängliga, beroende på vilken typ av mål du ansluter och aktiverar segment till.

* För [!DNL Amazon] S3-anslutningar till e-postmarknadsföringsplattformar: `accessId`, `secretKey`
* För SFTP-anslutningar till e-postmarknadsföringsplattformar: `domain`, `port`, `username`, `password` eller `ssh key` (beroende på anslutningsmetoden till FTP-platsen)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska och valfria rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Resurser i [!DNL Experience Platform] kan isoleras till specifika virtuella sandlådor. I förfrågningar till [!DNL Platform] API:er kan du ange namn och ID för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

<!--

### Definitions

Before starting this tutorial, familiarize yourself with the following terms which we'll use throughout the tutorial:

**Flow**: 

**Base Connection**: 

**Target Connection**: 

**Source Connection**: 

-->

### Dokumentation för Swagger

Du hittar referensdokumentation för alla API-anrop i den här självstudiekursen i Swagger. Se [Flow Service API-dokumentationen på Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Vi rekommenderar att du använder den här självstudiekursen och dokumentationssidan för Swagger parallellt.

## Hämta listan över tillgängliga mål {#get-the-list-of-available-destinations}

![Översiktssteg för målsteg 1](/help/rtcdp/destinations/assets/flow-api-destinations-step1.png)

Som ett första steg bör du bestämma vilket e-postmarknadsföringsmål som data ska aktiveras till. Börja med att ringa ett samtal för att begära en lista över tillgängliga mål som du kan ansluta och aktivera segment till. Utför följande GET-begäran till `connectionSpecs` slutpunkten för att returnera en lista över tillgängliga destinationer:

**API-format**

```http
GET /connectionSpecs
```

**Begäran**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Svar**

Ett lyckat svar innehåller en lista över tillgängliga destinationer och deras unika identifierare (`id`). Lagra värdet för destinationen som du tänker använda, vilket krävs i ytterligare steg. Om du till exempel vill ansluta och leverera segment till Adobe Campaign ska du leta efter följande utdrag i svaret:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Anslut till dina [!DNL Experience Platform] data {#connect-to-your-experience-platform-data}

![Översiktssteg för målsteg 2](/help/rtcdp/destinations/assets/flow-api-destinations-step2.png)

Därefter måste du ansluta till dina [!DNL Experience Platform] data, så att du kan exportera profildata och aktivera dem på det önskade målet. Detta består av två ämnen som beskrivs nedan.

1. Först måste du ringa ett samtal för att auktorisera åtkomst till dina data i [!DNL Experience Platform]genom att konfigurera en basanslutning.
2. Med hjälp av basanslutnings-ID:t gör du sedan ett nytt anrop där du skapar en källanslutning som upprättar anslutningen till dina [!DNL Experience Platform] data.


### Ge åtkomst till dina data i [!DNL Experience Platform]

**API-format**

```http
POST /connections
```

**Begäran**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikations-ID för Unified Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa källanslutningen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Anslut till dina [!DNL Experience Platform] data

**API-format**

```http
POST /sourceConnections
```

**Begäran**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Använd det ID du fick i föregående steg.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikations-ID för [!DNL Unified Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen till [!DNL Unified Profile Service]. Detta bekräftar att du har anslutit till dina [!DNL Experience Platform] data. Lagra det här värdet som det behövs i ett senare steg.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Anslut till mål för e-postmarknadsföring {#connect-to-email-marketing-destination}

![Översikt över destinationssteg 3](/help/rtcdp/destinations/assets/flow-api-destinations-step3.png)

I det här steget skapar du en anslutning till det e-postmarknadsföringsmål du vill använda. Detta består av två ämnen som beskrivs nedan.

1. Först måste du ringa för att auktorisera åtkomst till e-postleverantören genom att konfigurera en basanslutning.
2. Med hjälp av basanslutnings-ID:t gör du sedan ett nytt anrop där du skapar en målanslutning, där du anger platsen i lagringskontot där exporterade data ska levereras samt formatet för de data som ska exporteras.

### Auktorisera åtkomst till e-postmarknadsföringsmålet

**API-format**

```http
POST /connections
```

**Begäran**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Använd det anslutningsspec-ID som du fick i steget [Hämta listan med tillgängliga mål](#get-the-list-of-available-destinations).
* `{S3 or SFTP}`: fylla i önskad anslutningstyp för det här målet. Bläddra till önskat mål i [målkatalogen](../../rtcdp/destinations/destinations-catalog.md)för att se om anslutningstyperna S3 och/eller SFTP stöds.
* `{ACCESS_ID}`: Ditt åtkomst-ID för din [!DNL Amazon] S3-lagringsplats.
* `{SECRET_KEY}`: Din hemliga nyckel för din [!DNL Amazon] S3-lagringsplats.

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa en målanslutning.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Ange lagringsplats och dataformat

**API-format**

```http
POST /targetConnections
```

**Begäran**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Använd det grundläggande anslutnings-ID som du fick i steget ovan.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikationen som du fick i steget [Hämta listan med tillgängliga mål](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`: Din [!DNL Amazon] S3-bucket, där CDP i realtid kommer att lagra dataexporten.
* `{FILEPATH}`: Sökvägen i [!DNL Amazon] S3-bucket-katalogen där CDP i realtid kommer att placera dataexporten.

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nya målanslutningen till ditt mål för e-postmarknadsföring. Lagra det här värdet som det behövs i senare steg.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Skapa ett dataflöde

![Översikt över destinationssteg 4](/help/rtcdp/destinations/assets/flow-api-destinations-step4.png)

Med de ID:n du fick i föregående steg kan du nu skapa ett dataflöde mellan dina [!DNL Experience Platform] data och målet där du vill aktivera data. Tänk på det här steget som att skapa en pipeline, genom vilken data sedan flödar mellan [!DNL Experience Platform] och önskat mål.

Om du vill skapa ett dataflöde ska du utföra en begäran om POST enligt nedan, med de värden som anges nedan i nyttolasten.

Utför följande begäran om POST för att skapa ett dataflöde.

**API-format**

```http
POST /flows
```

**Begäran**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`: Använd flödet för det e-postmarknadsföringsmål som du vill ansluta till. Om du vill hämta flödesspecifikationen utför du en GET-åtgärd på `flowspecs` slutpunkten. Se Swagger-dokumentation här: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. I svaret söker du efter `upsTo` och kopierar motsvarande ID för e-postmarknadsföringsmålet som du vill ansluta till. För Adobe Campaign söker du till exempel efter `upsToCampaign` och kopierar `id` parametern.
* `{SOURCE_CONNECTION_ID}`: Använd det källanslutnings-ID som du fick i steget [Anslut till Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Använd det målanslutnings-ID som du fick i steget [Ansluta till e-postmarknadsföringsmålet](#connect-to-email-marketing-destination).

**Svar**

Ett godkänt svar returnerar ID:t (`id`) för det nya dataflödet och ett `etag`. Notera båda värdena nedåt. som du kommer att göra i nästa steg, för att aktivera segment.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivera data till ditt nya mål

![Översikt över destinationssteg steg 5](/help/rtcdp/destinations/assets/flow-api-destinations-step5.png)

När ni har skapat alla anslutningar och dataflöden kan ni nu aktivera profildata för e-postmarknadsföringsplattformen. I det här steget väljer du vilka segment och vilka profilattribut du skickar till målet och du kan schemalägga och skicka data till målet.

Om du vill aktivera segment till det nya målet måste du utföra en JSON PATCH-åtgärd, som i exemplet nedan. Du kan aktivera flera segment och profilattribut i ett samtal. Mer information om JSON PATCH finns i [RFC-specifikationen](https://tools.ietf.org/html/rfc6902).

**API-format**

```http
PATCH /flows
```

**Begäran**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

* `{DATAFLOW_ID}`: Använd det dataflöde du fick i föregående steg.
* `{ETAG}`: Använd taggen som du fick i föregående steg.
* `{SEGMENT_ID}`: Ange det segment-ID som du vill exportera till det här målet. Om du vill hämta segment-ID:n för de segment som du vill aktivera går du till **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, väljer **[!UICONTROL Segmentation Service API]** i den vänstra navigeringsmenyn och letar efter `GET /segment/definitions` åtgärden i **[!UICONTROL Segment Definitions]**.
* `{PROFILE_ATTRIBUTE}`: Exempel, `"person.lastName"`

**Svar**

Håll utkik efter 202 OK-svar. Ingen svarstext returneras. Om du vill verifiera att begäran var korrekt går du till nästa steg, Validera dataflödet.

## Validera dataflödet

![Översiktssteg för målsteg 6](/help/rtcdp/destinations/assets/flow-api-destinations-step6.png)

Som ett sista steg i självstudiekursen bör du validera att segmenten och profilattributen verkligen har mappats korrekt till dataflödet.

Gör följande GET-förfrågan för att validera detta:

**API-format**

```http
GET /flows
```

**Begäran**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Använd dataflödet från föregående steg.
* `{ETAG}`: Använd taggen från föregående steg.

**Svar**

Det returnerade svaret ska i parametern inkludera de segment och profilattribut som du skickade in i det föregående steget. `transformations` En exempelparameter `transformations` i svaret kan se ut så här:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
            },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit CDP i realtid till ett av dina önskade mål för e-postmarknadsföring och ställt in ett dataflöde för respektive mål. Utgående data kan nu användas i målet för e-postkampanjer, riktad reklam och många andra användningsfall. Mer information finns på följande sidor:

* [Översikt över mål](../../rtcdp/destinations/destinations-overview.md)
* [Översikt över destinationskatalogen](../../rtcdp/destinations/destinations-catalog.md)