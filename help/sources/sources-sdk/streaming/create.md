---
title: Skapa en ny anslutningsspecifikation för Streaming SDK med API:t för Flow Service
description: I följande dokument beskrivs hur du skapar en anslutningsspecifikation med API:t för Flow Service och integrerar en ny källa med självbetjäningskällor.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Skapa en ny anslutningsspecifikation med API:t [!DNL Flow Service]

>[!NOTE]
>
>SDK för självbetjäningsströmning för källor är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

En anslutningsspecifikation representerar strukturen för en källa. Den innehåller information om en källas autentiseringskrav, definierar hur källdata kan utforskas och inspekteras samt ger information om attributen för en viss källa. Med slutpunkten `/connectionSpecs` i API:t [!DNL Flow Service] kan du programmässigt hantera anslutningsspecifikationerna inom organisationen.

Följande dokument innehåller steg om hur du skapar en anslutningsspecifikation med API:t [!DNL Flow Service] och integrerar en ny källa med självbetjäningskällor (Streaming SDK).

## Komma igång

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

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
| {your_source}-category.txt | Kategorin som källan tillhör, formaterad som en textfil. **Obs!** Om du tror att din källa inte passar in i någon av ovanstående kategorier kan du kontakta din Adobe-representant för att diskutera saken. | `medallia-category.txt` Ange källkategorin i filen, till exempel: `streaming`. |
| {your_source}-description.txt | En kort beskrivning av källan. | [!DNL Medallia] är en källa för automatiserad marknadsföring som du kan använda för att hämta [!DNL Medallia]-data till Experience Platform. |
| {your_source}-icon.svg | Bilden som ska användas för att representera källan i katalogen för Experience Platform-källor. Den här ikonen måste vara en SVG-fil. |
| {your_source}-label.txt | Källans namn så som det ska visas i katalogen Experience Platform sources. | Medallia |
| {your_source}-connectionSpec.json | En JSON-fil som innehåller anslutningsspecifikationen för källan. Den här filen behövs inte från början eftersom du fyller i anslutningsspecifikationen när du slutför den här guiden. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Under testperioden för anslutningsspecifikationen kan du i stället för nyckelvärden använda `text` i anslutningsspecifikationen.

När du har lagt till de nödvändiga filerna i din privata Git-databas måste du skapa en pull-begäran (PR) som Adobe kan granska. När din PR har godkänts och sammanfogats får du ett ID som kan användas för din anslutningsspecifikation för att hänvisa till källans etikett, beskrivning och ikon.

Följ sedan stegen som beskrivs nedan för att konfigurera anslutningsspecifikationen. Mer information om olika funktioner som du kan lägga till i källan, till exempel avancerad schemaläggning, anpassat schema eller olika sidnumreringstyper, finns i guiden [Konfigurera källspecifikationer](../config/sourcespec.md).

## Kopiera mall för anslutningsspecifikation

När du har samlat in de nödvändiga artefakterna kopierar och klistrar du in mallen för anslutningsspecifikation nedan i valfri textredigerare och uppdaterar sedan attributen inom hakparenteser `{}` med information som är relevant för just din källa.

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
    "documentationLink": "https://docs.adobe.com/content/help/sv-SE/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

En anslutningsspecifikation kan delas in i två skilda delar: källspecifikationerna och provspecifikationerna.

Mer information om avsnitten i en anslutningsspecifikation finns i följande dokument:

* [Konfigurera din källspecifikation](../config/sourcespec.md)
* [Konfigurera din specifikation för utforskande](../config/explorespec.md)

Med din specifikationsinformation uppdaterad kan du skicka den nya anslutningsspecifikationen genom att göra en POST-förfrågan till `/connectionSpecs`-slutpunkten för [!DNL Flow Service] API.

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
          "documentationLink": "https://docs.adobe.com/content/help/sv-SE/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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
        "documentationLink": "https://docs.adobe.com/content/help/sv-SE/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

Nu när du har skapat en ny anslutningsspecifikation måste du lägga till dess motsvarande anslutningsspecifikation-ID till en befintlig flödesspecifikation. Mer information finns i självstudiekursen [Uppdatera flödesspecifikationer](./update-flow-specs.md).

Om du vill ändra anslutningsspecifikationen som du har skapat kan du läsa självstudiekursen om [att uppdatera anslutningsspecifikationerna](./update-connection-specs.md).
