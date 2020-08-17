---
keywords: Experience Platform;home;popular topics; notifications
description: Med Adobe I/O Events kan du prenumerera på händelser och använda webbhooks för att få meddelanden om status för dina flödeskörningar. Dessa meddelanden innehåller information om hur flödeskörningen lyckades eller om fel som bidragit till ett körningsfel.
solution: Experience Platform
title: Flödeskörningsmeddelanden
topic: overview
translation-type: tm+mt
source-git-commit: a014a5efeebfcce5c36a9ea87f690bdcd605ef61
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Flödeskörningsmeddelanden

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) används för att samla in och centralisera kunddata från olika källor inom [!DNL Platform]. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

Med Adobe I/O Events kan du prenumerera på händelser och använda webbhooks för att få meddelanden om status för dina flödeskörningar. Dessa meddelanden innehåller information om hur flödeskörningen lyckades eller om fel som bidragit till ett körningsfel.

Det här dokumentet innehåller anvisningar om hur du prenumererar på händelser, registrerar webhooks och får meddelanden som innehåller information om statusen för dina flödeskörningar.

## Komma igång

Dokumentet kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform - datahantering]](../ingestion/home.md): [!DNL Data Ingestion] representerar de olika metoder som används för att [!DNL Platform] importera data från dessa källor samt hur dessa data bevaras inom [!DNL Data Lake] ramen för att användas av [!DNL Platform] tjänster i senare led.

Det här dokumentet kräver också en fungerande förståelse för webbhooks och hur du ansluter en webkrok från ett program till ett annat. Mer information om webbhooks finns i följande [dokumentation](https://requestbin.com/blog/working-with-webhooks/) .

## Registrera din webbkrok

Om du vill få meddelanden om status för flödeskörningen måste du registrera en webkrok genom att ange en unik webkroks-URL som en del av informationen om händelseregistreringen. Om du vill ansluta en webkrok till din [!DNL I/O Events] prenumeration går du till [webbkroktjänsten](https://webhook.site/) och kopierar den unika webbadressen.

![webkrok](./images/notifications/webhook-url.png)

## Prenumerera på event

När du har skaffat en unik webbhotell-URL går du till [Adobe I/O-händelser](https://www.adobe.io/apis/experienceplatform/events.html) och följer stegen som beskrivs i dokumentet med [dataöverföringsmeddelanden](../ingestion/quality/subscribe-events.md) för att börja prenumerera på händelser.

>[!IMPORTANT]
>Under prenumerationsprocessen kontrollerar du att du väljer [!DNL Platform] meddelanden som händelseleverantör och väljer följande händelseprenumerationer:
>
>* **[!UICONTROL Experience Platform Source's Flow Run Succeeded]**
>* **[!UICONTROL Experience Platform Source's Flow Run Failed]**

>
>
När du uppmanas att ange en webbkrokadress använder du den webbkroks-URL som du har hämtat tidigare.

## Ta emot meddelanden om flödeskörning

När din webkrok är ansluten och din händelseprenumeration är klar kan du börja ta emot meddelanden om flödeskörning via webbkrokinstrumentpanelen.

Ett meddelande returnerar information som antalet överföringsjobb som körs, filstorlek och fel. Ett meddelande returnerar också en nyttolast som är kopplad till ditt flöde som körs i JSON-format. Svarets nyttolast kan antingen klassificeras som `sources_flow_run_success` eller `sources_flow_run_failure`.

>[!IMPORTANT]
>Om partiellt intag är aktiverat under skapandet av flödet markeras ett flöde som innehåller både lyckade och misslyckade inmatningar som `sources_flow_run_success` bara om antalet fel är under det tröskelvärde som angetts under skapandet av flödet. Om en lyckad flödeskörning innehåller fel inkluderas dessa fel fortfarande som en del av returnyttolasten.

### Lyckades

Ett lyckat svar returnerar en uppsättning med `metrics` som definierar egenskaper för en specifik flödeskörning och `activities` som visar hur data omformas.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{IMS_ORG}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `metrics` | Definierar egenskaper för data i flödeskörningen. |
| `activities` | Definierar de olika steg och aktiviteter som utförs för att omvandla data. |
| `durationSummary` | Definierar start- och sluttiden för flödeskörningen. |
| `sizeSummary` | Definierar datavolymen i byte. |
| `recordSummary` | Definierar antalet poster i data. |
| `fileSummary` | Definierar antalet filer för data. |
| `fileInfo` | En URL som leder till en översikt över de importerade filerna. |
| `statusSummary` | Definierar om flödeskörningen är en lyckad eller misslyckad åtgärd. |

### Fel

Följande svar är ett exempel på en misslyckad flödeskörning, där ett fel inträffar när kopierade data bearbetas. Fel kan också uppstå när data kopieras från källan. Ett misslyckat flöde innehåller information om felen som bidrog till körningsfelet, inklusive fel och beskrivning.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{IMS_ORG}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Egenskap | Beskrivning |
| ---------- | ----------- |
| `fileInfo` | En URL som leder till en översikt över de filer som både kunde importeras och inte kunde hämtas. |

>[!NOTE]
>Mer information om felmeddelanden finns i [bilagan](#errors) .

## Nästa steg

Du kan nu prenumerera på händelser som gör att du kan få meddelanden i realtid om flödeskörningsstatus. Mer information om flödeskörningar och källor finns i [Källor - översikt](./home.md).

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med meddelanden om flödeskörning.

### Om felmeddelanden {#errors}

Inmatningsfel kan uppstå när data kopieras från källan eller när kopierade data bearbetas till [!DNL Platform]. Se tabellen nedan för mer information om specifika fel.

| Fel | Beskrivning |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Ett fel uppstod när data kopierades från en källa. |
| `CONNECTOR-2001-500` | Ett fel uppstod när kopierade data bearbetades till [!DNL Platform]. Det här felet kan gälla parsning, validering eller omformning. |