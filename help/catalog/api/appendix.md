---
keywords: Experience Platform;hem;populära ämnen;Katalogtjänst;katalog api;appendix
solution: Experience Platform
title: API-handbok för katalogtjänst
description: Det här dokumentet innehåller ytterligare information som kan hjälpa dig att arbeta med katalog-API:t i Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# [!DNL Catalog Service] API-guide, tillägg

Det här dokumentet innehåller ytterligare information som kan hjälpa dig att arbeta med [!DNL Catalog] API.

## Visa relaterade objekt {#view-interrelated-objects}

Några [!DNL Catalog] objekt kan kopplas samman med andra [!DNL Catalog] objekt. Alla fält som föregås av `@` som svarsnyttolaster betecknar relaterade objekt. Värdena för dessa fält har formen av en URI, som kan användas i en separat GET-begäran för att hämta relaterade objekt som de representerar.

Exempeldatauppsättningen som returneras i dokumentet den [söka efter en specifik datauppsättning](look-up-object.md) innehåller en `files` fält med följande URI-värde: `"@/datasetFiles?datasetId={DATASET_ID}"`. Innehållet i `files` kan visas med denna URI som sökväg för en ny GET-begäran.

**API-format**

```http
GET {OBJECT_URI}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_URI}` | URI:n som tillhandahålls av det interrelaterade objektfältet (exklusive `@` symbol). |

**Begäran**

Följande begäran använder den URI som anges i exempeldatauppsättningens `files` för att hämta en lista över datauppsättningens associerade filer.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Ytterligare begäranderubriker

[!DNL Catalog] innehåller flera huvudkonventioner som hjälper dig att upprätthålla integriteten för dina data under uppdateringar.

### If-Match

Det är en god vana att använda objektversionshantering för att förhindra den typ av datafel som uppstår när ett objekt sparas av flera användare nästan samtidigt.

När du uppdaterar ett objekt bör du först göra ett API-anrop för att visa (GET) det objekt som ska uppdateras. Finns i svaret (och alla anrop där svaret innehåller ett enda objekt) är ett `E-Tag` sidhuvud som innehåller objektets version. Lägga till objektversionen som ett begärandehuvud med namnet `If-Match` i din uppdatering (PUT eller PATCH) kommer uppdateringsanrop endast att lyckas om versionen fortfarande är densamma, vilket förhindrar att data kolliderar.

Om versionerna inte matchar (objektet ändrades av en annan process sedan du hämtade det) får du HTTP-status 412 (Förhandsvillkor misslyckades) som anger att åtkomst till målresursen har nekats.

### Pragma

Ibland kanske du vill validera ett objekt utan att spara informationen. Använda `Pragma` header med värdet `validate-only` Med kan du skicka POST- eller PUT-begäranden endast i valideringssyfte, vilket förhindrar att ändringar i data bevaras.

## Datakomprimering

Komprimering är en [!DNL Experience Platform] som sammanfogar data från små filer till större filer utan att ändra några data. Av prestandaskäl kan det ibland vara bra att kombinera en uppsättning små filer till större filer för att ge snabbare åtkomst till data när frågor ställs.

När filerna i en inkapslad grupp har komprimerats, associeras de [!DNL Catalog] objektet uppdateras i övervakningssyfte.
