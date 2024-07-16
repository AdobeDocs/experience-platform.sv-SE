---
title: Slutpunkt för tilläggspaket
description: Lär dig hur du anropar slutpunkten /extension_packages i Reactor API.
exl-id: a91c6f32-6c72-4118-a43f-2bd8ef50709f
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# Slutpunkt för tilläggspaket

>[!WARNING]
>
>Implementeringen av slutpunkten `/extension_packages` börjar fungera när funktioner läggs till, tas bort och omarbetas.

Ett tilläggspaket representerar ett [tillägg](./extensions.md) som har skapats av en tilläggsutvecklare. Ett tilläggspaket definierar ytterligare funktioner som kan göras tillgängliga för tagganvändare. De här funktionerna är oftast i form av [regelkomponenter](./rule-components.md) (händelser, villkor och åtgärder) och [dataelement](./data-elements.md), men kan även innehålla huvudmoduler och delade moduler.

Tilläggspaket visas i tilläggskatalogen i användargränssnittet för datainsamling och Adobe Experience Platform så att användare kan installera dem. Du kan lägga till ett tilläggspaket till en egenskap genom att skapa ett tillägg med en länk till tilläggspaketet.

Ett tilläggspaket tillhör [företaget](./companies.md) för den utvecklare som skapade det.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

Förutom att förstå hur du anropar Reactor API är det också viktigt att du förstår hur attributen `status` och `availability` för ett tilläggspaket påverkar vilka åtgärder du kan utföra på det. Dessa förklaras i avsnitten nedan.

### Status

Tilläggspaket har tre möjliga statusvärden: `pending`, `succeeded` och `failed`.

| Status | Beskrivning |
| --- | --- |
| `pending` | När ett tilläggspaket skapas ställs dess `status` in på `pending`. Detta anger att systemet har tagit emot informationen för tilläggspaketet och kommer att påbörja bearbetningen. Tilläggspaket med statusen `pending` är inte tillgängliga för användning. |
| `succeeded` | Statusen för ett tilläggspaket uppdateras till `succeeded` om bearbetningen slutförs. |
| `failed` | Statusen för ett tilläggspaket uppdateras till `failed` om bearbetningen inte slutförs. Ett tilläggspaket med statusen `failed` kan uppdateras tills bearbetningen har slutförts. Tilläggspaket med statusen `failed` är inte tillgängliga för användning. |

### Tillgänglighet

Det finns nivåer för ett tilläggspaket: `development`, `private` och `public`.

| Tillgänglighet | Beskrivning |
| --- | --- |
| `development` | Ett tilläggspaket i `development` är bara synligt för och tillgängligt i det företag som äger det. Dessutom kan den bara användas på egenskaper som är konfigurerade för tilläggsutveckling. |
| `private` | Ett `private`-tilläggspaket är bara synligt för det företag som äger det och kan bara installeras på egenskaper som företaget äger. |
| `public` | Ett `public`-tilläggspaket är synligt och tillgängligt för alla företag och egenskaper. |

>[!NOTE]
>
>När ett tilläggspaket skapas ställs `availability` in på `development`. När testningen har slutförts kan du överföra tilläggspaketet till antingen `private` eller `public`.

## Hämta en lista med tilläggspaket {#list}

Du kan hämta en lista över tilläggspaket genom att göra en GET-förfrågan till `/extension_packages`.

**API-format**

