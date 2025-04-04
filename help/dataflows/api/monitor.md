---
keywords: Experience Platform;home;populära topics;monitor data aflows;flow service api;Flow Service
solution: Experience Platform
title: Övervaka dataflöden med API:t för flödestjänsten
type: Tutorial
description: Den här självstudiekursen beskriver stegen för övervakning av körningsdata för flöde för fullständighet, fel och mätvärden med API:t för Flow Service.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Övervaka dataflöden med API:t för Flow Service

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du får möjlighet att strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra. Dessutom tillåter Experience Platform att data aktiveras för externa partner.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor och mål som stöds kan anslutas från.

I den här självstudiekursen beskrivs stegen för övervakning av körningsdata för flöde för fullständighet, fel och mätvärden med hjälp av [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

I den här självstudiekursen måste du ha ID-värdet för ett giltigt dataflöde. Om du inte har något giltigt dataflödes-ID väljer du den önskade anslutningen i [källöversikten](../../sources/home.md) eller [målöversikten](../../destinations/catalog/overview.md) och följer instruktionerna innan du försöker med den här självstudien.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

- [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga program som möjliggör smidig aktivering av data från Experience Platform för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
- [Källor](../../sources/home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna övervaka flödeskörningar med API:t [!DNL Flow Service].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en extra medietypsrubrik:

- `Content-Type: application/json`

## Körningar av bildskärmsflöde

När du har gjort ett dataflöde utför du en GET-begäran till API:t [!DNL Flow Service].

**API-format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Det unika `id`-värdet för dataflödet som du vill övervaka. |

**Begäran**

Följande begäran hämtar specifikationerna för ett befintligt dataflöde.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om flödeskörningen, inklusive information om dess skapandedatum, käll- och målanslutningar samt flödets unika identifierare (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `items` | Innehåller en enda nyttolast av metadata som är associerade med din specifika flödeskörning. |
| `metrics` | Egenskaperna för data i flödeskörningen. |
| `activities` | Visar hur data omformas. |
| `durationSummary` | Start- och sluttiden för flödeskörningen. |
| `sizeSummary` | Datavolymen i byte. |
| `recordSummary` | Antal poster för data. |
| `fileSummary` | Filen räknar data. |
| `fileSummary.extensions` | Innehåller information som är specifik för aktiviteten. `manifest` är till exempel bara en del av tävlingsaktiviteten, och därför ingår den i objektet `extensions`. |
| `statusSummary` | Visar om flödeskörningen är en lyckad eller misslyckad åtgärd. |

## Nästa steg

Genom att följa den här självstudiekursen har du hämtat mått och felinformation för ditt dataflöde med API:t [!DNL Flow Service]. Du kan nu fortsätta att övervaka ditt dataflöde, beroende på ditt intag, för att spåra dess status och intag. Mer information om hur du övervakar dataflöden för källor finns i [övervakningsdataflödena för källor med hjälp av användargränssnittet](../ui/monitor-sources.md). Mer information om hur du övervakar dataflöden för mål finns i [övervakningsdataflödena för mål med hjälp av användargränssnittet](../ui/monitor-destinations.md).
