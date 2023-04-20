---
keywords: Experience Platform;populära ämnen;Analyskällkoppling;Analyskontakt;Analyskälla;analys;filtrering;filtrering för profil;kundprofil i realtid;filter;filterprofildata;radfiltrering;filtrering på kolumnnivå
title: Skapa en Adobe Analytics Source Connection i användargränssnittet
description: Lär dig hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra konsumentdata till Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 23a99a46cfd6e42dd0f4815bb972dbe46104b60f
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 0%

---

# Skapa en Adobe Analytics-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra data från Adobe Analytics rapportsvit till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [Kundprofil i realtid](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Viktiga termer

Det är viktigt att förstå följande nyckeltermer som används i hela det här dokumentet:

* **Standardattribut**: Standardattribut är alla attribut som är fördefinierade av Adobe. De har samma betydelse för alla kunder och finns i [!DNL Analytics] källdata och [!DNL Analytics] schemafältgrupper.
* **Eget attribut**: Anpassade attribut är alla attribut i den anpassade variabelhierarkin i [!DNL Analytics]. Anpassade attribut används i en Adobe Analytics-implementering för att samla in specifik information i en rapportserie, och de kan skilja sig åt när det gäller användningen från rapportsviten till rapportsviten. Anpassade attribut är eVars, props och lists. Se följande [[!DNL Analytics] dokumentation om konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) för mer information om eVars.
* **Alla attribut i anpassade fältgrupper**: Attribut som härstammar från fältgrupper som skapats av kunder är alla användardefinierade och betraktas varken som standardattribut eller anpassade attribut.
* **Eget namn**: Vänliga namn är etiketter som tillhandahålls av människor för anpassade variabler i en [!DNL Analytics] implementering. Se följande [[!DNL Analytics] dokumentation om konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) om du vill ha mer information om egna namn.

## Skapa en källanslutning med Adobe Analytics

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka källor som visas.

Under **[!UICONTROL Adobe applications]** kategori, välj **[!UICONTROL Adobe Analytics]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/analytics/catalog.png)

### Markera data

>[!IMPORTANT]
>
>Rapportsviterna som visas på skärmen kan komma från olika regioner. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform tvärregioner. Se till att ditt företag tillåter detta.

The **[!UICONTROL Analytics source add data]** innehåller en lista med [!DNL Analytics] skapa en källanslutning med rapportsvitdata.

En rapportsvit är en databehållare som utgör grunden för [!DNL Analytics] rapportering. En organisation kan ha många rapportsviter, som alla innehåller olika datauppsättningar.

Du kan importera rapportsviter från alla regioner (USA, Storbritannien och Singapore) så länge de mappas till samma organisation som den Experience Platform sandlådeinstans i vilken källanslutningen skapas. En rapportsvit kan bara importeras med ett enda aktivt dataflöde. En rapportsvit som inte kan markeras har redan importerats, antingen i sandlådan som du använder eller i en annan sandlåda.

Flera ingående anslutningar kan göras för att överföra flera rapportsviter till samma sandlåda. Om rapportsviterna har olika scheman för variabler (t.ex. eVars eller events) bör de mappas till specifika fält i de anpassade fältgrupperna och datakonflikter undviks med [Dataprep](../../../../../data-prep/ui/mapping.md). Rapportsviter kan bara läggas till i en enda sandlåda.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Data från flera rapportsviter kan bara aktiveras för kundprofilen i realtid om det inte finns några datakonflikter, till exempel två anpassade egenskaper (eVars, lists och props) som har olika innebörd.

Skapa en [!DNL Analytics] källanslutning, välj en rapportserie och välj sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Rapportsviter för analyser kan konfigureras för en sandlåda i taget. Om du vill importera samma Report Suite till en annan sandlåda måste datauppsättningsflödet tas bort och instansieras igen via konfiguration för en annan sandlåda.—>

### Mappning

>[!IMPORTANT]
>
>Omformningar av dataförberedelser kan öka fördröjningen i det övergripande dataflödet. Den extra fördröjning som läggs till varierar beroende på komplexiteten i omvandlingslogiken.

Innan du kan mappa [!DNL Analytics] data för XDM-målschemat måste du först välja om du använder ett standardschema eller ett anpassat schema.

