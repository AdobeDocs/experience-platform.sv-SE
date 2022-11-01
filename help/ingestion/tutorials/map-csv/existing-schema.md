---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mappa en CSV-fil till ett befintligt XDM-schema
topic-legacy: tutorial
type: Tutorial
description: I den här självstudiekursen beskrivs hur du mappar en CSV-fil till ett befintligt XDM-schema med Adobe Experience Platform användargränssnitt.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 160a75a1811afa002717e167887550715eee5471
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Mappa en CSV-fil till ett befintligt XDM-schema

>[!NOTE]
>
>Det här dokumentet beskriver hur du mappar en CSV-fil till ett befintligt XDM-schema. Information om hur du använder det AI-genererade rekommendationsverktyget (som för närvarande är betaversioner) finns i dokumentet om [mappa en CSV-fil med maskininlärningsrekommendationer](./recommendations.md).

För att kunna importera CSV-data till [!DNL Adobe Experience Platform]måste data mappas till en [!DNL Experience Data Model] (XDM) schema. I den här självstudiekursen beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.
- [Batchförtäring](../../batch-ingestion/overview.md): Den metod som [!DNL Platform] importerar data från datafiler som användaren anger.
- [Adobe Experience Platform Data Prep](../../batch-ingestion/overview.md): En uppsättning funktioner som gör att du kan mappa och omvandla inkapslade data så att de överensstämmer med XDM-scheman. Dokumentationen om [Förinställningsfunktioner för data](../../../data-prep/functions.md) är särskilt relevant för schemamappning.

Den här självstudien kräver också att du redan har skapat en datauppsättning att importera dina CSV-data till. Anvisningar om hur du skapar en datauppsättning i användargränssnittet finns i [dataimport, genomgång](../ingest-batch-data.md).

## Välj ett mål

Logga in på [[!DNL Adobe Experience Platform]](https://platform.adobe.com) och sedan markera **[!UICONTROL Workflows]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Workflows]** arbetsyta.

Från **[!UICONTROL Workflows]** skärm, välja **[!UICONTROL Map CSV to XDM schema]** under **[!UICONTROL Data ingestion]** och sedan markera **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

The **[!UICONTROL Map CSV to XDM schema]** arbetsflödet visas, med början på **[!UICONTROL Destination]** steg. Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera dina CSV-data till en befintlig datauppsättning väljer du **[!UICONTROL Use existing dataset]**. Du kan antingen hämta en befintlig datauppsättning med sökfunktionen eller genom att bläddra igenom listan med befintliga datauppsättningar i panelen.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Om du vill importera dina CSV-data till en ny datauppsättning väljer du **[!UICONTROL Create new dataset]** och ange ett namn och en beskrivning för datauppsättningen i de angivna fälten. Välj ett schema med antingen sökfunktionen eller genom att bläddra igenom listan med scheman. Välj **[!UICONTROL Next]** för att fortsätta.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Lägg till data

The **[!UICONTROL Add data]** visas. Dra och släpp CSV-filen i det tillgängliga utrymmet, eller välj **[!UICONTROL Choose files]** om du vill ange en CSV-fil manuellt.

![](../../images/tutorials/map-a-csv-file/add-data.png)

The **[!UICONTROL Sample data]** visas när filen har överförts och de första tio raderna med data visas. När du har bekräftat att data har överförts som förväntat väljer du **[!UICONTROL Next]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## Mappa CSV-fält till XDM-schemafält

The **[!UICONTROL Mapping]** visas. Kolumnerna i CSV-filen listas under **[!UICONTROL Source Field]**, med motsvarande XDM-schemafält listade under **[!UICONTROL Target Field]**.

[!DNL Platform] ger automatiskt intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Om du vill acceptera alla automatiskt genererade mappningsvärden markerar du kryssrutan &quot;[!UICONTROL Accept all target fields]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Ibland finns det mer än en rekommendation för källschemat. När detta inträffar visas den mest framträdande rekommendationen på mappningskortet, följt av en blå cirkel som innehåller antalet tillgängliga ytterligare rekommendationer. Om du väljer glödlampsikonen visas en lista med ytterligare rekommendationer. Du kan välja en av de alternativa rekommendationerna genom att markera kryssrutan bredvid den rekommendation du vill mappa till i stället.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Du kan också välja att manuellt mappa källschemat till målschemat. Håll pekaren över det källschema som du vill mappa och välj sedan plusikonen.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

The **[!UICONTROL Map source to target field]** popover visas. Här väljer du vilket fält som ska mappas, följt av **[!UICONTROL Save]** för att lägga till din nya mappning.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Om du vill ta bort en av mappningarna för du pekaren över mappningen och väljer minusikonen.

### Lägg till beräknat fält {#add-calculated-field}

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till.

Välj **[!UICONTROL Add calculated field]** för att fortsätta

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

The **[!UICONTROL Create calculated field]** visas. Den vänstra dialogrutan innehåller de fält, funktioner och operatorer som stöds i beräkningsfält. Välj en av flikarna för att börja lägga till funktioner, fält eller operatorer i uttrycksredigeraren.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabb | Beskrivning |
| --------- | ----------- |
| Fält | Fliken Fält visar de fält och attribut som är tillgängliga i källschemat. |
| Funktioner | På fliken Funktioner visas de funktioner som är tillgängliga för att omforma data. Om du vill veta mer om funktionerna som du kan använda i beräkningsfält kan du läsa guiden på [använda funktioner för dataförberedelse (Mapper)](../../../data-prep/functions.md). |
| Operatorer | På fliken Operatorer visas de operatorer som är tillgängliga för att omforma data. |

Du kan lägga till fält, funktioner och operatorer manuellt med uttrycksredigeraren i mitten. Välj redigeraren för att börja skapa ett uttryck.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Välj **[!UICONTROL Save]** för att fortsätta.

Mappningsskärmen visas igen med det nya källfältet. Tillämpa motsvarande målfält och välj **[!UICONTROL Finish]** för att slutföra mappningen.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Övervaka datainmatning

När CSV-filen har mappats och skapats kan du övervaka de data som hämtas genom den. Mer information om hur du övervakar dataöverföring finns i självstudiekursen om [övervaka datainmatning](../../../ingestion/quality/monitor-data-ingestion.md).

## Nästa steg

I den här självstudiekursen har du mappat en platt CSV-fil till ett XDM-schema och infogat den i [!DNL Platform]. Dessa data kan nu användas av underordnade [!DNL Platform] tjänster som [!DNL Real-time Customer Profile]. Se översikten för [[!DNL Real-time Customer Profile]](../../../profile/home.md) för mer information.
