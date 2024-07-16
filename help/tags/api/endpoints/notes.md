---
title: Anteckningsslutpunkt
description: Lär dig hur du anropar slutpunkten /notes i Reactor API.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---

# Anteckningsslutpunkt

I Reaktors-API:t är anteckningar textanteckningar som du kan lägga till i vissa resurser. Anteckningar är i huvudsak kommentarer om deras respektive resurser. Innehållet i anteckningarna påverkar inte resursbeteendet och kan användas för en mängd olika användningsområden, bland annat följande:

* Ange bakgrundsinformation
* Fungerar som att göra-listor
* Skicka rådgivning om resursanvändning
* Ge instruktioner till andra teammedlemmar
* Inspelningshistorik

Med slutpunkten `/notes` i Reaktors API kan du hantera anteckningarna programmatiskt.

Anteckningar kan användas med följande resurser:

* [Dataelement](./data-elements.md)
* [Tillägg](./extensions.md)
* [Bibliotek](./libraries.md)
* [Egenskaper](./properties.md)
* [Regelkomponenter](./rule-components.md)
* [Regler](./rules.md)
* [Hemligheter](./secrets.md)

Dessa sex typer kallas tillsammans för&quot;betydande&quot; resurser. När en anteckningsbar resurs tas bort, tas även tillhörande anteckningar bort.

>[!NOTE]
>
>För resurser som kan ha flera versioner måste anteckningar skapas för den aktuella huvudrevisionen. De får inte bifogas andra revisioner.
>
>Anteckningar kan dock fortfarande läsas från revideringar. I sådana fall returnerar API bara de anteckningar som fanns innan ändringen skapades. De ger en ögonblicksbild av anteckningarna som de var när revisionen klipptes ut. Om du däremot läser anteckningar från den aktuella huvudrevisionen, returneras alla anteckningar.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta en lista med anteckningar {#list}

Du kan hämta en lista med anteckningar för en resurs genom att lägga till `/notes` i sökvägen för en GET-förfrågan för den aktuella resursen.

**API-format**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beskrivning |
| --- | --- |
| `RESOURCE_TYPE` | Den typ av resurs som du hämtar anteckningar för. Måste vara något av följande värden: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | `id` för den specifika resurs vars anteckningar du vill visa. |

{style="table-layout:auto"}

**Begäran**

Följande begäran visar anteckningarna som är kopplade till ett bibliotek.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med anteckningar som är kopplade till den angivna resursen.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Söka efter en anteckning {#lookup}

Du kan söka efter en anteckning genom att ange dess ID i sökvägen till en GET-förfrågan.

**API-format**

```http
GET /notes/{NOTE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `NOTE_ID` | `id` av anteckningen som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar informationen i anteckningen.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Skapa en anteckning {#create}

>[!WARNING]
>
>Innan du skapar en ny anteckning bör du tänka på att anteckningar inte kan redigeras, och det enda sättet att ta bort dem är att ta bort motsvarande resurs.

Du kan skapa en ny anteckning genom att lägga till `/notes` i sökvägen för en POST-förfrågan för resursen i fråga.

**API-format**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beskrivning |
| --- | --- |
| `RESOURCE_TYPE` | Den typ av resurs som du skapar en anteckning för. Måste vara något av följande värden: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | `id` för den specifika resurs som du vill skapa en anteckning för. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skapar en ny anteckning för en egenskap.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `type` | **(Obligatoriskt)** Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `notes`. |
| `attributes.text` | **(Obligatoriskt)** Texten som omfattar anteckningen. Varje anteckning är begränsad till 512 Unicode-tecken. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om den nya anteckningen.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
