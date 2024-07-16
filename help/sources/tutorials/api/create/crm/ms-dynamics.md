---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-basanslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter plattformen till ett Microsoft Dynamics-konto med API:t för Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Skapa en [!DNL Microsoft Dynamics]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Microsoft Dynamics] (kallas nedan [!DNL Dynamics]) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta plattformen till ett Dynamics-konto med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Dynamics] måste du ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `serviceUri` | Tjänst-URL:en för din [!DNL Dynamics]-instans. |
| `username` | Användarnamnet för ditt [!DNL Dynamics]-användarkonto. |
| `password` | Lösenordet för ditt [!DNL Dynamics]-konto. |

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `servicePrincipalId` | Klient-ID för ditt [!DNL Dynamics]-konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

>[!ENDTABS]

Mer information om hur du kommer igång finns i [det här [!DNL Dynamics] dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Dynamics]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL Dynamics] som en del av parametrarna för begäran.

### Skapa en [!DNL Dynamics]-basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Dynamics]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Det första steget i att skapa en källanslutning är att autentisera [!DNL Dynamics]-källan och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL Dynamics] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill skapa en [!DNL Dynamics]-basanslutning med grundläggande autentisering kan du göra en POST-förfrågan till [!DNL Flow Service]-API:t och ange värden för din anslutnings `serviceUri`, `username` och `password`.

+++Begäran

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
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med din [!DNL Dynamics]-instans. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Dynamics]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Dynamics]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++svar

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Huvudnyckelbaserad autentisering för tjänst]

Om du vill skapa en [!DNL Dynamics]-basanslutning med huvudnyckelbaserad autentisering, ska du göra en POST-förfrågan till [!DNL Flow Service]-API:t och ange värden för din anslutnings `serviceUri`, `servicePrincipalId` och `servicePrincipalKey`.

+++Begäran

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
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med din [!DNL Dynamics]-instans. |
| `auth.params.servicePrincipalId` | Klient-ID för ditt [!DNL Dynamics]-konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `auth.params.servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++svar

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Microsoft Dynamics]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/crm.md)
