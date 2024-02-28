---
keywords: Experience Platform;home;populära topics;query service;api guide;Query service;query service accounts;accounts;
solution: Experience Platform
title: API-slutpunkt för konton
description: Du kan skapa ett frågetjänstkonto för beständig .
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Kontoslutpunkt

I Adobe Experience Platform Query Service används konton för att skapa autentiseringsuppgifter som inte förfaller och som du kan använda med externa SQL-klienter. Du kan använda `/accounts` -slutpunkten i frågetjänstens API, som gör att du kan skapa, hämta, redigera och ta bort integrationskonton för frågetjänsten automatiskt (kallas även tekniskt konto).

## Komma igång

Slutpunkterna som används i den här guiden ingår i API:t för frågetjänsten. Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Skapa ett konto

Du kan skapa ett integrationskonto för frågetjänsten genom att göra en POST-förfrågan till `/accounts` slutpunkt.

**API-format**

```http
POST /accounts
```

**Begäran**

Följande begäran skapar ett nytt integrationskonto för frågetjänsten för din organisation.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `accountName` | **Obligatoriskt** Namnet på Query Service-integrationskontot. |
| `assignedToUser` | **Obligatoriskt** Det Adobe ID som Query Service-integrationskontot ska skapas för. |
| `credential` | *(Valfritt)* Autentiseringsuppgiften som används för integreringen av frågetjänsten. Om inget anges genereras en autentiseringsuppgift automatiskt. |
| `description` | *(Valfritt)* En beskrivning av Query Service-integrationskontot. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200, med information om ditt nya Query Service-integrationskonto. Du kan använda dessa kontouppgifter för att ansluta frågetjänsten till externa klienter.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `technicalAccountName` | Namnet på ditt Query Service-integrationskonto. |
| `technicalAccountId` | ID:t för ditt Query Service-integrationskonto. Detta, tillsammans med `credential`skapar ditt lösenord för ditt konto. |
| `credential` | Autentiseringsuppgifterna för ditt Query Service-integrationskonto. Detta, tillsammans med `technicalAccountId`skapar ditt lösenord för ditt konto. |

## Uppdatera ett konto

Du kan uppdatera integrationskontot för frågetjänsten genom att göra en PUT-förfrågan till `/accounts` slutpunkt.

**API-format**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID:t för det Query Service-integrationskonto som du vill uppdatera. |

**Begäran**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `accountName` | *(Valfritt)* Det uppdaterade namnet för Query Service-integrationskontot. |
| `assignedToUser` | *(Valfritt)* Det uppdaterade Adobe ID som Query Service-integrationskontot är länkat till. |
| `credential` | *(Valfritt)* Uppdaterade autentiseringsuppgifter för ditt Query Service-konto. |
| `description` | *(Valfritt)* Den uppdaterade beskrivningen för Query Service-integrationskontot. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nya Query Service-integrationskonto.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Visa alla konton

Du kan hämta en lista över alla integrationskonton för frågetjänsten genom att göra en GET-förfrågan till `/accounts` slutpunkt.

**API-format**

```http
GET /accounts
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över alla Query Service-integrationskonton.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Ta bort ett konto

Du kan ta bort integrationskontot för frågetjänsten genom att göra en DELETE-förfrågan till `/accounts` slutpunkt.

**API-format**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{ACCOUNT_ID}` | ID:t för det Query Service-integrationskonto som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med ett meddelande om att kontot har tagits bort.

```json
{
    "result": "Success"
}
```
