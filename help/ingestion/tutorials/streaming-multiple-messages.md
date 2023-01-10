---
keywords: Experience Platform;hemmabruk;populära ämnen;direktuppspelningsuppläsning;förtäring;direktuppspelning av flera meddelanden;flera meddelanden;
solution: Experience Platform
title: Skicka flera meddelanden i en enda HTTP-begäran
type: Tutorial
description: Det här dokumentet innehåller en självstudiekurs för att skicka flera meddelanden till Adobe Experience Platform inom en enda HTTP-begäran med direktuppspelningsinmatning.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 1%

---

# Skicka flera meddelanden i en enda HTTP-begäran

När du direktuppspelar data till Adobe Experience Platform kan det vara dyrt att ringa ett antal HTTP-anrop. I stället för att skapa 200 HTTP-begäranden med 1 kB-nyttolaster är det till exempel mycket effektivare att skapa 1 HTTP-begäran med 200 meddelanden på 1 kB vardera, med en enda nyttolast på 200 kB. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera data som skickas till [!DNL Experience Platform].

Det här dokumentet innehåller en självstudiekurs för att skicka flera meddelanden till [!DNL Experience Platform] inom en enda HTTP-begäran med direktuppspelning.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för Adobe Experience Platform [!DNL Data Ingestion]. Läs följande dokumentation innan du börjar den här självstudiekursen:

- [Översikt över datainmatning](../home.md): Täcker kärnbegrepp i [!DNL Experience Platform Data Ingestion], inklusive intag-metoder och dataanslutningar.
- [Översikt över direktuppspelning](../streaming-ingestion/overview.md): Arbetsflödet och byggstenarna för strömmande ingång, som strömmande anslutningar, datauppsättningar, [!DNL XDM Individual Profile]och [!DNL XDM ExperienceEvent].

Den här självstudiekursen kräver även att du har slutfört [Autentisering till Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) självstudiekurs för att ringa [!DNL Platform] API:er. När du slutför självstudiekursen för autentisering får du det värde för auktoriseringshuvud som krävs för alla API-anrop i den här självstudiekursen. Rubriken visas i exempelanrop enligt följande:

- Behörighet: Bearer `{ACCESS_TOKEN}`

Alla begäranden om POSTER kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Skapa en direktuppspelningsanslutning

Du måste först skapa en direktuppspelningsanslutning innan du kan starta direktuppspelningsdata till [!DNL Experience Platform]. Läs [skapa en direktuppspelningsanslutning](./create-streaming-connection.md) för att lära dig hur du skapar en direktuppspelningsanslutning.

När du har registrerat en direktuppspelningsanslutning får du som DataProducer en unik URL som kan användas för att strömma data till Platform.

## Strömma till en datauppsättning

I följande exempel visas hur du skickar flera meddelanden till en viss datauppsättning i en enda HTTP-begäran. Infoga datauppsättnings-ID:t i meddelanderubriken om du vill att meddelandet ska infogas direkt i det.

