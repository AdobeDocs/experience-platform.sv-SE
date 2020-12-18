---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Skapa en Salesforce-koppling med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta plattformen till ett Salesforce-konto för att samla in CRM-data.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---


# Skapa en [!DNL Salesforce]-koppling med hjälp av API:t [!DNL Flow Service]

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t [!DNL Flow Service] för att vägleda dig genom stegen för att ansluta [!DNL Platform] till ett [!DNL Salesforce]-konto för att samla in CRM-data.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Platform] till ett [!DNL Salesforce]-konto med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Salesforce] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en för [!DNL Salesforce]-källinstansen. |
| `username` | Användarnamnet för användarkontot [!DNL Salesforce]. |
| `password` | Lösenordet för användarkontot [!DNL Salesforce]. |
| `securityToken` | Säkerhetstoken för användarkontot [!DNL Salesforce]. |

Mer information om hur du kommer igång finns i [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](../../../../../tutorials/authentication.md) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Salesforce]-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Salesforce]-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Salesforce] är `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Salesforce]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Salesforce]-konto. |
| `auth.params.securityToken` | Säkerhetstoken som är associerad med ditt [!DNL Salesforce]-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för ditt [!DNL Salesforce]-konto har hämtats i föregående steg. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Salesforce]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta ID i nästa självstudiekurs när du lär dig hur du [utforskar CRM-system med API:t för Flow Service](../../explore/crm.md).