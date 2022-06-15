---
keywords: Experience Platform;hem;populära ämnen;veeva crm;Veeva CRM;Veeva;
solution: Experience Platform
title: Skapa en Vector CRM-basanslutning med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Veeva CRM med API:t för Flow Service.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: ea20a850a5d83f648c699119913aa31e2ea16233
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# Skapa en [!DNL Veeva CRM] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Veeva CRM] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Veeva CRM] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Veeva CRM]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en till [!DNL Veeva CRM] -instans. |
| `username` | Användarnamnsvärdet för din [!DNL Veeva CRM] konto. |
| `password` | Lösenordsvärdet för [!DNL Veeva CRM] konto. |
| `securityToken` | Säkerhetstoken för din [!DNL Veeva CRM] -instans. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Veeva CRM] är: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Mer information om dessa värden finns i [[!DNL Veeva CRM] dokument](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Veeva CRM] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på [!DNL Veeva CRM] basanslutning. Du kan använda det här namnet för att söka efter [!DNL Veeva CRM] basanslutning. |
| `description` | En valfri beskrivning av [!DNL Veeva CRM] basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.environmentUrl` | URL:en till [!DNL Veeva CRM] -instans. |
| `auth.params.username` | Användarnamnsvärdet för din [!DNL Veeva CRM] konto. |
| `auth.params.password` | Lösenordsvärdet för [!DNL Veeva CRM] konto. |
| `auth.params.securityToken` | Säkerhetstoken för din [!DNL Veeva CRM] -instans. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Veeva CRM] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med [!DNL Flow Service] API](../../collect/crm.md)