Du kan hämta ID:t för en befintlig datauppsättning med [!DNL Platform] Använda ett gränssnitt eller en liståtgärd i API:t. Datauppsättnings-ID:t finns på [Experience Platform](https://platform.adobe.com) genom att gå till **[!UICONTROL Datasets]** klickar du på den datauppsättning som du vill ha ID:t för och kopierar strängen från datamängd-ID:t på **[!UICONTROL Info]** -fliken. Se [Katalogtjänst - översikt](../../catalog/home.md) om du vill ha information om hur du hämtar datauppsättningar med API:t.

I stället för att använda en befintlig datauppsättning kan du skapa en ny datauppsättning. Läs [skapa en datauppsättning med API:er](../../catalog/api/create-dataset.md) självstudiekurs om du vill ha mer information om hur du skapar en datauppsättning med API:er.

**API-format**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID:t för den skapade direktuppspelningsanslutningen. |

**Begäran**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 207 (Multi-status). En granskning av svarstexten ger mer information om huruvida varje metod som körs i begäran har lyckats eller inte. Ett svar returneras för varje element i arrayen för begärandemeddelanden. Nedan visas ett exempel på ett lyckat svar utan meddelandefel:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Mer information om statuskoder finns i [svarskoder](#response-codes) tabellen i bilagan till den här självstudiekursen.

## Identifiera misslyckade meddelanden

Jämfört med att skicka en begäran med ett enda meddelande finns det ytterligare faktorer att tänka på när du skickar en HTTP-begäran med flera meddelanden, till exempel: hur du identifierar när data inte har skickats, vilka specifika meddelanden som inte har kunnat skickas och hur de kan hämtas, och vad som händer med data som lyckas när andra meddelanden i samma begäran misslyckas.

Innan du fortsätter med den här självstudiekursen bör du först granska [hämta misslyckade batchar](../quality/retrieve-failed-batches.md) guide.

### Skicka nyttolast för begäran med giltiga och ogiltiga meddelanden

I följande exempel visas vad som händer när gruppen innehåller giltiga och ogiltiga meddelanden.

Nyttolasten för begäran är en array med JSON-objekt som representerar händelsen i XDM-schemat. Observera att följande villkor måste vara uppfyllda för att meddelandet ska kunna valideras:
- The `imsOrgId` fältet i meddelandehuvudet måste matcha inletsdefinitionen. Om nyttolasten för begäran inte innehåller en `imsOrgId` fält, [!DNL Data Collection Core Service] (DCCS) lägger automatiskt till fältet.
- Meddelandets huvud ska referera till ett befintligt XDM-schema som skapats i [!DNL Platform] Gränssnitt.
- The `datasetId` fältet måste referera till en befintlig datamängd i [!DNL Platform]och dess schema måste matcha det schema som anges i `header` -objekt i varje meddelande som ingår i begärandetexten.

**API-format**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID:t för det skapade dataintaget. |

**Begäran**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Svar**

Svarsnyttolasten innehåller en status för varje meddelande tillsammans med ett GUID i `xactionId` som kan användas för kalkering.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

Exemplet ovan visar felmeddelanden för föregående begäran. Genom att jämföra det här svaret med det föregående giltiga svaret kan du observera att begäran resulterade i en partiell framgång, där ett meddelande kunde hämtas och tre meddelanden resulterade i fel. Observera att båda svaren returnerar statuskoden 207. Mer information om statuskoder finns i [svarskoder](#response-codes) tabellen i bilagan till den här självstudiekursen.

Det första meddelandet har skickats till [!DNL Platform] och påverkas inte av resultaten från de andra meddelandena. Därför behöver du inte ta med det här meddelandet igen när du försöker skicka om de misslyckade meddelandena.

Det andra meddelandet misslyckades eftersom det saknade meddelandetext. Samlingsbegäran förväntar sig att meddelandeelement har giltiga huvud- och brödavsnitt. Om du lägger till följande kod efter rubriken i det andra meddelandet rättas begäran till, vilket gör att det andra meddelandet godkänns i valideringen:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Det tredje meddelandet misslyckades på grund av att ett ogiltigt IMS-organisations-ID användes i huvudet. IMS-organisationen måste matcha den {CONNECTION_ID} som du försöker publicera till. För att avgöra vilket IMS-organisations-ID som matchar den direktuppspelningsanslutning du använder kan du utföra en `GET inlet` begäran med [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Se [hämta en direktuppspelningsanslutning](./create-streaming-connection.md#get-data-collection-url) om du vill ha ett exempel på hur du hämtar tidigare skapade direktuppspelningsanslutningar.

Det fjärde meddelandet misslyckades eftersom det inte följde det förväntade XDM-schemat. The `xdmSchema` som ingår i begärans huvud och brödtext matchar inte XDM-schemat i `{DATASET_ID}`. Om du korrigerar schemat i meddelandehuvudet och meddelandetexten kan det godkänna DCCS-validering och skickas till [!DNL Platform]. Meddelandetexten måste också uppdateras för att matcha XDM-schemat i `{DATASET_ID}` för att det ska klara direktuppspelningsvalidering [!DNL Platform]. Mer information om vad som händer med meddelanden som har direktuppspelats till Platform finns i [bekräfta inkapslade meddelanden](#confirm-messages-ingested) i den här självstudiekursen.

### Hämta misslyckade meddelanden från [!DNL Platform]

Misslyckade meddelanden identifieras av en felstatuskod i svarsmatrisen.
De ogiltiga meddelandena samlas in och lagras i en felbatch i den datamängd som anges av `{DATASET_ID}`.

Läs [hämta misslyckade batchar](../quality/retrieve-failed-batches.md) för mer information om hur du återställer misslyckade gruppmeddelanden.

## Bekräfta inkapslade meddelanden

Meddelanden som godkänns vid DCCS-validering direktuppspelas i [!DNL Platform]. På [!DNL Platform]testas batchmeddelandena med direktuppspelningsvalidering innan de hämtas till [!DNL Data Lake]. Statusen för batchar, vare sig de lyckades eller inte, visas i den datauppsättning som anges av `{DATASET_ID}`.

Du kan visa status för batchmeddelanden som har direktuppspelats till [!DNL Platform] med [Experience Platform UI](https://platform.adobe.com) genom att gå till **[!UICONTROL Datasets]** -fliken, klicka på den datauppsättning som du direktuppspelar till och kontrollera **[!UICONTROL Dataset Activity]** -fliken.

Batchmeddelanden som godkänns vid direktuppspelningsvalidering [!DNL Platform] är inkapslade i [!DNL Data Lake]. Meddelandena är sedan tillgängliga för analys eller export.

## Nästa steg

Nu när du vet hur du skickar flera meddelanden i en enda begäran och verifierar när meddelanden har importerats till måldatauppsättningen, kan du börja direktuppspela dina egna data till [!DNL Platform]. En översikt över hur du hämtar inkapslade data från [!DNL Platform], se [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) guide.

## Bilaga

Det här avsnittet innehåller ytterligare information om självstudiekursen.

### Svarskoder

I följande tabell visas statuskoder som returnerats av slutförda och misslyckade svarsmeddelanden.

| Statuskod | Beskrivning |
| :---: | --- |
| 207 | Även om&quot;207&quot; används som övergripande svarsstatuskod måste mottagaren läsa innehållet i flerstatussvarstexten för att få mer information om huruvida metoden har körts eller inte. Svarskoden används i lyckade, partiella framgångar och även i felsituationer. |
| 400 | Ett problem uppstod med begäran. I svarstexten finns ett mer specifikt felmeddelande (till exempel saknas obligatoriska fält för meddelandenyttolasten eller meddelandet var okänt xdm-format). |
| 401 | Obehörig: begäran saknar giltigt auktoriseringshuvud. Detta returneras endast för inmatningar som har autentisering aktiverat. |
| 403 | Obehörig: Angiven auktoriseringstoken är ogiltig eller har gått ut. Detta returneras endast för inmatningar som har autentisering aktiverat. |
| 413 | Nyttolasten är för stor - utlöses när den totala nyttolastbegäran är större än 1 MB. |
| 429 | För många begäranden inom angiven tidsperiod. |
| 500 | Fel vid bearbetning av nyttolast. I svarstexten finns ett mer specifikt felmeddelande (till exempel har inte meddelandenyttolastschemat angetts eller matchar inte XDM-definitionen i [!DNL Platform]). |
| 503 | Tjänsten är inte tillgänglig för tillfället. Kunderna bör försöka igen minst tre gånger med en exponentiell strategi för bakåtjustering. |
