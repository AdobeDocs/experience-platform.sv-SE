---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-basanslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter plattformen till ett Microsoft Dynamics-konto med API:t för Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Skapa en [!DNL Microsoft Dynamics] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Microsoft Dynamics] (nedan kallad[!DNL Dynamics]&quot;) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta plattformen till ett Dynamics-konto med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta till [!DNL Dynamics]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänstens URL [!DNL Dynamics] -instans. |
| `username` | Ditt användarnamn [!DNL Dynamics] användarkonto. |
| `password` | Lösenordet för [!DNL Dynamics] konto. |
| `servicePrincipalId` | Klient-ID för din [!DNL Dynamics] konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Dynamics] är: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Mer information om hur du kommer igång finns på [this [!DNL Dynamics] dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Dynamics] autentiseringsuppgifter som en del av parametrarna för begäran.

### Skapa en [!DNL Dynamics] basanslutning med grundläggande autentisering

Skapa en [!DNL Dynamics] basanslutning med grundläggande autentisering, gör en POST-förfrågan till [!DNL Flow Service] API när du anger värden för anslutningen `serviceUri`, `username`och `password`.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med din [!DNL Dynamics] -instans. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Dynamics] konto. |
| `auth.params.password` | Lösenordet som är kopplat till [!DNL Dynamics] konto. |
| `connectionSpec.id` | The [!DNL Dynamics] anslutningsspecifikation-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Skapa en [!DNL Dynamics] basanslutning med huvudnyckelbaserad autentisering

Skapa en [!DNL Dynamics] basanslutning med huvudnyckelbaserad autentisering, gör en POST-förfrågan till [!DNL Flow Service] API när du anger värden för anslutningen `serviceUri`, `servicePrincipalId`och `servicePrincipalKey`.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med din [!DNL Dynamics] -instans. |
| `auth.params.servicePrincipalId` | Klient-ID för din [!DNL Dynamics] konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `auth.params.servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `connectionSpec.id` | The [!DNL Dynamics] anslutningsspecifikation-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Microsoft Dynamics] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med [!DNL Flow Service] API](../../collect/crm.md)
