---
keywords: Experience Platform;hem;populära ämnen;källor;API;utforska;flödestjänst
title: Utforska en Source i tabellformat med API:t för Flow Service
description: I den här självstudien används API:t för Flow Service för att utforska innehållet och strukturen i en tabellbaserad källa.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Utforska datatabeller med API:t [!DNL Flow Service]

I den här självstudiekursen beskrivs hur du utforskar och förhandsgranskar strukturen och innehållet i datatabeller med hjälp av API:t [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> För att kunna utforska datatabellerna måste du redan ha ett giltigt ID för basanslutning för en tabellkälla. Om du inte har det här ID:t kan du följa de här självstudiekurserna för hur du skapar ett grundläggande anslutnings-ID för en tabellkälla: <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Kundens framgång](../../../home.md#customer-success)</li><li>[Databas](../../../home.md#database)</li><li>[E-handel](../../../home.md#ecommerce)</li><li>[Automatisering av marknadsföring](../../../home.md#marketing-automation)</li><li>[Betalningar](../../../home.md#payments)</li><li>[Protokoll](../../../home.md#protocols)</li></ul>

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../landing/api-guide.md).

## Utforska era datatabeller

Du kan hämta information om strukturen för dina datatabeller genom att göra en GET-förfrågan till [!DNL Flow Service]-API:t och samtidigt ange källans anslutnings-ID.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Källans grundläggande anslutnings-ID. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med tabeller från källan. Hitta tabellen som du vill hämta till Platform och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect tabellstrukturen

Om du vill inspektera innehållet i datatabellerna utför du en GET-förfrågan till [!DNL Flow Service]-API:t samtidigt som du anger sökvägen till en tabell som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Källans grundläggande anslutnings-ID. |
| `{TABLE_PATH}` | Egenskapen path för den tabell som du vill inspektera. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om innehållet och strukturen i den angivna tabellen. Information om var och en av tabellens kolumner finns inom elementen i arrayen `columns`.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du samlat in information om strukturen och innehållet i dina datatabeller. Dessutom har du hämtat sökvägen till tabellen som du vill importera till Platform. Du kan använda den här informationen för att skapa en källanslutning och ett dataflöde för att överföra data till plattformen. I följande självstudiekurser finns mer information om hur du skapar en källanslutning och ett dataflöde med API:t [!DNL Flow Service]:

* [Advertising-källor](../collect/advertising.md)
* [CRM-källor](../collect/crm.md)
* [Kundframgångskällor](../collect/customer-success.md)
* [Databaskällor](../collect/database-nosql.md)
* [E-handelskällor](../collect/ecommerce.md)
* [Källor för automatiserad marknadsföring](../collect/marketing-automation.md)
* [Betalningskällor](../collect/payments.md)
* [Protokollkällor](../collect/protocols.md)
