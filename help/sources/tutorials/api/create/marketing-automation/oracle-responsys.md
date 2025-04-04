---
keywords: Experience Platform;home;populära topics;Oracle;
title: (Beta) Skapa en Oracle Responsys Base Connection med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Responsys med API:t för Flow Service.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# (Beta) Skapa en [!DNL Oracle Responsys]-basanslutning med API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Oracle Responsys] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Oracle Responsys] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Responsys] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Oracle Responsys] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `endpoint` | URL:en för REST-autentiseringsslutpunkten för din [!DNL Oracle Responsys]-instans. |
| `clientId` | Klient-ID för din [!DNL Oracle Responsys]-instans. |
| `clientSecret` | Klienthemligheten för din [!DNL Oracle Responsys]-instans. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Värdet för anslutningsspecifikations-ID:t för källan [!DNL Oracle Responsys] är fast som: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Responsys] finns i [[!DNL Oracle Responsys] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Oracle Responsys]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på din [!DNL Oracle Responsys]-basanslutning. Du bör ange ett beskrivande namn eftersom du kan använda det här värdet för att leta upp din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan ta med för att ge ytterligare information om din basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.endpoint` | URL:en för REST-autentiseringsslutpunkten för [!DNL Oracle Responsys]-servern. |
| `auth.params.clientId` | Klient-ID för din [!DNL Oracle Responsys]-instans. |
| `auth.params.clientSecret` | Klienthemligheten för din [!DNL Oracle Responsys]-instans. |
| `connectionSpec.id` | Värdet för anslutningsspecifikations-ID:t för källan [!DNL Oracle Responsys] är fast som: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Oracle Responsys]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att överföra automatiserade marknadsföringsdata till Experience Platform med  [!DNL Flow Service] API](../../collect/marketing-automation.md)
