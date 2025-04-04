---
title: Skapa en Microsoft Dynamics-basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Experience Platform till ett Microsoft Dynamics-konto med API:t för Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---

# Anslut [!DNL Microsoft Dynamics] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill veta hur du kan ansluta din [!DNL Microsoft Dynamics]-källa till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta Experience Platform till ett Dynamics-konto med API:t [!DNL Flow Service].

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

## Skapa en basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Dynamics]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Dynamics]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill skapa en [!DNL Dynamics]-basanslutning med grundläggande autentisering gör du en POST-begäran till [!DNL Flow Service]-API:t och anger värden för din anslutnings `serviceUri`, `username` och `password`.

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL Dynamics]-källa med grundläggande autentisering.

+++Markera för att visa ett exempel på en begäran

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

**Svar**

Ett svar returnerar den nyskapade basanslutningen, inklusive dess unika identifierare (`id`).

+++Markera för att visa svarsexempel

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Huvudnyckelbaserad autentisering för tjänst]

Om du vill skapa en [!DNL Dynamics]-basanslutning med huvudnyckelbaserad autentisering skapar du en POST-begäran till [!DNL Flow Service]-API:t och anger värden för `serviceUri`, `servicePrincipalId` och `servicePrincipalKey` för anslutningen.

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL Dynamics]-källa med grundläggande nyckelbaserad autentisering av tjänstens huvudnyckel.

+++Markera för att visa ett exempel på en begäran

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

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

+++Markera för att visa svarsexempel

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Utforska era datatabeller

Om du vill utforska dina [!DNL Dynamics]-datatabeller skickar du en GET-begäran till `/connections/{BASE_CONNECTION_ID}/explore`-slutpunkten och anger ditt grundläggande anslutnings-ID som en del av frågeparametrarna.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen. Använd det här ID:t för att utforska källans innehåll och struktur. |

**Begäran**

Följande begäran hämtar listan med tillgängliga tabeller och vyer för en [!DNL Dynamics]-källa med basanslutnings-ID: `dd668808-25da-493f-8782-f3433b976d1e`.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett lyckat svar returnerar katalogen [!DNL Dynamics] för tabeller och vyer på rotnivån.

+++Markera för att visa svarsexempel

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### Använd primärnyckeln för att optimera datautforskandet

>[!NOTE]
>
>Du kan bara använda attribut som inte är sökbara när du använder primärnyckeln för optimering.

Du kan optimera utforska frågor genom att ange `primaryKey` som en del av dina frågeparametrar. Du måste ange primärnyckeln för tabellen [!DNL Dynamics] när du inkluderar `primaryKey` som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen. Använd det här ID:t för att utforska källans innehåll och struktur. |
| `preview` | Ett booleskt värde som möjliggör förhandsgranskning av data. |
| `{OBJECT}` | Det [!DNL Dynamics]-objekt som du vill utforska. |
| `{OBJECT_TYPE}` | Objektets typ. |
| `previewCount` | En begränsning som begränsar den returnerade förhandsvisningen till ett visst antal poster. |
| `{PRIMARY_KEY}` | Primärnyckeln för tabellen som du hämtar för förhandsgranskning. |

**Begäran**

+++Markera för att visa ett exempel på en begäran

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## Inspektera strukturen i en tabell

Om du vill inspektera strukturen för en viss tabell gör du en GET-begäran till `/connections/{BASE_CONNECTION_ID}/explore` och anger sökvägen till den specifika tabellen som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Frågeparameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen. Använd det här ID:t för att utforska källans innehåll och struktur. |
| `{TABLE_PATH}` | Sökvägen till den tabell som du vill utforska. |

**Begäran**

Följande begäran hämtar strukturen och innehållet i en [!DNL Dynamics]-tabell med sökvägen `workflowdependency`.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett godkänt svar returnerar innehållet i sökvägen `workflowdependency`.

+++Markera för att visa svarsexempel

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Granska strukturen för en vy

I [!DNL Dynamics] refererar en vy till de kolumner som ska visas, bredden på varje kolumn, standardsystemet där en lista med poster sorteras och standardfiltren som används för att begränsa vilka poster som ska visas i listan.

Om du vill inspektera strukturen för en vy gör du en GET-förfrågan till `/connections/{BASE_CONNECTION_ID}/explore` och anger visningssökvägen i frågeparametrarna. Dessutom måste du ange `objectType` som `view`.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Frågeparameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen. Använd det här ID:t för att utforska källans innehåll och struktur. |
| `{VIEW_PATH}` | Sökvägen till den vy som du vill inspektera. |

**Begäran**

Följande begäran hämtar `accountView1`.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett lyckat svar returnerar strukturen för `accountView1`.

+++Markera för att visa svarsexempel

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Förhandsgranska entitetstypvy

Om du vill förhandsgranska innehållet i en vy skickar du en GET-begäran till `/connections/{BASE_CONNECTION_ID}/explore` och tar med vysökvägen samt `preview=true` i frågeparametrarna.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Frågeparameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen. Använd det här ID:t för att utforska källans innehåll och struktur. |
| `{VIEW_PATH}` | Sökvägen till den vy som du vill inspektera. |


**Begäran**

Följande begäran förhandsgranskar innehållet i `accountView1`.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett godkänt svar returnerar innehållet i `accountView1`.

+++Markera för att visa svarsexempel

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Skapa en källanslutning till importvyn

Om du vill skapa en källanslutning och importera en vy gör du en POST-begäran till `/sourceConnections`-slutpunkten, anger tabellnamnet och anger `entityType` as `view` i begärandetexten.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en [!DNL Dynamics]-källanslutning och importerar vyer.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Svar**

Ett lyckat svar returnerar det nyligen genererade källanslutnings-ID:t och dess motsvarande tagg.

+++Markera för att visa svarsexempel

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### Använd primärnyckeln för att optimera dataflödet

Du kan även optimera dataflödet för [!DNL Dynamics] genom att ange primärnyckeln som en del av textparametrarna för din begäran.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en [!DNL Dynamics]-källanslutning när primärnyckeln anges som `contactid`.

+++Markera för att visa ett exempel på en begäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `baseConnectionId` | ID för basanslutningen. |
| `data.format` | Dataformatet. |
| `params.tableName` | Namnet på tabellen i [!DNL Dynamics]. |
| `params.primaryKey` | Primärnyckeln för tabellen som optimerar frågor. |
| `connectionSpec.id` | Anslutningens spec-ID som motsvarar källan [!DNL Dynamics]. |

+++

**Svar**

Ett lyckat svar returnerar det nyligen genererade källanslutnings-ID:t och dess motsvarande tagg.

+++Markera för att visa svarsexempel

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Microsoft Dynamics]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till Experience Platform med  [!DNL Flow Service] API](../../collect/crm.md)
