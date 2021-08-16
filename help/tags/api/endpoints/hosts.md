---
title: Värdslutpunkt
description: Lär dig hur du anropar slutpunkten /hosts i Reaktors API.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Värdslutpunkt

>[!NOTE]
>
>I det här dokumentet beskrivs hur du hanterar värdar i Reaktors API. Mer allmän information om värdar för taggar finns i guiden om [värdar översikt](../../ui/publishing/hosts/hosts-overview.md) i publiceringsdokumentationen.

I Reactor API definierar en värd ett mål där en [build](./builds.md) kan levereras.

När ett bygge begärs av en tagganvändare i Adobe Experience Platform kontrollerar systemet biblioteket för att avgöra vilken [miljö](./environments.md) biblioteket ska byggas på. Varje miljö har en relation med en värd som visar var bygget ska levereras.

En värd tillhör exakt en [egenskap](./properties.md), medan en egenskap kan ha många värdar. En egenskap måste ha minst en värd innan du kan publicera.

En värd kan användas av mer än en miljö i en egenskap. Det är vanligt att ha en enda värd på en egenskap, och att alla miljöer på den egenskapen använder samma värd.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta en lista med värdar {#list}

Du kan hämta en lista över värdar för en egenskap genom att ta med egenskapens ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | `id` för egenskapen som äger värdarna. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade värdar filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Mer information finns i guiden [filtrera svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar en lista med värdar för den angivna egenskapen.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Söka efter en värd {#lookup}

Du kan söka efter en värd genom att ange dess ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /hosts/{HOST_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `HOST_ID` | `id` för värden som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar informationen om värden.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Skapa en värd {#create}

Du kan skapa en ny värd genom att göra en POST-förfrågan.

**API-format**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | `id` för den [egenskap](./properties.md) som du definierar värden under. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran skapar en ny värd för den angivna egenskapen. Anropet associerar även värden med ett befintligt tillägg via egenskapen `relationships`. Mer information finns i guiden om [relationer](../guides/relationships.md).

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.name` | **(Obligatoriskt)** Ett läsbart namn för värden. |
| `attributes.type_of` | **(Obligatoriskt)** Typ av värd. Kan vara ett av två alternativ: <ul><li>`akamai` för värdar som hanteras av  [Adobe](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` för  [SFTP-värdar](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | En valfri privat nyckel som ska användas för värdautentisering. |
| `attributes.path` | Sökvägen som ska läggas till i URL:en för `server`. |
| `attributes.port` | Ett heltal som anger vilken serverport som ska användas. |
| `attributes.server` | Serverns värd-URL. |
| `attributes.username` | Ett valfritt användarnamn för autentisering. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `hosts`. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade värden.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Uppdatera en värd {#update}

>[!NOTE]
>
>Endast SFTP-värdar kan uppdateras.

Du kan uppdatera en värd genom att inkludera dess ID i sökvägen för en PATCH-begäran.

**API-format**

```http
PATCH /hosts/{HOST_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `HOST_ID` | `id` för värden som du vill uppdatera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran uppdaterar `name` för en befintlig värd.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | Ett objekt vars egenskaper representerar attributen som ska uppdateras för värden. Följande attribut kan uppdateras för en värd: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | `id` för värden som du vill uppdatera. Detta ska matcha `{HOST_ID}`-värdet som anges i sökvägen till begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `hosts`. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den uppdaterade värden.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Ta bort en värd

Du kan ta bort en värd genom att ta med dess ID i sökvägen för en DELETE-begäran.

**API-format**

```http
DELETE /hosts/{HOST_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `HOST_ID` | `id` för värden som du vill ta bort. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext, vilket anger att värden har tagits bort.

## Hämta relaterade resurser för en värd {#related}

Följande anrop visar hur du hämtar relaterade resurser för en värd. När [söker upp en värd](#lookup) listas dessa relationer under egenskapen `relationships`.

Se [relationsguiden](../guides/relationships.md) för mer information om relationer i Reactor API.

### Söka efter den relaterade egenskapen för en värd {#property}

Du kan söka efter egenskapen som äger en värd genom att lägga till `/property` i sökvägen för en sökbegäran.

**API-format**

```http
GET /hosts/{HOST_ID}/property
```

| Parameter | Beskrivning |
| --- | --- |
| `{HOST_ID}` | `id` för värden vars egenskap du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om den angivna värdens egenskap.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
