---
description: Lär dig hur du använder API:t för måltestning för att generera exempelprofiler för ditt mål för direktuppspelning, som du kan använda i måltestning.
title: Generera exempelprofiler baserat på ett källschema
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---


# Generera exempelprofiler baserat på ett källschema {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-slutpunkt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/sample-profiles`.

## Generera olika profiltyper för olika API:er {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Använd den här API-slutpunkten om du vill generera exempelprofiler för två olika användningsområden. Du kan antingen:
>* generera profiler som ska användas när [skapar och testar en meddelandetransformeringsmall](create-template.md) - genom att använda *mål-ID* som en frågeparameter.
>* generera profiler som ska användas vid anrop till [testning om målet är korrekt konfigurerat](streaming-destination-testing-overview.md) - genom att använda *målinstans-ID* som en frågeparameter.

Du kan generera exempelprofiler baserade på Adobe XDM-källschemat (som används när du testar ditt mål) eller det målschema som stöds av ditt mål (som du använder när du skapar mallen). Om du vill förstå skillnaden mellan Adobe XDM-källschemat och målschemat läser du översiktsavsnittet i artikeln [Meddelandeformat](../../functionality/destination-server/message-format.md).

Observera att de syften för vilka exempelprofilerna kan användas inte är utbytbara. Profiler som genereras baserat på *mål-ID* kan bara användas för att skapa meddelandeomformningsmallar och profiler som genereras baserat på *målinstans-ID* kan bara användas för att testa målslutpunkten.

## Komma igång med API-åtgärder för generering av exempelprofiler {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Generera exempelprofiler baserat på källschemat som ska användas vid testning av målet {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Lägg till exempelprofilerna som genereras här i HTTP-anrop när [du testar ditt mål](streaming-destination-testing-overview.md).

Du kan generera exempelprofiler baserat på källschemat genom att göra en GET-begäran till `authoring/sample-profiles/`-slutpunkten och ange ID:t för en målinstans som du har skapat baserat på målkonfigurationen som du vill testa.

Om du vill hämta ID:t för en målinstans måste du först skapa en anslutning i Experience Platform-gränssnittet till målet innan du försöker testa målet. Läs [Aktivera målsjälvstudiekursen](../../../ui/activation-overview.md) och se tipset nedan för hur du får destinationsinstansens ID att använda för detta API.

>[!IMPORTANT]
>
>* Om du vill använda detta API måste du ha en befintlig anslutning till målet i Experience Platform-gränssnittet. Läs [anslut till mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) och [aktivera profiler och målgrupper till ett mål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) om du vill ha mer information.
> * När du har upprättat anslutningen till målet hämtar du det målinstans-ID som du bör använda i API-anrop till den här slutpunkten när du [bläddrar i en anslutning till målet](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>![Användargränssnittsbild för att hämta målinstans-ID ](../../assets/testing-api/get-destination-instance-id.png)

**API-format**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID:t för målinstansen som du genererar exempelprofiler utifrån. |
| `{COUNT}` | *Valfritt*. Antalet exempelprofiler som du genererar. Parametern kan ha värden mellan `1 - 1000`. <br> Om parametern count inte anges bestäms standardantalet genererade profiler av värdet `maxUsersPerRequest` i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Om den här egenskapen inte är definierad genereras en exempelprofil i Adobe. |

{style="table-layout:auto"}


**Begäran**

Följande begäran genererar exempelprofiler, konfigurerade av frågeparametrarna `{DESTINATION_INSTANCE_ID}` och `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med målgruppsmedlemskap, identiteter och profilattribut som motsvarar XDM-källschemat.

>[!TIP]
>
> Svaret returnerar endast målgruppsmedlemskap, identiteter och profilattribut som används i målinstansen. Även om källschemat innehåller andra fält ignoreras dessa.

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
| `segmentMembership` | Ett kartobjekt som beskriver personens målgruppsmedlemskap. Mer information om `segmentMembership` finns i [Information om målgruppsmedlemskap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `xdm:status` | Ett strängfält som anger om målgruppsmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`realized`: Profilen ingår i segmentet.</li><li>`exited`: Profilen avslutar målgruppen som en del av den aktuella begäran.</li></ul> |
| `identityMap` | Ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Mer information om `identityMap` finns i [Grundläggande om schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap). |

{style="table-layout:auto"}

## Generera exempelprofiler baserade på målschemat som ska användas när en meddelandeomformningsmall skapas {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Använd exempelprofilerna som genereras här när du skapar mallen i [återgivningsmallsteget](render-template-api.md#multiple-profiles-with-body).

Du kan generera exempelprofiler baserat på målschemat och göra en GET-begäran till `authoring/sample-profiles/`-slutpunkten och ange mål-ID:t för målkonfigurationen som du skapar mallen utifrån.

>[!TIP]
>
>* Mål-ID som du bör använda här är `instanceId` som motsvarar en målkonfiguration, som skapas med slutpunkten `/destinations`. Mer information finns i [Hämta en målkonfiguration](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**API-format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Frågeparameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för målkonfigurationen baserat på vilket du genererar exempelprofiler. |
| `{COUNT}` | *Valfritt*. Antalet exempelprofiler som du genererar. Parametern kan ha värden mellan `1 - 1000`. <br> Om parametern count inte anges bestäms standardantalet genererade profiler av värdet `maxUsersPerRequest` i [målserverkonfigurationen](../../authoring-api/destination-server/create-destination-server.md). Om den här egenskapen inte är definierad genereras en exempelprofil i Adobe. |

{style="table-layout:auto"}

**Begäran**

Följande begäran genererar exempelprofiler, konfigurerade av frågeparametrarna `{DESTINATION_ID}` och `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med det angivna antalet exempelprofiler, med målgruppsmedlemskap, identiteter och profilattribut som motsvarar mål-XDM-schemat.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
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
                    "status": "realized"
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
                    "status": "realized"
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

Destination SDK API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du genererar exempelprofiler som ska användas när [du testar en meddelandeomformningsmall](create-template.md) eller när [testar om målet är korrekt konfigurerat](streaming-destination-testing-overview.md).
