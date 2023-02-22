---
title: Skapa en ny anslutningsspecifikation för Streaming SDK med API:t för Flow Service
description: I följande dokument beskrivs hur du skapar en anslutningsspecifikation med API:t för Flow Service och integrerar en ny källa med självbetjäningskällor.
hide: true
hidefromtoc: true
source-git-commit: 6b78ed695bca5912c9af4371a8423fdcd7471bde
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Skapa en ny anslutningsspecifikation med [!DNL Flow Service] API

En anslutningsspecifikation representerar strukturen för en källa. Den innehåller information om en källas autentiseringskrav, definierar hur källdata kan utforskas och inspekteras samt ger information om attributen för en viss källa. The `/connectionSpecs` slutpunkt i [!DNL Flow Service] Med API kan du programmässigt hantera anslutningsspecifikationerna inom organisationen.

I följande dokument beskrivs hur du skapar en anslutningsspecifikation med [!DNL Flow Service] API och integrera en ny källa via självbetjäningskällor (Streaming SDK).

## Komma igång

Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Samla in artefakter

Om du vill skapa en ny direktuppspelningskälla med hjälp av självbetjäningskällor måste du först koordinera med Adobe, begära en privat Git-databas och anpassa dig till Adobe om källans etikett, beskrivning, kategori och ikon.

När du har angett den måste du strukturera din privata Git-databas så här:

* Källor
   * {your_source}
      * Artefakter
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefakter (filnamn) | Beskrivning | Exempel |
| --- | --- | --- |
| {your_source} | Namnet på källan. Den här mappen bör innehålla alla artefakter som hör till källan i din privata Git-databas. | `medallia` |
| {your_source}-category.txt | Kategorin som källan tillhör, formaterad som en textfil. **Anteckning**: Om du tror att din källa inte passar in i någon av ovanstående kategorier kan du kontakta din Adobe-representant för att diskutera detta. | `medallia-category.txt` Ange källans kategori i filen, som: `streaming`. |
| {your_source}-description.txt | En kort beskrivning av källan. | [!DNL Medallia] är en källa för automatiserad marknadsföring som ni kan använda för att [!DNL Medallia] data till Experience Platform. |
| {your_source}-icon.svg | Bilden som ska användas för att representera källan i katalogen för Experience Platform-källor. Den här ikonen måste vara en SVG-fil. |
| {your_source}-label.txt | Källans namn så som det ska visas i katalogen Experience Platform sources. | Medallia |
| {your_source}-connectionSpec.json | En JSON-fil som innehåller anslutningsspecifikationen för källan. Den här filen behövs inte från början eftersom du fyller i anslutningsspecifikationen när du slutför den här guiden. | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Under testperioden för anslutningsspecifikationen kan du i stället för nyckelvärden använda `text` i anslutningsspecifikationen.

När du har lagt till de nödvändiga filerna i din privata Git-databas måste du skapa en pull-begäran (PR) som Adobe kan granska. När din PR har godkänts och sammanfogats får du ett ID som kan användas för din anslutningsspecifikation för att hänvisa till källans etikett, beskrivning och ikon.

Följ sedan stegen som beskrivs nedan för att konfigurera anslutningsspecifikationen. Mer information om olika funktioner som du kan lägga till i källan, till exempel avancerad schemaläggning, anpassat schema eller olika sidnumreringstyper, finns i handboken [konfigurera källspecifikationer](../config/sourcespec.md).

## Kopiera mall för anslutningsspecifikation

När du har samlat in de nödvändiga artefakterna kopierar och klistrar du in mallen för anslutningsspecifikationen nedan i valfri textredigerare och uppdaterar sedan attributen inom hakparentes `{}` med information som är relevant för just er källa.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Skapa en anslutningsspecifikation {#create}

När du har skaffat en mall för anslutningsspecifikation kan du nu börja skapa en ny anslutningsspecifikation genom att fylla i de värden som motsvarar källan.

En anslutningsspecifikation kan delas in i två skilda delar: källspecifikationer och specifikationer.

Mer information om avsnitten i en anslutningsspecifikation finns i följande dokument:

* [Konfigurera källspecifikationen](../config/sourcespec.md)
* [Konfigurera din utforskarspecifikation](../config/explorespec.md)

Med informationen om din specifikation uppdaterad kan du skicka den nya anslutningsspecifikationen genom att göra en POST-förfrågan till `/connectionSpecs` slutpunkt för [!DNL Flow Service] API.

**API-format**

```http
POST /connectionSpecs
```

**Begäran**

Följande begäran är ett exempel på en fullständigt skriven anslutningsspecifikation för en direktuppspelningskälla:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningsspecifikationen, inklusive dess unika `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## Nästa steg

Nu när du har skapat en ny anslutningsspecifikation måste du lägga till dess motsvarande anslutningsspecifikation-ID till en befintlig flödesspecifikation. Se självstudiekursen om [uppdatera flödesspecifikationer](./update-flow-specs.md) för mer information.

Om du vill ändra anslutningsspecifikationen som du har skapat kan du se självstudiekursen om [uppdatera anslutningsspecifikationer](./update-connection-specs.md).
