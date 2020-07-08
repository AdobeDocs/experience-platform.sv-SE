---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Enheter - Kundprofils-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---


# Entitetens slutpunkt (profilåtkomst)

Med Adobe Experience Platform kan du komma åt kundprofildata i realtid med RESTful API:er eller användargränssnittet. I den här handboken beskrivs hur du får åtkomst till entiteter, som ofta kallas&quot;profiler&quot;, med API:t. Mer information om hur du får åtkomst till profiler med hjälp av användargränssnittet i Platform finns i användarhandboken [för](../ui/user-guide.md)profiler.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [kundprofils-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)i realtid. Innan du fortsätter bör du läsa [Komma igång-guiden](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Åtkomst till profildata via identitet

Du kan komma åt en profilentitet genom att göra en GET-begäran till `/access/entities` slutpunkten och ange entitetens identitet som en serie frågeparametrar. Den här identiteten består av ett ID-värde (`entityId`) och identitetsnamnutrymmet (`entityIdNS`).

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;). En fullständig lista över giltiga parametrar finns i avsnittet med [frågeparametrar](#query-parameters) i bilagan.

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Begäran**

Följande begäran hämtar en kunds e-postadress och namn med hjälp av en identitet:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

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

>[!NOTE]
>Om ett relaterat diagram länkar mer än 50 identiteter returnerar den här tjänsten HTTP-status 422 och meddelandet&quot;För många relaterade identiteter&quot;. Om du får det här felet kan du lägga till fler frågeparametrar för att begränsa sökningen.

## Åtkomst till profildata via lista över identiteter

Du kan komma åt flera profilentiteter genom att göra en POST-begäran till `/access/entities` slutpunkten och ange identiteterna i nyttolasten. Dessa identiteter består av ett ID-värde (`entityId`) och ett identitetsnamnutrymme (`entityIdNS`).

**API-format**

```http
POST /access/entities
```

**Begäran**

Följande begäran hämtar namnen och e-postadresserna för flera kunder med hjälp av en lista över identiteter:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `schema.name` | ***(Obligatoriskt)*** Namnet på XDM-schemat som entiteten tillhör. |
| `fields` | XDM-fälten som ska returneras, som en array med strängar. Som standard returneras alla fält. |
| `identities` | ***(Obligatoriskt)*** En array som innehåller en lista över identiteter för de entiteter som du vill komma åt. |
| `identities.entityId` | ID:t för en enhet som du vill komma åt. |
| `identities.entityIdNS.code` | Namnområdet för ett enhets-ID som du vill komma åt. |
| `timeFilter.startTime` | Starttid för tidsintervallfiltret, som ingår. Ska vara i millisekundens granularitet. Om inget anges är standardvärdet början av tillgänglig tid. |
| `timeFilter.endTime` | Sluttid för tidsintervallfilter, exkluderad. Ska vara i millisekundens granularitet. Om inget anges är standardvärdet slutet av tillgänglig tid. |
| `limit` | Antal poster som ska returneras. Gäller endast antalet returnerade upplevelsehändelser. Standard: 1000. |
| `orderby` | Sorteringsordningen för hämtade upplevelsehändelser efter tidsstämpel, skriven som `(+/-)timestamp` med standardvärdet `+timestamp`. |
| `withCA` | Funktionsflagga för aktivering av beräknade attribut för sökning. Standard: false. |

**Svar** Ett lyckat svar returnerar de begärda fälten för entiteter som anges i begärandetexten.

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

## Åtkomst till tidsseriehändelser för en profil per identitet

Du kan komma åt tidsseriehändelser via identiteten för deras associerade profilentitet genom att göra en GET-begäran till `/access/entities` slutpunkten. Den här identiteten består av ett ID-värde (`entityId`) och ett identitetsnamnutrymme (`entityIdNS`).

Frågeparametrar som anges i sökvägen anger vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;). En fullständig lista över giltiga parametrar finns i avsnittet med [frågeparametrar](#query-parameters) i bilagan.

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Begäran**

Följande begäran hittar en profilentitet efter ID och hämtar värdena för egenskaperna `endUserIDs`, `web`och `channel` för alla tidsseriehändelser som är associerade med entiteten.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en numrerad lista över händelser i tidsserier och associerade fält som har angetts i frågeparametrarna för begäran.

>[!NOTE]
>I begäran angavs en gräns på ett (`limit=1`), och därför är svaret `count` nedan 1 och endast en enhet returneras.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
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
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Åtkomst till en efterföljande resultatsida

Resultaten sidnumreras när tidsseriehändelser hämtas. Om det finns efterföljande resultatsidor kommer egenskapen att innehålla ett ID: `_page.next` . Dessutom innehåller egenskapen en URI för begäran om att hämta nästa sida `_links.next.href` . Om du vill hämta resultaten gör du en annan GET-begäran till `/access/entities` slutpunkten, men du måste vara säker på att ersätta `/entities` med värdet för den angivna URI:n.

>[!NOTE]
>Se till att du inte råkar upprepa `/entities/` i sökvägen för begäran. Den ska bara visas en gång. `/access/entities?start=...`

**API-format**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beskrivning |
|---|---|
| `{NEXT_URI}` | URI-värdet som hämtas från `_links.next.href`. |

**Begäran**

Följande begäran hämtar nästa resultatsida genom att använda URI:n `_links.next.href` som begärandesökväg.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar nästa resultatsida. Det här svaret har inga efterföljande resultatsidor, vilket anges av de tomma strängvärdena för `_page.next` och `_links.next.href`.

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

## Få åtkomst till tidsseriehändelser för flera profiler per identitet

Du kan komma åt tidsseriehändelser från flera associerade profiler genom att göra en POST-begäran till `/access/entities` slutpunkten och ange profilidentiteterna i nyttolasten. Dessa identiteter består av ett ID-värde (`entityId`) och ett identitetsnamnutrymme (`entityIdNS`).

**API-format**

```http
POST /access/entities
```

**Begäran**

Följande begäran hämtar användar-ID:n, lokala tider och landskoder för tidsseriehändelser som är associerade med en lista över profilidentiteter:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Egenskap | Beskrivning |
|---|---|
| `schema.name` | **(OBLIGATORISKT)** XDM-schemat för den entitet som ska hämtas |
| `relatedSchema.name` | Om `schema.name` är `_xdm.context.experienceevent` det här värdet måste ange schemat för den profilentitet som tidsseriehändelser är relaterade till. |
| `identities` | **(OBLIGATORISKT)** En lista med profiler som associerade tidsseriehändelser ska hämtas från. Varje post i arrayen anges på ett av två sätt: 1) med en fullständigt kvalificerad identitet som består av ID-värde och namnutrymme eller 2) som tillhandahåller ett XID. |
| `fields` | Isolerar de data som returneras till en angiven uppsättning fält. Använd detta för att filtrera vilka schemafält som ska inkluderas i hämtade data. Exempel: personalEmail,person.namn,person.kön |
| `mergePolicyId` | Identifierar den sammanslagningsprincip som ska användas för att styra returnerade data. Om ingen anges i servicesamtalet kommer din organisations standardinställning för det schemat att användas. Om ingen standardprincip för sammanslagning har konfigurerats är standardinställningen ingen profilsammanslagning och ingen identitetssammanfogning. |
| `orderby` | Sorteringsordningen för hämtade upplevelsehändelser efter tidsstämpel, skriven som `(+/-)timestamp` med standardvärdet `+timestamp`. |
| `timeFilter.startTime` | Ange starttid för att filtrera tidsserieobjekt (i millisekunder). |
| `timeFilter.endTime` | Ange sluttiden för filtrering av tidsserieobjekt (i millisekunder). |
| `limit` | Numeriskt värde som anger det maximala antalet objekt som ska returneras. Standard: 1000 |
| `withCA` | Funktionsflagga för aktivering av beräknade attribut för sökning. Standard: false |

