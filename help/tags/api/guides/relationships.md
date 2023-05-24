---
title: Relationer i reaktors-API
description: Lär dig hur resursrelationer etableras i Reactor API, inklusive relationskraven för varje resurs.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# Relationer i reaktors-API

Resurserna i Reaktors API är ofta relaterade till varandra. Det här dokumentet innehåller en översikt över hur resursrelationer är upprättade i API:t och relationskraven för varje resurstyp.

Beroende på vilken typ av resurs det gäller krävs vissa relationer. En obligatorisk relation innebär att den överordnade resursen inte kan finnas utan relationen. Alla andra relationer är valfria.

Oberoende av om de är obligatoriska eller valfria etableras relationer antingen automatiskt av systemet när relevanta resurser skapas, eller också måste de skapas manuellt. Om du skapar relationer manuellt finns det två möjliga metoder beroende på den aktuella resursen:

* [Skapa med nyttolast](#payload)
* [Skapa efter URL](#url) (endast för bibliotek)

Se avsnittet om [relationskrav](#requirements) en lista över kompatibla relationer för varje resurstyp och de metoder som krävs för att upprätta dessa relationer, där så är tillämpligt.

## Skapa en relation med nyttolast {#payload}

Vissa relationer måste upprättas manuellt när du skapar en resurs. För att uppnå detta måste du ange en `relationship` -objektet i nyttolasten för begäran när du först skapar den överordnade resursen. Exempel på sådana relationer är:

* [Skapa ett dataelement](../endpoints/data-elements.md#create) med de tillägg som krävs
* [Skapa en miljö](../endpoints/environments.md#create) med den värdrelation som krävs

**API-format**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{PROPERTY_ID}` | ID för egenskapen som resursen tillhör. |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska skapas. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skapar en ny `rule_component`, upprätta relationer med `rules` och `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `relationships` | Ett objekt som måste anges när relationer skapas med nyttolast. Varje nyckel i det här objektet representerar en specifik relationstyp. I exemplet ovan `extension` och `rules` det upprättas relationer som särskilt `rule_components`. Mer information om kompatibla relationstyper för olika resurser finns i avsnittet om [relationskrav per resurs](#relationship-requirements-by-resource). |
| `data` | Varje relationstyp som tillhandahålls under `relationship` objektet måste innehålla `data` -egenskap, som refererar till `id` och `type` för den resurs som en relation upprättas med. Du kan skapa en relation med flera resurser av samma typ genom att formatera `data` som en array med objekt, där varje objekt innehåller `id` och `type` för en tillämplig resurs. |
| `id` | Unikt ID för en resurs. Varje `id` måste åtföljas av ett syskon `type` egenskap, som anger resurstypen i fråga. |
| `type` | Resurstypen som refereras av ett jämlikt objekt `id` fält. Godkända värden är `data_elements`, `rules`, `extensions`och `environments`. |

{style="table-layout:auto"}

## Skapa en relation utifrån URL {#url}

Till skillnad från andra resurser upprättar bibliotek relationer genom sina egna `/relationship` slutpunkter. Exempel:

* [Lägga till tillägg, dataelement och regler i ett bibliotek](../endpoints/libraries.md#add-resources)
* [Tilldela ett bibliotek till en miljö](../endpoints/libraries.md#environment)

**API-format**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{PROPERTY_ID}` | ID för egenskapen som biblioteket tillhör. |
| `{LIBRARY_ID}` | ID:t för det bibliotek som du vill skapa en relation för. |
| `{RESOURCE_TYPE}` | Den typ av resurs som relationen har som mål. Tillgängliga värden inkluderar `environment`, `data_elements`, `extensions`och `rules`. |

**Begäran**

Följande begäran använder `/relationships/environment` slutpunkt för ett bibliotek för att skapa en relation med en miljö.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `data` | Ett objekt som refererar till `id` och `type` av målresursen för relationen. Om du skapar en relation med flera resurser av samma typ (till exempel `extensions` och `rules`), `data` -egenskapen måste formateras som en array med objekt, där varje objekt innehåller `id` och `type` för en tillämplig resurs. |
| `id` | Unikt ID för en resurs. Varje `id` måste åtföljas av ett syskon `type` egenskap, som anger resurstypen i fråga. |
| `type` | Resurstypen som refereras av ett jämlikt objekt `id` fält. Godkända värden är `data_elements`, `rules`, `extensions`och `environments`. |

{style="table-layout:auto"}

## Relationskrav per resurs {#requirements}

I följande tabeller beskrivs de tillgängliga relationerna för varje resurstyp, oavsett om dessa relationer är nödvändiga eller inte, och den metod som accepteras för att manuellt skapa relationen där det är tillämpligt.

>[!NOTE]
>
>Om en relation inte listas som skapad av nyttolast eller URL tilldelas den automatiskt av systemet.

### Granskningshändelser

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### Bygger

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Återanrop

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Företag

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### Dataelement

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Miljöer

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Tillägg

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Värdar

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Bibliotek

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style="table-layout:auto"}

### Anteckningar

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### Egenskaper

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### Regelkomponenter

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### Regler

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### Hemligheter

| Relation | Obligatoriskt | Skapa med nyttolast | Skapa efter URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

