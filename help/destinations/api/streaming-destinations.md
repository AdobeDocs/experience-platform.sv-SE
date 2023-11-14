---
keywords: Experience Platform;home;populära topics; API tutorials; streaming destination API; Platform
solution: Experience Platform
title: Ansluta till direktuppspelningsmål och aktivera data med API:t för Flow Service i Adobe Experience Platform
description: I det här dokumentet beskrivs hur du skapar direktuppspelningsmål med hjälp av Adobe Experience Platform API
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '2231'
ht-degree: 0%

---

# Ansluta till direktuppspelningsmål och aktivera data med API:t för Flow Service

>[!IMPORTANT]
> 
>Om du vill ansluta till ett mål behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions).
>
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
>
>Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

I den här självstudien visas hur du använder API-anrop för att ansluta till dina Adobe Experience Platform-data, skapa en anslutning till ett direktuppspelat molnlagringsmål ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) eller [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md)), skapa ett dataflöde till det nya målet och aktivera data till det nya målet.

I den här självstudiekursen används [!DNL Amazon Kinesis] mål i alla exempel, men stegen är identiska för [!DNL Azure Event Hubs].

![Översikt - stegen för att skapa ett direktuppspelningsmål och aktivera målgrupper](../assets/api/streaming-destination/overview.png)

Om du föredrar att använda användargränssnittet i Platform för att ansluta till ett mål och aktivera data finns mer information i [Anslut ett mål](../ui/connect-destination.md) och [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../ui/activate-segment-streaming-destinations.md) självstudier.

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] är registersystemet för dataplats och datalinje inom Experience Platform.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna aktivera data för direktuppspelningsmål i Platform.

### Samla in nödvändiga inloggningsuppgifter

För att slutföra stegen i den här självstudiekursen bör du ha följande autentiseringsuppgifter tillgängliga, beroende på vilken typ av mål du ansluter och aktiverar målgrupper till.

