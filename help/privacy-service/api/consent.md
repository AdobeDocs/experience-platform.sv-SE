---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Godkännande
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Godkännande

Vissa bestämmelser kräver uttryckligt samtycke från kunden innan deras personuppgifter kan samlas in. Med `/consent` slutpunkten i [!DNL Privacy Service] API kan du bearbeta förfrågningar om kundsamtycke och integrera dem i ditt sekretessarbetsflöde.

Innan du använder den här guiden bör du läsa avsnittet [Komma igång](./getting-started.md) för information om de autentiseringshuvuden som visas i exemplet på API-anrop nedan.

## Bearbeta en begäran om kundgodkännande

Godkännandebegäranden bearbetas genom att en POST skickas till `/consent` slutpunkten.

**API-format**

```http
POST /consent
```

**Begäran**

Följande begäran skapar ett nytt medgivandejobb för de användar-ID som anges i `entities` arrayen.

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
| `optOutOfSale` | Om värdet är true innebär det att de användare som anges under `entities` vill avanmäla sig från försäljning eller delning av sina personuppgifter. |
| `entities` | En array med objekt som anger vilka användare som medgivandebegäran gäller för. Varje objekt innehåller en `namespace` och en array med `values` som matchar enskilda användare med det namnutrymmet. |
| `nameSpace` | Varje objekt i `entities` arrayen måste innehålla ett av de [standardnamnutrymmen](./appendix.md#standard-namespaces) för identitet som känns igen av Privacy Services-API:t. |
| `values` | En array med värden för varje användare, som motsvarar den angivna `nameSpace`. |

>[!NOTE]
>
>Mer information om hur du avgör vilka värden för kundidentitet som ska skickas till [!DNL Privacy Service]finns i guiden om [att tillhandahålla identitetsdata](../identity-data.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) utan nyttolast, vilket anger att begäran accepterades av [!DNL Privacy Service] och håller på att bearbetas.