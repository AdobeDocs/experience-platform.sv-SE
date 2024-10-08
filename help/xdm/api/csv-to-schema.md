---
title: CSV-mall till API-slutpunkt för schemakonvertering
description: Med slutpunkten /rpc/csv2schema i API:t för schemaregister kan du använda CSV-mallar för att automatiskt skapa XDM-scheman (Experience Data Model).
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 3%

---

# CSV-mall till API-slutpunkt för schemakonvertering

Med slutpunkten `/rpc/csv2schema` i API:t [!DNL Schema Registry] kan du automatiskt skapa ett XDM-schema (Experience Data Model) med en CSV-fil som mall. Med den här slutpunkten kan du skapa mallar för att massimportera schemafält och skära ned på manuellt API- eller gränssnittsarbete.

## Komma igång

Slutpunkten `/rpc/csv2schema` är en del av [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Adobe Experience Platform-API.

Slutpunkten `/rpc/csv2schema` är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i API:t [!DNL Schema Registry] kräver RPC-slutpunkter inga ytterligare rubriker som `Accept` eller `Content-Type`, och använder inte `CONTAINER_ID`. I stället måste de använda namnutrymmet `/rpc`, vilket visas i API-anropen nedan.

## Krav för CSV-filer

Om du vill använda den här slutpunkten måste du först skapa en CSV-fil med lämpliga kolumnrubriker och motsvarande värden. Vissa kolumner är obligatoriska, medan resten är valfria. Tabellen nedan beskriver de här kolumnerna och deras roll när det gäller att skapa scheman.

| CSV-rubrikposition | CSV-rubriknamn | Obligatoriskt/valfritt | Beskrivning |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Valfritt | När det är inkluderat och inställt på `true`, anger att fältet inte är klart för API-överföring och ska ignoreras. |
| 2 | `isCustom` | Obligatoriskt | Anger om fältet är ett anpassat fält eller inte. |
| 3 | `fieldGroupId` | Valfritt | ID:t för fältgruppen som ett anpassat fält ska associeras med. |
| 4 | `fieldGroupName` | (Se beskrivning) | Namnet på fältgruppen som det här fältet ska associeras med.<br><br>Valfritt för anpassade fält som inte utökar befintliga standardfält. Om inget anges tilldelas namnet automatiskt.<br><br>Krävs för standardfält eller anpassade fält som utökar standardfältgrupper, som används för att fråga `fieldGroupId`. |
| 5 | `fieldPath` | Obligatoriskt | Den fullständiga XED-punktnotation-sökvägen för fältet. Om du vill ta med alla fält från en standardfältgrupp (som anges under `fieldGroupName`) anger du värdet `ALL`. |
| 6 | `displayName` | Valfritt | Fältets rubrik eller egna visningsnamn. Kan även vara ett alias för titeln om det finns något. |
| 7 | `fieldDescription` | Valfritt | En beskrivning av fältet. Kan även vara ett alias för beskrivningen om det finns ett sådant. |
| 8 | `dataType` | (Se beskrivning) | Anger fältets [grundläggande datatyp](../schema/field-constraints.md#basic-types). Krävs för alla anpassade fält.<br><br>Om `dataType` är inställt på `object` måste antingen `properties` eller `$ref` också definieras för samma rad, men inte båda. |
| 9 | `isRequired` | Valfritt | Anger om fältet är obligatoriskt för dataöverföring. |
| 10 | `isArray` | Valfritt | Anger om fältet är en matris av det angivna `dataType`. |
| 11 | `isIdentity` | Valfritt | Anger om fältet är ett identitetsfält. |
| 12 | `identityNamespace` | Krävs om `isIdentity` är sant | [ID-namnområdet](../../identity-service/features/namespaces.md) för identitetsfältet. |
| 13 | `isPrimaryIdentity` | Valfritt | Anger om fältet är schemats primära identitet. |
| 14 | `minimum` | Valfritt | (Endast för numeriska fält) Det lägsta värdet för fältet. |
| 15 | `maximum` | Valfritt | (Endast för numeriska fält) Det maximala värdet för fältet. |
| 16 | `enum` | Valfritt | En lista med uppräkningsvärden för fältet, uttryckt som en array (t.ex. `[value1,value2,value3]`). |
| 17 | `stringPattern` | Valfritt | (Endast för strängfält) Ett regex-mönster som strängvärdet måste matcha för att validering ska kunna utföras under dataöverföring. |
| 18 | `format` | Valfritt | (Endast för strängfält) Strängfältets format. |
| 19 | `minLength` | Valfritt | (Endast för strängfält) Strängfältets minimilängd. |
| 20 | `maxLength` | Valfritt | (Endast för strängfält) Strängfältets maximala längd. |
| 21 | `properties` | (Se beskrivning) | Krävs om `dataType` är inställt på `object` och `$ref` inte är definierad. Detta definierar objektets innehåll som en JSON-sträng (t.ex. `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Se beskrivning) | Krävs om `dataType` är inställt på `object` och `properties` inte är definierad. Detta definierar `$id` för det refererade objektet för objekttypen (till exempel `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Valfritt | När `isIgnored` är inställt på `true` används den här kolumnen för att ange schemats rubrikinformation. |

{style="table-layout:auto"}

Mer information om hur CSV-filen ska formateras finns i följande [CSV-mall](../assets/sample-csv-template.csv).

## Skapa en exportnyttolast från en CSV-fil

När du har konfigurerat CSV-mallen kan du skicka filen till `/rpc/csv2schema`-slutpunkten och konvertera den till en exportnyttolast.

**API-format**

```http
POST /rpc/csv2schema
```

**Begäran**

Nyttolasten för begäran måste använda formulärdata som format. Nödvändiga formulärfält visas nedan.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Egenskap | Beskrivning |
| --- | --- |
| `csv-file` | Sökvägen till CSV-mallen som lagras på den lokala datorn. |
| `schema-class-id` | `$id` för XDM-klassen [class](../schema/composition.md#class) som det här schemat använder. |
| `schema-name` | Schemats visningsnamn. |
| `schema-description` | En beskrivning av schemat. |

**Svar**

Ett godkänt svar returnerar en exportnyttolast som genererades från CSV-filen. Nyttolasten har en form av en array, och varje arrayobjekt är ett objekt som representerar en beroende XDM-komponent för schemat. Markera avsnittet nedan om du vill visa ett fullständigt exempel på en exportnyttolast som genererats från en CSV-fil.

+++ Exempel på nyttolast för svar

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importera schemanyttolasten

När du har genererat exportnyttolasten från CSV-filen kan du skicka den nyttolasten till `/rpc/import`-slutpunkten för att generera schemat.

Mer information om hur du genererar scheman från exportnyttolaster finns i [importguiden](./import.md).