* För [!DNL Amazon Kinesis] anslutningar: `accessKeyId`, `secretKey`, `region` eller `connectionUrl`
* För [!DNL Azure Event Hubs] anslutningar: `sasKeyName`, `sasKey`, `namespace`

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska och valfria rubriker {#gather-values}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Resurser i Experience Platform kan isoleras till specifika virtuella sandlådor. I förfrågningar till plattforms-API:er kan du ange namnet och ID:t för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

### Dokumentation för Swagger {#swagger-docs}

Du hittar referensdokumentation för alla API-anrop i den här självstudiekursen i Swagger. Se [API-dokumentation för Flow Service på Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Vi rekommenderar att du använder den här självstudiekursen och dokumentationssidan för Swagger parallellt.

## Hämta listan över tillgängliga mål för direktuppspelning {#get-the-list-of-available-streaming-destinations}

![Översiktssteg för målsteg 1](../assets/api/streaming-destination/step1.png)

Som ett första steg bör du bestämma vilket mål för direktuppspelning som data ska aktiveras till. Börja med att ringa ett samtal för att begära en lista över tillgängliga destinationer som du kan ansluta och aktivera målgrupper till. Utför följande GET-förfrågan till `connectionSpecs` slutpunkt för att returnera en lista över tillgängliga destinationer:

**API-format**

```http
GET /connectionSpecs
```

**Begäran**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Svar**

Ett lyckat svar innehåller en lista över tillgängliga destinationer och deras unika identifierare (`id`). Lagra värdet för destinationen som du tänker använda, vilket krävs i ytterligare steg. Om du till exempel vill ansluta och leverera målgrupper till [!DNL Amazon Kinesis] eller [!DNL Azure Event Hubs]söker du efter följande utdrag i svaret:

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
2. Med basanslutnings-ID:t gör du sedan ett nytt anrop där du skapar en källanslutning som upprättar anslutningen till dina Experience Platform-data.


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
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: Använd det ID du fick i föregående steg.
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspec-ID för profiltjänsten - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen till profiltjänsten. Detta bekräftar att du har anslutit till dina Experience Platform-data. Lagra det här värdet som det behövs i ett senare steg.

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
>Exemplet nedan innehåller kodkommentarer med prefix `//`. Dessa kommentarer visar var olika värden måste användas för olika direktuppspelningsmål. Ta bort kommentarerna innan du använder fragmentet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

* `{CONNECTION_SPEC_ID}`: Använd det anslutningsspec-ID som du fick i steget [Hämta listan över tillgängliga mål](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: fyll i namnet på ditt mål för direktuppspelning: `Aws Kinesis authentication credentials` eller `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *För [!DNL Amazon Kinesis] anslutningar.* Ditt åtkomst-ID för din lagringsplats för Amazon Kinesis.
* `{SECRET_KEY}`: *För [!DNL Amazon Kinesis] anslutningar.* Din hemliga nyckel för din lagringsplats för Amazon Kinesis.
* `{REGION}`: *För [!DNL Amazon Kinesis] anslutningar.* Regionen i ditt [!DNL Amazon Kinesis] konto där Platform kan strömma era data.
* `{SAS_KEY_NAME}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i ditt SAS-nyckelnamn. Lär dig mer om autentisering av [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i SAS-nyckeln. Lär dig mer om autentisering av [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i [!DNL Azure Event Hubs] namnutrymme där Platform direktuppspelar data. Mer information finns i [Skapa ett namnutrymme för händelsehubbar](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) i [!DNL Microsoft] dokumentation.

**Svar**

Ett godkänt svar innehåller basanslutningens unika identifierare (`id`). Lagra det här värdet som det behövs i nästa steg för att skapa en målanslutning.

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
>Exemplet nedan innehåller kodkommentarer med prefix `//`. Dessa kommentarer visar var olika värden måste användas för olika direktuppspelningsmål. Ta bort kommentarerna innan du använder fragmentet.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
* `{CONNECTION_SPEC_ID}`: Använd anslutningsspecifikationen som du fick i steget [Hämta listan över tillgängliga mål](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *För [!DNL Amazon Kinesis] anslutningar.* Ange namnet på din befintliga dataström i din [!DNL Amazon Kinesis] konto. Plattformen exporterar data till den här strömmen.
* `{REGION}`: *För [!DNL Amazon Kinesis] anslutningar.* Den region på ditt Amazon Kinesis-konto där Platform strömmar dina data.
* `{EVENT_HUB_NAME}`: *För [!DNL Azure Event Hubs] anslutningar.* Fyll i [!DNL Azure Event Hub] namn där plattformen ska strömma dina data. Mer information finns i [Skapa en händelsehubb](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) i [!DNL Microsoft] dokumentation.

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade målanslutningen till ditt mål för direktuppspelning. Lagra det här värdet som det behövs i senare steg.

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
-H 'x-gw-ims-org-id: {ORG_ID}' \
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

* `{FLOW_SPEC_ID}`: Flödesspekt-ID för profilbaserade mål är `71471eba-b620-49e4-90fd-23f1fa0174d8`. Använd det här värdet i anropet.
* `{SOURCE_CONNECTION_ID}`: Använd det källanslutnings-ID som du fick i steget [Anslut till din Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Använd det ID för målanslutning som du fick i steget [Anslut till direktuppspelningsmål](#connect-to-streaming-destination).

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet och `etag`. Notera båda värdena nedåt. som ni kommer att göra i nästa steg, för att aktivera målgrupper.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivera data till ditt nya mål {#activate-data}

![Översikt över destinationssteg steg 5](../assets/api/streaming-destination/step5.png)

När du har skapat alla anslutningar och dataflödet kan du nu aktivera dina profildata till direktuppspelningsplattformen. I det här steget väljer du vilka målgrupper och vilka profilattribut du skickar till målet, och du kan schemalägga och skicka data till målet.

Om du vill aktivera målgrupper till ditt nya mål måste du utföra en JSON PATCH-åtgärd, som i exemplet nedan. Du kan aktivera flera målgrupper och profilattribut i ett samtal. Mer information om JSON PATCH finns i [RFC-specifikation](https://tools.ietf.org/html/rfc6902).

**API-format**

```http
PATCH /flows
```

**Begäran**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
        "name": "Name of the audience that you are activating",
        "description": "Description of the audience that you are activating",
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

| Egenskap | Beskrivning |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Använd ID:t för dataflödet som du skapade i föregående steg i URL-adressen. |
| `{ETAG}` | Skaffa `{ETAG}` från svaret i föregående steg, [Skapa ett dataflöde](#create-dataflow). Svarsformatet i föregående steg har escape-citattecken. Du måste använda värdena för unescape-konvertering i huvudet i begäran. Se exemplet nedan: <br> <ul><li>Exempel på svar: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Värde att använda i din begäran: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Värdet för etag uppdateras med varje lyckad uppdatering av ett dataflöde. |
| `{SEGMENT_ID}` | Ange det målgrupps-ID som du vill exportera till det här målet. Information om hur du hämtar målgrupps-ID:n för de målgrupper du vill aktivera finns i [hämta en publikdefinition](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) i API-referensen för Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Exempel: `"person.lastName"` |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. Använd kommandot `add` operation. |
| `path` | Definierar den del av flödet som ska uppdateras. När du lägger till en målgrupp i ett dataflöde använder du den sökväg som anges i exemplet. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |
| `id` | Ange ID:t för målgruppen som du lägger till i måldataflödet. |
| `name` | *Valfritt*. Ange namnet på målgruppen som du lägger till i måldataflödet. Observera att det här fältet inte är obligatoriskt och att du kan lägga till en målgrupp i måldataflödet utan att ange dess namn. |

**Svar**

Håll utkik efter 202 OK-svar. Ingen svarstext returneras. Om du vill verifiera att begäran var korrekt går du till nästa steg, Validera dataflödet.

## Validera dataflödet

![Översiktssteg för målsteg 6](../assets/api/streaming-destination/step6.png)

Som ett sista steg i självstudiekursen bör du validera att målgrupper och profilattribut verkligen har mappats korrekt till dataflödet.

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
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Använd dataflödet från föregående steg.
* `{ETAG}`: Använd taggen från föregående steg.

**Svar**

Det returnerade svaret ska innehålla `transformations` anger målgrupper och profilattribut som du skickade i föregående steg. Ett exempel `transformations` parametern i svaret kan se ut så här:

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
> Förutom profilattributen och målgrupperna i steget [Aktivera data till ditt nya mål](#activate-data), exporterade data i [!DNL AWS Kinesis] och [!DNL Azure Event Hubs] innehåller även information om identitetskartan. Detta representerar identiteten för de exporterade profilerna (till exempel [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), mobilt ID, Google ID, e-postadress osv.). Se ett exempel nedan.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "realized"
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

## Använda [!DNL Postman] samlingar att ansluta till direktuppspelningsmål  {#collections}

Om du vill ansluta till de direktuppspelningsmål som beskrivs i den här självstudiekursen på ett effektivare sätt kan du använda [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] är ett verktyg som du kan använda för att göra API-anrop och hantera bibliotek med fördefinierade anrop och miljöer.

Följande gäller för den här självstudiekursen [!DNL Postman] samlingar har bifogats:

* [!DNL AWS Kinesis] [!DNL Postman] samling
* [!DNL Azure Event Hubs] [!DNL Postman] samling

Klicka [här](../assets/api/streaming-destination/DestinationPostmanCollection.zip) för att hämta samlingsarkivet.

Varje samling innehåller nödvändiga begäranden och miljövariabler för [!DNL AWS Kinesis]och [!DNL Azure Event Hub], respektive

### Så här använder du [!DNL Postman] samlingar {#how-to-use-postman-collections}

För att ansluta till målen med hjälp av den bifogade [!DNL Postman] samlingar, följ dessa steg:

* Hämta och installera [!DNL Postman];
* [Ladda ned](../assets/api/streaming-destination/DestinationPostmanCollection.zip) och packa upp de bifogade samlingarna,
* Importera samlingar från deras motsvarande mappar till [!DNL Postman];
* Fyll i miljövariablerna enligt instruktionerna i denna artikel.
* Kör [!DNL API] förfrågningar från [!DNL Postman]enligt instruktionerna i den här artikeln.

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudiekursen följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](/help/landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](/help/landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen för mer information om hur du tolkar felsvar.

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du anslutit plattformen till ett av dina önskade direktuppspelningsmål och konfigurerat ett dataflöde till respektive mål. Utgående data kan nu användas i målet för kundanalys eller andra dataåtgärder som du kanske vill utföra. Mer information finns på följande sidor:

* [Översikt över mål](../home.md)
* [Översikt över destinationskatalogen](../catalog/overview.md)
