---
keywords: Experience Platform;home;populära topics;Teradata Vantage
title: Skapa en Teradata Vantage Base-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Teradata Vantage med API:t för Flow Service.
exl-id: 88707dca-3c7a-43c7-9d71-473ad9715fc6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Skapa en [!DNL Teradata Vantage]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Teradata Vantage] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Teradata Vantage] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Teradata Vantage] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | En anslutningssträng är en sträng som innehåller information om en datakälla och hur du kan ansluta till den. Anslutningssträngsmönstret för [!DNL Teradata Vantage] är `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Teradata Vantage] är: `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

Mer information om hur du kommer igång finns i det här [[!DNL Teradata Vantage] dokumentet](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Teradata Vantage]-autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Teradata Vantage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till din [!DNL Teradata Vantage]-instans. Anslutningssträngsmönstret för [!DNL Teradata Vantage] är `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Teradata Vantage]: `2fa8af9c-2d1a-43ea-a253-f00a00c74412`. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Genom att följa den här självstudiekursen har du skapat en [!DNL Teradata Vantage]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
