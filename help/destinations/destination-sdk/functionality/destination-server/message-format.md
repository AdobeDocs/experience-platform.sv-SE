---
description: På den här sidan behandlas meddelandeformatet och profilomvandlingen i data som exporteras från Adobe Experience Platform till mål.
title: Meddelandeformat
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2489'
ht-degree: 0%

---

# Meddelandeformat

## Krav - Adobe Experience Platform koncept {#prerequisites}

Om du vill veta mer om meddelandeformat, profilkonfiguration och transformeringsprocess på Adobe kan du bekanta dig med följande koncept för Experience Platform:

* **Experience Data Model (XDM)**. [XDM-översikt](../../../../xdm/home.md) och [Så här skapar du ett XDM-schema i Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Klass**. [Skapa och redigera klasser i användargränssnittet](../../../../xdm/ui/resources/classes.md).
* **IdentityMap**. Identitetskartan representerar en karta över alla slutanvändaridentiteter i Adobe Experience Platform. Se `xdm:identityMap` i [XDM-fältordlistan](../../../../xdm/schema/field-dictionary.md).
* **Segmentmedlemskap**. XDM-attributet [segmentMembership](../../../../xdm/schema/field-dictionary.md) informerar vilka målgrupper en profil tillhör. Läs dokumentationen om schemafältgruppen [Information om målgruppsmedlemskap](../../../../xdm/field-groups/profile/segmentation.md) för de tre olika värdena i fältet `status`.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja (endast steg 1 och 2 i diagrammet längre ned) |

## Översikt {#overview}

På den här sidan behandlas meddelandeformatet och profilomvandlingen i data som exporteras från Adobe Experience Platform till mål.

Adobe Experience Platform exporterar data till ett stort antal destinationer, i olika dataformat. Några exempel på destinationstyper är annonsplattformar (Google), sociala nätverk (Facebook) och molnlagringsplatser (Amazon S3, Azure Event Hubs).

Experience Platform kan justera meddelandeformatet för exporterade profiler så att de matchar det förväntade formatet på din sida. För att förstå den här anpassningen är följande koncept viktiga:

* Källa (1) och mål (2) XDM-schema i Adobe Experience Platform
* Det förväntade meddelandeformatet på partnersidan (3), och
* Omformningslagret mellan XDM-schema och det förväntade meddelandeformatet, som du kan definiera genom att skapa en [meddelandeomformningsmall](#using-templating).

![Schema till JSON-omvandling](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform använder XDM-scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Source XDM-schema (1)**: Det här objektet refererar till det schema som kunder använder i Experience Platform. I Experience Platform, i [mappningssteget](../../../ui/activate-segment-streaming-destinations.md#mapping) för aktiveringsmålarbetsflödet, mappar kunder fält från sitt XDM-schema till målschemat (2) för ditt mål.

**Mål-XDM-schema (2)**: Baserat på JSON-standardschemat (3) för målets förväntade format och de attribut som destinationen kan tolka, kan du definiera profilattribut och identiteter i mål-XDM-schemat. Du kan göra detta i målkonfigurationen, i objekten [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) och [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) .

**JSON-standardschema för målprofilattributen (3)**: Det här exemplet representerar ett [JSON-schema](https://json-schema.org/learn/miscellaneous-examples.html) med alla profilattribut som din plattform stöder och deras typer (t.ex. objekt, sträng, matris). Exempelfält som ditt mål kan stödja kan vara `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` och så vidare. Du behöver en [meddelandeomformningsmall](#using-templating) för att anpassa data som exporteras från Experience Platform till det förväntade formatet.

Baserat på schemaomvandlingarna som beskrivs ovan, är det här hur en profilkonfiguration ändras mellan käll-XDM-schemat och ett exempelschema på partnersidan:

![Exempel på omformningsmeddelande](../../assets/functionality/destination-server/transformations-with-examples.png)

## Komma igång - omforma tre grundläggande attribut {#getting-started}

För att demonstrera profilomvandlingsprocessen använder exemplet nedan tre vanliga profilattribut i Adobe Experience Platform: **förnamn**, **efternamn** och **e-postadress**.

>[!NOTE]
>
>Kunden mappar attributen från XDM-källschemat till XDM-partnerschemat i Adobe Experience Platform-gränssnittet i **Mapping**-steget i [aktivera målarbetsflödet](../../../ui/activate-segment-streaming-destinations.md#mapping).

Anta att din plattform kan ta emot ett meddelandeformat som:

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Med tanke på meddelandeformatet är motsvarande omformningar följande:

| Attribut i partner-XDM-schema på Adobe | Omformning | Attribut i HTTP-meddelande på din sida |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Profilstruktur i Experience Platform {#profile-structure}

För att förstå exemplen längre ned på sidan är det viktigt att du känner till strukturen för en profil i Experience Platform.

Profiler har tre avsnitt:

* `segmentMembership` (finns alltid i en profil)
   * det här avsnittet innehåller alla målgrupper som finns i profilen. Målgrupperna kan ha en av två statusvärden: `realized` eller `exited`.
* `identityMap` (finns alltid i en profil)
   * det här avsnittet innehåller alla identiteter som finns i profilen (e-post, Google GAID, Apple IDFA och så vidare) och som användaren har mappat för export i aktiveringsarbetsflödet.
* attribut (beroende på målkonfigurationen kan dessa finnas i profilen). Det finns också en liten skillnad mellan fördefinierade attribut och frihandsattribut:
   * för *frihandsattribut* innehåller de en `.value`-sökväg om attributet finns i profilen (se attributet `lastName` från exempel 1). Om de inte finns med i profilen innehåller de inte sökvägen `.value` (se attributet `firstName` från exempel 1).
   * för *fördefinierade attribut* innehåller de ingen `.value`-sökväg. Alla mappade attribut som finns i en profil finns i attributmappningen. De som inte finns kommer inte att finnas (se exempel 2 - attributet `firstName` finns inte i profilen).

Se två exempel på profiler i Experience Platform nedan:

### Exempel 1 med `segmentMembership`, `identityMap` och attribut för frihandsattribut {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Exempel 2 med `segmentMembership`, `identityMap` och attribut för fördefinierade attribut {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Använda ett mallspråk för omvandlingar av identitet, attribut och målgruppsmedlemskap {#using-templating}

Adobe använder [dubbelmallar](https://pebbletemplates.io/), ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), för att omvandla fälten från Experience Platform XDM-schemat till ett format som stöds av ditt mål.

Det här avsnittet innehåller flera exempel på hur dessa omformningar görs - från XDM-indataschemat, via mallen och från utdata i nyttolastformat som accepteras av målet. Exemplen nedan presenteras av ökad komplexitet, enligt följande:

1. Exempel på enkla omformningar. Lär dig hur mallar fungerar med enkla omformningar för fälten [Profilattribut](#attributes), [Målgruppsmedlemskap](#segment-membership) och [Identitet](#identities).
2. Exemplen på ökad komplexitet för mallar som kombinerar fälten ovan: [Skapa en mall som skickar målgrupper och identiteter](./message-format.md#segments-and-identities) och [Skapa en mall som skickar segment, identiteter och profilattribut](#segments-identities-attributes).
3. Mallar som innehåller aggregeringsnyckeln. När du använder [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) i målkonfigurationen grupperar Experience Platform de profiler som exporteras till ditt mål baserat på kriterier som målgrupps-ID, målgruppsstatus eller identitetsnamnutrymmen.

### Profilattribut {#attributes}

Information om hur du omformar profilattributen som exporteras till ditt mål finns i JSON- och kodexemplen nedan.

>[!IMPORTANT]
>
>En lista över alla tillgängliga profilattribut i Adobe Experience Platform finns i [XDM-fältordlistan](../../../../xdm/schema/field-dictionary.md).


**Indata**

Profil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Profil 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultat**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Målgruppsmedlemskap {#audience-membership}

XDM-attributet [segmentMembership](../../../../xdm/schema/field-dictionary.md) informerar vilka målgrupper en profil tillhör.
Läs dokumentationen om schemafältgruppen [Information om målgruppsmedlemskap](../../../../xdm/field-groups/profile/segmentation.md) för de tre olika värdena i fältet `status`.

**Indata**

Profil 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Profil 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultat**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identiteter {#identities}

Mer information om identiteter i Experience Platform finns i [Namnområdesöversikten för identitet](../../../../identity-service/features/namespaces.md).

**Indata**

Profil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Profil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultat**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Skapa en mall som skickar målgrupper och identiteter {#segments-and-identities}

I det här avsnittet finns ett exempel på en vanlig omvandling mellan Adobe XDM-schemat och partnermålschemat.
I exemplet nedan visas hur du omvandlar målgruppsmedlemskap och identiteter och skickar dem till ditt mål.

**Indata**

Profil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering audiences by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultat**

`json` nedan representerar data som exporteras från Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Skapa en mall som skickar segment, identiteter och profilattribut {#segments-identities-attributes}

I det här avsnittet finns ett exempel på en vanlig omvandling mellan Adobe XDM-schemat och partnermålschemat.

Ett annat vanligt användningsexempel är export av data som innehåller målgruppsmedlemskap, identiteter (till exempel e-postadress, telefonnummer, reklam-ID) och profilattribut. Se exemplet nedan om du vill exportera data på det här sättet:

**Indata**

Profil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Resultat**

`json` nedan representerar data som exporteras från Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Inkludera aggregeringsnyckel i mallen för att få åtkomst till exporterade profiler grupperade efter olika villkor {#template-aggregation-key}

När du använder [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) i målkonfigurationen kan du gruppera de profiler som exporteras till ditt mål baserat på kriterier som målgrupps-ID, målgruppalias, målgruppsmedlemskap eller identitetsnamnutrymmen.

I meddelandeomformningsmallen kan du komma åt de aggregeringsnycklar som nämns ovan, vilket visas i exemplen i följande avsnitt. Använd aggregeringsnycklar för att strukturera HTTP-meddelandet som exporterats utanför Experience Platform så att det matchar de format- och hastighetsbegränsningar som förväntas av ditt mål.

#### Använd aggregeringsnyckeln för målgrupps-ID i mallen {#aggregation-key-segment-id}

Om du använder [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) och anger `includeSegmentId` som true grupperas profilerna i HTTP-meddelandena som exporteras till ditt mål efter målgrupps-ID. Se nedan hur du kan komma åt målgrupps-ID i mallen.

**Indata**

Tänk på de fyra profilerna nedan, där:

* de första två är en del av målgruppen med målgrupps-ID `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* den tredje profilen är en del av målgruppen med målgrupps-ID `8f812592-3f06-416b-bd50-e7831848a31a`
* den fjärde profilen är en del av båda målgrupperna ovan.

Profil 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observera nedan hur `audienceId` används i mallen för att komma åt målgrupps-ID:n. I det här exemplet antas att du använder `audienceId` som målgruppsmedlemskap i din måltaxonomi. Du kan använda vilket annat fältnamn som helst, beroende på din egen taxonomi.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultat**

När profilerna exporteras till ditt mål delas de upp i två grupper utifrån deras målgrupps-ID.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Använd aggregeringsnyckeln för målgruppsalias i mallen {#aggregation-key-segment-alias}

Om du använder [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) och anger `includeSegmentId` som true kan du även få åtkomst till målgruppsalias i mallen.

Lägg till raden nedan i mallen för att komma åt de exporterade profilerna grupperade efter målgruppsalias.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Använd aggregeringsnyckeln för målgruppsstatus i mallen {#aggregation-key-segment-status}

Om du använder [konfigurerbar aggregering](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) och anger `includeSegmentId` och `includeSegmentStatus` till true kan du komma åt målgruppsstatusen i mallen. På så sätt kan du gruppera profiler i de HTTP-meddelanden som exporteras till ditt mål baserat på om profilerna ska läggas till eller tas bort från segment.

Möjliga värden är:

* realiserad
* befintlig
* avslutad

Lägg till raden nedan i mallen för att lägga till eller ta bort profiler från segment baserat på värdena ovan:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Använd aggregering för identitetsnamnrymd i mallen {#aggregation-key-identity}

Nedan visas ett exempel där den [konfigurerbara aggregeringen](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) i målkonfigurationen är inställd på att aggregera exporterade profiler efter identitetsnamnutrymmen, i formatet `"namespaces": ["email", "phone"]` och `"namespaces": ["GAID", "IDFA"]`. Mer information om gruppering finns i `groups`-parametern i dokumentationen för [skapa destinationskonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md).

**Indata**

Profil 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Profil 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""`, innan du infogar [mallen](../../functionality/destination-server/templating-specs.md) i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observera att `input.aggregationKey.identityNamespaces` används i mallen nedan

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Resultat**

När profilerna exporteras till ditt mål delas de upp i två grupper utifrån deras ID-namnutrymmen. E-post och telefon finns i en grupp, medan GAID och IDFA är i en annan.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Använda aggregeringsnyckeln i en URL-mall {#aggregation-key-url-template}

Beroende på ditt användningssätt kan du även använda de aggregeringsnycklar som beskrivs här i en URL, som visas nedan:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referens: Kontext och funktioner som används i omformningsmallar {#reference}

Kontexten som anges för mallen innehåller `input` (profilerna/data som exporteras i det här anropet) och `destination` (data om målet som Adobe skickar data till, giltigt för alla profiler).

Tabellen nedan innehåller beskrivningar av funktionerna i exemplen ovan.

| Funktion | Beskrivning | Exempel |
|---------|----------|----------|
| `input.profile` | Profilen, representerad som en [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Följer det XDM-schema för partner som nämns ovan på den här sidan. |
| `hasSegments` | Den här funktionen tar en karta över ID:n för namnområdesmålgrupp som parameter. Funktionen returnerar `true` om det finns minst en publik på kartan (oavsett dess status), och i annat fall `false`. Du kan använda den här funktionen för att bestämma om du vill iterera över en karta med målgrupper eller inte. | `hasSegments(input.profile.segmentMembership)` |
| `destination.namespaceSegmentAliases` | Mappa från målgrupps-ID:n i ett specifikt Adobe Experience Platform-namnområde till målgruppsalias i partnerns system. | `destination.namespaceSegmentAliases["ups"]["seg-id-1"]` |
| `destination.namespaceSegmentNames` | Mappa från målgruppsnamn i specifika Adobe Experience Platform-namnutrymmen till målgruppsnamn i partnersystemet. | `destination.namespaceSegmentNames["ups"]["seg-name-1"]` |
| `destination.namespaceSegmentTimestamps` | Returnerar den tid då en målgrupp skapades, uppdaterades eller aktiverades i UNIX-tidsstämpelformat. | <ul><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].createdAt`: returnerar den tid då segmentet med ID `seg-id-1`, från namnområdet `ups`, skapades i UNIX-tidsstämpelformat.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].updatedAt`: returnerar den tid då målgruppen med ID `seg-id-1` från namnområdet `ups` uppdaterades i UNIX-tidsstämpelformat.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingCreatedAt`: returnerar den tid då målgruppen med ID `seg-id-1`, från namnområdet `ups`, aktiverades till målet i UNIX-tidsstämpelformat.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingUpdatedAt`: returnerar den tid då målgruppsaktiveringen uppdaterades på målet, i UNIX-tidsstämpelformat.</li></ul> |
| `addedSegments(mapOfNamespacedSegmentIds)` | Returnerar endast de målgrupper som har statusen `realized`, i alla namnutrymmen. | `addedSegments(input.profile.segmentMembership)` |
| `removedSegments(mapOfNamespacedSegmentIds)` | Returnerar endast de målgrupper som har statusen `exited`, i alla namnutrymmen. | `removedSegments(input.profile.segmentMembership)` |
| `destination.segmentAliases` | **Föråldrad. Ersatt av`destination.namespaceSegmentAliases`** <br><br> Mappa från målgrupps-ID:n i Adobe Experience Platform-namnområdet till målgruppsalias i partnerns system. | `destination.segmentAliases["seg-id-1"]` |
| `destination.segmentNames` | **Föråldrad. Ersatt av`destination.namespaceSegmentNames`** <br><br> Mappa från målgruppsnamn i Adobe Experience Platform-namnområdet till målgruppsnamn i partnerns system. | `destination.segmentNames["seg-name-1"]` |
| `destination.segmentTimestamps` | **Föråldrad. Ersatt av`destination.namespaceSegmentTimestamps`** <br><br> Returnerar den tid då en målgrupp skapades, uppdaterades eller aktiverades i UNIX-tidsstämpelformat. | <ul><li>`destination.segmentTimestamps["seg-id-1"].createdAt`: returnerar den tid då målgruppen med ID:t `seg-id-1` skapades, i UNIX-tidsstämpelformat.</li><li>`destination.segmentTimestamps["seg-id-1"].updatedAt`: returnerar den tid då målgruppen med ID `seg-id-1` uppdaterades, i UNIX-tidsstämpelformat.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingCreatedAt`: returnerar den tid då målgruppen med ID `seg-id-1` aktiverades till målet, i UNIX-tidsstämpelformat.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingUpdatedAt`: returnerar den tid då målgruppsaktiveringen uppdaterades på målet, i UNIX-tidsstämpelformat.</li></ul> |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst det här dokumentet kan du nu se hur data som exporteras från Experience Platform omformas. Läs sedan följande sidor för att lära dig mer om hur du skapar meddelandeomformningsmallar för ditt mål:

* [Skapa och testa en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md)
* [API-åtgärder för återgivningsmall](../../testing-api/streaming-destinations/render-template-api.md)
* [Omformningsfunktioner som stöds i Destinationen SDK](../destination-server/supported-functions.md)

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](server-specs.md)
* [Mallspecifikationer](templating-specs.md)
* [Filformateringskonfiguration](file-formatting.md)
