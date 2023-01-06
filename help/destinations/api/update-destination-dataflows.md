---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;uppdatera måldataflöden
solution: Experience Platform
title: Uppdatera måldataflöden med API:t för Flow Service
type: Tutorial
description: I den här självstudiekursen beskrivs stegen för att uppdatera ett måldataflöde. Lär dig hur du aktiverar eller inaktiverar dataflödet, uppdaterar basinformationen eller lägger till och tar bort segment och attribut med API:t för Flow Service.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 0%

---

# Uppdatera måldataflöden med API:t för Flow Service

I den här självstudiekursen beskrivs stegen för att uppdatera ett måldataflöde. Lär dig hur du aktiverar eller inaktiverar dataflödet, uppdaterar basinformationen eller lägger till och tar bort segment och attribut med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Mer information om hur du redigerar måldataflöden med användargränssnittet i Experience Platform finns i [Redigera aktiveringsflöden](/help/destinations/ui/edit-activation.md).

## Komma igång {#get-started}

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har ett giltigt flödes-ID väljer du önskat mål på menyn [målkatalog](../catalog/overview.md) och följa de steg som beskrivs nedan för att [ansluta till målet](../ui/connect-destination.md) och [aktivera data](../ui/activation-overview.md) innan du provar den här självstudiekursen.

