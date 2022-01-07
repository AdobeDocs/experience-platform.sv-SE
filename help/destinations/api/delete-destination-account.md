---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;ta bort destinationskonton;ta bort;api
solution: Experience Platform
title: Ta bort ett målkonto med API:t för Flow Service
type: Tutorial
description: Lär dig hur du tar bort ett målkonto med API:t för Flow Service.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Ta bort ett målkonto med API:t för Flow Service

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

Innan du aktiverar data måste du ansluta till målet genom att först konfigurera ett målkonto. I den här självstudiekursen beskrivs stegen för att ta bort destinationskonton som inte längre behövs med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Det finns endast stöd för att ta bort målkonton i API:t för Flow Service. Det går inte att ta bort destinationskonton med hjälp av användargränssnittet i Experience Platform.

## Komma igång {#get-started}

Den här självstudiekursen kräver att du har ett giltigt anslutnings-ID. Anslutnings-ID representerar kontoanslutningen till målet. Om du inte har något giltigt anslutnings-ID väljer du önskat mål på menyn [målkatalog](../catalog/overview.md) och följa de steg som beskrivs nedan för att [ansluta till målet](../ui/connect-destination.md) innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ta bort ett målkonto med hjälp av [!DNL Flow Service] API.

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om `x-sandbox-name` ingen rubrik har angetts, begäranden har lösts under `prod` sandlåda.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Hitta anslutnings-ID:t för målkontot som du vill ta bort {#find-connection-id}

>[!NOTE]
>I den här självstudiekursen används [Luftfartygets destination](../catalog/mobile-engagement/airship-attributes.md) som ett exempel, men de steg som beskrivs ovan gäller för alla [tillgängliga destinationer](../catalog/overview.md).

Det första steget i att ta bort ett målkonto är att ta reda på det anslutnings-ID som motsvarar målkontot som du vill ta bort.

I användargränssnittet för Experience Platform går du till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** och välj det konto du vill ta bort genom att markera numret i **[!UICONTROL Destinations]** kolumn.

![Välj målkonto att ta bort](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Därefter kan du hämta anslutnings-ID:t för målkontot från URL:en i webbläsaren.

![Hämta anslutnings-ID från URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Ta bort anslutning {#delete-connection}

>[!IMPORTANT]
>
>Innan du tar bort målkontot måste du ta bort alla befintliga dataflöden till målkontot.
>Om du vill ta bort befintliga dataflöden kan du läsa sidorna nedan:
>* [Använda användargränssnittet i Experience Platform](../ui/delete-destinations.md) ta bort befintliga dataflöden,
>* [Använda API:t för Flow Service](delete-destination-dataflow.md) om du vill ta bort befintliga dataflöden.


När du har ett anslutnings-ID och har säkerställt att det inte finns några dataflöden till destinationskontot utför du en DELETE-begäran till [!DNL Flow Service] API.

**API-format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Unika `id` värdet för anslutningen som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på anslutningen. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att målkontot har tagits bort.

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudien följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!DNL Flow Service] API för att ta bort befintliga målkonton.
