---
title: Använda Offer decisioning med Platform Web SDK
description: Adobe Experience Platform Web SDK kan leverera och återge personaliserade erbjudanden som hanteras i Offer decisioning. Du kan skapa erbjudanden och andra relaterade objekt med hjälp av Offera decisioningens gränssnitt eller API.
keywords: offer decisioning;beslut;Web SDK;Platform Web SDK;personaliserade erbjudanden;leverera erbjudanden;erbjudandeleverans;erbjudandepersonalisering;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 1%

---

# Använda Offer decisioning med Platform Web SDK

>[!NOTE]
>
>Offer decisioning i Adobe Experience Platform Web SDK är tillgänglig i ett tidigt skede för vissa användare. Den här funktionen är inte tillgänglig för alla organisationer.

Adobe Experience Platform [!DNL Web SDK] kan leverera och återge personaliserade erbjudanden som hanteras i Offer decisioning. Du kan skapa erbjudanden och andra relaterade objekt med hjälp av användargränssnittet (UI) eller API:erna för Offera decisioningen.

## Förutsättningar

* Organisationen är aktiverad för kantbeslut
* Erbjudanden, skapade aktiviteter
* Datastream publiceras

## Terminologi

Det är viktigt att förstå följande terminologi när du arbetar med Offer decisioning. Mer information och ytterligare villkor finns på [Offera decisioningens ordlista](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Behållare:** En behållare är en isoleringsmekanism för att hålla olika bekymmer isär. Behållar-ID är det första sökvägselementet för alla databas-API:er. Alla beslutsobjekt finns i en behållare.

* **Beslutsomfattningar:** För Offer decisioning är beslutsomfattningar de Base64-kodade strängarna i JSON som innehåller de aktivitets- och placerings-ID som du vill att offera decisioningen ska använda för att föreslå erbjudanden.

  *Beslutsomfattelse JSON:*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *Beslutsomfattare Base64-kodad sträng:*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >Du kan kopiera värdet för beslutsomfånget från **Översikt över aktivitet** i användargränssnittet.

  ![Inställningar för beslutskopiering.](assets/decision-scope-copy.png)

* **Datastreams:** Mer information finns i [datastreams](../../../datastreams/overview.md) dokumentation.

* **Identitet**: Mer information finns i den här dokumentationen. [Platform Web SDK använder identitetstjänst](../../identity/overview.md).

## Aktivera Offer decisioning

Så här aktiverar du Offer decisioning:

1. Aktivera Adobe Experience Platform i dina [datastream](../../../datastreams/overview.md) och markera rutan Offer decisioning

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Följ instruktionerna för att [installera SDK](../../fundamentals/installing-the-sdk.md) (SDK kan installeras fristående eller via användargränssnittet. Se [snabbstartsguide för taggar](../../../tags/quick-start/quick-start.md)) om du vill ha mer information.
1. [Konfigurera SDK](../../fundamentals/configuring-the-sdk.md) för Offer decisioning. Ytterligare Offer decisioning-specifika steg finns nedan.

   * Installera fristående SDK

      1. Konfigurera åtgärden sendEvent med `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```

   * Installera SDK via taggar

      1. [Skapa en taggegenskap](../../../tags/ui/administration/companies-and-properties.md)
      1. [Lägg till inbäddningskoden](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Installera och konfigurera Platform Web SDK-tillägget med den dataström du skapade genom att välja konfigurationen i listrutan Datastream. Läs dokumentationen om [tillägg](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Skapa de nödvändiga [Dataelement](../../../tags/ui/managing-resources/data-elements.md). Minimikravet är att du måste skapa en plattformsbaserad SDK-identitetskarta och ett XDM-objektdataelement för plattformswebben.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Skapa [Regler](../../../tags/ui/managing-resources/rules.md).

         * Lägg till en SDK-sändningshändelse för en plattform och lägg till relevant `decisionScopes` till åtgärdens konfiguration

           ![send-event-action-DecisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [Skapa och publicera ett bibliotek](../../../tags/ui/publishing/libraries.md) som innehåller alla relevanta regler, dataelement och tillägg som du har konfigurerat

## Exempelbegäranden och svar

### Ett `decisionScopes` value

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
| `identityMap` | Ja | Se detta [Identitetstjänstens dokumentation](../../identity/overview.md). | En identitet per begäran. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Obs! Användare behöver inte inkludera `ECID` i API-anropet. Den här parametern läggs automatiskt till i samtalet om det behövs. |
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

### Flera `decisionScopes` values

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
| `identityMap` | Ja | Se detta [Identitetstjänstens dokumentation](../../identity/overview.md). | En identitet per begäran. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Obs! Användare behöver inte inkludera `ECID` i API-anropet. Den här parametern läggs automatiskt till i samtalet om det behövs. |
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

Vissa begränsningar för erbjudanden stöds för närvarande inte i arbetsflödena för mobila Edge-nätverk, till exempel Capping. Fältvärdet för begränsning anger hur många gånger ett erbjudande kan visas för alla användare. Mer information finns i [Dokumentation om regler och begränsningar för erbjudanden](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