Ett standardschema skapar ett nytt schema åt dig och innehåller [!DNL Adobe Analytics ExperienceEvent Template] fältgrupp. Om du vill använda ett standardschema väljer du **[!UICONTROL Default schema]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Med ett anpassat schema kan du välja valfritt tillgängligt schema för [!DNL Analytics] data, förutsatt att schemat har [!DNL Adobe Analytics ExperienceEvent Template] fältgrupp. Om du vill använda ett anpassat schema väljer du **[!UICONTROL Custom schema]**.

![anpassat schema](../../../../images/tutorials/create/analytics/custom-schema.png)

The [!UICONTROL Mapping] På sidan finns ett gränssnitt för att mappa källfält till rätt målschemafält. Härifrån kan du mappa anpassade variabler till nya schemafältgrupper och använda beräkningar som stöds av Data Prep. Välj ett målschema för att starta mappningsprocessen.

>[!TIP]
>
>Endast scheman som har [!DNL Adobe Analytics ExperienceEvent Template] fältgruppen visas på schemamarkeringsmenyn. Andra scheman utelämnas. Om det inte finns några lämpliga scheman tillgängliga för dina Report Suite-data måste du skapa ett nytt schema. Detaljerade anvisningar om hur du skapar scheman finns i handboken på [skapa och redigera scheman i användargränssnittet](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

The [!UICONTROL Map standard fields] -avsnittet visar paneler för [!UICONTROL Standard mappings applied], [!UICONTROL Non matching standard mappings] och [!UICONTROL Custom mappings]. Se följande tabell för specifik information om varje kategori:

| Mappa standardfält | Beskrivning |
| --- | --- |
| [!UICONTROL Standard mappings applied] | The [!UICONTROL Standard mappings applied] visas det totala antalet mappade attribut. Standardmappningar refererar till mappningsuppsättningar mellan alla attribut i källan [!DNL Analytics] data och motsvarande attribut i [!DNL Analytics] fältgrupp. Dessa är förmappade och kan inte redigeras. |
| [!UICONTROL Non matching standard mappings] | The [!UICONTROL Non matching standard mappings] panel avser antalet mappade attribut som innehåller egna namnkonflikter. Dessa konflikter visas när du återanvänder ett schema som redan har en ifylld uppsättning fältbeskrivningar från en annan rapportserie. Du kan fortsätta med [!DNL Analytics] dataflöde även med egna namnkonflikter. |
| [!UICONTROL Custom mappings] | The [!UICONTROL Custom mappings] På panelen visas antalet mappade anpassade attribut, inklusive eVars, props och listor. Anpassade mappningar refererar till mappningsuppsättningar mellan anpassade attribut i källan [!DNL Analytics] data och attribut i anpassade fältgrupper som ingår i det valda schemat. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Förhandsgranska [!DNL Analytics] ExperienceEvent-mallens schemafältgrupp, välj **[!UICONTROL View]** i [!UICONTROL Standard mappings applied] -panelen.

![visa](../../../../images/tutorials/create/analytics/view.png)

The [!UICONTROL Adobe Analytics ExperienceEvent Template Schema Field Group] på sidan finns ett gränssnitt som du kan använda för att inspektera strukturen i ditt schema. När du är klar väljer du **[!UICONTROL Close]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Plattformen identifierar automatiskt dina mappningsuppsättningar för eventuella egna namnkonflikter. Om det inte finns några konflikter med dina mappningsuppsättningar väljer du **[!UICONTROL Next]** för att fortsätta.

![mappning](../../../../images/tutorials/create/analytics/mapping.png)

Om det finns egna namnkonflikter mellan din käll-Report Suite och ditt valda schema kan du fortsätta med ditt [!DNL Analytics] dataflöde, bekräfta att fältbeskrivningarna inte kommer att ändras. Du kan också välja att skapa ett nytt schema med en tom uppsättning beskrivningar.

Välj **[!UICONTROL Next]** för att fortsätta.

![försiktighet](../../../../images/tutorials/create/analytics/caution.png)

#### Anpassade mappningar

Om du vill använda förinställningsfunktioner för data och lägga till ny mappning eller beräknade fält för anpassade attribut väljer du **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Nästa, välj **[!UICONTROL Add new mapping]**.

Beroende på dina behov kan du välja **[!UICONTROL Add new mapping]** eller **[!UICONTROL Add calculated field]** från alternativen som visas.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

En tom mappningsuppsättning visas. Välj mappningsikonen för att lägga till ett källfält.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Du kan använda gränssnittet för att navigera i källschemastrukturen och identifiera det nya källfältet som du vill använda. När du har valt det källfält som du vill mappa väljer du **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Välj sedan mappningsikonen under [!UICONTROL Target Field] för att mappa det valda källfältet till rätt målfält.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

På samma sätt som källschemat kan du använda gränssnittet för att navigera i målschemastrukturen och välja det målfält som du vill mappa till. När du har valt rätt målfält väljer du **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Välj **[!UICONTROL Next]** för att fortsätta.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

I följande dokumentation finns mer information om dataprep, beräkningsfält och mappningsfunktioner:

* [Översikt över datapreflight](../../../../../data-prep/home.md)
* [Funktioner för datapersonmappning](../../../../../data-prep/functions.md)
* [Lägg till beräknade fält](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Filtrera efter kundprofil i realtid {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Skapa filterregler"
>abstract="Definiera filtreringsregler på rad- och kolumnnivå när du skickar data till kundprofilen i realtid. Använd filtrering på radnivå för att tillämpa villkor och ange vilka data som ska **inkludera för profilinmatning**. Använd filtrering på kolumnnivå för att markera de datakolumner som du vill använda **exkludera för profilinmatning**. Filtreringsreglerna gäller inte för data som skickas till datasjön."

När du är klar med mappningarna för [!DNL Analytics] kan ni använda filtreringsregler och filtreringsvillkor för att selektivt inkludera eller exkludera data från konsumtion i realtidskundprofilen. Stöd för filtrering finns endast för [!DNL Analytics] data och data filtreras endast innan de anges [!DNL Profile.] Alla data hämtas in i sjön.

#### Filtrering på radnivå

>[!IMPORTANT]
>
>Använd filtrering på radnivå för att tillämpa villkor och ange vilka data som ska **inkludera för profilinmatning**. Använd filtrering på kolumnnivå för att markera de datakolumner som du vill använda **exkludera för profilinmatning**.

Du kan filtrera data för [!DNL Profile] intag på radnivå och kolumnnivå. Med filtrering på radnivå kan du definiera villkor som strängen innehåller, är lika med, börjar eller slutar med. Du kan också använda filtrering på radnivå för att koppla villkor med `AND` och `OR`och negera villkor med `NOT`.

Filtrera [!DNL Analytics] på radnivå, markera **[!UICONTROL Row filter]**.

![radfilter](../../../../images/tutorials/create/analytics/row-filter.png)

Använd den vänstra listen för att navigera i schemahierarkin och välj det schemaattribut du vill ha för att ytterligare detaljgranska ett visst schema.

![vänster-räl](../../../../images/tutorials/create/analytics/left-rail.png)

När du har identifierat attributet som du vill konfigurera markerar du och drar attributet från den vänstra listen till filtreringspanelen.

![filtreringspanel](../../../../images/tutorials/create/analytics/filtering-panel.png)

Om du vill konfigurera olika villkor väljer du **[!UICONTROL equals]** och välj sedan ett villkor i listrutan som visas.

Listan över konfigurerbara villkor omfattar:

* [!UICONTROL equals]
* [!UICONTROL does not equal]
* [!UICONTROL starts with]
* [!UICONTROL ends with]
* [!UICONTROL does not end with]
* [!UICONTROL contains]
* [!UICONTROL does not contain]
* [!UICONTROL exists]
* [!UICONTROL does not exist]

![villkor](../../../../images/tutorials/create/analytics/conditions.png)

Ange sedan de värden som du vill inkludera baserat på det attribut som du har valt. I exemplet nedan [!DNL Apple] och [!DNL Google] väljs för konsumtion som en del av **[!UICONTROL Manufacturer]** -attribut.

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Om du vill specificera filtervillkoren ytterligare lägger du till ett attribut från schemat och lägger sedan till värden baserade på det attributet. I exemplet nedan är **[!UICONTROL Model]** attribut läggs till och modeller som [!DNL iPhone 13] och [!DNL Google Pixel 6] filtreras för förtäring.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Om du vill lägga till en ny behållare markerar du ellipserna (`...`) längst upp till höger i filtreringsgränssnittet och välj sedan **[!UICONTROL Add container]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

När en ny behållare har lagts till väljer du **[!UICONTROL Include]** och sedan markera **[!UICONTROL Exclude]** i listrutan som visas.

![exclude](../../../../images/tutorials/create/analytics/exclude.png)

Slutför sedan samma process genom att dra schemaattribut och lägga till deras motsvarande värden som du vill utesluta från filtreringen. I exemplet nedan är [!DNL iPhone 12], [!DNL iPhone 12 mini]och [!DNL Google Pixel 5] filtreras alla från att exkluderas från **[!UICONTROL Model]** attribute, landscape is exclude from the **[!UICONTROL Screen orientation]** och modellnummer [!DNL A1633] är exkluderad från **[!UICONTROL Model number]**.

När du är klar väljer du **[!UICONTROL Next]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filtrering på kolumnnivå

Välj **[!UICONTROL Column filter]** från rubriken för att använda filtrering på kolumnnivå.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

Sidan uppdateras till ett interaktivt schematräd och visar dina schemaattribut på kolumnnivå. Här kan du välja de datakolumner som du vill utesluta från [!DNL Profile] intag. Du kan också expandera en kolumn och välja särskilda attribut för uteslutning.

Som standard är alla [!DNL Analytics] gå till [!DNL Profile] och den här processen gör det möjligt att undanta grenar av XDM-data från [!DNL Profile] intag.

När du är klar väljer du **[!UICONTROL Next]**.

![kolumner-markerade](../../../../images/tutorials/create/analytics/columns-selected.png)

### Ange information om dataflöde

The **[!UICONTROL Dataflow detail]** visas där du måste ange ett namn och en valfri beskrivning för dataflödet. Välj **[!UICONTROL Next]** när du är klar.

![dataflöde-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Granska

The [!UICONTROL Review] visas så att du kan granska det nya Analytics-dataflödet innan det skapas. Detaljerna om anslutningen är grupperade efter kategorier, inklusive:

* [!UICONTROL Connection]: Visar anslutningens källplattform.
* [!UICONTROL Data type]: Visar den markerade rapportsviten och dess motsvarande Report Suite-ID.

![recension](../../../../images/tutorials/create/analytics/review.png)

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det. Från [!UICONTROL Catalog] skärm, välja **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till ditt Analytics-konto.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

The **Dataflöden** visas. På den här sidan finns ett par datauppsättningsflöden, inklusive information om namn, källdata, skapandetid och status.

Kopplingen instansierar två datauppsättningsflöden. Det ena flödet representerar data för bakåtfyllnad och det andra för livedata. Backfill-data är inte konfigurerade för profil, men skickas till datasjön för analytiska och datavetenskapliga användningsfall.

Mer information om bakåtfyllnad, livedata och deras respektive latenser finns i [Översikt över Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Välj det datauppsättningsflöde du vill visa i listan.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

The **[!UICONTROL Dataset activity]** visas. På den här sidan visas hur många meddelanden som används i form av ett diagram. Välj **[!UICONTROL Data governance]** från den övre rubriken för att komma åt etikettfälten.

![datauppsättningsaktivitet](../../../../images/tutorials/create/analytics/dataset-activity.png)

Du kan visa ett datauppsättningsflödes ärvda etiketter från [!UICONTROL Data governance] skärm. Mer information om etikettering av data från Analytics finns på [etikettguide för dataanvändning](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Om du vill ta bort ett dataflöde går du till [!UICONTROL Dataflows] och sedan markera ellipserna (`...`) bredvid dataflödets namn och välj [!UICONTROL Delete].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Nästa steg och ytterligare resurser

När anslutningen har skapats skapas dataflödet automatiskt för att innehålla inkommande data och fylla i en datauppsättning med det valda schemat. Dessutom sker datainfyllning och inmatning av historiska data i upp till 13 månader. När det första intaget är klart, [!DNL Analytics] data och användas av plattformstjänster längre fram i kedjan, t.ex. [!DNL Real-Time Customer Profile] och segmenteringstjänst. Mer information finns i följande dokument:

* [[!DNL Real-Time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] översikt](../../../../../query-service/home.md)

Följande video är tänkt att ge stöd för din förståelse av hur data importeras med Adobe Analytics Source Connector:

>[!WARNING]
>
> The [!DNL Platform] Gränssnittet som visas i följande video är inaktuellt. Läs dokumentationen ovan för de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
