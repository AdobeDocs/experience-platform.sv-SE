---
title: Använda Offer Decisioning med Experience Platform Web SDK
description: Adobe Experience Platform Web SDK kan leverera och återge personaliserade erbjudanden som hanteras i Offer Decisioning. Du kan skapa erbjudanden och andra relaterade objekt med Offer Decisioning gränssnitt eller API.
keywords: offertbeslut;beslut;Web SDK;Experience Platform Web SDK;personaliserade erbjudanden;leverera erbjudanden;erbjudandeleverans;erbjudandepersonalisering;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Använda Offer Decisioning med Experience Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kan leverera och återge personaliserade erbjudanden som hanteras i Offer Decisioning. Du kan skapa erbjudanden och andra relaterade objekt med Offer Decisioning användargränssnitt (UI) eller API:er.

## Förhandskrav

* Organisationen är aktiverad för kantbeslut
* Erbjudanden, skapade aktiviteter
* Datastream publiceras

## Terminologi

Det är viktigt att förstå följande terminologi när du arbetar med Offer Decisioning. Om du vill ha mer information och visa ytterligare villkor går du till [Offer Decisioning-ordlistan](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html?lang=sv-SE).

* **Beslutsomfattningar:** För Offer Decisioning är beslutsomfattningar de Base64-kodade strängarna för JSON som innehåller de aktivitets- och placerings-ID som du vill att beslutsprocessen för erbjudandet ska använda för att föreslå erbjudanden.

  *Beslutsomfattnings-JSON:*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *Beslutsomfattarens Base64-kodade sträng:*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >Du kan kopiera värdet för beslutsomfånget från sidan **Aktivitetsöversikt** i användargränssnittet.

  ![Inställningar för beslutskopiering.](assets/decision-scope-copy.png)

* **Datastreams:** Mer information finns i dokumentationen för [datastreams](/help/datastreams/overview.md).

* **Identitet**: Mer information finns i den här dokumentationen som beskriver hur [Experience Platform Web SDK använder identitetstjänsten](../../identity/overview.md).

## Aktivera Offer Decisioning

Så här aktiverar du Offer Decisioning:

1. Aktivera Adobe Experience Platform i din [datastream](/help/datastreams/overview.md) och markera kryssrutan Offer Decisioning

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Följ instruktionerna för att [installera SDK](/help/web-sdk/install/overview.md) (SDK kan installeras fristående eller via användargränssnittet. Mer information finns i [snabbstartsguiden för taggar](/help/tags/quick-start/quick-start.md)).
1. Konfigurera SDK för Offer Decisioning med `personalization.decisionScopes`. Ytterligare Offer Decisioning-specifika steg finns nedan.

   * Installera den fristående SDK

      1. Konfigurera åtgärden sendEvent med `personalization.decisionScopes`

     ```javascript
     alloy("sendEvent", {
       ...
       "personalization": {
         "decisionScopes": [
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
         ]
       }
     });
     ```

   * Installera SDK via taggar

      1. [Skapa en taggegenskap](/help/tags/ui/administration/companies-and-properties.md)
      1. [Lägg till inbäddningskoden](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=sv-SE)
      1. Installera och konfigurera Experience Platform Web SDK-tillägget med den dataström du skapade genom att välja konfigurationen i listrutan Datastream. Mer information finns i dokumentationen om [tillägg](/help/tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Skapa nödvändiga [dataelement](/help/tags/ui/managing-resources/data-elements.md). Du måste skapa en Experience Platform Web SDK Identity Map och ett Experience Platform Web SDK XDM Object-dataelement.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Skapa dina [regler](/help/tags/ui/managing-resources/rules.md).

         * Lägg till en Skicka-händelse för Experience Platform Web SDK och lägg till relevant `decisionScopes` i åtgärdens konfiguration

         ![send-event-action-DecisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [Skapa och publicera ett bibliotek](/help/tags/ui/publishing/libraries.md) som innehåller alla relevanta regler, dataelement och tillägg som du har konfigurerat

## Exempelbegäranden och svar

### Ett `decisionScopes`-värde

**Begäran**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Egenskap | Obligatoriskt | Beskrivning | Gränser | Exempel |
|---|---|---|---|---|
| `identityMap` | Ja | Se [Identitetstjänstens dokumentation](../../identity/overview.md). | En identitet per begäran. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Obs! Användare behöver inte ta med parametern `ECID` i API-anropet. Den här parametern läggs automatiskt till i samtalet om det behövs. |
| `decisionScopes` | Ja | En array med Base64-kodade strängar av JSON som innehåller aktivitets- och placerings-ID:n. | Högst 30 `decisionScopes` per begäran. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Svar**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Egenskap | Beskrivning | Exempel |
|---|---|---|
| `scope` | Beslutets omfattning som resulterade i de föreslagna erbjudandena. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Unikt ID för erbjudandeaktiviteten. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Erbjudandets unika ID. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schemat för innehållet som är associerat med det föreslagna erbjudandet. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Formatet på innehållet som är associerat med det föreslagna erbjudandet. | `"format": "text/html"` |
| `language` | En array med språk som är associerade med innehållet i det föreslagna erbjudandet. | `"language": [ "en-US" ]` |
| `content` | Innehåll som är associerat med det föreslagna erbjudandet i form av en sträng. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinnehåll som är associerat med det föreslagna erbjudandet i formatet för en URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Egenskaper som är kopplade till det föreslagna erbjudandet i formatet JSON-objekt. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Flera `decisionScopes`-värden

**Begäran**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Egenskap | Obligatoriskt | Beskrivning | Gränser | Exempel |
|---|---|---|---|---|
| `identityMap` | Ja | Se [Identitetstjänstens dokumentation](../../identity/overview.md). | En identitet per begäran. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Obs! Användare behöver inte ta med parametern `ECID` i API-anropet. Den här parametern läggs automatiskt till i samtalet om det behövs. |
| `decisionScopes` | Ja | En array med Base64-kodade strängar av JSON som innehåller aktivitets- och placerings-ID:n. | Högst 30 `decisionScopes` per begäran. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Svar**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Egenskap | Beskrivning | Exempel |
|---|---|---|
| `scope` | Beslutets omfattning som resulterade i de föreslagna erbjudandena. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Unikt ID för erbjudandeaktiviteten. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | Erbjudandets unika ID. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Schemat för innehållet som är associerat med det föreslagna erbjudandet. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Formatet på innehållet som är associerat med det föreslagna erbjudandet. | `"format": "text/text"` |
| `language` | En array med språk som är associerade med innehållet i det föreslagna erbjudandet. | `"language": [ "en-US" ]` |
| `content` | Innehåll som är associerat med det föreslagna erbjudandet i form av en sträng. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinnehåll som är associerat med det föreslagna erbjudandet i formatet för en URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Egenskaper som är kopplade till det föreslagna erbjudandet i formatet JSON-objekt. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Begränsningar

Vissa begränsningar för erbjudanden stöds för närvarande inte i Edge Network mobila arbetsflöden, till exempel Capping. Fältvärdet för begränsning anger hur många gånger ett erbjudande kan visas för alla användare. Mer information finns i [Erbjud berättiganderegler och begränsningsdokumentation](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html?lang=sv-SE#eligibility).
