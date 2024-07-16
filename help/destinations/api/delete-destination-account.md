---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;ta bort målkonton;ta bort;api
solution: Experience Platform
title: Ta bort ett målkonto med API:t för Flow Service
type: Tutorial
description: Lär dig hur du tar bort ett målkonto med API:t för Flow Service.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Ta bort ett målkonto med API:t för Flow Service

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

Innan du aktiverar data måste du ansluta till målet genom att först konfigurera ett målkonto. I den här självstudiekursen beskrivs stegen för att ta bort målkonton som inte längre behövs med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Det finns endast stöd för att ta bort målkonton i API:t för Flow Service. Det går inte att ta bort destinationskonton med hjälp av användargränssnittet i Experience Platform.

## Komma igång {#get-started}

Den här självstudiekursen kräver att du har ett giltigt anslutnings-ID. Anslutnings-ID representerar kontoanslutningen till målet. Om du inte har något giltigt anslutnings-ID väljer du önskat mål i [målkatalogen](../catalog/overview.md) och följer instruktionerna som beskrivs för att [ansluta till målet](../ui/connect-destination.md) innan du försöker med den här självstudien.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ta bort ett målkonto med API:t [!DNL Flow Service].

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om rubriken `x-sandbox-name` inte anges löses förfrågningar under sandlådan `prod`.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Hitta anslutnings-ID:t för målkontot som du vill ta bort {#find-connection-id}

>[!NOTE]
>I den här självstudien används [Airship-destinationen](../catalog/mobile-engagement/airship-attributes.md) som exempel, men de angivna stegen gäller för alla [tillgängliga destinationer](../catalog/overview.md).

Det första steget i att ta bort ett målkonto är att ta reda på det anslutnings-ID som motsvarar målkontot som du vill ta bort.

I användargränssnittet för Experience Platform bläddrar du till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** och markerar det konto som du vill ta bort genom att markera numret i kolumnen **[!UICONTROL Destinations]**.

![Välj målkonto som ska tas bort](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
>* [Använd användargränssnittet i Experience Platform](../ui/delete-destinations.md) för att ta bort befintliga dataflöden;
>* [Använd API:t för Flow Service ](delete-destination-dataflow.md) för att ta bort befintliga dataflöden.

När du har ett anslutnings-ID och har säkerställt att det inte finns några dataflöden till målkontot, kan du utföra en DELETE-begäran till [!DNL Flow Service]-API:t.

**API-format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Det unika `id`-värdet för anslutningen som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på anslutningen. API returnerar ett HTTP 404-fel (Hittades inte) som anger att målkontot har tagits bort.

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudiekursen följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

Genom att följa den här självstudiekursen har du använt API:t [!DNL Flow Service] för att ta bort befintliga målkonton. Mer information om hur du använder mål finns i [målöversikten](/help/destinations/home.md).