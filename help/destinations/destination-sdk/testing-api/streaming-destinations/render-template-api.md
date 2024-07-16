---
description: Lär dig hur du använder API:t för måltestning för att validera utdata till ditt direktuppspelningsmål, baserat på din meddelandeomvandlingsmall.
title: Validera exporterad profilstruktur
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Validera exporterad profilstruktur {#render-template-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/testing/template/render` för att återge exporterade profiler som matchar målets förväntade format, baserat på din [meddelandeomformningsmall](../../functionality/destination-server/message-format.md#using-templating). En beskrivning av de funktioner som stöds av den här slutpunkten finns i [Skapa mall](create-template.md).

## Komma igång med åtgärder för återgivningsmall-API {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Återge exporterade profiler baserat på mallen för meddelandeomformning {#render-exported-data}

Du kan återge exporterade profiler genom att göra en POST-förfrågan till `authoring/testing/template/render`-slutpunkten och ange mål-ID:t för målkonfigurationen och den mall som du skapade med [exempelmallens API-slutpunkt](sample-template-api.md).

Du kan börja med en enkel mall som exporterar dina Raw-profiler utan att använda några omformningar och sedan gå vidare till en mer komplex mall som tillämpar omformningar på profiler. Syntaxen för den enkla mallen är: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

>[!TIP]
>
>* Mål-ID som du bör använda här är `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Mer information finns i [Hämta en målkonfiguration](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**API-format**


```http
POST authoring/testing/template/render
```

| Begäranparameter | Beskrivning |
| -------- | ----------- |
| `destinationId` | ID:t för målkonfigurationen som du återger exporterade profiler för. |
| `template` | Den teckenescape-version av mallen som du återger exporterade profiler utifrån. |
| `profiles` | *Valfritt*. Du kan lägga till profiler i begärandetexten. Om du inte lägger till några profiler genereras och läggs profiler till i begäran automatiskt i Experience Platform. <br> Om du vill lägga till profiler i anropets brödtext kan du generera några med hjälp av [API:t för generering av exempelprofiler](sample-profile-generation-api.md). |

{style="table-layout:auto"}

Observera att svaret som returneras av återgivningsmallens API-slutpunkt skiljer sig åt baserat på målaggregeringsprincipen. Om målet har en konfigurerbar aggregeringsprincip returneras också aggregeringsnyckeln som bestämmer hur profiler aggregeras i svaret. Läs mer om [aggregeringsprinciper](../../functionality/destination-configuration/aggregation-policy.md).

| Svarsparameter | Beskrivning |
| -------- | ----------- |
| `aggregationKey` | Representerar den princip som används för att samla profiler i exporter till ditt mål. Den här parametern är valfri och kommer bara att finnas om målaggregeringsprincipen är inställd på `CONFIGURABLE_AGGREGATION`. |
| `profiles` | Visar profilerna som anges i begäran eller de automatiskt genererade profilerna om inga profiler angavs i begäran. |
| `output` | Återgiven profil eller profiler, som en escape-sträng, baserad på den angivna meddelandeomvandlingsmallen |

Avsnitten nedan innehåller detaljerade förfrågningar och svar för båda de fall som beskrivs ovan.

* [Bästa ansträngningsaggregering och en profil ingår i begärandetexten](#best-effort)
* [Konfigurerbar aggregering och konfigurerbara profiler som ingår i begärandetexten](#configurable-aggregation)

### Rendera exporterade profiler med bästa möjliga ansträngning och en enda profil som ingår i begärandetexten {#best-effort}

**Begäran**

Följande begäran återger en exporterad profil som matchar det format som förväntas av ditt mål. I det här exemplet motsvarar mål-ID en destinationskonfiguration med bästa ansträngningsaggregering, och en exempelprofil ingår i innehållet i begäran.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "947c1c46-008d-40b0-92ec-3af86eaf41c1",
    "template": "{#- THIS is an example template for a single profile -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"identities\": [\r\n    {%- for idMapEntry in input.profile.identityMap -%}\r\n    {%- set namespace = idMapEntry.key -%}\r\n        {%- for identity in idMapEntry.value %}\r\n        {\r\n            \"type\": \"{{ namespace }}\",\r\n            \"id\": \"{{ identity.id }}\"\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n        {%- for segment in input.profile.segmentMembership.ups | added %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n        {#- Alternative syntax for filtering audiences by status: -#}\r\n        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "gaid": [
                    {
                        "id": "gaid-BLAcJ"
                    }
                ],
                "idfa": [
                    {
                        "id": "idfa-Iv5AG"
                    }
                ],
                "email": [
                    {
                        "id": "email-rbN62"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**Svar**

Svaret returnerar resultatet av återgivningen av mallen eller eventuella fel som påträffats.
Ett lyckat svar returnerar HTTP-status 200 med information om exporterade data. Hitta den exporterade profilen i parametern `output` som en escape-sträng.
Ett misslyckat svar returnerar HTTP-status 400 tillsammans med beskrivningar av de fel som påträffats.

```json
{
    "results": [
        {
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                                "status": "realized"
                            },
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                                "status": "exited"
                            },
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "gaid": [
                            {
                                "id": "gaid-BLAcJ"
                            }
                        ],
                        "idfa": [
                            {
                                "id": "idfa-Iv5AG"
                            }
                        ],
                        "email": [
                            {
                                "id": "email-rbN62"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"identities\": [\r\n        {\r\n            \"type\": \"gaid\",\r\n            \"id\": \"gaid-BLAcJ\"\r\n        },\r\n        {\r\n            \"type\": \"idfa\",\r\n            \"id\": \"idfa-Iv5AG\"\r\n        },\r\n        {\r\n            \"type\": \"email\",\r\n            \"id\": \"email-rbN62\"\r\n        }\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            \"segmentid1\",\r\n            \"segmentid2\"\r\n        ],\r\n        \"remove\": [\r\n            \"segmentid3\"\r\n        ]\r\n    }\r\n}"
        }
    ]
}    
```

### Återge exporterade profiler med konfigurerbar aggregering och profiler som ingår i begärandetexten {#configurable-aggregation}

**Begäran**


Följande begäran återger flera exporterade profiler som matchar det format som förväntas av ditt mål. I det här exemplet motsvarar mål-ID en målkonfiguration med konfigurerbar aggregering. Det finns två profiler i ansökan, var och en med tre målgruppskvalifikationer och fem identiteter. Du kan generera profiler som ska skickas vid samtalet med hjälp av [API:t för generering av exempelprofiler](sample-profile-generation-api.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
    "destinationId": "c2bc84c5-589c-43a1-96ea-becfa941f5be",
    "template": "{#- THIS is an example template for multiple profiles -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"profiles\": [\r\n    {%- for profile in input.profiles %}\r\n        {\r\n            \"identities\": [\r\n            {%- for idMapEntry in profile.identityMap -%}\r\n            {%- set namespace = idMapEntry.key -%}\r\n                {%- for identity in idMapEntry.value %}\r\n                {\r\n                    \"type\": \"{{ namespace }}\",\r\n                    \"id\": \"{{ customerData }}\"\r\n                }{%- if not loop.last -%},{%- endif -%}\r\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n            {% endfor %}\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                {%- for segment in profile.segmentMembership.ups | added %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ],\r\n                \"remove\": [\r\n                {#- Alternative syntax for filtering audiences by status: -#}\r\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ]\r\n            }\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ]\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947859Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-biCbJ"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-0Q3hp"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-mN1Hw"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-MVw4L"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-2OjnN"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        },
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948187Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-fxt2p"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-sboQe"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-MRelR"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-M46ze"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-40Vrf"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**Svar**

Svaret returnerar resultatet av återgivningen av mallen eller eventuella fel som påträffats.
Ett lyckat svar returnerar HTTP-status 200 med information om exporterade data. Lägg märke till hur profilerna sammanställs baserat på målgruppsmedlemskap och identiteter i svaret. Sök efter de exporterade profilerna i parametern `output` som en escape-sträng.
Ett misslyckat svar returnerar HTTP-status 400 tillsammans med beskrivningar av de fel som påträffats.

```json
{
    "results": [
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        }
    ]
}
```

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du använder meddelandeomformningsmallen för att generera exporterade profiler som matchar målets förväntade dataformat. Läs [om hur du använder Destination SDK för att konfigurera ditt mål](../../guides/configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
