---
title: Using Offer Decisioning with the Platform Web SDK
description: The Adobe Experience Platform Web SDK can deliver and render personalized offers managed in Offer Decisioning. You can create your offers and other related objects using the Offer Decisioning UI or API.
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: b0cc2343a502e180267d86bca4a699c02f2d6f3d
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 1%

---

# Using Offer Decisioning with the Platform Web SDK

>[!NOTE]
>
>The use of Offer Decisioning in Adobe Experience Platform Web SDK is available in early access to select users. This functionality is not available to all IMS organizations.

[!DNL Web SDK] You can create your offers and other related objects using the Offer Decisioning user interface (UI) or APIs.

## Förutsättningar

* IMS organization is enabled for edge decisioning
* Offers, Activities created
* Datastream is published

## Terminologi

It is important to understand the following terminology when working with Offer Decisioning. [](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)

* **** The container ID is the first path element for all repository APIs. All decisioning objects reside within a container.

* ****

   **

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   **

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >****

   ![](assets/decision-scope-copy.png)

* ****[](../../fundamentals/datastreams.md)

* ****[](../../identity/overview.md)

## Enabling Offer Decisioning

To enable Offer Decisioning, perform the following steps:

1. [](../../fundamentals/datastreams.md)

   ![](./assets/offer-decisioning-edge-config.png)

1. [](../../fundamentals/installing-the-sdk.md)[](https://experience.adobe.com/#/data-collection/) [](../../../tags/quick-start/quick-start.md)
1. [](../../fundamentals/configuring-the-sdk.md) Additional Offer Decisioning specific steps are provided below.

   * Install the standalone SDK

      1. `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * Install the SDK through tags

      1. [Create a tag property](../../../tags/ui/administration/companies-and-properties.md)
      1. [](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Install and configure the Platform Web SDK extension with the Datastream you created by selecting the configuration from the &quot;Datastream&quot; dropdown. [](../../../tags/ui/managing-resources/extensions/overview.md)

         ![](./assets/install-aep-web-sdk-extension.png)

         ![](./assets/configure-aep-web-sdk-extension.png)

      1. [](../../../tags/ui/managing-resources/data-elements.md) At the bare minimum, you must create a Platform Web SDK Identity Map and a Platform Web SDK XDM Object data element.

         ![](./assets/identity-map-data-element.png)

         ![](./assets/xdm-object-data-element.png)

      1. [](../../../tags/ui/managing-resources/rules.md)

         * `decisionScopes`

            ![](./assets/send-event-action-decisionScopes.png)
      1. [](../../../tags/ui/publishing/libraries.md)



## Sample requests and responses

### `decisionScopes`

****

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

| Property | Required | Beskrivning | Limits | Exempel |
|---|---|---|---|---|
| `identityMap` | Ja | [](../../identity/overview.md) | One identity per request. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br>`ECID` This parameter is automatically added to the call if needed. |
| `decisionScopes` | Ja | An array of Base64 encoded strings of JSON containing the activity and placement IDs. | `decisionScopes` | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

****

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

| Property | Beskrivning | Exempel |
|---|---|---|
| `scope` | The decision scope that resulted in the proposed offers. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | The unique ID of the offer activity. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | The unique ID of the offer placement. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | The ID of the proposed offer. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | The schema of the content associated with the proposed offer. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | The ID of the proposed offer. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | The format of the content associated with the proposed offer. | `"format": "text/html"` |
| `language` | An array of languages associated with the content from the proposed offer. | `"language": [ "en-US" ]` |
| `content` | Content associated with the proposed offer in the format of a string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Image content associated with the proposed offer in the format of a URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Characteristics associated with the proposed offer in the format of a JSON object. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### `decisionScopes`

****

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

| Property | Required | Beskrivning | Limits | Exempel |
|---|---|---|---|---|
| `identityMap` | Ja | [](../../identity/overview.md) | One identity per request. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br>`ECID` This parameter is automatically added to the call if needed. |
| `decisionScopes` | Ja | An array of Base64 encoded strings of JSON containing the activity and placement IDs. | `decisionScopes` | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

****

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

| Property | Beskrivning | Exempel |
|---|---|---|
| `scope` | The decision scope that resulted in the proposed offers. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | The unique ID of the offer activity. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | The unique ID of the offer placement. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | The ID of the proposed offer. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | The schema of the content associated with the proposed offer. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | The ID of the proposed offer. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | The format of the content associated with the proposed offer. | `"format": "text/text"` |
| `language` | An array of languages associated with the content from the proposed offer. | `"language": [ "en-US" ]` |
| `content` | Content associated with the proposed offer in the format of a string. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Image content associated with the proposed offer in the format of a URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Characteristics associated with the proposed offer in the format of a JSON object. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Begränsningar

Some offer constraints are currently not supported with the mobile Experience Edge workflows, for example Capping. The Capping field value specifies the number of times an offer can be presented across all users. [](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility)
