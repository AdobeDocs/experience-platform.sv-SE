---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guiden för katalogtjänstutvecklare - tillägg
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# [!DNL Catalog Service] utvecklarhandbok bilaga

Det här dokumentet innehåller ytterligare information som hjälper dig att arbeta med [!DNL Catalog] API:t.

## Visa relaterade objekt {#view-interrelated-objects}

Vissa [!DNL Catalog] objekt kan vara sammankopplade med andra [!DNL Catalog] objekt. Alla fält som prefixeras av `@` som svarsnyttolaster betecknar relaterade objekt. Värdena för dessa fält har formen av en URI, som kan användas i en separat GET-begäran för att hämta relaterade objekt som de representerar.

Exempeldatauppsättningen som returneras i dokumentet när en specifik datauppsättning [](look-up-object.md) söks igenom innehåller ett `files` fält med följande URI-värde: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Innehållet i `files` fältet kan visas med denna URI som sökväg för en ny GET-begäran.

**API-format**

```http
GET {OBJECT_URI}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_URI}` | Den URI som anges av det interrelaterade objektfältet (exklusive `@` symbolen). |

**Begäran**

Följande begäran använder den URI som anges för exempeldatauppsättningens `files` egenskap för att hämta en lista över datauppsättningens associerade filer.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med relaterade objekt. I det här exemplet returneras en lista med datauppsättningsfiler.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Göra flera förfrågningar i ett enda samtal

Rotslutpunkten för [!DNL Catalog] API:t tillåter att flera begäranden görs inom ett enda anrop. Nyttolasten för begäran innehåller en array med objekt som representerar vad som normalt skulle vara enskilda begäranden, som sedan utförs i ordning.

Om dessa begäranden är ändringar eller tillägg [!DNL Catalog] och någon av ändringarna misslyckas, återställs alla ändringar.

**API-format**

```http
POST /
```

**Begäran**

I följande begäran skapas en ny datauppsättning och sedan skapas relaterade vyer för den datauppsättningen. I det här exemplet visas hur mallspråk används för att komma åt värden som returnerats i tidigare anrop för användning i efterföljande anrop.

Om du till exempel vill referera till ett värde som returnerats från en tidigare underbegäran kan du skapa en referens i formatet: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (där `{REQUEST_ID}` är användarangivet ID för underbegäran, vilket visas nedan). Du kan referera till alla attribut som är tillgängliga i brödtexten för en tidigare underbegärans svarsobjekt med hjälp av dessa mallar.

>[!NOTE]
>
>När en utförd underbegäran endast returnerar referensen till ett objekt (som är standard för de flesta POST- och PUT-begäranden i Catalog-API:t), får referensen alias för värdet `id` och kan användas som `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Användar-ID som är kopplat till svarsobjektet så att du kan matcha begäranden mot svar. [!DNL Catalog] lagrar inte det här värdet och returnerar det bara i svaret i referenssyfte. |
| `resource` | Resurssökvägen relativ till roten för [!DNL Catalog] API:t. Protokollet och domänen ska inte ingå i det här värdet, och det ska föregås av &quot;/&quot;. <br/><br/> När du använder PATCH eller DELETE som underbegäran `method`tar du med objekt-ID:t i resurssökvägen. För att inte blandas ihop med användaren `id`använder resurssökvägen ID:t för själva [!DNL Catalog] objektet (till exempel `resource: "/dataSets/1234567890"`). |
| `method` | Namnet på den metod (GET, PUT, POST, PATCH eller DELETE) som är relaterad till åtgärden som utförs i begäran. |
| `body` | JSON-dokumentet som normalt skulle överföras som nyttolast i en POST-, PUT- eller PATCH-begäran. Den här egenskapen krävs inte för GET- eller DELETE-begäranden. |

**Svar**

Ett lyckat svar returnerar en array med objekt som innehåller `id` den som du tilldelade varje begäran, HTTP-statuskoden för den enskilda begäran och svaret `body`. Eftersom de tre exempelbegärandena var alla för att skapa nya objekt är `body` för varje objekt en array som bara innehåller ID:t för det nya objektet, vilket är standard med de mest framgångsrika POSTERNA i [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Var försiktig när du inspekterar svar på en flerbegäran eftersom du måste verifiera koden för varje enskild underbegäran och inte bara förlita dig på HTTP-statuskoden för den överordnade POSTEN.  Det är möjligt att en enda underbegäran returnerar 404 (t.ex. en GET-begäran för en ogiltig resurs) medan den totala begäran returnerar 200.

## Ytterligare begäranderubriker

[!DNL Catalog] innehåller flera huvudkonventioner som hjälper dig att upprätthålla integriteten för dina data under uppdateringar.

### If-Match

Det är en god vana att använda objektversionshantering för att förhindra den typ av datafel som uppstår när ett objekt sparas av flera användare nästan samtidigt.

När du uppdaterar ett objekt bör du först göra ett API-anrop för att visa (GET) det objekt som ska uppdateras. Finns i svaret (och alla anrop där svaret innehåller ett enda objekt) är en rubrik som innehåller objektets version `E-Tag` . Om du lägger till objektversionen som ett begärandehuvud med namnet `If-Match` i uppdateringsanropet (PUT eller PATCH) kommer uppdateringen bara att lyckas om versionen fortfarande är densamma, vilket förhindrar datakonflikter.

Om versionerna inte matchar (objektet ändrades av en annan process sedan du hämtade det) får du HTTP-status 412 (Förhandsvillkor misslyckades) som anger att åtkomst till målresursen har nekats.

### Pragma

Ibland kanske du vill validera ett objekt utan att spara informationen. Om du använder huvudet med värdet `Pragma` `validate-only` 1 kan du skicka POST- eller PUT-begäranden endast i valideringssyfte, vilket förhindrar att ändringar i data bevaras.

## Datakomprimering

Komprimering är en [!DNL Experience Platform] tjänst som sammanfogar data från små filer till större filer utan att ändra några data. Av prestandaskäl kan det ibland vara bra att kombinera en uppsättning små filer till större filer för att ge snabbare åtkomst till data när frågor ställs.

När filerna i en inkapslad grupp har komprimerats uppdateras dess associerade [!DNL Catalog] objekt i övervakningssyfte.