---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Konfigurera ett beräknat attributfält
type: Documentation
description: Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med API:t för schemaregister för att definiera ett schema och en anpassad fältgrupp som innehåller det beräknade attributfältet.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# (Alfa) Konfigurera ett beräknat attributfält med API:t för schemaregister

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med API:t för schemaregister för att definiera ett schema och en anpassad schemafältgrupp som innehåller det beräknade attributfältet. Vi rekommenderar att du skapar ett separat&quot;Beräknade attribut&quot;-schema och en fältgrupp där din organisation kan lägga till attribut som ska användas som beräknade attribut. På så sätt kan din organisation separera det beräknade attributschemat från andra scheman som används för datainmatning på ett rent sätt.

Arbetsflödet i det här dokumentet visar hur du använder API:t för schemaregister för att skapa ett profilaktiverat&quot;beräknat attribut&quot;-schema som refererar till en anpassad fältgrupp. Det här dokumentet innehåller exempelkod för beräknade attribut, men se [API-guide för schemaregister](../../xdm/api/overview.md) om du vill ha detaljerad information om hur du definierar fältgrupper och scheman med API:t.

## Skapa en fältgrupp för beräknade attribut

Om du vill skapa en fältgrupp med API:t för schemaregister börjar du med att göra en POST-förfrågan till `/tenant/fieldgroups` slutpunkt och med information om fältgruppen i begärandetexten. Mer information om hur du arbetar med fältgrupper med API:t för schemaregister finns i [API-slutpunktsguide för fältgrupper](../../xdm/api/field-groups.md).

**API-format**

```http
POST /tenant/fieldgroups
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `title` | Namnet på fältgruppen som du skapar. |
| `meta:intendedToExtend` | Den XDM-klass som fältgruppen kan användas med. |

**Svar**

En slutförd begäran returnerar HTTP-svarsstatus 201 (Skapad) med en svarstext som innehåller information om den nyligen skapade fältgruppen, inklusive `$id`, `meta:altIt`och `version`. Dessa värden är skrivskyddade och tilldelas av schemaregistret.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Uppdatera fältgrupp med ytterligare beräknade attribut

När fler beräknade attribut behövs kan du uppdatera fältgruppen med beräknade attribut genom att göra en PUT-begäran till `/tenant/fieldgroups` slutpunkt. Denna begäran kräver att du inkluderar det unika ID:t för fältgruppen som du skapade i sökvägen och alla nya fält som du vill lägga till i brödtexten.

Mer information om hur du uppdaterar en fältgrupp med API:t för schemaregister finns i [API-slutpunktsguide för fältgrupper](../../xdm/api/field-groups.md).

**API-format**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Begäran**

Den här begäran lägger till nya fält som är relaterade till `purchaseSummary` information.

>[!NOTE]
>
>När du uppdaterar en fältgrupp via en PUT-begäran, måste texten innehålla alla fält som krävs när en ny fältgrupp skapas i en POST-begäran.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Svar**

Ett godkänt svar returnerar information om den uppdaterade fältgruppen.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa ett profilaktiverat schema

Om du vill skapa ett schema med API:t för schemaregistret börjar du med att göra en POST-förfrågan till `/tenant/schemas` slutpunkt och information om schemat i begärandetexten. Schemat måste även aktiveras för [!DNL Profile] och visas som en del av unionsschemat för schemaklassen.

Mer information om [!DNL Profile]-aktiverade scheman och föreningsscheman, se [[!DNL Schema Registry] API-guide](../../xdm/api/overview.md) och [grundläggande dokumentation för schemakomposition](../../xdm/schema/composition.md).

**API-format**

```http
POST /tenants/schemas
```

**Begäran**

Följande begäran skapar ett nytt schema som refererar till `computedAttributesFieldGroup` som har skapats tidigare i det här dokumentet (med dess unika ID) och är aktiverat för profilföreningsschemat (med `meta:immutableTags` array). Detaljerade instruktioner om hur du skapar ett schema med API:t för schematabellen finns i [slutpunktshandbok för schemas API](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om det nyligen skapade schemat, inklusive `$id`, `meta:altId`och `version`. Dessa värden är skrivskyddade och tilldelas av schemaregistret.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Nästa steg

Nu när du har skapat ett schema och en fältgrupp där dina beräknade attribut ska lagras, kan du skapa det beräknade attributet med `/computedattributes` API-slutpunkt. Följ stegen i [API-slutpunktsguide för beräknade attribut](ca-api.md).
