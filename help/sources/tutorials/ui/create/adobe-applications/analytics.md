---
keywords: Experience Platform;hem;populära ämnen;Analyskällekontakt;Analyskontakt;Analyskälla;Analytics
solution: Experience Platform
title: Skapa en Adobe Analytics Source Connection i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra konsumentdata till Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: e28158bbd4e89e5fcf19f4dc89f266d737b34e65
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Skapa en Adobe Analytics-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att hämta [!DNL Analytics] Report Suite-data till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [Kundprofil](../../../../../profile/home.md) i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Viktiga termer

Det är viktigt att förstå följande nyckeltermer som används i hela det här dokumentet:

* **Standardattribut**: Standardattribut är alla attribut som är fördefinierade av Adobe. De innehåller samma innebörd för alla kunder och är tillgängliga i källdata för [!DNL Analytics] och schemafältgrupper för [!DNL Analytics].
* **Anpassat attribut**: Anpassade attribut är alla attribut i den anpassade variabelhierarkin i  [!DNL Analytics]. Anpassade attribut används i en Adobe Analytics-implementering för att samla in specifik information i en Report Suite, och de kan skilja sig åt när det gäller användningen från Report Suite till Report Suite. Anpassade attribut är eVars, props och lists. Mer information om eVars finns i följande [[!DNL Analytics] dokumentation om konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en).
* **Alla attribut i anpassade fältgrupper**: Attribut som härstammar från fältgrupper som skapats av kunder är alla användardefinierade och betraktas varken som standardattribut eller anpassade attribut.
* **Eget namn**: Eget namn är etiketter som tillhandahålls av människor för anpassade variabler i en  [!DNL Analytics] implementering. Mer information om egna namn finns i följande [[!DNL Analytics] dokumentation om konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en).

## Skapa en källanslutning med Adobe Analytics

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka källor som visas.

Under kategorin **[!UICONTROL Adobe applications]** väljer du **[!UICONTROL Adobe Analytics]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/analytics/catalog.png)

### Markera data

**[!UICONTROL Analytics source add data]**-steget visas. Välj **[!UICONTROL Report Suite]** om du vill börja skapa en källanslutning för analysrapportsvitdata och välj sedan den rapportsvit som du vill importera. Rapportsviter som inte kan markeras har redan importerats, antingen i den här sandlådan eller i en annan sandlåda. Välj **[!UICONTROL Next]** för att fortsätta.

>[!NOTE]
>
>Flera ingående anslutningar kan göras för att ta in flera rapportsviter, men endast en Report Suite kan användas med kunddataplattformen i realtid.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Mappning

>[!IMPORTANT]
>
>Data Prep-stödfunktionen för källan [!DNL Analytics] finns i betaversionen.

Sidan [!UICONTROL Mapping] innehåller ett gränssnitt för att mappa källfält till lämpliga målschemafält. Härifrån kan du mappa anpassade variabler till nya schemafältgrupper och använda beräkningar som stöds av Data Prep. Välj ett målschema för att starta mappningsprocessen.

