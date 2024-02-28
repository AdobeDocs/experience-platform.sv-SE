---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-slutpunkt för samtycke
description: Lär dig hur du hanterar förfrågningar om kundsamtycke för Experience Cloud-program med Privacy Service-API:t.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Slutpunkt för samtycke

Vissa bestämmelser kräver uttryckligt samtycke från kunden innan deras personuppgifter kan samlas in. The `/consent` slutpunkt i [!DNL Privacy Service] Med API kan ni behandla förfrågningar om kundsamtycke och integrera dem i ert sekretessarbetsflöde.

Innan du använder den här handboken bör du läsa [komma igång](./getting-started.md) guide för information om nödvändiga autentiseringshuvuden som presenteras i exemplet på API-anrop nedan.

## Bearbeta en begäran om kundgodkännande

Begäran om samtycke behandlas genom att en POST skickas till `/consent` slutpunkt.

**API-format**

```http
POST /consent
```

**Begäran**

Följande begäran skapar ett nytt medgivandejobb för användar-ID:n som anges i `entities` array.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `optOutOfSale` | Om värdet är true visar det att användarna som anges under `entities` vill avanmäla försäljning eller delning av personuppgifter. |
| `entities` | En array med objekt som anger vilka användare som medgivandebegäran gäller för. Varje objekt innehåller en `namespace` och en array med `values` för att matcha enskilda användare med det namnutrymmet. |
| `nameSpace` | Varje objekt i `entities` måste innehålla en av [standardidentitetsnamnutrymmen](./appendix.md#standard-namespaces) känns igen av Privacy Service-API:t. |
| `values` | En array med värden för varje användare, som motsvarar den angivna `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mer information om hur du avgör vilka ID-värden för kunder som ska skickas till [!DNL Privacy Service], se guiden på [tillhandahålla identitetsdata](../identity-data.md).

**Svar**

Ett godkänt svar returnerar HTTP-status 202 (Accepterad) utan nyttolast, vilket anger att begäran accepterades av [!DNL Privacy Service] och genomgår bearbetning.
