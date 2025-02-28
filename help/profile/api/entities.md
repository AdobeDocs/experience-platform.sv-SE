---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för entiteter (profilåtkomst)
type: Documentation
description: Med Adobe Experience Platform kan du få åtkomst till kundprofildata i realtid med RESTful API:er eller användargränssnittet. I den här handboken beskrivs hur du får åtkomst till entiteter, som ofta kallas"profiler", med hjälp av profilens API.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: efebf8e341b17fdd71586827753eadfe1c2cfa15
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 0%

---

# Entitetens slutpunkt (profilåtkomst)

>[!IMPORTANT]
>
>ExperienceEvent-sökning med API:t för profilåtkomst kommer att bli inaktuell. Använd funktioner som beräknade attribut för användningsfall som kräver att du tittar upp med ExperienceEvents. Mer information om den här ändringen får du av Adobe kundtjänst.

Med Adobe Experience Platform kan du komma åt [!DNL Real-Time Customer Profile]-data med RESTful API:er eller användargränssnittet. I den här handboken beskrivs hur du får åtkomst till entiteter, som ofta kallas&quot;profiler&quot;, med API:t. Mer information om hur du får åtkomst till profiler med hjälp av användargränssnittet för [!DNL Platform] finns i [användarhandboken för profilen](../ui/user-guide.md).

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Hämta en entitet {#retrieve-entity}

Du kan hämta en profilentitet genom att göra en GET-begäran till `/access/entities`-slutpunkten tillsammans med de obligatoriska frågeparametrarna.

>[!BEGINTABS]

>[!TAB Profilentitet]

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;).

Om du vill komma åt en profilentitet måste **du** ange följande frågeparametrar:

- `schema.name`: Namnet på entitetens XDM-schema. I det här fallet `schema.name=_xdm.context.profile`.
- `entityId`: ID:t för entiteten som du försöker hämta.
- `entityIdNS`: Namnområdet för entiteten som du försöker hämta. Det här värdet måste anges om `entityId` är **inte** ett XID.

En fullständig lista över giltiga parametrar finns i avsnittet [frågeparametrar](#query-parameters) i bilagan.

**Begäran**

Följande begäran hämtar en kunds e-postadress och namn med hjälp av en identitet.

+++ Ett exempel på en begäran om att hämta en entitet med en identitet

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med den begärda entiteten.

+++ Ett exempelsvar som innehåller den begärda entiteten

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "johnsmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

+++

>[!NOTE]
>
>Om ett relaterat diagram länkar mer än 50 identiteter returnerar den här tjänsten HTTP-status 422 och meddelandet&quot;För många relaterade identiteter&quot;. Om du får det här felet kan du lägga till fler frågeparametrar för att begränsa sökningen.

>[!TAB B2B-konto]

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;).

Om du vill komma åt B2B-kontodata **måste** ange följande frågeparametrar:

- `schema.name`: Namnet på entitetens XDM-schema. I det här fallet är värdet `schema.name=_xdm.context.account`.
- `entityId`: ID:t för entiteten som du försöker hämta.
- `entityIdNS`: Namnområdet för entiteten som du försöker hämta. Det här värdet måste anges om `entityId` är **inte** ett XID.

En fullständig lista över giltiga parametrar finns i avsnittet [frågeparametrar](#query-parameters) i bilagan.

**Begäran**

+++ Ett exempel på en begäran om att hämta ett B2B-konto

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med den begärda entiteten.

+++ Ett exempelsvar som innehåller den begärda entiteten

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB B2B-säljprojekt]

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;).

Om du vill komma åt en B2B-säljprojektsenhet **måste** ange följande frågeparametrar:

- `schema.name`: Namnet på entitetens XDM-schema. I det här fallet `schema.name=_xdm.context.opportunity`.
- `entityId`: ID:t för entiteten som du försöker hämta.
- `entityIdNS`: Namnområdet för entiteten som du försöker hämta. Det här värdet måste anges om `entityId` är **inte** ett XID.

