---
title: Skapa och aktivera en extern publik
type: Tutorial
description: Lär dig hur du skapar en extern publik i Adobe Experience Platform med Experience Platform API:er.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---


# Skapa och aktivera en extern målgrupp med API:t

Den här självstudiekursen går igenom de steg som krävs för att skapa en extern publik med Adobe Experience Platform API:er.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Experience Platform-tjänster som är inblandade i att skapa en extern publik. Innan du börjar den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Källor](../../sources/home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att du kan skapa målgrupper från externa data.
- [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga program som möjliggör smidig aktivering av data från Experience Platform för flerkanaliga marknadsföringskampanjer, e-postkampanjer, riktad reklam och mycket annat.

### Obligatoriska rubriker

Den här självstudien kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Experience Platform] API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla POST-, PUT- och PATCH-förfrågningar kräver ytterligare en rubrik:

- Content-Type: application/json

## Förbered den externa publiken {#prepare}

Innan du kan skapa en extern målgrupp inom Experience Platform måste du förbereda en fil som innehåller målgruppsdata.

I det här exemplet bör du använda en CSV-fil. Kontrollera att din CSV-fil innehåller **minst** en kolumn med ett identitetsvärde som ett ECID, e-post-ID eller CRM-ID. Se även till att innehåller alla berikningsattribut du behöver för segmentering och aktivering.

Du måste också se till att filen uppfyller Experience Platform schemats krav. Mer information om hur du skapar ett schema finns i [självstudiekursen om hur du skapar ett schema med API](/help/xdm/tutorials/create-schema-api.md) eller i [självstudiekursen om hur du skapar ett schema med användargränssnittet](/help/xdm/tutorials/create-schema-ui.md).

När du har bekräftat att CSV-filen innehåller all information du behöver och följer schemat, måste du överföra CSV-filen till din molnlagringsleverantör så att du kan använda källor för att importera data till Experience Platform. Mer information om hur du använder en molnlagringskälla finns i [självstudiekursen om hur du utforskar molnlagringsalternativ med API](/help/sources/tutorials/api/explore/cloud-storage.md) eller [källorna i översikt](/help/sources/home.md#cloud-storage).

## Skapa en extern publik {#create}

När du har preparerat CSV-filen kan du nu börja skapa den externa målgruppen.

Du kan skapa en extern målgrupp genom att göra en POST-begäran till slutpunkten `/external-audience/`.

När du gör den här begäran måste du ange följande information:

- Målgruppens namn
- En beskrivning av målgruppen
- Motsvarande fält mellan CSV och schemat
- Källspecifikationsinformation
   - Detta inkluderar filsökvägen för CSV-filen för inhämtning
      - Filsökvägen **får inte innehålla blanksteg**. Om sökvägen till exempel är `activation/sample-source/Example CSV File.csv` anger du sökvägen till `activation/sample-source/ExampleCSVFile.csv`.

Mer detaljerad information om hur du använder den här slutpunkten finns i [handboken för externa målgrupper](/help/segmentation/api/external-audiences.md#create-audience).

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

När du har gjort den här begäran ska du anteckna `operationId` som du får från svaret så att du kan hämta målar-ID:t.

## Hämta målgrupps-ID {#retrieve-audience-id}

Nu när ni har skapat den externa målgruppen måste ni skaffa målgrupps-ID:t så att ni kan importera målgruppen till Experience Platform.

Du kan hämta målgrupps-ID genom att göra en GET-begäran till `/external-audiences/operations`-slutpunkten och ange ID:t för den åtgärd som du tidigare fått från svaret på Skapa extern målgrupp.

Mer detaljerad information om hur du använder den här slutpunkten finns i [handboken för externa målgrupper](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Begäran

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

När du har gjort den här begäran ska du observera `audienceId` som du får från svaret så att du kan utlösa det för målgruppen.

## Starta målgruppsintag {#start-ingestion}

Eftersom du har fått din `audienceId` kan du nu utlösa att din externa målgrupp har importerats till Experience Platform.

Du kan påbörja en målgruppsinmatning genom att göra en POST-begäran till följande slutpunkt och samtidigt ange målar-ID. Dessutom måste du ange starttiden för att avgöra vilka filer som ska bearbetas.

Mer detaljerad information om hur du använder den här slutpunkten finns i [handboken för externa målgrupper](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

När du har gjort den här begäran bör du notera `runId` som du får från svaret så att du kan övervaka intagsstatus.

## Övervaka inmatningsstatus {#monitor-ingestion}

När ni har aktiverat målgruppsintaget kan ni nu övervaka hur det kommer att gå till för att bekräfta att intaget lyckades och validera målgruppens tillgänglighet för aktivering längre fram i kedjan.

Du kan hämta status för ett målgruppsintag genom att göra en GET-begäran till följande slutpunkt samtidigt som du anger både målgrupps- och kör-ID:n.

Mer detaljerad information om hur du använder den här slutpunkten finns i [handboken för externa målgrupper](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Begäran

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Nästa steg {#next-steps}

>[!IMPORTANT]
>
>Om du vill använda den externt genererade målgruppen **måste** vänta tills det dagliga segmenteringsjobbet har slutförts.

När du har bekräftat att den externa målgruppen har importerats korrekt kan du se den i Audience Portal och använda den i tjänster längre fram i kedjan, till exempel destinationer.

Mer information om Audience Portal finns i [Användarhandboken för målportalen](/help/segmentation/ui/audience-portal.md). Mer information om mål finns i [målöversikten](/help/destinations/home.md).

