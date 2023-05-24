---
keywords: Experience Platform;hem;populära ämnen;schema;schema;xdm;Experience data model;namespace;namespaces;compatibility mode;xed;
solution: Experience Platform
title: Namnavstånd i Experience Data Model (XDM)
description: Lär dig hur namnavstånd i Experience Data Model (XDM) gör att du kan utöka dina scheman och förhindra fältkollisioner när olika schemakomponenter sammanförs.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Namnavstånd i Experience Data Model (XDM)

Alla fält i XDM-scheman (Experience Data Model) har ett associerat namnutrymme. Med dessa namnutrymmen kan du utöka dina scheman och förhindra fältkollisioner när olika schemakomponenter sammanförs. Det här dokumentet innehåller en översikt över namnutrymmen i XDM och hur de visas i [API för schemaregister](../api/overview.md).

Med namnmellanrum kan du definiera ett fält i ett namnutrymme så att det betyder något annat än samma fält i ett annat namnutrymme. I praktiken visar namnutrymmet för ett fält vem som skapade fältet (till exempel standard-XDM (Adobe), en leverantör eller din organisation).

Ta till exempel ett XDM-schema som använder [[!UICONTROL Personal Contact Details] fältgrupp](../field-groups/profile/demographic-details.md), som har en standard `mobilePhone` fält som finns i `xdm` namnutrymme. I samma schema kan du även skapa en separat `mobilePhone` fält under ett annat namnutrymme (din [klient-ID](../api/getting-started.md#know-your-tenant_id)). Båda dessa fält kan samexistera med olika underliggande betydelse eller begränsningar.

## Namnområdessyntax

I följande avsnitt visas hur namnutrymmen tilldelas i XDM-syntax.

### Standard XDM {#standard}

Standardsyntaxen för XDM ger insikt i hur namnutrymmen representeras i scheman (inklusive [hur de översätts i Adobe Experience Platform](#compatibility)).

Standard-XDM använder [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) syntax för att tilldela namnutrymmen till fält. Det här namnutrymmet kommer i form av en URI (som `https://ns.adobe.com/xdm` för `xdm` namnutrymme), eller som ett kortskriftsprefix som har konfigurerats i `@context` för ett schema.

Följande är ett exempelschema för en produkt i standard-XDM-syntax. Med undantag av `@id` (den unika identifieraren enligt JSON-LD-specifikationen), varje fält under `properties` börjar med ett namnutrymme och slutar med fältnamnet. Om du använder ett kortskriftsprefix som definieras under `@context`avgränsas namnutrymmet och fältnamnet med ett kolon (`:`). Om du inte använder ett prefix avgränsas namnutrymmet och fältnamnet med ett snedstreck (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@context` | Ett objekt som definierar kortskriftsprefixen som kan användas i stället för ett fullständigt namnområdes-URI under `properties`. |
| `@id` | En unik identifierare för posten som den definieras av [JSON-LD spec](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Ett exempel på ett fält där ett kortskriftsprefix används för att ange ett namnutrymme. I detta fall `xdm` är namnutrymmet (`https://ns.adobe.com/xdm`), och `sku` är fältnamnet. |
| `https://ns.adobe.com/xdm/channels/application` | Ett exempel på ett fält som använder den fullständiga namnområdes-URI:n. I detta fall `https://ns.adobe.com/xdm/channels` är namnutrymmet, och `application` är fältnamnet. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Fält som tillhandahålls av leverantörsresurser använder sina egna unika namnutrymmen. I det här exemplet `https://ns.adobe.com/vendorA/product` är leverantörens namnutrymme, och `stockNumber` är fältnamnet. |
| `tenantId:internalSku` | Fält som definieras av din organisation använder ditt unika klientorganisations-ID som namnutrymme. I det här exemplet `tenantId` är innehavarens namnutrymme (`https://ns.adobe.com/tenantId`), och `internalSku` är fältnamnet. |

{style="table-layout:auto"}

### Kompatibilitetsläge {#compatibility}

I Adobe Experience Platform representeras XDM-scheman i [Kompatibilitetsläge](../api/appendix.md#compatibility) syntax, som inte använder JSON-LD-syntax för att representera namnutrymmen. I stället konverterar Platform namnutrymmet till ett överordnat fält (med början med ett understreck) och kapslar fälten under det.

Standard-XDM `repo:createdDate` konverteras till `_repo.createdDate` och skulle visas under följande struktur i kompatibilitetsläge:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Fält som använder `xdm` namnutrymmet visas som rotfält under `properties` och släpp `xdm:` prefix som skulle visas i [XDM-standardsyntax](#standard). Till exempel: `xdm:sku` anges bara som `sku` i stället.

Följande JSON visar hur standardexemplet på XDM-syntax översätts till kompatibilitetsläge.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Nästa steg

I den här guiden finns en översikt över XDM-namnutrymmen och hur de visas i JSON. Mer information om hur du konfigurerar XDM-scheman med API:t finns i [API-guide för schemaregister](../api/overview.md).