En fullständig lista över giltiga parametrar finns i avsnittet [frågeparametrar](#query-parameters) i bilagan.

**Begäran**

+++ En exempelbegäran om att hämta en B2B-säljprojektsenhet

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med den begärda entiteten.

+++ Ett exempelsvar som innehåller den begärda entiteten

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Hämta flera entiteter {#retrieve-entities}

Du kan hämta flera profilentiteter genom att göra en POST-begäran till `/access/entities`-slutpunkten och ange identiteterna i nyttolasten.

>[!BEGINTABS]

>[!TAB Profilentiteter]

**API-format**

```http
POST /access/entities
```

**Begäran**

Följande begäran hämtar namnen och e-postadresserna för flera kunder med hjälp av en lista över identiteter.

+++En exempelbegäran för att hämta flera entiteter

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp"
      }'
```

| Egenskap | Typ | Beskrivning |
| -------- |----- | ----------- |
| `schema.name` | Sträng | **(Obligatoriskt)** Namnet på XDM-schemat som entiteten tillhör. |
| `fields` | Array | XDM-fälten som ska returneras, som en array med strängar. Som standard returneras alla fält. |
| `identities` | Array | **(Obligatoriskt)** En array som innehåller en lista över identiteter för de entiteter som du vill komma åt. |
| `identities.entityId` | Sträng | ID för en enhet som du vill komma åt. |
| `identities.entityIdNS.code` | Sträng | Namnområdet för ett enhets-ID som du vill komma åt. |
| `timeFilter.startTime` | Heltal | Anger starttiden för filtrering av profilentiteter (i millisekunder). Som standard anges det här värdet som början av tillgänglig tid. |
| `timeFilter.endTime` | Heltal | Anger sluttiden för filtrering av profilentiteter (i millisekunder). Som standard är det här värdet inställt som slutet på tillgänglig tid. |
| `limit` | Heltal | Det maximala antalet poster som ska returneras. Som standard är det här värdet 1 000. |
| `orderby` | Sträng | Sorteringsordningen för hämtade upplevelsehändelser efter tidsstämpel, skriven som `(+/-)timestamp` med standardvärdet `+timestamp`. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med de begärda fälten för entiteter angivna i begärandetexten.

+++ Ett exempelsvar som innehåller begärda entiteter

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

+++

>[!TAB B2B-konto]

**API-format**

```http
POST /access/entities
```

**Begäran**

Följande begäran hämtar begärda B2B-konton.

+++En exempelbegäran för att hämta flera entiteter

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Egenskap | Typ | Beskrivning |
| -------- |----- | ----------- |
| `schema.name` | Sträng | **(Obligatoriskt)** Namnet på XDM-schemat som entiteten tillhör. |
| `identities` | Array | **(Obligatoriskt)** En array som innehåller en lista över identiteter för de entiteter som du vill komma åt. |
| `identities.entityId` | Sträng | ID för en enhet som du vill komma åt. |
| `identities.entityIdNS.code` | Sträng | Namnområdet för ett enhets-ID som du vill komma åt. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med de begärda entiteterna.

+++ Ett exempelsvar som innehåller begärda entiteter

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB B2B-säljprojekt]

**API-format**

```http
POST /access/entities
```

**Begäran**

Följande begäran hämtar de begärda B2B-affärsmöjligheterna.

+++ En exempelbegäran om att hämta flera entiteter

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Egenskap | Typ | Beskrivning |
| -------- |----- | ----------- |
| `schema.name` | Sträng | **(Obligatoriskt)** Namnet på XDM-schemat som entiteten tillhör. |
| `identities` | Array | **(Obligatoriskt)** En array som innehåller en lista över identiteter för de entiteter som du vill komma åt. |
| `identities.entityId` | Sträng | ID för en enhet som du vill komma åt. |
| `identities.entityIdNS.code` | Sträng | Namnområdet för ett enhets-ID som du vill komma åt. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med de begärda entiteterna.

+++ Ett exempelsvar som innehåller begärda entiteter

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Åtkomst till en efterföljande resultatsida

Resultaten sidnumreras när tidsseriehändelser hämtas. Om det finns efterföljande resultatsidor kommer egenskapen `_page.next` att innehålla ett ID. Dessutom innehåller egenskapen `_links.next.href` en URI för begäran för hämtning av nästa sida. Om du vill hämta resultaten gör du en annan GET-begäran till `/access/entities`-slutpunkten och ersätter `/entities` med värdet för den angivna URI:n.

>[!NOTE]
>
>Se till att du inte oavsiktligt upprepar `/entities/` i sökvägen för begäran. Den får bara visas en gång, `/access/entities?start=...`

**API-format**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beskrivning |
|---|---|
| `{NEXT_URI}` | URI-värdet är taget från `_links.next.href`. |

**Begäran**

Följande begäran hämtar nästa resultatsida genom att använda URI:n `_links.next.href` som begärandesökväg.

+++ Ett exempel på en förfrågan om att få åtkomst till nästa resultatsida

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett godkänt svar returnerar nästa resultatsida. Det här svaret har inga efterföljande resultatsidor, vilket anges av de tomma strängvärdena `_page.next` och `_links.next.href`.

+++ Ett exempelsvar som innehåller nästa sida med entiteter

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

+++

## Ta bort en entitet {#delete-entity}

Du kan ta bort en entitet från profilarkivet genom att göra en DELETE-begäran till `/access/entities`-slutpunkten tillsammans med de obligatoriska frågeparametrarna.

**API-format**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;).

Om du vill ta bort en entitet **måste** ange följande frågeparametrar:

- `schema.name`: Namnet på entitetens XDM-schema. I det här fallet kan du **endast** använda `schema.name=_xdm.context.profile`.
- `entityId`: ID:t för entiteten som du försöker hämta.
- `entityIdNS`: Namnområdet för entiteten som du försöker hämta. Det här värdet måste anges om `entityId` är **inte** ett XID.
- `mergePolicyId`: Enhetens ID för sammanslagningsprincip. Sammanslagningsprincipen innehåller information om identitetssammanfogning och XDM-objektsammanfogning med nyckelvärden. Om det här värdet inte anges används standardprincipen för sammanslagning.

**Begäran**

Följande begäran tar bort den angivna entiteten.

+++ En exempelbegäran om att ta bort en entitet

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 202 med en tom svarstext.

## Nästa steg

Genom att följa den här vägledningen har du fått åtkomst till [!DNL Real-Time Customer Profile] datafält, profiler och tidsseriedata. Mer information om hur du får åtkomst till andra dataresurser som lagras i [!DNL Platform] finns i [Dataåtkomstöversikten](../../data-access/home.md).

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om åtkomst av [!DNL Profile]-data med API:t.

### Frågeparametrar {#query-parameters}

Följande parametrar används i sökvägen för GET-begäranden till slutpunkten `/access/entities`. De används för att identifiera den profilentitet som du vill komma åt och filtrera data som returneras i svaret. Obligatoriska parametrar är märkta, medan resten är valfria.

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `schema.name` | **(Obligatoriskt)** Namnet på entitetens XDM-schema. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | Om `schema.name` är `_xdm.context.experienceevent` måste det här värdet **** ange schemat för den profilentitet som tidsseriehändelserna är relaterade till. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Obligatoriskt)** ID för entiteten. Om värdet för den här parametern inte är ett XID måste även en identitetsnamnområdesparameter (`entityIdNS`) anges. | `entityId=janedoe@example.com` |
| `entityIdNS` | Om `entityId` inte anges som ett XID måste **** ange identitetsnamnområdet i det här fältet. | `entityIdNS=email` |
| `relatedEntityId` | Om `schema.name` är `_xdm.context.experienceevent` måste det här värdet **** ange den relaterade profilentitetens ID. Det här värdet följer samma regler som `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Om `schema.name` är&quot;_xdm.context.experienceevent&quot; måste det här värdet ange identitetsnamnutrymmet för entiteten som anges i `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtrerar de data som returneras i svaret. Använd detta för att ange vilka schemafältvärden som ska inkluderas i hämtade data. För flera fält avgränsar du värden med kommatecken utan blanksteg mellan. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifierar den sammanfogningsprincip som ska användas för att styra returnerade data. Om ingen anges i samtalet används organisationens standardvärde för det schemat. Om ingen standardprincip för sammanslagning har konfigurerats är standardinställningen ingen profilsammanslagning och ingen identitetssammanfogning. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Sorteringsordningen för hämtade entiteter efter tidsstämpel. Detta skrivs som `(+/-)timestamp`, med standardvärdet `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Anger starttiden som entiteterna ska filtreras (i millisekunder). | `startTime=1539838505` |
| `endTime` | Anger sluttiden för filtrering av enheter (i millisekunder). | `endTime=1539838510` |
| `limit` | Anger det maximala antalet enheter som ska returneras. Som standard är det här värdet 1 000. | `limit=100` |
| `property` | Filtrerar efter egenskapsvärdet. Frågeparametern stöder följande utvärderare: =, !=, &lt;, &lt;=, >, >=. Detta kan bara användas med upplevelsehändelser, med maximalt tre egenskaper som stöds. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
