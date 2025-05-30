---
keywords: Experience Platform;hemmabruk;populära ämnen;e-handel;e-handel
solution: Experience Platform
title: Utforska en e-handelsanslutning med API:t för flödestjänsten
description: I den här självstudien används API:t för Flow Service för att utforska e-handelsanslutningar.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Utforska en eCommerce-anslutning med API:t [!DNL Flow Service]

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används [!DNL Flow Service]-API:t för att utforska en anslutning från tredje part, **[!UICONTROL eCommerce]**.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du får möjlighet att strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en **[!UICONTROL eCommerce]**-anslutning med API:t [!DNL Flow Service].

### Hämta ett anslutnings-ID

För att kunna utforska din **[!UICONTROL eCommerce]**-anslutning med [!DNL Experience Platform] API:er måste du ha ett giltigt anslutnings-ID. Om du inte redan har en anslutning för den **[!UICONTROL eCommerce]**-anslutning du vill arbeta med kan du skapa en genom följande självstudie:

* [Förminska](../create/ecommerce/shopify.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en extra medietypsrubrik:

* `Content-Type: application/json`

## Utforska era datatabeller

Med ditt anslutnings-ID för **[!UICONTROL eCommerce]** kan du utforska datatabeller genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Experience Platform].

**API-format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONNECTION_ID}` | Ditt **[!UICONTROL eCommerce]**-anslutnings-ID. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en matris med tabeller från din **[!UICONTROL eCommerce]**-anslutning. Hitta tabellen som du vill hämta till [!DNL Experience Platform] och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspektera strukturen i en tabell

Om du vill inspektera strukturen för en tabell från din **[!UICONTROL eCommerce]**-anslutning utför du en GET-begäran samtidigt som du anger sökvägen till en tabell i en `object` -frågeparameter.

**API-format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Anslutnings-ID för din **[!UICONTROL eCommerce]**-anslutning. |
| `{TABLE_PATH}` | Sökvägen till en tabell i din **[!UICONTROL eCommerce]**-anslutning. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den angivna tabellen. Information om var och en av tabellens kolumner finns inom elementen i arrayen `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Nästa steg

Genom att följa den här självstudien har du undersökt din **[!UICONTROL eCommerce]**-anslutning, hittat sökvägen till tabellen som du vill importera till [!DNL Experience Platform] och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in e-handelsdata och hämta dem till Experience Platform](../collect/ecommerce.md).
