---
keywords: Experience Platform;hem;populära ämnen;schema;schema;xdm;Experience data model;namespace;namespaces;compatibility mode;xed;
solution: Experience Platform
title: Namnavstånd i Experience Data Model (XDM)
description: Lär dig hur namnavstånd i Experience Data Model (XDM) gör att du kan utöka dina scheman och förhindra fältkollisioner när olika schemakomponenter sammanförs.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Namnavstånd i Experience Data Model (XDM)

>[!IMPORTANT]
>
>I XDM används namnutrymmet (avsnittet på den här sidan) för att särskilja fält i ett schema. Detta skiljer sig från begreppet identitetsnamnutrymme i identitetstjänsten, där namnutrymme används för att skilja på identitetsvärden. Mer information finns i dokumentationen om [namnområdet i identitetstjänsten](../../identity-service/features/namespaces.md).

Alla fält i XDM-scheman (Experience Data Model) har ett associerat namnutrymme. Med dessa namnutrymmen kan du utöka dina scheman och förhindra fältkollisioner när olika schemakomponenter sammanförs. Det här dokumentet innehåller en översikt över namnutrymmen i XDM och hur de visas i [API:t för schemaregister](../api/overview.md).

Med namnmellanrum kan du definiera ett fält i ett namnutrymme så att det betyder något annat än samma fält i ett annat namnutrymme. I praktiken visar namnutrymmet för ett fält vem som skapade fältet (till exempel standard-XDM (Adobe), en leverantör eller din organisation).

Ta till exempel ett XDM-schema som använder fältgruppen [[!UICONTROL Personal Contact Details] ](../field-groups/profile/demographic-details.md), som har ett standardfält `mobilePhone` som finns i namnområdet `xdm`. I samma schema kan du även skapa ett separat `mobilePhone`-fält under ett annat namnområde (ditt [klientorganisations-ID](../api/getting-started.md#know-your-tenant_id)). Båda dessa fält kan samexistera med olika underliggande betydelse eller begränsningar.

## Namnområdessyntax

I följande avsnitt visas hur namnutrymmen tilldelas i XDM-syntax.

### Standard XDM {#standard}

Standardsyntaxen för XDM ger dig insikt i hur namnutrymmen representeras i scheman (inklusive [hur de översätts i Adobe Experience Platform](#compatibility)).

Standard-XDM använder [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts)-syntax för att tilldela namnutrymmen till fält. Det här namnutrymmet kommer i form av en URI (till exempel `https://ns.adobe.com/xdm` för namnutrymmet `xdm`) eller som ett kortskriftsprefix som har konfigurerats i attributet `@context` för ett schema.

Följande är ett exempelschema för en produkt i standard-XDM-syntax. Med undantag för `@id` (den unika identifieraren som definieras av JSON-LD-specifikationen), börjar varje fält under `properties` med ett namnutrymme och slutar med fältnamnet. Om du använder ett kortskriftsprefix som definieras under `@context` avgränsas namnutrymmet och fältnamnet med ett kolon (`:`). Om inget prefix används avgränsas namnutrymmet och fältnamnet med ett snedstreck (`/`).

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
| `@id` | En unik identifierare för posten som den definieras av [JSON-LD-specifikationen](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Ett exempel på ett fält där ett kortskriftsprefix används för att ange ett namnutrymme. I det här fallet är `xdm` namnutrymmet (`https://ns.adobe.com/xdm`) och `sku` fältnamnet. |
| `https://ns.adobe.com/xdm/channels/application` | Ett exempel på ett fält som använder den fullständiga namnområdes-URI:n. I det här fallet är `https://ns.adobe.com/xdm/channels` namnutrymmet och `application` fältnamnet. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Fält som tillhandahålls av leverantörsresurser använder sina egna unika namnutrymmen. I det här exemplet är `https://ns.adobe.com/vendorA/product` leverantörens namnområde och `stockNumber` är fältnamnet. |
| `tenantId:internalSku` | Fält som definieras av din organisation använder ditt unika klientorganisations-ID som namnutrymme. I det här exemplet är `tenantId` innehavarens namnutrymme (`https://ns.adobe.com/tenantId`) och `internalSku` är fältnamnet. |

{style="table-layout:auto"}

### Kompatibilitetsläge {#compatibility}

I Adobe Experience Platform representeras XDM-scheman i syntaxen [Kompatibilitetsläge](../api/appendix.md#compatibility) , som inte använder JSON-LD-syntaxen för att representera namnutrymmen. I stället konverterar Platform namnutrymmet till ett överordnat fält (med början med ett understreck) och kapslar fälten under det.

Standard-XDM `repo:createdDate` konverteras till `_repo.createdDate` och visas under följande struktur i kompatibilitetsläge:

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

Fält som använder namnutrymmet `xdm` visas som rotfält under `properties` och släpper prefixet `xdm:` som skulle visas i [standard-XDM-syntax](#standard). Till exempel visas `xdm:sku` bara som `sku` i stället.

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

I den här handboken finns en översikt över XDM-namnutrymmen och hur de representeras i JSON. Mer information om hur du konfigurerar XDM-scheman med API:t finns i [API-guiden för schemaregister](../api/overview.md).
