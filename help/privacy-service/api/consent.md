---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-slutpunkt för samtycke
topic: developer guide
description: Lär dig hur du hanterar förfrågningar om kundsamtycke för Experience Cloud-program med Privacy Service-API:t.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Slutpunkt för samtycke

Vissa bestämmelser kräver uttryckligt samtycke från kunden innan deras personuppgifter kan samlas in. Med slutpunkten `/consent` i API:t [!DNL Privacy Service] kan du bearbeta förfrågningar om kundsamtycke och integrera dem i ditt sekretessarbetsflöde.

Innan du använder den här guiden bör du läsa avsnittet [komma igång](./getting-started.md) för information om de autentiseringshuvuden som visas i exemplet på API-anrop nedan.

## Bearbeta en begäran om kundgodkännande

Godkännandebegäranden bearbetas genom att en POST begärs till `/consent`-slutpunkten.

**API-format**

```http
POST /consent
```

**Begäran**

Följande begäran skapar ett nytt medgivandejobb för de användar-ID som anges i `entities`-arrayen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optOutOfSale` | Om värdet är true anger det att de användare som anges i `entities` vill avanmäla sig från försäljning eller delning av sina personuppgifter. |
| `entities` | En array med objekt som anger vilka användare som medgivandebegäran gäller för. Varje objekt innehåller en `namespace` och en array med `values` som matchar enskilda användare med det namnutrymmet. |
| `nameSpace` | Varje objekt i `entities`-arrayen måste innehålla ett av de [standardidentitetsnamnutrymmen](./appendix.md#standard-namespaces) som känns igen av Privacy Service-API:t. |
| `values` | En array med värden för varje användare, som motsvarar den angivna `nameSpace`. |

>[!NOTE]
>
>Mer information om hur du avgör vilka värden för kundidentitet som ska skickas till [!DNL Privacy Service] finns i guiden [som tillhandahåller identitetsdata](../identity-data.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) utan nyttolast, vilket anger att begäran accepterades av [!DNL Privacy Service] och håller på att bearbetas.