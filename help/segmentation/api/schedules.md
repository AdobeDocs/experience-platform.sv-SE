---
solution: Experience Platform
title: API-slutpunkt för scheman
description: Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 0%

---

# Slutpunkt för scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda slutpunkten `/config/schedules` för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med scheman {#retrieve-list}

Du kan hämta en lista över alla scheman för din organisation genom att göra en GET-förfrågan till slutpunkten `/config/schedules`.

**API-format**

Slutpunkten `/config/schedules` har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla scheman som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**Frågeparametrar**

+++ En lista med tillgängliga frågeparametrar.

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Anger vilken sida förskjutningen ska börja från. Som standard är det här värdet 0. | `start=5` |
| `limit` | Anger antalet returnerade scheman. Som standard är värdet 100. | `limit=20` |

+++

**Begäran**

Följande förfrågan hämtar de tio senaste scheman som publicerats inom din organisation.

+++ En exempelbegäran om att hämta en lista med scheman.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över scheman för den angivna organisationen som JSON.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme och visar endast det första schemat som returnerats.

+++ Ett exempelsvar när en lista med scheman hämtas.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `_page.totalCount` | Det totala antalet returnerade scheman. |
| `_page.pageSize` | Sidstorleken för scheman. |
| `children.name` | Schemats namn som en sträng. |
| `children.type` | Typ av jobb som en sträng. De två typer som stöds är&quot;batch_segmentation&quot; och&quot;export&quot;. |
| `children.properties` | Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `children.properties.segments` | Om du använder `["*"]` säkerställs att alla segment inkluderas. |
| `children.schedule` | En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i bilagan i formatet [cron expression](#appendix). I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras kl. 1.00 varje dag. |
| `children.state` | En sträng som innehåller schematillståndet. De två lägen som stöds är &quot;active&quot; och &quot;inactive&quot;. Som standard är läget inställt på &quot;inaktiv&quot;. |

+++

## Skapa ett nytt schema {#create}

Du kan skapa ett nytt schema genom att göra en POST-förfrågan till slutpunkten `/config/schedules`.

**API-format**

```http
POST /config/schedules
```

**Begäran**

+++ En exempelbegäran om att skapa ett schema.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `name` | **Krävs.** Schemats namn som en sträng. |
| `type` | **Krävs.** Den typ av jobb som en sträng. De två typer som stöds är&quot;batch_segmentation&quot; och&quot;export&quot;. |
| `properties` | **Krävs.** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **Krävs när `type` är lika med&quot;batch_segmentation&quot;.** Om du använder `["*"]` säkerställs att alla segment inkluderas. |
| `schedule` | *Valfritt.* En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i bilagan i formatet [cron expression](#appendix). I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras kl. 1.00 varje dag. <br><br>Om strängen inte anges genereras ett systemgenererat schema automatiskt. |
| `state` | *Valfritt.* En sträng som innehåller schematillståndet. De två lägen som stöds är &quot;active&quot; och &quot;inactive&quot;. Som standard är läget inställt på &quot;inaktiv&quot;. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

+++ Ett exempelsvar när du skapar ett schema.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

+++

## Hämta ett specifikt schema {#get}

Du kan hämta detaljerad information om ett specifikt schema genom att göra en GET-förfrågan till slutpunkten `/config/schedules` och ange ID:t för det schema som du vill hämta i sökvägen till begäran.

**API-format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill hämta. |

**Begäran**

+++ En exempelbegäran om att hämta ett schema.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna schemat.

+++ Ett exempelsvar när ett schema hämtas.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `name` | Schemats namn som en sträng. |
| `type` | Typ av jobb som en sträng. De två typer som stöds är `batch_segmentation` och `export`. |
| `properties` | Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | Om du använder `["*"]` säkerställs att alla segment inkluderas. |
| `schedule` | En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i bilagan i formatet [cron expression](#appendix). I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras kl. 1.00 varje dag. |
| `state` | En sträng som innehåller schematillståndet. De två lägen som stöds är `active` och `inactive`. Som standard är läget inställt på `inactive`. |

+++

## Uppdatera information för ett specifikt schema {#update}

Du kan uppdatera ett specifikt schema genom att göra en PATCH-begäran till slutpunkten `/config/schedules` och ange ID:t för det schema som du försöker uppdatera i sökvägen till begäran.

Med PATCH-begäran kan du uppdatera antingen [state](#update-state) eller [cron schedule](#update-schedule) för ett enskilt schema.

**API-format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill uppdatera. |

>[!BEGINTABS]

>[!TAB Uppdatera schematillstånd]

Du kan använda en JSON-lagningsåtgärd för att uppdatera schemats status. Om du vill uppdatera läget deklarerar du egenskapen `path` som `/state` och anger `value` som antingen `active` eller `inactive`. Mer information om JSON Patch finns i [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) -dokumentationen.

**Begäran**

+++ Ett exempel på en begäran om att uppdatera schemats tillstånd.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

+++

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet `path` till /state eftersom du uppdaterar schemats tillstånd. |
| `value` | Det uppdaterade värdet för schemats tillstånd. Värdet kan antingen anges som aktivt eller inaktivt för att aktivera eller inaktivera schemat. Observera att du **inte kan** inaktivera ett schema om organisationen har aktiverats för direktuppspelning. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

>[!TAB Uppdatera kundschema]

Du kan använda en JSON-korrigeringsåtgärd för att uppdatera kronschemat. Om du vill uppdatera schemat deklarerar du egenskapen `path` som `/schedule` och ställer in `value` på ett giltigt cron-schema. Mer information om JSON Patch finns i [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) -dokumentationen. Mer information om cron-scheman finns i bilagan i formatet [cron expression](#appendix).

>[!ENDTABS]

**Begäran**

+++ Ett exempel på en begäran om att uppdatera schemat.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill uppdatera. I det här fallet måste du ange värdet `path` till `/schedule` eftersom du uppdaterar cron-schemat. |
| `value` | Det uppdaterade värdet för cron-schemat. Värdet måste anges i form av ett kronschema. I det här exemplet körs schemat den andra varje månad. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

## Ta bort ett specifikt schema

Du kan begära att ett visst schema ska tas bort genom att göra en DELETE-begäran till slutpunkten `/config/schedules` och ange ID:t för det schema som du vill ta bort i sökvägen till begäran.

**API-format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill ta bort. |

**Begäran**

+++ En exempelbegäran om att ta bort ett schema.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur scheman fungerar.

## Bilaga {#appendix}

I följande bilaga förklaras formatet för de cron-uttryck som används i scheman.

### Format

Ett cron-uttryck är en sträng som består av 6 eller 7 fält. Uttrycket skulle se ut ungefär så här:

`0 0 12 * * ?`

I en cron-uttryckssträng representerar det första fältet sekunder, det andra representerar minuter, det tredje representerar timmar, det fjärde fältet representerar dag i månaden, det femte fältet representerar månad och det sjätte fältet representerar veckodag. Du kan också inkludera ett sjunde fält som representerar året.

| Fältnamn | Obligatoriskt | Möjliga värden | Specialtecken tillåts |
| ---------- | -------- | --------------- | -------------------------- |
| Sekunder | Ja | 0-59 | `, - * /` |
| Minuter | Ja | 0-59 | `, - * /` |
| Timmar | Ja | 0-23 | `, - * /` |
| Dag i månaden | Ja | 1-31 | `, - * ? / L W` |
| Månad | Ja | 1-12, JAN-DEC | `, - * /` |
| Veckodag | Ja | 1-7, SUN-SAT | `, - * ? / L #` |
| År | Nej | Empty, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Namnen på månaderna och namnen på veckodagarna är **inte** skiftlägeskänsliga. Därför motsvarar `SUN` användningen av `sun`.

De specialtecken som tillåts har följande betydelse:

| Specialtecken | Beskrivning |
| ----------------- | ----------- |
| `*` | Det här värdet används för att välja **alla** värden i ett fält. Om du till exempel placerar `*` i timfältet innebär det **var** timme. |
| `?` | Detta värde innebär att inget specifikt värde krävs. Detta används vanligtvis för att ange något i ett fält där tecknet är tillåtet, men inte för att ange det i det andra. Om du till exempel vill att en händelse ska utlösas var tredje månad, men inte bryr dig om vilken veckodag den är, placerar du `3` i fältet Dag i månaden och `?` i fältet Dag i veckan. |
| `-` | Det här värdet används för att ange **inkluderande** intervall för fältet. Om du till exempel placerar `9-15` i fältet Timmar innebär det att timmarna skulle innehålla 9, 10, 11, 12, 13, 14 och 15. |
| `,` | Det här värdet används för att ange ytterligare värden. Om du till exempel placerar `MON, FRI, SAT` i veckodag innebär det att veckodagarna omfattar måndag, fredag och lördag. |
| `/` | Det här värdet används för att ange steg. Värdet som placeras före `/` avgör varifrån det ökas, medan värdet som placeras efter `/` avgör hur mycket det ökar med. Om du till exempel placerar `1/7` i minutfältet innebär det att minuterna innehåller 1, 8, 15, 22, 29, 36, 43, 50 och 57. |
| `L` | Det här värdet används för att ange `Last` och har en annan betydelse beroende på vilket fält det används av. Om den används med dagen i månadsfältet representerar det den sista dagen i månaden. Om den används med veckodagen i fältet representerar den den sista veckodagen, som är lördag (`SAT`). Om den används med veckodagen i fältet tillsammans med ett annat värde representerar den sista dagen i den typen för månaden. Om du t.ex. placerar `5L` i veckodag kommer **endast** att inkludera den sista fredagen i månaden. |
| `W` | Det här värdet används för att ange närmaste veckodag till angiven dag. Om du till exempel placerar `18W` på dagen i månadsfältet, och den 18 i den månaden var en lördag, utlöses den 17:e fredagen, vilket är den närmaste veckodagen. Om den 18:e månaden var en söndag skulle den utlösas måndag den 19:e, vilket är den närmaste veckodagen. Observera, att om du anger `1W` som dag i månadsfältet och den närmast veckodagen kommer att vara föregående månad, kommer händelsen fortfarande att utlösas på den närmaste veckodagen i **current** -månaden.</br></br>Dessutom kan du kombinera `L` och `W` för att skapa `LW`, vilket skulle ange den sista veckodagen i månaden. |
| `#` | Det här värdet används för att ange den n:e dagen i veckan i en månad. Värdet som placerats före `#` representerar veckodagen, medan värdet som placerats efter `#` representerar vilken förekomst i månaden det är. Om du till exempel placerar `1#3` utlöses händelsen den tredje söndagen i månaden. Observera, att om du skickar `X#5` och det inte finns någon femte förekomst av veckodagen den månaden, kommer händelsen **inte** att utlösas. Om du till exempel skickar `1#5` och det inte finns någon femte söndag den månaden, kommer händelsen **inte** att utlösas. |

### Exempel

I följande tabell visas exempel på strängar för cron-uttryck och en förklaring av vad de betyder.

| Uttryck | Förklaring |
| ---------- | ----------- |
| `0 0 13 * * ?` | Evenemanget utlöses klockan 12.00 varje dag. |
| `0 30 9 * * ? 2022` | Evenemanget utlöses varje dag kl. 9.30 2022. |
| `0 * 18 * * ?` | Evenemanget utlöses varje minut, med början 18.00 och avslutning 18.59, varje dag. |
| `0 0/10 17 * * ?` | Evenemanget utlöses var 10:e minut, med början 17:00 och avslutning 18:00, varje dag. |
| `0 13,38 5 ? 6 WED` | Evenemanget utlöses kl. 5.13 och kl. 17.38 varje onsdag i juni. |
| `0 30 12 ? * 4#3` | Evenemanget utlöses kl. 12.30 den tredje onsdagen varje månad. |
| `0 30 12 ? * 6L` | Evenemanget utlöses kl. 12.30 sista fredagen varje månad. |
| `0 45 11 ? * MON-THU` | Evenemanget utlöses kl. 11.45 varje måndag, tisdag, onsdag och torsdag. |