>[!TIP]
>
>Endast scheman som har mallfältsgruppen [!DNL Analytics] visas på schemamarkeringsmenyn. Andra scheman utelämnas. Om det inte finns några lämpliga scheman tillgängliga för dina Report Suite-data måste du skapa ett nytt schema. Detaljerade steg för hur du skapar scheman finns i guiden [skapa och redigera scheman i användargränssnittet](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

Avsnittet [!UICONTROL Map standard fields] visar paneler för [!UICONTROL Standard mappings applied], [!UICONTROL Non matching standard mappings] och [!UICONTROL Custom mappings]. Se följande tabell för specifik information om varje kategori:

| Mappa standardfält | Beskrivning |
| --- | --- |
| [!UICONTROL Standard mappings applied] | På panelen [!UICONTROL Standard mappings applied] visas det totala antalet mappade attribut. Standardmappningar refererar till mappningsuppsättningar mellan alla attribut i källan [!DNL Analytics]-data och motsvarande attribut i fältgruppen [!DNL Analytics]. Dessa är förmappade och kan inte redigeras. |
| [!UICONTROL Non matching standard mappings] | Panelen [!UICONTROL Non matching standard mappings] refererar till antalet mappade attribut som innehåller egna namnkonflikter. Dessa konflikter visas när du återanvänder ett schema som redan har en ifylld uppsättning fältbeskrivningar från en annan rapportserie. Du kan fortsätta med ditt [!DNL Analytics]-dataflöde även med egna namnkonflikter. |
| [!UICONTROL Custom mappings] | På panelen [!UICONTROL Custom mappings] visas antalet mappade anpassade attribut, inklusive eVars, props och listor. Anpassade mappningar refererar till mappningsuppsättningar mellan anpassade attribut i källan [!DNL Analytics]-data och attribut i anpassade fältgrupper som ingår i det valda schemat. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Om du vill förhandsgranska schemafältgruppen [!DNL Analytics] ExperienceEvent-mallen väljer du **[!UICONTROL View]** på panelen [!UICONTROL Standard mappings applied].

![visa](../../../../images/tutorials/create/analytics/view.png)

Sidan [!UICONTROL Adobe Analytics ExperienceEvent Template Schema Field Group] innehåller ett gränssnitt som du kan använda för att inspektera schemats struktur. När du är klar väljer du **[!UICONTROL Close]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Plattformen identifierar automatiskt dina mappningsuppsättningar för eventuella egna namnkonflikter. Om det inte finns några konflikter med mappningsuppsättningarna väljer du **[!UICONTROL Next]** för att fortsätta.

![mappning](../../../../images/tutorials/create/analytics/mapping.png)

Om det finns egna namnkonflikter mellan din käll-Report Suite och ditt valda schema kan du fortfarande fortsätta med ditt [!DNL Analytics]-dataflöde och bekräfta att fältbeskrivningarna inte kommer att ändras. Du kan också välja att skapa ett nytt schema med en tom uppsättning beskrivningar.

Välj **[!UICONTROL Next]** för att fortsätta.

![försiktighet](../../../../images/tutorials/create/analytics/caution.png)

#### Anpassade mappningar

Om du vill använda dataprep-funktioner och lägga till ny mappning eller beräknade fält för anpassade attribut väljer du **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Välj sedan **[!UICONTROL Add new mapping]**.

Beroende på dina behov kan du välja **[!UICONTROL Add new mapping]** eller **[!UICONTROL Add calculated field]** bland de alternativ som visas.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

En tom mappningsuppsättning visas. Välj mappningsikonen för att lägga till ett källfält.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Du kan använda gränssnittet för att navigera i källschemastrukturen och identifiera det nya källfältet som du vill använda. När du har valt det källfält som du vill mappa väljer du **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Välj sedan mappningsikonen under [!UICONTROL Target Field] för att mappa det valda källfältet till rätt målfält.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

På samma sätt som källschemat kan du använda gränssnittet för att navigera i målschemastrukturen och välja det målfält som du vill mappa till. När du har valt rätt målfält väljer du **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

När den anpassade mappningen är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

I följande dokumentation finns mer information om dataprep, beräkningsfält och mappningsfunktioner:

* [Översikt över datapreflight](../../../../../data-prep/home.md)
* [Funktioner för datapersonmappning](../../../../../data-prep/functions.md)
* [Lägg till beräknade fält](../../../../../data-prep/calculated-fields.md)

### Ange information om dataflöde

Steget **[!UICONTROL Dataflow detail]** visas där du måste ange ett namn och en valfri beskrivning av dataflödet. Välj **[!UICONTROL Next]** när du är klar.

![dataflöde-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Granska

[!UICONTROL Review]-steget visas så att du kan granska det nya Analytics-dataflödet innan det skapas. Detaljerna om anslutningen är grupperade efter kategorier, inklusive:

* [!UICONTROL Connection]: Visar anslutningens källplattform.
* [!UICONTROL Data type]: Visar den markerade rapportsviten och dess motsvarande Report Suite-ID.

![recension](../../../../images/tutorials/create/analytics/review.png)

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det. På skärmen [!UICONTROL Catalog] väljer du **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till ditt Analytics-konto.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Skärmen **Dataflöden** visas. På den här sidan finns ett par datauppsättningsflöden, inklusive information om namn, källdata, skapandetid och status.

Kopplingen instansierar två datauppsättningsflöden. Det ena flödet representerar data för bakåtfyllnad och det andra för livedata. Backfill-data är inte konfigurerade för profil, men skickas till datasjön för analytiska och datavetenskapliga användningsfall.

Mer information om förifyllning, livedata och deras respektive latenser finns i [Analytics Data Connector overview](../../../../connectors/adobe-applications/analytics.md).

Välj det datauppsättningsflöde du vill visa i listan.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Sidan **[!UICONTROL Dataset activity]** visas. På den här sidan visas hur många meddelanden som används i form av ett diagram. Välj **[!UICONTROL Data governance]** i den övre rubriken för att komma åt etikettfälten.

![datauppsättningsaktivitet](../../../../images/tutorials/create/analytics/dataset-activity.png)

Du kan visa ett datauppsättningsflödes ärvda etiketter från skärmen [!UICONTROL Data governance]. Mer information om hur du etiketterar data som kommer från Analytics finns i [etikettguiden för dataanvändning](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Om du vill ta bort ett dataflöde går du till sidan [!UICONTROL Dataflows] och markerar ellipserna (`...`) bredvid dataflödets namn och väljer sedan [!UICONTROL Delete].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Nästa steg och ytterligare resurser

När anslutningen har skapats skapas dataflödet automatiskt för att innehålla inkommande data och fylla i en datauppsättning med det valda schemat. Dessutom sker datainfyllning och inmatning av historiska data i upp till 13 månader. När det inledande intaget är klart ska [!DNL Analytics]-data användas av plattformstjänster längre fram i kedjan, till exempel [!DNL Real-time Customer Profile] och segmenteringstjänsten. Mer information finns i följande dokument:

* [[!DNL Real-time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] översikt](../../../../../query-service/home.md)

Följande video är tänkt att ge stöd för din förståelse av hur data importeras med Adobe Analytics Source Connector:

>[!WARNING]
>
> Användargränssnittet [!DNL Platform] som visas i följande video är inaktuellt. Läs dokumentationen ovan för de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