```http
GET /extension_packages
```

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade tilläggspaket filtreras baserat på följande attribut:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Mer information finns i guiden om [filtrering av svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med tilläggspaket.

```json
{
  "data": [
    {
      "id": "EP6860e2485de2413ea9b295d6f5321ad3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP6860e2485de2413ea9b295d6f5321ad3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:32.694Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944710",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:35.754Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP6860e2485de2413ea9b295d6f5321ad3"
      }
    },
    {
      "id": "EP1b173c8316954e0986e5a405b4e715e3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP1b173c8316954e0986e5a405b4e715e3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:34.632Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944712",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:36.655Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP1b173c8316954e0986e5a405b4e715e3"
      }
    },
    {
      "id": "EPb8eca81769a64af3892af5202a57ce15",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EPb8eca81769a64af3892af5202a57ce15",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T18:32:29.271Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604946740",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T18:32:43.710Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EPb8eca81769a64af3892af5202a57ce15"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 3
    }
  }
}
```

## Söka efter ett tilläggspaket {#lookup}

Du kan söka efter ett tilläggspaket genom att ange dess ID i sökvägen till en GET-begäran.

**API-format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `id` för tilläggspaketet som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om tilläggspaketet, inklusive dess delegatresurser som `actions`, `conditions`, `data_elements` med flera. Exemplet nedan har trunkerats för blanksteg.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Skapa ett tilläggspaket {#create}

Tilläggspaket skapas med ett Node.js-byggnadsverktyg och sparas på den lokala datorn innan de skickas till Reactor API. Mer information om hur du konfigurerar ett tilläggspaket finns i guiden [Komma igång med tilläggsutveckling](../../extension-dev/getting-started.md).

När du har skapat tilläggspaketfilen kan du skicka den till Reactor API via en POST-begäran.

**API-format**

```http
POST /extension_packages
```

**Begäran**

Följande begäran skapar ett nytt tilläggspaket. Den lokala sökvägen till den paketfil som överförs refereras till som formulärdata (`package`), och därför krävs `Content-Type` header för den här slutpunkten `multipart/form-data`.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Svar**

Ett godkänt svar returnerar information om det nya tilläggspaketet.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Uppdatera ett tilläggspaket {#update}

Du kan uppdatera ett tilläggspaket genom att ta med dess ID i sökvägen för en PATCH-begäran.

**API-format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `id` för tilläggspaketet som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Precis som när [skapar ett tilläggspaket](#create) måste en lokal version av det uppdaterade paketet överföras via formulärdata.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Svar**

Ett godkänt svar returnerar information om det uppdaterade tilläggspaketet.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Frigör ett tilläggspaket privat {#private-release}

När du har testat tilläggspaketet kan du frigöra det privat. Detta gör den tillgänglig för alla ägor i företaget.

När du har släppt privat kan du påbörja den offentliga releaseprocessen genom att fylla i formuläret [för begäran om offentlig release](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest).

**API-format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `id` för tilläggspaketet som du vill ska frisläppas privat. |

{style="table-layout:auto"}

**Begäran**

En privat release uppnås genom att en `action` med värdet `release_private` i `meta` för begärandedata tillhandahålls.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "meta": {
            "action": "release_private"
          },
          "id": "EP27e9323eb585411fae6086fc78a3b70b",
          "type": "extension_packages"
        }
      }'
```

**Svar**

Ett godkänt svar returnerar information om tilläggspaketet.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Avbryt ett tilläggspaket {#discontinue}

Du kan avbryta ett tilläggspaket genom att ange attributet `discontinued` till `true` via en PATCH-begäran.

**API-format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `id` för tilläggspaketet som du vill avbryta. |

{style="table-layout:auto"}

**Begäran**

En privat release uppnås genom att en `action` med värdet `release_private` i `meta` för begärandedata tillhandahålls.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "discontinued": true
          },
          "id": "EP5705a5d99aba406692e0ac666fcab160",
          "type": "extension_packages"
        }
      }'
```

**Svar**

Ett godkänt svar returnerar information om tilläggspaketet.

```json
{
  "data": {
    "id": "EP5705a5d99aba406692e0ac666fcab160",
    "type": "extension_packages",
    "attributes": {
      "actions": [

      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP5705a5d99aba406692e0ac666fcab160",
      "conditions": [

      ],
      "configuration": null,
      "created_at": "2020-12-14T17:39:36.932Z",
      "data_elements": [

      ],
      "description": "Provides nothing.",
      "discontinued": true,
      "display_name": "Kessel Template Test",
      "events": [

      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "test-1607967575",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-12-14T17:39:43.883Z",
      "version": "1.0.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP5705a5d99aba406692e0ac666fcab160"
    }
  }
}
```

## Lista versionerna för ett tilläggspaket

Du kan lista versionerna av ett tilläggspaket genom att lägga till `/versions` i sökvägen för en sökningsbegäran.

**API-format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/versions
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `id` för tilläggspaketet vars versioner du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172/versions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar en array med tidigare versioner av tilläggspaketet. Ett exempelsvar har utelämnats för blanksteg.
