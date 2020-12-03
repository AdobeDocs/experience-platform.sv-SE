---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: Ansluta till direktuppspelningsmål och aktivera data
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 6a1552cbd7da998e3fe7d7c985611e634fc7546a
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 0%

---


# Ansluta till direktuppspelningsmål och aktivera data med API-anrop i Adobe Real-time Customer Data Platform

>[!NOTE]
>
>Målen [!DNL Amazon Kinesis] och [!DNL Azure Event Hubs] destinationerna i CDP i realtid är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

I den här självstudiekursen visas hur du använder API-anrop för att ansluta till dina Adobe Experience Platform-data, skapa en anslutning till ett direktuppspelat molnlagringsmål ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) eller [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md)), skapa ett dataflöde till ditt nya skapade mål och aktivera data till ditt nya skapade mål.

I den här självstudien används målet i alla exempel, men stegen är identiska för [!DNL Amazon Kinesis] [!DNL Azure Event Hubs].

![Översikt - stegen för att skapa ett direktuppspelningsmål och aktivera segment](../assets/api/streaming-destination/overview.png)

Om du föredrar att använda användargränssnittet i Adobe CDP i realtid för att ansluta till ett mål och aktivera data, se [Koppla ett mål](../ui/connect-destination.md) och [Aktivera profiler och segment till en målsjälvstudiekurs](../ui/activate-destinations.md) .

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] är registersystemet för dataplats och datalinje inom Experience Platform.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna aktivera data till direktuppspelningsdestinationer i CDP i realtid.

### Samla in nödvändiga inloggningsuppgifter

Om du vill slutföra stegen i den här självstudiekursen bör du ha följande autentiseringsuppgifter tillgängliga, beroende på vilken typ av mål du ansluter och aktiverar segment till.

