---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Anslut till e-postmarknadsföringsmål och aktivera data med API:t för Flow Service
description: I det här dokumentet beskrivs hur du skapar e-postmarknadsföringsmål med hjälp av Adobe Experience Platform API
topic-legacy: tutorial
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# Anslut till e-postmarknadsföringsmål och aktivera data med API:t för Flow Service

I den här självstudiekursen visas hur du använder API-anrop för att ansluta till dina Adobe Experience Platform-data, skapa en [e-postmarknadsföringsmål](../catalog/email-marketing/overview.md), skapa ett dataflöde till det nya målet och aktivera data till det nya målet.

I den här självstudien används Adobe Campaign-destinationen i alla exempel, men stegen är identiska för alla e-postmarknadsföringsmål.

![Översikt - stegen för att skapa ett mål och aktivera segment](../assets/api/email-marketing/overview.png)

Om du föredrar att använda användargränssnittet i Platform för att ansluta ett mål och aktivera data finns mer information i [Anslut ett mål](../ui/connect-destination.md) och [Aktivera målgruppsdata för att batchprofilera exportmål](../ui/activate-batch-profile-destinations.md) självstudiekurser.

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] är systemet för registrering av dataplatser och -rader inom [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna aktivera data för e-postmarknadsföringsmål i Platform.

### Samla in nödvändiga inloggningsuppgifter

Om du vill slutföra stegen i den här självstudiekursen bör du ha följande autentiseringsuppgifter tillgängliga, beroende på vilken typ av mål du ansluter och aktiverar segment till.

* För [!DNL Amazon] S3-anslutningar till e-postmarknadsföringsplattformar: `accessId`, `secretKey`
* För SFTP-anslutningar till e-postmarknadsföringsplattformar: `domain`, `port`, `username`, `password` eller `ssh key` (beroende på anslutningsmetoden till FTP-platsen)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska och valfria rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Resurser i [!DNL Experience Platform] kan isoleras till specifika virtuella sandlådor. I förfrågningar till [!DNL Platform] API:er kan du ange namn och ID för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

### Dokumentation för Swagger

Du hittar referensdokumentation för alla API-anrop i den här självstudiekursen i Swagger. Se [API-dokumentation för Flow Service på Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Vi rekommenderar att du använder den här självstudiekursen och dokumentationssidan för Swagger parallellt.

## Hämta listan över tillgängliga mål {#get-the-list-of-available-destinations}

![Översiktssteg för målsteg 1](../assets/api/email-marketing/step1.png)

Som ett första steg bör du bestämma vilket e-postmarknadsföringsmål som data ska aktiveras till. Börja med att ringa ett samtal för att begära en lista över tillgängliga mål som du kan ansluta och aktivera segment till. Utför följande GET-förfrågan till `connectionSpecs` slutpunkt för att returnera en lista över tillgängliga destinationer:

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

## Anslut till [!DNL Experience Platform] data {#connect-to-your-experience-platform-data}

![Översiktssteg för målsteg 2](../assets/api/email-marketing/step2.png)

Sedan måste du ansluta till [!DNL Experience Platform] så att du kan exportera profildata och aktivera dem på det önskade målet. Detta består av två ämnen som beskrivs nedan.

1. Först måste du ringa för att ge behörighet till dina data i [!DNL Experience Platform]genom att konfigurera en basanslutning.
2. Sedan gör du ett nytt anrop med hjälp av det grundläggande anslutnings-ID:t där du skapar en källanslutning som upprättar anslutningen till [!DNL Experience Platform] data.


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
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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


* `{CONNECTION_SPEC_ID}`: Använd anslutningsspec-ID för profiltjänsten - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett godkänt svar innehåller basanslutningens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa källanslutningen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Anslut till [!DNL Experience Platform] data {#connect-to-platform-data}

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
  "name": "Connecting to Profile Service",
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
            "name": "Connecting to Profile Service",
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
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: Använd det ID du fick i föregående steg.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspec-ID för [!DNL Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen till [!DNL Profile Service]. Detta bekräftar att du har anslutit till [!DNL Experience Platform] data. Lagra det här värdet som det behövs i ett senare steg.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Anslut till mål för e-postmarknadsföring {#connect-to-email-marketing-destination}

![Översikt över destinationssteg 3](../assets/api/email-marketing/step3.png)

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
    "description": "summer advertising campaign",
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

* `{CONNECTION_SPEC_ID}`: Använd det anslutningsspec-ID som du fick i steget [Hämta listan över tillgängliga mål](#get-the-list-of-available-destinations).
* `{S3 or SFTP}`: fylla i önskad anslutningstyp för det här målet. I [målkatalog](../catalog/overview.md)bläddrar du till önskat mål för att se om det finns stöd för anslutningstyperna S3 och/eller SFTP.
* `{ACCESS_ID}`: Ditt åtkomst-ID för din [!DNL Amazon] Lagringsplats för S3.
* `{SECRET_KEY}`: Din hemliga nyckel för din [!DNL Amazon] Lagringsplats för S3.

**Svar**

Ett godkänt svar innehåller basanslutningens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa en målanslutning.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Ange lagringsplats och dataformat

[!DNL Adobe Experience Platform] exporterar data för e-postmarknadsföring och molnlagringsdestinationer i form av [!DNL CSV] filer.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] delar automatiskt upp exportfilerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil.
>
>Delade filnamn läggs till med en siffra som anger att filen är en del av en större export: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

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
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikationen som du fick i steget [Hämta listan över tillgängliga mål](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`: Dina [!DNL Amazon] S3-bucket, där Platform placerar dataexporten.
* `{FILEPATH}`: Sökvägen i [!DNL Amazon] S3-bucket-katalog där Platform placerar dataexporten.

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nya målanslutningen till ditt mål för e-postmarknadsföring. Lagra det här värdet som det behövs i senare steg.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Skapa ett dataflöde

![Översikt över destinationssteg 4](../assets/api/email-marketing/step4.png)

Med de ID:n du fick i föregående steg kan du nu skapa ett dataflöde mellan [!DNL Experience Platform] data och målet dit du ska aktivera data. Föreställ dig det här steget som att skapa pipeline, genom vilken data sedan flödar mellan [!DNL Experience Platform] och det mål du vill ha.

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

* `{FLOW_SPEC_ID}`: Använd flödet för det e-postmarknadsföringsmål som du vill ansluta till. Om du vill hämta flödesspecifikationen utför du en GET på `flowspecs` slutpunkt. Se Swagger-dokumentation här: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. I svaret kan du söka efter `upsTo` och kopiera motsvarande ID för det e-postmarknadsföringsmål som du vill ansluta till. För Adobe Campaign kan du till exempel söka efter `upsToCampaign` och kopiera `id` parameter.
* `{SOURCE_CONNECTION_ID}`: Använd det källanslutnings-ID som du fick i steget [Anslut till Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Använd det ID för målanslutning som du fick i steget [Anslut till mål för e-postmarknadsföring](#connect-to-email-marketing-destination).

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet och `etag`. Notera båda värdena nedåt. som du kommer att göra i nästa steg, för att aktivera segment.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivera data till ditt nya mål

![Översikt över destinationssteg steg 5](../assets/api/email-marketing/step5.png)

När ni har skapat alla anslutningar och dataflöden kan ni nu aktivera profildata för e-postmarknadsföringsplattformen. I det här steget väljer du vilka segment och vilka profilattribut du skickar till målet och du kan schemalägga och skicka data till målet.

Om du vill aktivera segment till det nya målet måste du utföra en JSON PATCH-åtgärd, som i exemplet nedan. Du kan aktivera flera segment och profilattribut i ett samtal. Mer information om JSON PATCH finns i [RFC-specifikation](https://tools.ietf.org/html/rfc6902).

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
* `{SEGMENT_ID}`: Ange det segment-ID som du vill exportera till det här målet. Om du vill hämta segment-ID:n för de segment som du vill aktivera går du till **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, markera **[!UICONTROL Segmentation Service API]** i den vänstra navigeringsmenyn och leta efter `GET /segment/definitions` operation in **[!UICONTROL Segment Definitions]**.
* `{PROFILE_ATTRIBUTE}`: Exempel, `"person.lastName"`

**Svar**

Håll utkik efter 202 OK-svar. Ingen svarstext returneras. Om du vill verifiera att begäran var korrekt går du till nästa steg, Validera dataflödet.

## Validera dataflödet

![Översiktssteg för målsteg 6](../assets/api/email-marketing/step6.png)

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

Det returnerade svaret ska innehålla `transformations` parametern segmenten och profilattributen som du skickade i föregående steg. Ett exempel `transformations` parametern i svaret kan se ut så här:

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

Genom att följa den här självstudiekursen har du anslutit Plattform till ett av de e-postmarknadsföringsmål du föredrar och konfigurerat ett dataflöde till respektive mål. Utgående data kan nu användas i målet för e-postkampanjer, riktad reklam och många andra användningsfall. Mer information finns på följande sidor:

* [Översikt över mål](../home.md)
* [Översikt över destinationskatalogen](../catalog/overview.md)