>[!NOTE]
>
> Villkoren *flöde* och *dataflöde* används omväxlande i den här självstudiekursen. I den här självstudiekursen har de samma betydelse.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna uppdatera ditt dataflöde med [!DNL Flow Service] API.

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i Experience Platform, inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om `x-sandbox-name` ingen rubrik har angetts, begäranden har lösts under `prod` sandlåda.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Söka efter dataflödesdetaljer {#look-up-dataflow-details}

Det första steget för att uppdatera måldataflödet är att hämta dataflödesinformation med ditt flödes-ID. Du kan visa den aktuella informationen om ett befintligt dataflöde genom att göra en GET-förfrågan till `/flows` slutpunkt.

**API-format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för måldataflödet som du vill hämta. |

**Begäran**

Följande begäran hämtar information om ditt flödes-ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar aktuell information om dataflödet, inklusive version, unik identifierare (`id`) och annan relevant information.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Uppdatera namn och beskrivning för dataflöde {#update-dataflow}

Uppdatera dataflödets namn och beskrivning genom att utföra en PATCH-begäran till [!DNL Flow Service] API när du anger ditt flödes-ID, version och de nya värden du vill använda.

>[!IMPORTANT]
>
>The `If-Match` måste anges när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av dataflödet som du vill uppdatera. Värdet för etag uppdateras med varje lyckad uppdatering av ett dataflöde.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran uppdaterar dataflödets namn och beskrivning.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aktivera eller inaktivera dataflöde {#enable-disable-dataflow}

När det här alternativet är aktiverat exporteras profiler till målet med ett dataflöde. Dataflöden är aktiverade som standard, men kan inaktiveras för att pausa profilexporter.

Du kan aktivera eller inaktivera ett befintligt måldataflöde genom att göra en begäran om POST till [!DNL Flow Service] API och ange att du vill uppdatera flödet till.

**API-format**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Begäran**

Följande begäran uppdaterar dataflödets tillstånd till aktiverat.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Följande begäran uppdaterar dataflödets tillstånd till inaktiverat.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Lägga till ett segment i ett dataflöde {#add-segment}

Om du vill lägga till ett segment i måldataflödet utför du en PATCH-begäran i [!DNL Flow Service] API när du anger ditt flödes-ID, version och det segment du vill lägga till.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran lägger till ett nytt segment i ett befintligt måldataflöde.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. Om du vill lägga till ett segment i ett dataflöde använder du `add` operation. |
| `path` | Definierar den del av flödet som ska uppdateras. När du lägger till ett segment i ett dataflöde använder du den sökväg som anges i exemplet. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |
| `id` | Ange ID:t för det segment som du lägger till i måldataflödet. |
| `name` | **(Valfritt)**. Ange namnet på segmentet som du lägger till i måldataflödet. Observera att det här fältet inte är obligatoriskt och att du kan lägga till ett segment i måldataflödet utan att ange dess namn. |
| `filenameTemplate` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du lägger till ett segment i ett dataflöde i exportmål för batchfiler som Amazon S3, SFTP eller Azure Blob. <br> Det här fältet avgör filnamnsformatet för de filer som exporteras till ditt mål. <br> Följande alternativ är tillgängliga: <br> <ul><li>`%DESTINATION_NAME%`: Obligatoriskt. De exporterade filerna innehåller målnamnet.</li><li>`%SEGMENT_ID%`: Obligatoriskt. De exporterade filerna innehåller ID:t för det exporterade segmentet.</li><li>`%SEGMENT_NAME%`: **(Valfritt)**. De exporterade filerna innehåller namnet på det exporterade segmentet.</li><li>`DATETIME(YYYYMMdd_HHmmss)` eller `%TIMESTAMP%`: **(Valfritt)**. Välj något av dessa två alternativ för filerna så att de innehåller den tid då de genereras av Experience Platform.</li><li>`custom-text`: **(Valfritt)**. Ersätt den här platshållaren med eventuell egen text som du vill lägga till i slutet av filnamnen.</li></ul> <br> Mer information om hur du konfigurerar filnamn finns i [konfigurera filnamn](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) i satskörningsguiden. |
| `exportMode` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du lägger till ett segment i ett dataflöde i exportmål för batchfiler som Amazon S3, SFTP eller Azure Blob. <br> Obligatoriskt. Välj `"DAILY_FULL_EXPORT"` eller `"FIRST_FULL_THEN_INCREMENTAL"`. Mer information om de två alternativen finns i [exportera fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [exportera inkrementella filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) i satskörningssjälvstudiekursen. |
| `startDate` | Välj det datum då segmentet ska börja exportera profiler till målet. |
| `frequency` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du lägger till ett segment i ett dataflöde i exportmål för batchfiler som Amazon S3, SFTP eller Azure Blob. <br> Obligatoriskt. <br> <ul><li>För `"DAILY_FULL_EXPORT"` exportläge kan du välja `ONCE` eller `DAILY`.</li><li>För `"FIRST_FULL_THEN_INCREMENTAL"` exportläge kan du välja `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du väljer `"DAILY_FULL_EXPORT"` i `frequency` väljare. <br> Obligatoriskt. <br> <ul><li>Välj `"AFTER_SEGMENT_EVAL"` så att aktiveringsjobbet körs omedelbart när det dagliga gruppsegmenteringsjobbet för plattformen har slutförts. Detta garanterar att de senaste profilerna exporteras till ditt mål när aktiveringsjobbet körs.</li><li>Välj `"SCHEDULED"` för att få aktiveringsjobbet att köras på en fast tid. Detta säkerställer att profildata exporteras vid samma tidpunkt varje dag, men de profiler du exporterar kanske inte är de mest aktuella, beroende på om gruppsegmenteringsjobbet har slutförts innan aktiveringsjobbet startar. När du väljer det här alternativet måste du även lägga till en `startTime` ange vid vilken tidpunkt i UTC den dagliga exporten ska ske.</li></ul> |
| `endDate` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du lägger till ett segment i ett dataflöde i exportmål för batchfiler som Amazon S3, SFTP eller Azure Blob. <br> Ej tillämpligt vid val `"exportMode":"DAILY_FULL_EXPORT"` och `"frequency":"ONCE"`. <br> Anger det datum då segmentmedlemmar slutar att exporteras till målet. |
| `startTime` | För *batchdestinationer* endast. Det här fältet är endast obligatoriskt när du lägger till ett segment i ett dataflöde i exportmål för batchfiler som Amazon S3, SFTP eller Azure Blob. <br> Obligatoriskt. Välj den tidpunkt då filer som innehåller medlemmar i segmentet ska genereras och exporteras till målet. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ta bort ett segment från ett dataflöde {#remove-segment}

Om du vill ta bort ett segment från ett befintligt måldataflöde utför du en PATCH-begäran till [!DNL Flow Service] API när du anger ditt flödes-ID, version och indexväljaren för det segment som du vill ta bort. Indexeringen börjar vid `0`. Exempelbegäran nedan tar till exempel bort det första och andra segmentet från dataflödet.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran tar bort två segment från ett befintligt måldataflöde.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. Om du vill ta bort ett segment från ett dataflöde använder du `remove` operation. |
| `path` | Anger vilket befintligt segment som ska tas bort från måldataflödet, baserat på segmentväljarens index. Om du vill hämta segmentens ordning i ett dataflöde ska du ringa GET till `/flows` slutpunkt och inspektera `transformations.segmentSelectors` -egenskap. Om du vill ta bort det första segmentet i dataflödet använder du `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Uppdatera komponenter i ett segment i ett dataflöde {#update-segment}

Du kan uppdatera komponenter i ett segment i ett befintligt måldataflöde. Du kan till exempel ändra exportfrekvensen eller redigera filnamnsmallen. Gör detta genom att göra en PATCH-förfrågan till [!DNL Flow Service] API när du anger ditt flödes-ID, version och indexväljare för det segment som du vill uppdatera. Indexeringen börjar vid `0`. Begäran nedan uppdaterar till exempel det nionde segmentet i ett dataflöde.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

När du uppdaterar ett segment i ett befintligt måldataflöde bör du först utföra en GET-åtgärd för att hämta information om det segment som du vill uppdatera. Ange sedan all segmentinformation i nyttolasten, inte bara de fält som du vill uppdatera. I exemplet nedan läggs egen text till i slutet av filnamnsmallen och exportschemafrekvensen uppdateras från 6 timmar till 12 timmar.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Beskrivningar av egenskaperna i nyttolasten finns i avsnittet [Lägga till ett segment i ett dataflöde](#add-segment).


**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Se exemplen nedan för fler exempel på segmentkomponenter som du kan uppdatera i ett dataflöde.

## Uppdatera exportläget för ett segment från schemalagd till efter segmentutvärdering {#update-export-mode}

+++ Klicka här om du vill se ett exempel där en segmentexport uppdateras från att aktiveras varje dag vid en viss tidpunkt till att aktiveras varje dag efter att batch-segmenteringsjobbet för plattformen har slutförts.

Segmentet exporteras varje dag kl. 16.00 UTC.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Segmentet exporteras varje dag när det dagliga gruppsegmenteringsjobbet har slutförts.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Uppdatera filnamnsmallen så att den innehåller fler fält i filnamnet {#update-filename-template}

+++ Klicka här om du vill se ett exempel där filnamnsmallen uppdateras för att inkludera ytterligare fält i filnamnet

De exporterade filerna innehåller målnamn och Experience Platform-segment-ID

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

De exporterade filerna innehåller målnamn, Experience Platform segment-ID, datum och tid då filen skapades av Experience Platform och egen text i slutet av filerna.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Lägga till ett profilattribut i ett dataflöde {#add-profile-attribute}

Om du vill lägga till ett profilattribut i måldataflödet utför du en PATCH-begäran i [!DNL Flow Service] API när du anger ditt flödes-ID, version och det profilattribut som du vill lägga till.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran lägger till ett nytt profilattribut i ett befintligt måldataflöde.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. Om du vill lägga till ett profilattribut i ett dataflöde använder du `add` operation. |
| `path` | Definierar den del av flödet som ska uppdateras. När du lägger till ett profilattribut i ett dataflöde använder du sökvägen som anges i exemplet. |
| `value.path` | Värdet på profilattributet som du lägger till i dataflödet. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ta bort ett profilattribut från ett dataflöde {#remove-profile-attribute}

Om du vill ta bort ett profilattribut från ett befintligt måldataflöde utför du en PATCH-begäran till [!DNL Flow Service] API när du anger ditt flödes-ID, version och indexväljaren för det profilattribut som du vill ta bort. Indexeringen börjar vid `0`. Exempelbegäran nedan tar till exempel bort femte profilattributet från dataflödet.


**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran tar bort ett profilattribut från ett befintligt måldataflöde.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. Om du vill ta bort ett segment från ett dataflöde använder du `remove` operation. |
| `path` | Anger vilket befintligt profilattribut som ska tas bort från måldataflödet, baserat på segmentväljarens index. Om du vill hämta profilattributens ordning i ett dataflöde, ska du göra ett GET-anrop till `/flows` slutpunkt och inspektera `transformations.profileSelectors` -egenskap. Om du vill ta bort det första segmentet i dataflödet använder du `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudien följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](/help/landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](/help/landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen för mer information om hur du tolkar felsvar.

## Nästa steg {#next-steps}

Genom att följa den här självstudien har du lärt dig hur du uppdaterar olika komponenter i ett måldataflöde, som att lägga till eller ta bort segment eller profilattribut med [!DNL Flow Service] API. Mer information om destinationer finns i [destinationer, översikt](../home.md).
