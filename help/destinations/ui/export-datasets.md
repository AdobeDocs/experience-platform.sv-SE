---
title: (Beta) Exportera datauppsättningar till molnlagringsmål
type: Tutorial
description: Lär dig hur du exporterar datauppsättningar från Adobe Experience Platform till den molnlagringsplats du föredrar.
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# (Beta) Exportera datauppsättningar till molnlagringsmål

>[!IMPORTANT]
>
>* Funktionen för att exportera datauppsättningar finns för närvarande i Beta och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.
>* Den här betafunktionen stöder export av första generationens data, enligt definitionen i Real-time Customer Data Platform [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Den här funktionaliteten är tillgänglig för kunder som har köpt Real-Time CDP Prime och Ultimate. Kontakta din Adobe-representant om du vill ha mer information.


I den här artikeln förklaras vilket arbetsflöde som krävs för att exportera [datauppsättningar](/help/catalog/datasets/overview.md) från Adobe Experience Platform till den molnlagringsplats du föredrar, till exempel [!DNL Amazon S3], SFTP-platser, eller [!DNL Google Cloud Storage].

## När ska segment aktiveras eller datauppsättningar exporteras {#when-to-activate-segments-or-activate-datasets}

Vissa filbaserade mål i Experience Platform-katalogen stöder både segmentaktivering och datauppsättningsexport.

* Överväg att aktivera segment när ni vill att era data ska struktureras i profiler grupperade efter målgruppsintressen eller kvalifikationer.
* Du kan också överväga att exportera datauppsättningar när du vill exportera rådatauppsättningar, som inte grupperas eller struktureras efter målgruppsintressen eller kvalifikationer. Du kan använda dessa data för rapportering, datavetenskapliga arbetsflöden, för att uppfylla efterlevnadskrav och många andra användningsfall.

Det här dokumentet innehåller all information som behövs för att exportera datauppsättningar. Om du vill aktivera segment för molnlagring eller e-postmarknadsföring läser du [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md).

## Förutsättningar {#prerequisites}

Om du vill exportera datauppsättningar till molnlagringsmål måste du ha lyckats [ansluten till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de mål som stöds och konfigurera det mål som du vill använda.

### Nödvändiga behörigheter {#permissions}

Om du vill exportera datauppsättningar behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Bläddra i målkatalogen för att kontrollera att du har de behörigheter som krävs för att exportera datauppsättningar och att målet har stöd för att exportera datauppsättningar. Om ett mål har en **[!UICONTROL Activate]** eller en **[!UICONTROL Export datasets]** har du rätt behörighet.

## Välj mål {#select-destination}

Följ instruktionerna för att välja ett mål där du kan exportera datauppsättningar:

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Fliken Målkatalog med katalogkontrollen markerad.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Välj **[!UICONTROL Activate]** eller **[!UICONTROL Export datasets]** på kortet som motsvarar målet som du vill exportera datauppsättningar till.

   ![Fliken Målkatalog med aktiveringskontrollen markerad.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Välj **[!UICONTROL Data type Datasets]** och välj den målanslutning som du vill exportera datauppsättningar till och välj sedan **[!UICONTROL Next]**.

>[!TIP]
> 
>Om du vill konfigurera ett nytt mål för att exportera datauppsättningar väljer du **[!UICONTROL Configure new destination]** för att aktivera [Anslut till mål](/help/destinations/ui/connect-destination.md) arbetsflöde.

![Arbetsflöde för målaktivering med datauppsättningskontroll markerat.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. The **[!UICONTROL Select datasets]** visas. Gå till nästa avsnitt för att [välj dina datauppsättningar](#select-datasets) för export.

## Välj datauppsättningar {#select-datasets}

Använd kryssrutorna till vänster om datauppsättningsnamnen för att välja de datauppsättningar som du vill exportera till målet och markera sedan **[!UICONTROL Next]**.

![Arbetsflöde för dataexport med steget Välj datauppsättningar där du kan välja vilka datauppsättningar som ska exporteras.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Schemalägg datauppsättningsexport {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Filexportalternativ för datauppsättningar"
>abstract="Välj **Exportera inkrementella filer** om du bara vill exportera data som har lagts till i datauppsättningen sedan den senaste exporten. <br> Den första stegvisa filexporten innehåller alla data i datauppsättningen, vilket fungerar som en förifyllning. Framtida inkrementella filer innehåller endast de data som har lagts till i datauppsättningen sedan den första exporten."

I **[!UICONTROL Scheduling]** kan du ange ett startdatum och en exportgräns för datauppsättningsexporter.

The **[!UICONTROL Export incremental files]** alternativet väljs automatiskt. Detta utlöser en export där den första filen är en fullständig ögonblicksbild av datauppsättningen och efterföljande filer är inkrementella tillägg till datauppsättningen sedan den föregående exporten.

>[!IMPORTANT]
>
>Den första exporterade stegvisa filen innehåller alla befintliga data i datauppsättningen, och fungerar som en bakgrundsfyllning.

![Arbetsflöde för dataexport med schemaläggningssteget.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Använd **[!UICONTROL Frequency]** för att välja exportfrekvens:

   * **[!UICONTROL Daily]**: Schemalägg stegvis filexport en gång om dagen, varje dag, vid den tidpunkt du anger.
   * **[!UICONTROL Hourly]**: Schemalägg stegvis filexport var 3, 6, 8 eller 12:e timme.

2. Använd **[!UICONTROL Time]** väljaren för att välja tid på dagen, i [!DNL UTC] format, när exporten ska ske.

3. Använd **[!UICONTROL Date]** för att välja intervallet när exporten ska ske. Observera att det inte går att ange ett slutdatum för exporten i betaversionen av funktionen. Mer information finns i [kända begränsningar](#known-limitations) -avsnitt.

4. Välj **[!UICONTROL Next]** för att spara schemat och fortsätta till **[!UICONTROL Review]** steg.

>[!NOTE]
> 
>För datauppsättningsexporter har filnamnen en förinställning, standardformat, som inte kan ändras. Se avsnittet [Verifiera datauppsättningsexport](#verify) för mer information och exempel på exporterade filer.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja exportera datauppsättningar till målet.

![Arbetsflöde för dataexport med granskningssteget.](/help/destinations/assets/ui/export-datasets/review.png)

## Verifiera datauppsättningsexport {#verify}

När du exporterar datauppsättningar skapas en `.json` eller `.parquet` filen på lagringsplatsen som du angav. Förvänta dig att en ny fil ska placeras på din lagringsplats enligt det exportschema som du angav.

Experience Platform skapar en mappstruktur på den lagringsplats du angav, där den sparar de exporterade datauppsättningsfilerna. En ny mapp skapas för varje exporttid enligt mönstret nedan:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Standardfilnamnet genereras slumpmässigt och säkerställer att de exporterade filnamnen är unika.

### Exempeldatauppsättningsfiler {#sample-files}

De här filerna finns i din lagringsplats, vilket är en bekräftelse på att exporten lyckades. Om du vill veta hur de exporterade filerna är strukturerade kan du hämta ett exempel [.parquet-fil](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) eller [.json-fil](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## Ta bort datauppsättning från mål {#remove-dataset}

Så här tar du bort en datauppsättning från ett befintligt dataflöde:

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Browse]** i det övre sidhuvudet för att visa befintliga måldataflöden.

   ![Målvyn med en målanslutning visas och resten suddigt.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Markera filterikonen ![Filterikon](../assets/ui/edit-activation/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

1. Från **[!UICONTROL Activation data]** markerar du datauppsättningskontrollen för att visa alla datauppsättningar som är mappade till det här exportdataflödet.

   ![Navigeringsalternativet för tillgängliga datamängder är markerat i kolumnen Aktiveringsdata.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. The **[!UICONTROL Activation data]** målsidan visas. Välj **[!UICONTROL Remove dataset]** i den högra listen för att aktivera bekräftelsedialogrutan för borttagning av datauppsättning.

   ![Dialogrutan Ta bort datauppsättning med kontrollen Ta bort datauppsättning i den högra listen.](../assets/ui/export-datasets/remove-dataset-control.png)

1. I bekräftelsedialogrutan väljer du **[!UICONTROL Remove]** för att omedelbart ta bort datauppsättningen från exporter till destinationen.

   ![Dialogruta med alternativet Bekräfta borttagning av datauppsättning från dataflödet.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Kända begränsningar {#known-limitations}

Tänk på följande begränsningar för betaversionen av datauppsättningsexporter:

* Det finns för närvarande en enda behörighet (**[!UICONTROL Manage and Activate Dataset Destinations]**) som inkluderar hantering och aktivering av behörigheter för datauppsättningsmål. Dessa kontroller delas upp i framtiden i mer detaljerade behörigheter. Granska [nödvändiga behörigheter](#permissions) om du vill se en fullständig lista över behörigheter som du behöver för att exportera datauppsättningar.
* För närvarande kan du bara exportera inkrementella filer och ett slutdatum kan inte väljas för datauppsättningsexporter.
* De exporterade filnamnen kan för närvarande inte anpassas.
* Gränssnittet blockerar för närvarande inte dig från att ta bort en datauppsättning som exporteras till ett mål. Ta inte bort datauppsättningar som exporteras till destinationer. [Ta bort datauppsättningen](#remove-dataset) från ett måldataflöde innan det tas bort.
* Övervakningsmåtten för datauppsättningsexport är för närvarande blandade med siffrorna för profilexporter, så de återspeglar inte de verkliga exportnumren.
