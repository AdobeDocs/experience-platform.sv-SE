---
keywords: Experience Platform;hem;populära ämnen;batchförbrukning;batchintag;partiellt intag;partiellt intag;Hämtningsfel;hämtningsfel;partiellt batchintag;partiellt batchintag;partiellt;intag;Inmatning;
solution: Experience Platform
title: Översikt över partiell gruppinmatning
description: Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Gruppinmatning](./overview.md): Den metod som [!DNL Experience Platform] använder för att importera och lagra data från datafiler, till exempel CSV och Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa [!DNL Experience Platform] API:er.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

## Aktivera en batch för partiell batchimport i API {#enable-api}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchimport med API:t. Instruktioner om hur du använder användargränssnittet finns i [aktivera en batch för partiell gruppinmatning i UI](#enable-ui) -steget.

Du kan skapa en ny grupp med partiellt intag aktiverat.

Om du vill skapa en ny grupp följer du stegen i [Utvecklarhandbok för batchimport](./api-overview.md). När du har nått steget **[!UICONTROL Create batch]** lägger du till följande fält i begärandetexten:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `enableErrorDiagnostics` | En flagga som tillåter [!DNL Experience Platform] att generera detaljerade felmeddelanden om din batch. |
| `partialIngestionPercent` | Procentandelen godtagbara fel innan hela gruppen misslyckas. I det här exemplet kan alltså maximalt 5 % av batchen vara fel, innan den misslyckas. |


## Aktivera en batch för partiell batchförbrukning i användargränssnittet {#enable-ui}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchförbrukning med användargränssnittet. Om du redan har aktiverat en batch för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Om du vill aktivera en batch för partiellt bruk via användargränssnittet i [!DNL Experience Platform] kan du skapa en ny grupp via källanslutningar, skapa en ny grupp i en befintlig datauppsättning eller skapa en ny grupp via [!UICONTROL Map CSV to XDM flow].

### Skapa en ny källanslutning {#new-source}

Om du vill skapa en ny källanslutning följer du stegen i listan i [Källöversikt](../../sources/home.md). När du har nått steget **[!UICONTROL Dataflow detail]** bör du notera fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Experience Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

### Använd en befintlig datamängd {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Experience Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

Nu kan du överföra data med knappen **Lägg till data** och det kommer att importeras delvis.

### Använd flödet [!UICONTROL Map CSV to XDM schema] {#map-flow}

Om du vill använda [!UICONTROL Map CSV to XDM schema]-flödet följer du stegen i [Mappa en CSV-fil ](../tutorials/map-csv/overview.md). När du har nått steget **[!UICONTROL Add data]** bör du notera fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Experience Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

## Aktivera partiell inmatnings- och feldiagnostik för ett befintligt dataflöde

Om ett dataflöde i Experience Platform skapades utan att partiellt intag eller feldiagnostik aktiverades, kan du fortfarande aktivera de här funktionerna utan att återskapa flödet. Genom att aktivera partiell inmatning och stabil feldiagnostik kan du förbättra tillförlitligheten och enkelheten i felsökningen i arbetsflödena för dataöverföring. Läs avsnitten nedan för att lära dig hur du aktiverar partiell import och feldiagnostik för ett befintligt dataflöde med API:t [!DNL Flow Service].

Som standard har dataflöden inte partiellt intag eller feldiagnostik aktiverat. De här funktionerna är användbara när du vill identifiera och isolera problem vid dataöverföring. Med API:t [!DNL Flow Service] kan du hämta din aktuella dataflödeskonfiguration och tillämpa de nödvändiga ändringarna med en PATCH-begäran.

Följ stegen nedan för att aktivera partiell import och feldiagnostik för ett befintligt dataflöde.

### Hämta flödesinformation

Om du vill hämta dina dataflödeskonfigurationer skickar du en GET-begäran till slutpunkten `/flows/{FLOW_ID}` och anger ID:t för dataflödet. Mer information om hur du hämtar dataflödesinformation finns i [Uppdatera dataflöden med hjälp av  [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md)-guiden.

Spara värdet för fältet `etag` som returneras i svaret. Detta är nödvändigt för att uppdateringsbegäran ska vara konsekvent.

### Uppdatera flödeskonfiguration

Gör sedan en PATCH-begäran till `/flows/`-slutpunkten och ange ID:t för det dataflöde som du vill aktivera partiell import och feldiagnostik för.

>[!IMPORTANT]
>
>- Inkludera det tidigare sparade `etag`-värdet i begärandehuvudet med hjälp av If-Match-nyckeln.
>- Du kan ändra värdet för `partialIngestionPercent` så att det passar dina specifika behov.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**Svar**

Ett lyckat svar returnerar dataflödets `id` och ett uppdaterat `etag`.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### Verifiera uppdateringen

När PATCH är klart gör du en GET-begäran och hämtar dataflödet för att bekräfta att ändringarna har slutförts.

**API-format**

```http
GET /flows/{FLOW_ID}
```

**Begäran**

Följande begäran hämtar uppdaterad information om ditt flödes-ID.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar dina dataflödesdetaljer, vilket bekräftar att partiellt intag och feldiagnostik nu är aktiverat i avsnittet `options`.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchkonsumtion finns i [Utvecklarhandboken för batchkonsumtion](./api-overview.md).

Mer information om övervakning av partiella intag-fel finns i diagnostikguiden för [batchproblem](../quality/error-diagnostics.md).
