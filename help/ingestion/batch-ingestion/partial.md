---
keywords: Experience Platform;hemmabruk;populära ämnen;batchförbrukning;batchintag;partiellt intag;partiellt intag;Hämtningsfel;hämtningsfel;partiellt batchintag;partiellt batchintag;intag;Inmatning;
solution: Experience Platform
title: Översikt över partiell batchöverföring
topic: overview
description: Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Batchförtäring](./overview.md): Den metod som används för att  [!DNL Platform] importera och lagra data från datafiler, till exempel CSV och Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:er för [!DNL Platform].

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Aktivera en batch för partiell batchimport i API {#enable-api}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchimport med API:t. Instruktioner om hur du använder användargränssnittet finns i [aktivera en batch för partiell batchförbrukning i steget UI](#enable-ui).

Du kan skapa en ny grupp med partiellt intag aktiverat.

Om du vill skapa en ny batch följer du stegen i [Utvecklarhandbok för batchimport](./api-overview.md). När du har nått steget **[!UICONTROL Create batch]** lägger du till följande fält i begärandetexten:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `enableErrorDiagnostics` | En flagga som gör att [!DNL Platform] kan generera detaljerade felmeddelanden om din batch. |
| `partialIngestionPercentage` | Procentandelen godtagbara fel innan hela gruppen misslyckas. I det här exemplet kan alltså maximalt 5 % av batchen vara fel, innan den misslyckas. |


## Aktivera en batch för partiell gruppinmatning i användargränssnittet {#enable-ui}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchförbrukning med användargränssnittet. Om du redan har aktiverat en batch för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Om du vill aktivera en batch för partiellt intag via användargränssnittet för [!DNL Platform] kan du skapa en ny grupp via källanslutningar, skapa en ny grupp i en befintlig datauppsättning eller skapa en ny grupp via &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Skapa en ny källanslutning {#new-source}

Om du vill skapa en ny källanslutning följer du stegen i [Källöversikt](../../sources/home.md). När du har nått steget **[!UICONTROL Dataflow detail]** ska du anteckna fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Med alternativet **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växeln **[!UICONTROL Error diagnostics]** visas bara när växeln **[!UICONTROL Partial ingestion]** är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

### Använd en befintlig datamängd {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Med alternativet **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växeln **[!UICONTROL Error diagnostics]** visas bara när växeln **[!UICONTROL Partial ingestion]** är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

Nu kan du överföra data med knappen **Lägg till data**, och den kommer att importeras delvis.

### Använd flödet [!UICONTROL Map CSV to XDM schema] {#map-flow}

Om du vill använda flödet [!UICONTROL Map CSV to XDM schema] följer du stegen i [Mappa en CSV-filsjälvstudiekurs](../tutorials/map-a-csv-file.md). När du har nått steget **[!UICONTROL Add data]** ska du anteckna fälten **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Med alternativet **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växeln **[!UICONTROL Error diagnostics]** visas bara när växeln **[!UICONTROL Partial ingestion]** är inaktiverad. Med den här funktionen kan [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om växeln **[!UICONTROL Partial ingestion]** är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** gör att du kan ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchförbrukning finns i [Utvecklarhandbok för batchkonsumtion](./api-overview.md).

Mer information om övervakning av partiella intag-fel finns i [diagnostikguiden för batchingfel](../quality/error-diagnostics.md).
