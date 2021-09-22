---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/sample-profiles` för att generera exempelprofiler som ska användas vid måltestning.
title: API-åtgärder för generering av exempelprofiler
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# API-åtgärder för generering av exempelprofiler {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/sample-profiles`.

Med den här API-slutpunkten kan du generera exempelprofiler som ska användas:
* När du testar en meddelandeomformningsmall. Läs mer i [Skapa och testa en meddelandeomformningsmall](./create-template.md).
* När du testar om målet är korrekt konfigurerat. Läs mer i [Testa målkonfigurationen](./test-destination.md).

Du kan generera exempelprofiler baserat på Adobe XDM-källschemat eller målschemat som stöds av ditt mål. Läs artikeln [Meddelandeformat](./message-format.md) om du vill veta skillnaden mellan källschemat och målschemat i Adobe XDM.

## Komma igång med API-åtgärder för generering av exempelprofiler {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Generera exempelprofiler baserat på källschemat {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Lägg till exempelprofilerna som genereras här för HTTP-anrop när [du testar ditt mål](./test-destination.md).

Du kan generera exempelprofiler baserat på källschemat genom att göra en GET-förfrågan till `authoring/sample-profiles/`-slutpunkten och ange ID:t för en målinstans som du har skapat baserat på målkonfigurationen som du vill testa.

>[!TIP]
>
>* Hämta det målinstans-ID som du bör använda här från webbadressen när du bläddrar i en anslutning till målet.
   >![Användargränssnittsbild för att hämta målinstans-ID](./assets/get-destination-instance-id.png)


**API-format**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID:t för målinstansen som du genererar exempelprofiler utifrån. |
| `{COUNT}` | *Valfritt*. Antalet exempelprofiler som du genererar. Parametern kan ha värden mellan `1 - 1000`. <br> Om parametern count inte anges bestäms standardantalet genererade profiler av  `maxUsersPerRequest` värdet i  [målserverkonfigurationen](./destination-server-api.md#create). Om den här egenskapen inte är definierad genereras en exempelprofil i Adobe. |

{style=&quot;table-layout:auto&quot;}


**Begäran**

Följande begäran genererar exempelprofiler, konfigurerade av frågeparametrarna `{DESTINATION_INSTANCE_ID}` och `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med segmentmedlemskap, identiteter och profilattribut som motsvarar XDM-källschemat.

>[!TIP]
>
> Svaret returnerar endast segmentmedlemskap, identiteter och profilattribut som används i målinstansen. Även om källschemat innehåller andra fält ignoreras dessa.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentMembership` | Ett kartobjekt som beskriver personens segmentmedlemskap. Mer information om `segmentMembership` finns i [Information om segmentmedlemskap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `xdm:status` | Anger om segmentmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`existing`: Profilen var redan en del av segmentet innan begäran gjordes och fortsätter att behålla medlemskapet.</li><li>`realized`: Profilen går in i segmentet som en del av den aktuella begäran.</li><li>`exited`: Profilen avslutar segmentet som en del av den aktuella begäran.</li></ul> |
| `identityMap` | Ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Mer information om `identityMap` finns i [Grundläggande om schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Generera exempelprofiler baserat på målschemat {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Använd exempelprofilerna som genereras här när du skapar mallen i [återgivningsmallsteget](./render-template-api.md#multiple-profiles-with-body).

Du kan generera exempelprofiler baserat på målschemat och göra en GET-förfrågan till `authoring/sample-profiles/`-slutpunkten och ange mål-ID:t för målkonfigurationen baserat på vilken du skapar mallen.

>[!TIP]
>
>* Det mål-ID som du bör använda här är det `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Se [API-referens för målkonfiguration](./destination-configuration-api.md#retrieve-list).


**API-format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för målkonfigurationen baserat på vilket du genererar exempelprofiler. |
| `{COUNT}` | *Valfritt*. Antalet exempelprofiler som du genererar. Parametern kan ha värden mellan `1 - 1000`. <br> Om parametern count inte anges bestäms standardantalet genererade profiler av  `maxUsersPerRequest` värdet i  [målserverkonfigurationen](./destination-server-api.md#create). Om den här egenskapen inte är definierad genereras en exempelprofil i Adobe. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran genererar exempelprofiler, konfigurerade av frågeparametrarna `{DESTINATION_ID}` och `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med segmentmedlemskap, identiteter och profilattribut som motsvarar mål-XDM-schemat.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API-felhantering {#api-error-handling}

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du genererar exempelprofiler som ska användas när [du testar en meddelandeomformningsmall](./create-template.md) eller när [testar om målet har konfigurerats korrekt](./test-destination.md).
