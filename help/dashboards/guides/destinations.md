---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilpanel;instrumentpanel
title: Guide för instrumentpanel för destinationer
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om organisationens aktiva destinationer.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 0%

---

# [!UICONTROL Destinations] kontrollpanel

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om din organisations aktiva mål, som den fångats in under en daglig ögonblicksbild. I den här handboken beskrivs hur du får åtkomst till och arbetar med kontrollpanelen för mål i användargränssnittet, och den innehåller mer information om mätvärdena som visas på kontrollpanelen.

En översikt över destinationer samt en katalog över alla tillgängliga destinationer i Experience Platform finns på [destinationsdokumentation](../../destinations/home.md).

## [!UICONTROL Destinations] instrumentpanelsdata {#destinations-dashboard-data}

På kontrollpanelen Destinationer visas en ögonblicksbild av de destinationer som din organisation har aktiverat i Experience Platform. Data i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för destinationer uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska [!UICONTROL Destinations] kontrollpanel {#explore}

Om du vill navigera till kontrollpanelen för mål i plattformsgränssnittet väljer du **[!UICONTROL Destinations]** i den vänstra listen väljer du **[!UICONTROL Overview]** för att visa kontrollpanelen.

Datum och tid för den senaste ögonblicksbilden visas högst upp i [!UICONTROL Overview] bredvid mållistrutan. Alla widgetdata är korrekta från och med det datumet och den tidpunkten. Tidsstämpeln för ögonblicksbilden anges i UTC. det ligger inte i den enskilda användarens eller organisationens tidszon.

>[!NOTE]
>
>Om din organisation är ny för Experience Platform och ännu inte har några aktiva destinationer visas kontrollpanelen Destinationer och [!UICONTROL Overview] -fliken visas inte. Välj i stället [!UICONTROL Destinations] från vänster navigering visas [!UICONTROL Catalog] -fliken. Läs mer om [!UICONTROL Catalog] -fliken, se [[!UICONTROL Destinations] arbetsytans guide](../../destinations/ui/destinations-workspace.md).

![Översikt över plattformsgränssnittets destinationer med den senaste ögonblicksbilden markerad.](../images/destinations/snapshot-timestamp.png)

### Ändra [!UICONTROL Destinations] kontrollpanel {#modify}

Välj **[!UICONTROL Modify dashboard]** om du vill ändra utseendet på kontrollpanelen för mål. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt få tillgång till widgetbiblioteket. Från widgetbiblioteket kan du utforska de tillgängliga widgetarna och skapa anpassade widgetar för din organisation.

Se [ändra kontrollpaneler](../customize/modify.md) och [widgetbibliotek - översikt](../customize/widget-library.md) dokumentation som lär dig mer.

### Lägg till widgetar {#add-widget}

Välj **[!UICONTROL Add widget]** för att navigera till widgetbiblioteket och se en lista över tillgängliga widgetar att lägga till på din instrumentpanel.

![Översikt över kontrollpanelen Destinationer med widgeten Lägg till markerad.](../images/destinations/destinations-overview-add-widget.png)

I widgetbiblioteket kan du bläddra bland alla standardwidgetar och anpassade målgruppswidgetar. Mer information om hur du lägger till widgetar finns i dokumentationen för widgetbiblioteket om hur du [lägga till en widget](../customize/widget-library.md#add-widgets).

## Standardwidgetar {#standard-widgets}

Adobe tillhandahåller flera standardwidgetar som du kan använda för att visualisera olika mätvärden som relaterar till dina destinationer och utvärdera hur fullständiga målgrupperna är för din dataanalys. Du kan också skapa anpassade widgetar som ska delas med din organisation med hjälp av [!UICONTROL Widget library]. Om du vill veta mer om hur du skapar anpassade widgetar börjar du med att läsa [Översikt över widgetbiblioteket](../customize/widget-library.md).

### Förutsättningar {#prerequisites}

Innan du fortsätter med beskrivningarna av standardwidgetar bör du kontrollera att du känner till definitionerna av följande nyckeltermer som används i hela dokumentationen:

* **Segmentdefinition:** En segmentdefinition är en **uppsättning regler** används för att beskriva en målgrupps viktigaste egenskaper eller beteenden. Dessa regler innehåller attribut och händelsedata som kvalificerar profilerna som en del av en målgrupp.
* **Målgrupp**: En uppsättning personer, konton, hushåll eller andra enheter som delar gemensamma egenskaper och beteenden.
* **Mappade/mappade**: Datamappning är processen att mappa källdatafält till relaterade målfält i ett mål.
* **Identitet**: En identitet är en identifierare som unikt representerar en enskild kund, till exempel ett cookie-ID, ett enhets-ID eller ett e-post-ID.
* **Aktivera**: Aktivera är den åtgärd som en användare vidtar för att mappa en målgrupp eller profiler till ett mål som Oracle Eloqua, Google eller Salesforce Marketing Cloud.

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated audiences]](#recently-activated-audiences)
* [[!UICONTROL Recently activated audiences by destination]](#recently-activated-audiences-by-destination)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Unmapped audiences by identity]](#unmapped-audiences-by-identity)
* [[!UICONTROL Mapped audiences by identity]](#mapped-audiences-by-identity)
* [[!UICONTROL Common audiences]](#common-audiences)
* [[!UICONTROL Mapped audiences]](#mapped-audiences)
* [[!UICONTROL Mapped audience health]](#mapped-audience-health)
* [[!UICONTROL Destinations count]](#destinations-count)
* [[!UICONTROL Destination status]](#destination-status)
* [[!UICONTROL Active destinations by destination platform]](#active-destinations-by-destination-platform)
* [[!UICONTROL Activated audiences across all destinations]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Activated audiences]](#activated-audiences)

### [!UICONTROL Most used destinations] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Mest använda destinationer"
>abstract="Den här widgeten visar organisationens mest aktiva mål utifrån antalet mappade målgrupper. Siffrorna är korrekta vid tidpunkten för den senaste ögonblicksbilden. Den här rankningen ger insikt i vilka destinationer som för närvarande används samtidigt som de som kan vara underutnyttjade markeras."

The **[!UICONTROL Most used destinations]** -widgeten visar organisationens främsta destinationer utifrån antalet mappade målgrupper, från och med den senaste ögonblicksbilden. Denna rankning ger insikt i vilka destinationer som används samtidigt som de som kan vara underutnyttjade också kan visas.

Om du till exempel konfigurerade ett mål i går men inte har mappat några målgrupper till det, kan du se att målet för närvarande är underutnyttjat.

Antalet mappade målgrupper som visas i [!UICONTROL Audience count] -kolumnen är exakt som den senaste ögonblicksbilden. När en ny målgrupp mappas till målet uppdateras inte antalet förrän nästa ögonblicksbild tas.

Välj namnet på ett mål i listan som visas på widgeten för att navigera till målinformationen för det aktuella målet. Du kan också välja **[!UICONTROL View All]** för att navigera till **[!UICONTROL Browse]** och sedan markera namnet på ett mål för att visa information om det.

![Fliken Översikt på kontrollpanelen Destinationer med widgeten Mest använda mål markerad.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Nyligen skapade mål"
>abstract="Den här widgeten visar en lista över de senast konfigurerade målplatserna i din organisation."

The **[!UICONTROL Recently created destinations]** kan du visa en lista över organisationens senast konfigurerade mål.

Det datum som visas motsvarar den senaste ögonblicksbilden. Om du skapar ett nytt mål kommer det alltså inte att visas i listan förrän nästa ögonblicksbild har tagits.

Om du väljer namnet på ett mål i den lista som visas på widgeten kommer du till målinformationen som länkad från **[!UICONTROL Browse]** -fliken. Du kan också välja **[!UICONTROL View All]** för att navigera till **[!UICONTROL Browse]** och sedan markera namnet på ett mål för att visa information om det.

Mer information om hur du konfigurerar särskilda typer av destinationer finns på [destinationsdokumentation](../../destinations/home.md).

![Fliken Översikt på kontrollpanelen Destinationer med widgeten Senast skapade mål markerad.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated audiences] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Nyligen aktiverade målgrupper"
>abstract="Den här widgeten innehåller en lista över de målgrupper som senast har mappats till ett mål. Den här listan innehåller en ögonblicksbild av de målgrupper och mål som används aktivt i systemet och kan hjälpa till att felsöka felaktiga mappningar."

The **[!UICONTROL Recently activated audiences]** widgeten innehåller en lista över de målgrupper som senast har mappats till ett mål. Den här listan innehåller en ögonblicksbild av de målgrupper och mål som används aktivt i systemet och kan hjälpa till att felsöka felaktiga mappningar.

The [!UICONTROL Updated] det datum som visas visar den senaste gången målgruppen aktiverades till målet och är exakt den senaste ögonblicksbilden. Det innebär att om du aktiverar en målgrupp till målet kommer det uppdaterade datumet inte att ändras förrän nästa ögonblicksbild har tagits.

Om du väljer namnet på en målgrupp i listan som visas på widgeten kommer du till målgruppsinformationen. Du kan också välja **[!UICONTROL View All]** för att navigera till [!UICONTROL Audiences] [!UICONTROL Browse] och sedan markera namnet på en målgrupp för att visa informationen.

Mer information om hur du arbetar med målgrupper i Experience Platform finns i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

![Fliken Översikt på kontrollpanelen Destinationer med widgeten Senast aktiverade målgrupper markerad.](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL Recently activated audiences by destination] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Nyligen aktiverade målgrupper efter mål"
>abstract="Den här widgeten visar de fem senast aktiverade målgrupperna i fallande ordning enligt det mål som valts i listrutan Översikt."

The **[!UICONTROL Recently activated audiences by destination]** widgeten visar de fem senast aktiverade målgrupperna i fallande ordning enligt det mål som valts i listrutan Översikt. Det liknar [!UICONTROL Recently activated audiences] widget, men data visas **endast** används för det valda målet.

Den här widgeten innehåller två mätvärden: målgruppsnamnet och det datum då målgrupperna senast aktiverades till målet. De data som visas är korrekta vid den senaste ögonblicksbilden.

Du kan visa information om en viss målgrupp genom att välja målgruppens namn i den lista som visas.

![De senast aktiverade målgrupperna efter målwidget.](../images/destinations/recently-activated-audiences-by-destination.png)

Se avsnittet Krav för [definitioner av termer som används](#prerequisites) i den här beskrivningen.

### [!UICONTROL Audience size trend] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Trend för målgruppsstorlek"
>abstract="Den här widgeten visar antalet profiler i målgruppen som skickas till målkontot dagligen. Den första listrutan justerar tidsperioden för målgruppstrenden. Den andra widgetens listruta väljer målgrupp för analys. Målet väljs i listrutan Översikt."

The **[!UICONTROL Audience size trend]** widgeten visar relationen mellan antalet profiler under en tidsperiod för en målgrupp som har mappats till det målkontot. Widgeten använder ett linjediagram för att illustrera antalet profiler i målgruppen som skickas till målkontot dagligen.

En tidsperiod för målgruppstrenden under de senaste 30 dagarna, 90 dagar eller 12 månaderna kan justeras med den första listrutan.

I den andra listrutan visas alla tillgängliga målgrupper som kan skickas till det målkonto som valts högst upp på kontrollpanelen.

![Widgeten för målgruppsstorlekstrend.](../images/destinations/audience-size-trend.png)

The **[!UICONTROL Audience size trend]** widgeten innehåller en [!UICONTROL Captions] i widgetens övre högra hörn. Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter. En maskininlärningsmodell genererar automatiskt bildtexter som beskriver viktiga trender och viktiga händelser genom att analysera diagram- och målgruppsdata.

![Dialogrutan med automatiska bildtexter för widgeten Storlekstrend för publik.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Unmapped audiences by identity] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Omappade målgrupper efter identitet"
>abstract="Den här widgeten visar de fem populäraste **omappad** målgrupper rangordnas efter fallande identitetsantal för ett visst mål och en viss identitet. De filter-ID:n som visas i widgetens listruta ändras beroende på vilket målkonto som är markerat högst upp på översiktssidan."

The **[!UICONTROL Unmapped audiences by identity]** widgeten listar de fem populäraste **omappad** målgrupper rangordnas efter fallande identitetsantal för ett visst mål och en viss identitet. Det markerar målgrupper som är mest fördelaktiga att mappa till det valda målkontot baserat på det valda ID:t.

Mål-ID-listrutan filtrerar de tillgängliga målgrupperna. Filtrerings-ID:n som visas i listrutan ändras beroende på vilket målkonto som är markerat högst upp på översiktssidan.

Kolumnen Identiteter räknar antalet käll-ID:n inom målgruppen som kan mappas till det ID som valts i listrutan för widget-ID.

![The Unmapped audiences by identity widget.](../images/destinations/unmapped-audiences-by-identity.png)

Se avsnittet Krav för [definitioner av termer som används](#prerequisites) i den här beskrivningen.

### [!UICONTROL Mapped audiences by identity] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Mappade målgrupper efter identitet"
>abstract="Den här widgeten innehåller de fem främsta listorna med **mappad** målgrupper. Listan ordnas från hög till låg enligt antalet käll-ID:n som finns inom målgrupperna. Det mål-ID som ska räknas väljs i listrutan under widgetens rubrik. Mål-ID:n som är tillgängliga i widgetens listruta beror på vilket mål som valts högst upp på översiktspanelen."

Den här widgeten innehåller de fem främsta listorna med **mappad** målgrupper. Listan ordnas från hög till låg enligt antalet käll-ID:n som finns inom målgrupperna. Det mål-ID som ska räknas väljs i listrutan under widgetens rubrik. Mål-ID:n som är tillgängliga i listrutan i widgeten ändras enligt det målkontofilter som valts högst upp på översiktspanelen.

![Mappade målgrupper efter identitetswidget.](../images/destinations/mapped-audiences-by-identity.png)

The **[!UICONTROL Mapped audiences by identity]** widgetens högdagrar snabbt sannolikheten för att lyckas rikta in profilmöjligheter för en kampanj inom det valda målet. En effektiv riktad kampanj beror inte på antalet profiler som skickas till målet, utan snarare på antalet käll-ID:n som troligen matchas med mål-ID:n för att ge användbara och användbara data.

### Gemensamma målgrupper {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Gemensamma målgrupper"
>abstract="Den här widgeten innehåller en lista över de fem populäraste målgrupperna som är aktiverade över det målkonto som valts längst upp på sidan och det mål som är markerat i widgetens listruta. Listan över målgrupper ordnas efter hur nyligen de har aktiverats. Den senast aktiverade publiken visas överst."

The **[!UICONTROL Common audiences]** widgeten innehåller en lista med de fem populäraste målgrupperna som är aktiverade över målkontot som är valt längst upp på sidan och det mål som är markerat i widgetens listruta. Listan över målgrupper ordnas efter hur nyligen de har aktiverats. Den senast aktiverade publiken visas överst.

The [!UICONTROL AUDIENCE SIZE] kolumn innehåller det totala antalet profiler för varje angiven målgrupp.

![The Common audiences widget.](../images/destinations/common-audiences.png)

### Mappade målgrupper {#mapped-audiences}

The [!UICONTROL Mapped audiences] visar det totala antalet mappade målgrupper som kan aktiveras för det valda målet överst på sidan.

Välj **[!UICONTROL Audiences]** för att navigera till kontrollpanelen Publiker [!UICONTROL Browse] -fliken. På den här arbetsytan visas en lista med alla segmentdefinitioner för din organisation.

![Widgeten för kartlagda målgrupper.](../images/destinations/mapped-audiences.png)

### Hälsa för mappade målgrupper {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Hälsa för mappade målgrupper"
>abstract="Den här widgeten innehåller en lista med upp till 20 mappade målgrupper vars totala antal profiler avviker med en faktor på minst en standardavvikelse från de 30 dagarnas genomsnittliga målgruppsstorlek som mappas till det målet. Den ger ett beräknat mått för spridning av målgruppsstorlekar från medelvärdet under de senaste 30 dagarna. Publiken sorteras från hög till låg."

Widgeten innehåller en lista med upp till 20 mappade målgrupper vars totala antal profiler, per den senaste ögonblicksbilden, avviker med en faktor på minst en standardavvikelse från de 30 dagarnas genomsnittliga målgruppsstorlek som mappas till det målet.

Sammanfattningsvis ger det ett beräknat mått för spridning av målgruppsstorlekar från medelvärdet under de senaste 30 dagarna. Jämför om dagens målgruppsstorlek ligger utanför den historiska standardavvikelse som har setts i data under de senaste 30 dagarna.

Alla målgruppsstorlekar i systemet sorteras från hög till låg målgruppsstorlek, vilket visas i [!UICONTROL LATEST SIZE] kolumn.

Om antalet mappade målgruppsprofiler ligger utanför en standardavvikelse från den genomsnittliga mappade profilstorleken under de senaste 30 dagarna, indikerar detta en avvikelse i systemet och bör undersökas.

Om en målgrupp inom [!UICONTROL Mapped audience health] widgeten avviker med en bred marginal bör du hänvisa till trenddiagrammet för målgruppens storlek och hitta den avvikande målgruppen. Trenden kan ge ytterligare insikter om er målgrupps hälsa.

>[!NOTE]
>
>Standardstorleken för den mappade publikens hälsowidget kan förhindra tabellinformationen. Ändra storleken på widgeten för att förbättra läsbarheten för mappade målgruppsnamn och kolumnrubriker. Mer information om hur du använder paneler finns i dokumentationen om hur du ändrar kontrollpaneler. [hur du ändrar storlek på en widget](../customize/modify.md).

![Mappad målgruppswidget.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Destinations count] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Antal destinationer"
>abstract="Den här widgeten visar totalt antal tillgängliga slutpunkter där en målgrupp kan aktiveras och levereras inom systemet. Detta nummer inkluderar både aktiva och inaktiva mål."

The [!UICONTROL Destinations count] widgeten anger det totala antalet tillgängliga slutpunkter där en målgrupp kan aktiveras och levereras inom systemet. Detta nummer inkluderar både aktiva och inaktiva mål.

Under det totala antalet väljer du **[!UICONTROL Destinations]** för att navigera till målfliken. På den här sidan visas en lista över alla mål som du har upprättat en anslutning till den aktuella.

![Widgeten för antal destinationer.](../images/destinations/destinations-count.png)

### [!UICONTROL Destination status] {#destination-status}

The [!UICONTROL Destination status] visar det totala antalet aktiverade destinationer som ett enda mått och visar den proportionella skillnaden mellan aktiverade och inaktiverade destinationer med hjälp av ett mundiagram.

Individuella antal för antingen aktiverade eller inaktiverade mål visas i en dialogruta när markören hålls över respektive avsnitt i mundiagrammet.

![Widgeten Målstatus.](../images/destinations/destination-status.png)

### [!UICONTROL Active destinations by destination platform] {#active-destinations-by-destination-platform}

Widgeten innehåller en tabell med två kolumner som visar en lista över aktiva målplattformar och det totala antalet aktiva destinationer för varje målplattform. Listan över målplattformar ordnas från hög till låg.

![Widgeten Aktiva destinationer efter målplattform.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Activated audiences across all destinations] {#activated-audiences-across-all-destinations}

The [!UICONTROL Activated audiences across all destinations] widgeten visar det totala antalet målgrupper som har aktiverats för alla destinationer i ett enda mätresultat. Den här siffran motsvarar den senaste ögonblicksbilden.

![De aktiverade målgrupperna i alla målwidgetar.](../images/destinations/activated-audiences-across-all-destinations.png)

Välj **[!UICONTROL Audiences]** för att navigera till destinationerna [!UICONTROL Browse] -fliken. Den här sidan innehåller en lista över alla aktiverade destinationer och en mängd relevanta mått. Mer information om [[!UICONTROL Browse] tab](../../destinations/ui/destinations-workspace.md#browse).

Se avsnittet Krav för [definitioner av termer som används](#prerequisites) i den här beskrivningen.

### [!UICONTROL Activated audiences] {#activated-audiences}

Den här widgeten ger ett enda mått för det totala antalet målgrupper som aktiveras för ett mål.

![Widgeten Aktiverade målgrupper.](../images/destinations/activated-audiences.png)

Välj **[!UICONTROL Audiences]** för att navigera till informationssidan på kontrollpanelen för mål. The [!UICONTROL Activation data] På -fliken visas en lista med målgrupper som har mappats till målet, inklusive startdatum och slutdatum (om tillämpligt) samt annan relevant information för dataexporten, t.ex. exporttyp, schema och frekvens. Om du vill visa information om en viss målgrupp väljer du dess namn på menyn [!UICONTROL Audience Name] kolumn.

![Sidan med information om kontrollpanelen för mål med fliken Aktiveringsdata markerad.](../images/destinations/activation-data-tab.png)

Den här widgeten hjälper dig att förstå värdet av dina destinationer baserat på det antal målgrupper som har aktiverats snabbt. Den ger också enkel tillgång till mer detaljerad information för ytterligare analys.

Se avsnittet Krav för [definitioner av termer som används](#prerequisites) i den här beskrivningen.

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta kontrollpanelen för destinationer och förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om att arbeta med destinationer i Experience Platform finns i [destinationsdokumentation](../../destinations/home.md).
