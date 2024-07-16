---
keywords: Experience Platform;hemmabruk;populära ämnen;batchförbrukning;batchintag;partiellt intag;partiellt intag;Hämtningsfel;hämtningsfel;partiellt batchintag;partiellt batchintag;intag;Inmatning;
solution: Experience Platform
title: Översikt över partiell gruppinmatning
description: Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Gruppinmatning](./overview.md): Den metod som [!DNL Platform] använder för att importera och lagra data från datafiler, till exempel CSV och Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata med.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa [!DNL Platform] API:er.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

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
| `enableErrorDiagnostics` | En flagga som tillåter [!DNL Platform] att generera detaljerade felmeddelanden om din batch. |
| `partialIngestionPercent` | Procentandelen godtagbara fel innan hela gruppen misslyckas. I det här exemplet kan alltså maximalt 5 % av batchen vara fel, innan den misslyckas. |


## Aktivera en batch för partiell batchförbrukning i användargränssnittet {#enable-ui}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchförbrukning med användargränssnittet. Om du redan har aktiverat en batch för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Om du vill aktivera en batch för partiellt bruk via användargränssnittet i [!DNL Platform] kan du skapa en ny grupp via källanslutningar, skapa en ny grupp i en befintlig datauppsättning eller skapa en ny grupp via [!UICONTROL Map CSV to XDM flow].

### Skapa en ny källanslutning {#new-source}

Om du vill skapa en ny källanslutning följer du stegen i listan i [Källöversikt](../../sources/home.md). När du har nått steget **[!UICONTROL Dataflow detail]** bör du notera fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

### Använd en befintlig datamängd {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

Nu kan du överföra data med knappen **Lägg till data** och det kommer att importeras delvis.

### Använd flödet [!UICONTROL Map CSV to XDM schema] {#map-flow}

Om du vill använda [!UICONTROL Map CSV to XDM schema]-flödet följer du stegen i [Mappa en CSV-fil ](../tutorials/map-csv/overview.md). När du har nått steget **[!UICONTROL Add data]** bör du notera fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Med växlingsknappen **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

**[!UICONTROL Error diagnostics]**-växeln visas bara när **[!UICONTROL Partial ingestion]**-växeln är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är det här värdet 5 %.

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchkonsumtion finns i [Utvecklarhandboken för batchkonsumtion](./api-overview.md).

Mer information om övervakning av partiella intag-fel finns i diagnostikguiden för [batchproblem](../quality/error-diagnostics.md).
