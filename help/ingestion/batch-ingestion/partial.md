---
keywords: Experience Platform;hemmabruk;populära ämnen;batchförbrukning;batchintag;partiellt intag;partiellt intag;Hämtningsfel;hämtningsfel;partiellt batchintag;partiellt batchintag;intag;Inmatning;
solution: Experience Platform
title: Översikt över partiell gruppinmatning
description: Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Batchförtäring](./overview.md): Den metod som [!DNL Platform] importerar och lagrar data från datafiler, som CSV och Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ringa [!DNL Platform] API:er.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

## Aktivera en batch för partiell batchimport i API {#enable-api}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchimport med API:t. Instruktioner om hur du använder användargränssnittet finns i [aktivera en batch för partiell batchförbrukning i användargränssnittet](#enable-ui) steg.

Du kan skapa en ny grupp med partiellt intag aktiverat.

Så här skapar du en ny grupp: [Utvecklarhandbok för batchintag](./api-overview.md). När du har nått **[!UICONTROL Create batch]** lägger du till följande fält i begärandetexten:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `enableErrorDiagnostics` | En flagga som tillåter [!DNL Platform] för att generera detaljerade felmeddelanden om din grupp. |
| `partialIngestionPercent` | Procentandelen godtagbara fel innan hela gruppen misslyckas. I det här exemplet kan alltså maximalt 5 % av batchen vara fel, innan den misslyckas. |


## Aktivera en batch för partiell batchförbrukning i användargränssnittet {#enable-ui}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchförbrukning med användargränssnittet. Om du redan har aktiverat en batch för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Aktivera en batch för partiellt intag via [!DNL Platform] I användargränssnittet kan du skapa en ny grupp via källanslutningar, skapa en ny grupp i en befintlig datauppsättning eller skapa en ny grupp via[!UICONTROL Map CSV to XDM flow]&quot;.

### Skapa en ny källanslutning {#new-source}

Om du vill skapa en ny källanslutning följer du stegen i listan i dialogrutan [Översikt över källor](../../sources/home.md). När du har nått **[!UICONTROL Dataflow detail]** notera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]** fält.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

The **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

The **[!UICONTROL Error diagnostics]** växlingsknappen visas endast när **[!UICONTROL Partial ingestion]** växlingen är inaktiverad. Den här funktionen tillåter [!DNL Platform] för att generera detaljerade felmeddelanden om dina inkapslade batchar. Om **[!UICONTROL Partial ingestion]** växeln är aktiverad, förbättrad feldiagnostik används automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

The **[!UICONTROL Error threshold]** gör att du kan ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

### Använd en befintlig datauppsättning {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

The **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

The **[!UICONTROL Error diagnostics]** växlingsknappen visas endast när **[!UICONTROL Partial ingestion]** växlingen är inaktiverad. Den här funktionen tillåter [!DNL Platform] för att generera detaljerade felmeddelanden om dina inkapslade batchar. Om **[!UICONTROL Partial ingestion]** växeln är aktiverad, förbättrad feldiagnostik används automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

The **[!UICONTROL Error threshold]** gör att du kan ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

Nu kan du överföra data med **Lägg till data** och kommer att förtäras med partiellt intag.

### Använd &quot;[!UICONTROL Map CSV to XDM schema]&quot; flöde {#map-flow}

Så här använder du[!UICONTROL Map CSV to XDM schema]&quot;, följ stegen i listan i [Mappa en CSV-fil, genomgång](../tutorials/map-csv/overview.md). När du har nått **[!UICONTROL Add data]** notera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]** fält.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

The **[!UICONTROL Partial ingestion]** kan du aktivera eller inaktivera användning av partiell gruppinmatning.

The **[!UICONTROL Error diagnostics]** växlingsknappen visas endast när **[!UICONTROL Partial ingestion]** växlingen är inaktiverad. Den här funktionen tillåter [!DNL Platform] för att generera detaljerade felmeddelanden om dina inkapslade batchar. Om **[!UICONTROL Partial ingestion]** växeln är aktiverad, förbättrad feldiagnostik används automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** gör att du kan ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchintag finns i [Utvecklarhandbok för batchintag](./api-overview.md).

Mer information om övervakning av partiella intag finns i [diagnostikguide för batchmatningsfel](../quality/error-diagnostics.md).