* För [!DNL Amazon Kinesis] anslutningar: `accessKeyId`, `secretKey`, `region` eller `connectionUrl`
* För [!DNL Azure Event Hubs] anslutningar: `sasKeyName`, `sasKey`, `namespace`

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska och valfria rubriker {#gather-values}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Resurser i Experience Platform kan isoleras till specifika virtuella sandlådor. I förfrågningar till plattforms-API:er kan du ange namnet och ID:t för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

### Dokumentation för Swagger {#swagger-docs}

Du hittar referensdokumentation för alla API-anrop i den här självstudiekursen i Swagger. Se [Flow Service API-dokumentationen på Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Vi rekommenderar att du använder den här självstudiekursen och dokumentationssidan för Swagger parallellt.

## Hämta listan över tillgängliga mål för direktuppspelning {#get-the-list-of-available-streaming-destinations}

![Översiktssteg för målsteg 1](../assets/api/streaming-destination/step1.png)

Som ett första steg bör du bestämma vilket mål för direktuppspelning som data ska aktiveras till. Börja med att ringa ett samtal för att begära en lista över tillgängliga mål som du kan ansluta och aktivera segment till. Utför följande GET-begäran till `connectionSpecs` slutpunkten för att returnera en lista över tillgängliga destinationer:

**API-format**

```http
GET /connectionSpecs
```

**Begäran**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Svar**

Ett lyckat svar innehåller en lista över tillgängliga destinationer och deras unika identifierare (`id`). Lagra värdet för destinationen som du tänker använda, vilket krävs i ytterligare steg. Om du till exempel vill ansluta och leverera segment till [!DNL Amazon Kinesis] eller [!DNL Azure Event Hubs]söker du efter följande utdrag i svaret:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Ansluta till dina Experience Platform-data {#connect-to-your-experience-platform-data}

![Översiktssteg för målsteg 2](../assets/api/streaming-destination/step2.png)

Därefter måste du ansluta till dina Experience Platform-data, så att du kan exportera profildata och aktivera dem på det önskade målet. Detta består av två ämnen som beskrivs nedan.

1. Först måste du ringa ett samtal för att ge behörighet till dina data i Experience Platform genom att konfigurera en basanslutning.
2. Med hjälp av basanslutnings-ID:t gör du sedan ett nytt anrop där du skapar en källanslutning som upprättar anslutningen till dina Experience Platform-data.


### Ge åtkomst till dina data i Experience Platform

**API-format**

```http
POST /connections
```

**Begäran**

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


* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikations-ID för Unified Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa källanslutningen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Ansluta till dina Experience Platform-data {#connect-to-platform-data}

**API-format**

```http
POST /sourceConnections
```

**Begäran**

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
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Använd det ID du fick i föregående steg.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikations-ID för Unified Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen till tjänsten för enhetlig profil. Detta bekräftar att du har anslutit till dina Experience Platform-data. Lagra det här värdet som det behövs i ett senare steg.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Anslut till direktuppspelningsmål {#connect-to-streaming-destination}

![Översikt över destinationssteg 3](../assets/api/streaming-destination/step3.png)

I det här steget skapar du en anslutning till det önskade direktuppspelningsmålet. Detta består av två ämnen som beskrivs nedan.

1. Först måste du ringa för att auktorisera åtkomst till direktuppspelningsmålet genom att konfigurera en basanslutning.
2. Med hjälp av basanslutnings-ID:t gör du sedan ett nytt anrop där du skapar en målanslutning, där du anger platsen i lagringskontot där exporterade data ska levereras samt formatet för de data som ska exporteras.

### Auktorisera åtkomst till direktuppspelningsmålet

**API-format**

```http
POST /connections
```

**Begäran**

>[!IMPORTANT]
>
>Exemplet nedan innehåller kodkommentarer som har prefixet `//`. Dessa kommentarer visar var olika värden måste användas för olika direktuppspelningsmål. Ta bort kommentarerna innan du använder fragmentet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Använd det anslutningsspec-ID som du fick i steget [Hämta listan med tillgängliga mål](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: Fyll i namnet på strömningsmålet: `Aws Kinesis authentication credentials` eller `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *För [!DNL Amazon Kinesis] anslutningar.* Ditt åtkomst-ID för din lagringsplats för Amazon Kinesis.
* `{SECRET_KEY}`: *För [!DNL Amazon Kinesis] anslutningar.* Din hemliga nyckel för din lagringsplats för Amazon Kinesis.
* `{REGION}`: *För [!DNL Amazon Kinesis] anslutningar.* Regionen på ditt [!DNL Amazon Kinesis] konto där CDP i realtid strömmar dina data.
* `{SAS_KEY_NAME}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i ditt SAS-nyckelnamn. Läs om hur du autentiserar [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i SAS-nyckeln. Läs om hur du autentiserar [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i [!DNL Azure Event Hubs] namnutrymmet där CDP för realtid strömmar dina data. Mer information finns i [Skapa ett namnutrymme](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) för händelsehubbar i [!DNL Microsoft] dokumentationen.

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

>[!IMPORTANT]
>
>Exemplet nedan innehåller kodkommentarer som har prefixet `//`. Dessa kommentarer visar var olika värden måste användas för olika direktuppspelningsmål. Ta bort kommentarerna innan du använder fragmentet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Använd det grundläggande anslutnings-ID som du fick i steget ovan.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikationen som du fick i steget [Hämta listan med tillgängliga mål](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *För [!DNL Amazon Kinesis] anslutningar.* Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto. CDP-data exporteras i realtid till den här strömmen.
* `{REGION}`: *För [!DNL Amazon Kinesis] anslutningar.* Den region på ditt Amazon Kinesis-konto där CDP i realtid strömmar dina data.
* `{EVENT_HUB_NAME}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i det [!DNL Azure Event Hub] namn där CDP för realtid strömmar era data. Mer information finns i [Skapa en händelsehubb](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) i [!DNL Microsoft] dokumentationen.

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade målanslutningen till ditt direktuppspelningsmål. Lagra det här värdet som det behövs i senare steg.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Skapa ett dataflöde

![Översikt över destinationssteg 4](../assets/api/streaming-destination/step4.png)

Med de ID:n du fick i föregående steg kan du nu skapa ett dataflöde mellan dina Experience Platform-data och det mål där du vill aktivera data. Tänk på det här steget som att skapa en pipeline, genom vilken data sedan flödar mellan Experience Platform och det önskade målet.

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
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
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
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: Flödesspec-ID:t för profilbaserade mål är `71471eba-b620-49e4-90fd-23f1fa0174d8`. Använd det här värdet i anropet.
* `{SOURCE_CONNECTION_ID}`: Använd det källanslutnings-ID som du fick i steget [Anslut till Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Använd det anslutnings-ID som du fick i steget [Ansluta till direktuppspelningsmål](#connect-to-streaming-destination).

**Svar**

Ett godkänt svar returnerar ID:t (`id`) för det nya dataflödet och ett `etag`. Notera båda värdena nedåt. som du kommer att göra i nästa steg, för att aktivera segment.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivera data till ditt nya mål {#activate-data}

![Översikt över destinationssteg steg 5](../assets/api/streaming-destination/step5.png)

När du har skapat alla anslutningar och dataflödet kan du nu aktivera dina profildata till direktuppspelningsplattformen. I det här steget väljer du vilka segment och vilka profilattribut du skickar till målet och du kan schemalägga och skicka data till målet.

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
* `{PROFILE_ATTRIBUTE}`: till exempel `personalEmail.address` eller `person.lastName`

**Svar**

Håll utkik efter 202 OK-svar. Ingen svarstext returneras. Om du vill verifiera att begäran var korrekt går du till nästa steg, Validera dataflödet.

## Validera dataflödet

![Översiktssteg för målsteg 6](../assets/api/streaming-destination/step6.png)

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
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
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

**Exporterade data**

>[!IMPORTANT]
>
> Förutom profilattributen och segmenten i steget [Aktivera data till det nya målet](#activate-data), kommer exporterade data i [!DNL AWS Kinesis] och [!DNL Azure Event Hubs] även att innehålla information om identitetskartan. Detta representerar de exporterade profilernas identiteter (till exempel [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), mobil-ID, Google-ID, e-postadress osv.). Se ett exempel nedan.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Använda Postman-samlingar för att ansluta till direktuppspelningsmål  {#collections}

Om du vill ansluta till de direktuppspelningsmål som beskrivs i den här självstudiekursen på ett effektivare sätt kan du använda [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] är ett verktyg som du kan använda för att göra API-anrop och hantera bibliotek med fördefinierade anrop och miljöer.

För den här självstudiekursen har följande [!DNL Postman] samlingar bifogats:

* [!DNL AWS Kinesis] [!DNL Postman] samling
* [!DNL Azure Event Hubs] [!DNL Postman] samling

Klicka [här](../assets/api/streaming-destination/DestinationPostmanCollection.zip) för att hämta samlingsarkivet.

Varje samling innehåller de nödvändiga förfrågningarna och miljövariablerna för [!DNL AWS Kinesis], [!DNL Azure Event Hub]respektive.

### Så här använder du Postman-samlingarna

Följ de här stegen för att ansluta till målen med de bifogade [!DNL Postman] samlingarna:

* Hämta och installera [!DNL Postman];
* [Ladda ned](../assets/api/streaming-destination/DestinationPostmanCollection.zip) och zippa upp de bifogade samlingarna,
* Importera samlingarna från deras motsvarande mappar till Postman.
* Fyll i miljövariablerna enligt instruktionerna i denna artikel.
* Kör [!DNL API] förfrågningarna från Postman utifrån instruktionerna i den här artikeln.

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit CDP i realtid till ett av dina önskade direktuppspelningsmål och ställt in ett dataflöde till respektive mål. Utgående data kan nu användas i målet för kundanalys eller andra dataåtgärder som du kanske vill utföra. Mer information finns på följande sidor:

* [Översikt över mål](../home.md)
* [Översikt över destinationskatalogen](../catalog/overview.md)