**Svar**

Ett lyckat svar returnerar en numrerad lista över händelser i tidsserier som är associerade med de flera profiler som anges i begäran.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

I det här exemplet ger den första listade profilen (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) ett värde för `_links.next.payload`, vilket innebär att det finns ytterligare resultatsidor för den här profilen. I följande avsnitt om [hur du får tillgång till ytterligare resultat](#access-additional-results) finns mer information om hur du får tillgång till dessa ytterligare resultat.

### Få tillgång till ytterligare resultat {#access-additional-results}

När tidsseriehändelser hämtas kan det finnas många resultat som returneras, och därför sidnumreras ofta resultaten. Om det finns efterföljande resultatsidor för en viss profil kommer värdet för den profilen att innehålla ett nyttolastobjekt `_links.next.payload` .

Om du använder den här nyttolasten i begärandetexten kan du utföra ytterligare en POST-begäran till slutpunkten för att hämta efterföljande sida med tidsseriedata för den profilen. `access/entities`

## Få åtkomst till tidsseriehändelser i flera schemaentiteter

Du kan komma åt flera enheter som är anslutna via en relationsbeskrivare. I följande exempel på API-anrop förutsätts att en relation redan har definierats mellan två scheman. Mer information om relationsbeskrivare finns i [slutpunktshandboken](../../xdm/api/descriptors.md)för programmeringsregistrets API-utvecklare.

Du kan inkludera frågeparametrar i sökvägen för begäran för att ange vilka data som ska användas. Du kan inkludera flera parametrar, avgränsade med et-tecken (&amp;). En fullständig lista över giltiga parametrar finns i avsnittet med [frågeparametrar](#query-parameters) i bilagan.

**API-format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Begäran**

Följande begäran hämtar en entitet som innehåller en tidigare etablerad relationsbeskrivare för att få tillgång till information över olika scheman.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar en numrerad lista över händelser i tidsserier som är associerade med de flera entiteterna.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Åtkomst till en efterföljande resultatsida

Resultaten sidnumreras när tidsseriehändelser hämtas. Om det finns efterföljande resultatsidor kommer egenskapen att innehålla ett ID: `_page.next` . Dessutom innehåller egenskapen en begärande-URI för att hämta den efterföljande sidan genom att göra ytterligare GET-begäranden till `_links.next.href` `access/entities` slutpunkten.

## Nästa steg

Genom att följa den här guiden har du fått åtkomst till datafält, profiler och tidsseriedata för kundprofiler i realtid. Mer information om hur du får åtkomst till andra dataresurser som lagras i Platform finns i [Dataåtkomstöversikten](../../data-access/home.md).

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om hur du får åtkomst till profildata med API:t.

### Frågeparametrar {#query-parameters}

Följande parametrar används i sökvägen för GET-begäranden till `/access/entities` slutpunkten. De används för att identifiera den profilentitet som du vill komma åt och filtrera data som returneras i svaret. Obligatoriska parametrar är märkta, medan resten är valfria.

| Parameter | Beskrivning | Exempel |
|---|---|---|
| `schema.name` | **(OBLIGATORISKT)** XDM-schemat för den entitet som ska hämtas | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Om `schema.name` är &quot;_xdm.context.experienceevent&quot; måste det här värdet ange schemat för den profilentitet som tidsseriehändelserna är relaterade till. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBLIGATORISKT)** Enhetens ID. Om värdet för den här parametern inte är ett XID måste även en identitetsnamnutrymmesparameter anges (se `entityIdNS` nedan). | `entityId=janedoe@example.com` |
| `entityIdNS` | Om `entityId` inte anges som ett XID måste ID-namnutrymmet anges i det här fältet. | `entityIdNE=email` |
| `relatedEntityId` | Om `schema.name` är &quot;_xdm.context.experienceevent&quot; måste det här värdet ange den relaterade profilentitetens identitetsnamnutrymme. Detta värde följer samma regler som `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Om `schema.name` är &quot;_xdm.context.experienceevent&quot; måste det här värdet ange identitetsnamnutrymmet för den entitet som anges i `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtrerar de data som returneras i svaret. Använd detta för att ange vilka schemafältvärden som ska inkluderas i hämtade data. För flera fält avgränsar du värden med kommatecken utan blanksteg mellan | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifierar den sammanslagningsprincip som ska användas för att styra returnerade data. Om ingen anges i samtalet används organisationens standardvärde för det schemat. Om ingen standardprincip för sammanslagning har konfigurerats är standardinställningen ingen profilsammanslagning och ingen identitetssammanfogning. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Sorteringsordningen för hämtade upplevelsehändelser efter tidsstämpel, skriven som `(+/-)timestamp` med standardvärdet `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Ange starttid för att filtrera tidsserieobjekt (i millisekunder). | `startTime=1539838505` |
| `endTime` | Ange sluttiden för filtrering av tidsserieobjekt (i millisekunder). | `endTime=1539838510` |
| `limit` | Numeriskt värde som anger det maximala antalet objekt som ska returneras. Standard: 1000 | `limit=100` |
| `withCA` | Funktionsflagga för aktivering av beräknade attribut för sökning. Standard: false | `withCA=true` |