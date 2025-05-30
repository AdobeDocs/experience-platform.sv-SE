---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;kampanj;kampanjhanterade tjänster
title: Skapa en källanslutning till Adobe Campaign Managed Cloud Services med Experience Platform UI
description: Lär dig hur du ansluter Adobe Experience Platform till Adobe Campaign Managed Cloud Services med Experience Platform användargränssnitt.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---

# Skapa en källanslutning till Adobe Campaign Managed Cloud Services med Experience Platform UI

I den här självstudiekursen beskrivs hur du skapar en källanslutning för att överföra dina Adobe Campaign Managed Cloud Services-data till Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Anslut Adobe Campaign Managed Cloud Services till Experience Platform

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka källor som visas.

Under kategorin **[!UICONTROL Adobe applications]** väljer du **[!UICONTROL Adobe Campaign Managed Cloud Services]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen som visar Adobe Campaign Managed Cloud Services-kortet.](../../../../images/tutorials/create/campaign/catalog.png)

### Markera data {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign-miljöinstans"
>abstract="Namnet på den Adobe Campaign-miljö som du vill använda."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Målmappning"
>abstract="Målmappningar är tekniska objekt som används av Campaign för att leverera meddelanden och innehåller alla tekniska inställningar som krävs för att skicka leveranser (adresser, telefonnummer, anmälningsindikatorer, ytterligare identifierare..)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Schemanamn"
>abstract="Namnet på den entitet som definieras i Adobe Campaign-databasen."
>text="Learn more in documentation"

Steget [!UICONTROL Select data] visas med ett gränssnitt för att konfigurera [!UICONTROL Adobe Campaign instance], [!UICONTROL Target mapping] och [!UICONTROL Schema name].

| Egenskap | Beskrivning |
| --- | --- |
| Adobe Campaign, instans | Namnet på den Adobe Campaign-miljöinstans som du använder. |
| Målmappning | De tekniska objekt som används av Campaign för att leverera meddelanden och innehåller alla tekniska inställningar som krävs för att skicka leveranser. |
| Schemanamn | Namnet på den schemaentitet som du ska skicka till Experience Platform. Exempel: Leveranslogg och spårningslogg. |

![Ett gränssnitt där du kan konfigurera din Adobe Campaign-instans, målmappning och schemanamn.](../../../../images/tutorials/create/campaign/select-data.png)

När du har angett värden för Campaign-instansen, målmappningen och schemanamnet uppdateras skärmen så att den visar en förhandsgranskning av ditt schema samt en exempeldatauppsättning. När du är klar väljer du **[!UICONTROL Next]**.

![En förhandsgranskning av schemahierarkin samt ett exempel på datauppsättningen](../../../../images/tutorials/create/campaign/preview.png)

### Använd en befintlig datamängd

På sidan [!UICONTROL Dataflow detail] kan du välja om du vill använda en befintlig datauppsättning eller konfigurera en ny datauppsättning för dataflödet.

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Du kan antingen hämta en befintlig datauppsättning med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga datauppsättningar i listrutan.

Ange ett namn för dataflödet och en valfri beskrivning när du har valt en datauppsättning.

![Ett gränssnitt som visar det befintliga datauppsättningsalternativet.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Använd en ny datauppsättning

Om du vill använda en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger sedan ett namn på utdatauppsättningen och en valfri beskrivning. Välj sedan ett schema att mappa till med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga scheman i listrutan. När du är klar väljer du **[!UICONTROL Next]**.

![Ett gränssnitt som visar det nya datauppsättningsalternativet.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Aktivera aviseringar

Du kan aktivera varningar för att få meddelanden om status för ditt dataflöde. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på källvarningar med användargränssnittet](../../alerts.md).

Välj **[!UICONTROL Next]** när du är klar med informationen om dataflödet.

![Ett urval av olika varningstyper som du kan aktivera för ditt dataflöde.](../../../../images/tutorials/create/campaign/alerts.png)

### Mappa datafält till ett XDM-schema

Steg [!UICONTROL Mapping] visas, och du får ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Experience Platform ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>När du mappar dina källfält till mål-XDM-fält måste du se till att du mappar det avsedda primära identitetsfältet till rätt mål-XDM-fält.
>
>För varje målgrupp kan du lägga till upp till 20 fält för att mappa till Adobe Campaign. Du kan ändra den här gränsen genom att uppdatera värdet för alternativet `NmsCdp_Aep_Sources_Max_Columns` i mappen Administration > Plattform > Alternativ i Campaign Explorer.

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Ett mappningsträd med fyra källdatafält mappade till sina motsvarande XDM-schemafält.](../../../../images/tutorials/create/campaign/mapping.png)

### Granska ditt dataflöde

Steg **[!UICONTROL Review]** visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![En granskningssida som visar anslutnings- och datauppsättningsinformation.](../../../../images/tutorials/create/campaign/review.png)

### Övervaka datauppsättningsaktiviteten

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om inkapslade frekvenser samt lyckade och misslyckade batchar.

Om du vill börja visa datauppsättningsaktiviteten väljer du **[!UICONTROL Dataflows]** i källkatalogen.

![Källkatalogsidan med dataflödets rubrikflik markerad.](../../../../images/tutorials/create/campaign/dataflows.png)

Välj sedan måldatauppsättningen i listan med dataflöden som visas.

![En lista över befintliga dataflöden med måldatauppsättningen Adobe Campaign Delivery Logs vald.](../../../../images/tutorials/create/campaign/target-dataset.png)

Sidan för datauppsättningsaktivitet visas. Härifrån kan du se information om dataflödets prestanda, bland annat hur snabbt data har importerats, slutförda batchar och misslyckade batchar.

På den här sidan finns också ett gränssnitt där du kan uppdatera metadatabeskrivningen för dataflödet, aktivera partiell import- och feldiagnostik samt lägga till nya data i datauppsättningen.

![Ett gränssnitt med diagram som representerar inmatningsfrekvensen för en markerad datauppsättning.](../../../../images/tutorials/create/campaign/dataset-activity.png)


>[!IMPORTANT]
>
>Du kan inte fylla i gamla händelseloggar baklänges med Adobe Campaign Managed Cloud Services-källan. Om bakåtfyllnad krävs använder du ett anpassat arbetsflöde eller en anpassad implementering för att exportera data till Amazon S3 eller Azure Blob, eller från Amazon S3 eller Azure Blob till en Adobe Experience Platform-datamängd.


## Nästa steg

I den här självstudiekursen har du skapat ett dataflöde som kan hämta leveransloggar för Campaign v8 och data för spårningsloggar till Experience Platform. Inkommande data kan nu användas av Experience Platform-tjänster längre fram i kedjan som [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

* [[!DNL Real-Time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)
