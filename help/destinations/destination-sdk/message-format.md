---
description: På den här sidan behandlas meddelandeformatet och profilomvandlingen i data som exporteras från Adobe Experience Platform till mål.
title: Meddelandeformat
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# Meddelandeformat

## Förutsättningar - Adobe Experience Platform-koncept {#prerequisites}

Om du vill veta mer om meddelandeformat, profilkonfiguration och transformeringsprocess på Adobe kan du bekanta dig med följande koncept för Experience Platform:

* **Experience Data Model (XDM)**. [XDM-](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) översikt och   [hur du skapar ett XDM-schema i Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Klass**. [Skapa och redigera klasser i användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. Identitetskartan representerar en karta över alla slutanvändaridentiteter i Adobe Experience Platform. Se `xdm:identityMap` i [XDM-fältordlistan](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. XDM-attributet [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) anger vilka segment en profil tillhör. För de tre olika värdena i fältet `status`, läs dokumentationen om schemafältgruppen [Information om segmentmedlemskap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Översikt {#overview}

Använd innehållet på den här sidan tillsammans med resten av [konfigurationsalternativen för partnermål](./configuration-options.md). På den här sidan behandlas meddelandeformatet och profilomvandlingen i data som exporteras från Adobe Experience Platform till mål. Den andra sidan behandlar information om anslutning och autentisering till ditt mål.

Adobe Experience Platform exporterar data till ett stort antal destinationer, i olika dataformat. Några exempel på destinationstyper är annonsplattformar (Google), sociala nätverk (Facebook) och molnlagringsplatser (Amazon S3, Azure Event Hubs).

Experience Platform kan justera meddelandeformatet för exporterade profiler så att de matchar det förväntade formatet på din sida. För att förstå den här anpassningen är följande koncept viktiga:
* Källa (1) och mål (2) XDM-schema i Adobe Experience Platform
* Det förväntade meddelandeformatet på partnersidan (3), och
* Omformningslagret mellan XDM-schemat och det förväntade meddelandeformatet, som du kan definiera genom att skapa en [meddelandeomformningsmall](./message-format.md#using-templating).

![Schema till JSON-omvandling](./assets/transformations-3-steps.png)

Experience Platform använder XDM-scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**XDM-källschema (1)**: Det här objektet refererar till det schema som kunder använder i Experience Platform. I Experience Platform, i [mappningssteget](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) för aktiveringsmålarbetsflödet, mappade kunder fält från sina källscheman till målschemat (2).

**Mål-XDM-schema (2)**: Baserat på JSON-standardschemat (3) för målets förväntade format kan du definiera profilattribut och identiteter i ditt mål-XDM-schema. Detta kan du göra i målkonfigurationen, i objekten [schemaConfig](./destination-configuration.md#schema-configuration) och [identityNamespaces](./destination-configuration.md#identities-and-attributes).

**JSON-standardschema för målprofilens attribut (3)**: Det här objektet representerar en  [JSON-](https://json-schema.org/learn/miscellaneous-examples.html) schema med alla profilattribut som din plattform stöder och deras typer (till exempel: object, string, array). Exempelfält som ditt mål kan ha stöd för kan vara `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` och så vidare. Du behöver en [meddelandeomformningsmall](./message-format.md#using-templating) för att anpassa data som exporteras från Experience Platform till det förväntade formatet.

Baserat på schemaomvandlingarna som beskrivs ovan, är det här hur en profilkonfiguration ändras mellan käll-XDM-schemat och ett exempelschema på partnersidan:

![Exempel på omformningsmeddelande](./assets/transformations-with-examples.png)

<br> 


## Komma igång - omforma tre grundläggande attribut {#getting-started}

I exemplet nedan används tre vanliga profilattribut i Adobe Experience Platform för att demonstrera profilomvandlingsprocessen: **förnamn**, **efternamn** och **e-postadress**.

>[!NOTE]
>
>Kunden mappar attributen från XDM-källschemat till XDM-partnerschemat i Adobe Experience Platform-användargränssnittet i **mappningssteget** i [aktivera målarbetsflödet](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Anta att din plattform kan ta emot ett meddelandeformat som:

```curl
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

## Använda ett mallspråk för identitet, attribut och segmentmedlemskapsomvandlingar {#using-templating}

Adobe använder ett mallspråk som liknar [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) för att omforma fälten från XDM-schemat till ett format som stöds av ditt mål.

Det här avsnittet innehåller flera exempel på hur dessa omformningar görs - från XDM-indataschemat, via mallen och från utdata i nyttolastformat som accepteras av ditt mål. Exemplen nedan presenteras av ökad komplexitet, enligt följande:

1. Exempel på enkla omformningar. Lär dig hur mallar fungerar med enkla omformningar för fälten [Profilattribut](./message-format.md#attributes), [Segmentmedlemskap](./message-format.md#segment-membership) och [Identitet](./message-format.md#identities).
2. Exempel på mallar som kombinerar fälten ovan blir mer komplicerade: [Skapa en mall som skickar segment och identiteter](./message-format.md#segments-and-identities) och [Skapa en mall som skickar segment, identiteter och profilattribut](./message-format.md#segments-identities-attributes).
3. Mallar som innehåller aggregeringsnyckeln. När du använder [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) i målkonfigurationen grupperar Experience Platform de profiler som exporteras till ditt mål baserat på villkor som segment-ID, segmentstatus eller identitetsnamnutrymmen.

### Profilattribut {#attributes}

Information om hur du omformar profilattributen som exporteras till ditt mål finns i JSON- och kodexemplen nedan.

>[!IMPORTANT]
>
>En lista över alla tillgängliga profilattribut i Adobe Experience Platform finns i [XDM-fältordlistan](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Segmentmedlemskap {#segment-membership}

XDM-attributet [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) anger vilka segment en profil tillhör.
För de tre olika värdena i fältet `status`, läs dokumentationen om schemafältgruppen [Information om segmentmedlemskap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

Mer information om identiteter i Experience Platform finns i [Översikt över identitetsnamnrymden](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv).

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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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


### Skapa en mall som skickar segment och identiteter {#segments-and-identities}

I det här avsnittet finns ett exempel på en vanlig omvandling mellan Adobe XDM-schemat och partnermålschemat.
I exemplet nedan visas hur du omformar segmentmedlemskapet och identiteterna och skickar dem till ditt mål.

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
              "status": "existing"
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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering segments by status: #}
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

Ett annat vanligt användningsexempel är export av data som innehåller segmentmedlemskap, identiteter (till exempel: e-postadress, telefonnummer, reklam-ID) och profilattribut. Se exemplet nedan om du vill exportera data på det här sättet:

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
              "status": "existing"
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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

När du använder [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) i målkonfigurationen kan du gruppera de profiler som exporteras till ditt mål baserat på villkor som segment-ID, segmentalias, segmentmedlemskap eller identitetsnamnutrymmen.

I meddelandeomformningsmallen kan du komma åt de aggregeringsnycklar som nämns ovan, vilket visas i exemplen i följande avsnitt. Använd aggregeringsnycklar för att strukturera HTTP-meddelandet som exporterats utanför Experience Platform så att det matchar de format- och hastighetsbegränsningar som förväntas av ditt mål.

#### Använd aggregeringsnyckeln för segment-ID i mallen {#aggregation-key-segment-id}

Om du använder [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) och anger `includeSegmentId` till true grupperas profilerna i HTTP-meddelandena som exporteras till ditt mål efter segment-ID. Se nedan hur du kan komma åt segment-ID:t i mallen.

**Indata**

Tänk på de fyra profilerna nedan, där:
* de första två är en del av segmentet med segment-ID `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* den tredje profilen är en del av segmentet med segment-ID `8f812592-3f06-416b-bd50-e7831848a31a`
* den fjärde profilen är en del av båda segmenten ovan.

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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**Mall**

>[!IMPORTANT]
>
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Observera nedan hur `audienceId` används i mallen för att komma åt segment-ID:n. I det här exemplet antas att du använder `audienceId` för segmentmedlemskap i måltaxonomin. Du kan använda vilket annat fältnamn som helst, beroende på din egen taxonomi.

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

När profilerna exporteras till ditt mål delas de upp i två grupper utifrån deras segment-ID.

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

#### Använd aggregeringsnyckeln för segmentalias i mallen {#aggregation-key-segment-alias}

Om du använder [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) och anger `includeSegmentId` till true kan du även komma åt segmentalias i mallen.

Lägg till raden nedan i mallen för att komma åt de exporterade profilerna grupperade efter segmentalias.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Använd segmentets statusaggregeringsnyckel i mallen {#aggregation-key-segment-status}

Om du använder [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) och anger `includeSegmentId` och `includeSegmentStatus` till true kan du komma åt segmentstatusen i mallen. På så sätt kan du gruppera profiler i de HTTP-meddelanden som exporteras till ditt mål baserat på om profilerna ska läggas till eller tas bort från segment.

Möjliga värden är:

* realiserad
* befintlig
* avslutad

Lägg till raden nedan i mallen för att lägga till eller ta bort profiler från segment baserat på värdena ovan:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Använd aggregering för identitetsnamnrymd i mallen {#aggregation-key-identity}

Nedan visas ett exempel där [konfigurerbar aggregering](./destination-configuration.md#configurable-aggregation) i målkonfigurationen är inställd på att aggregera exporterade profiler efter identitetsnamnutrymmen, i formatet `"namespaces": ["email", "phone"]` och `"namespaces": ["GAID", "IDFA"]`. Mer information om den här grupperingen finns i `groups`-parametern i [API-referensen för målkonfigurationen](./destination-configuration-api.md).

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
>För alla mallar som du använder måste du undvika ogiltiga tecken, till exempel dubbla citattecken `""` innan du infogar mallen i [målserverkonfigurationen](./server-and-template-configuration.md#template-specs). Mer information om att undvika dubbla citattecken finns i kapitel 9 i [JSON-standarden](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Kontexten som anges för mallen innehåller `input` (profilerna/data som exporteras i det här anropet) och `destination` (data om målet som Adobe skickar data till, giltiga för alla profiler).

Tabellen nedan innehåller beskrivningar av funktionerna i exemplen ovan.

|  -funktion | Beskrivning |
|---------|----------|
| `input.profile` | Profilen, representerad som en [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Följer det XDM-schema för partner som nämns ovan på den här sidan. |
| `destination.segmentAliases` | Mappa från segment-ID:n i Adobe Experience Platform-namnutrymmet till segmentalias i partnersystemet. |
| `destination.segmentNames` | Mappa från segmentnamn i Adobe Experience Platform-namnutrymmet till segmentnamn i partnersystemet. |
| `addedSegments(listOfSegments)` | Returnerar endast de segment som har status `realized` eller `existing`. |
| `removedSegments(listOfSegments)` | Returnerar endast de segment som har status `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
