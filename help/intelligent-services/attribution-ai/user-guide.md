---
keywords: Experience Platform;användarhandbok;attribuering;populära ämnen;region
feature: Attribution AI
title: Användargränssnittshandbok för Attribution AI
description: Det här dokumentet är en guide för interaktion med Attribution AI i användargränssnittet för intelligenta tjänster.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 0%

---

# Användargränssnittshandbok för Attribution AI

Attribution AI, som en del av Intelligent Services är en flerkanalig algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner i förhållande till angivna resultat. Med Attribution AI kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion i varje fas av kundresan.

Det här dokumentet är en guide för interaktion med Attribution AI i användargränssnittet för intelligenta tjänster.

## Skapa en modell

I [!DNL Adobe Experience Platform] Gränssnitt, välj **[!UICONTROL Services]** i den vänstra navigeringen. The **[!UICONTROL Services]** webbläsaren visas och tillgängliga intelligenta Adobe-tjänster visas. I behållaren för Attribution AI väljer du **[!UICONTROL Open]**.

![Åtkomst till din modell](./images/user-guide/open_Attribution_ai.png)

Attribution AI tjänstsida visas. På den här sidan visas tjänstmodeller med Attribution AI och information om dem, inklusive modellens namn, konverteringshändelser, hur ofta modellen körs och status för den senaste uppdateringen.

Du hittar **[!UICONTROL Total conversion events scored]** mätvärdena finns längst ned till höger på sidan **[!UICONTROL Create model]** behållare. Det här måttet spårar det totala antalet konverteringshändelser som har bedömts av Attribution AI för det aktuella kalenderåret, inklusive alla sandlådemiljöer och borttagna servicemodeller.

![totala konverteringar](./images/user-guide/total_conversions.png)

Tjänstmodeller kan redigeras, klonas och tas bort med kontrollerna till höger i användargränssnittet. Om du vill visa dessa kontroller väljer du en modell från din befintliga **[!UICONTROL Service models]**. Kontrollerna innehåller följande information:

- **[!UICONTROL Edit]**: Markering **[!UICONTROL Edit]** gör att du kan ändra en befintlig tjänstmodell. Du kan redigera namn, beskrivning, status, bedömningsfrekvens för modellen och ytterligare spalter för spaltdata.
- **[!UICONTROL Clone]**: Markering **[!UICONTROL Clone]** kopierar den valda tjänstmodellen. Du kan sedan ändra arbetsflödet för att göra mindre ändringar och byta namn på det som en ny modell.
- **[!UICONTROL Delete]**: Du kan ta bort en servicemodell, inklusive alla historiska körningar. Motsvarande utdatamängd kommer att tas bort från Platform. Poäng som synkroniserades till kundprofilen i realtid tas dock inte bort.
- **[!UICONTROL Data source]**: En länk till den datauppsättning som används. Om mer än en datauppsättning används av Attribution AI visas&quot;Flera&quot; följt av antalet datauppsättningar. När du väljer hyperlänken visas förhandsvisningsdrivrutinen för datauppsättningar.
- **[!UICONTROL Last run details]**: Detta visas bara när en körning misslyckas. Här visas information om varför körningen misslyckades, t.ex. felkoder.

![Sidruta](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL Conversion events]**: En snabb översikt över konverteringshändelserna som har konfigurerats för den här modellen.
- **[!UICONTROL Lookback window]**: Den tidsram du definierade som anger hur många dagar före kontaktytorna för konverteringshändelsen som ska tas med.
- **[!UICONTROL Touchpoints]**: En lista med alla kontaktytor som du definierade när du skapade den här modellen.

![](./images/user-guide/side_panel_2.png)

Välj **[!UICONTROL Create model]** till att börja.

![Skapa modell](./images/user-guide/landing_page.png)

Därefter visas konfigurationssidan för Attribution AI där du kan ange ett namn och en valfri beskrivning för din tjänstmodell.

![namnge en modell](./images/user-guide/naming_instance.png)

## Markera data {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

Attribution AI kan efter design använda data från Adobe Analytics, Experience Event och Consumer Experience Event för att beräkna attribueringspoäng. När du väljer en datauppsättning visas bara de som är kompatibla med Attribution AI. Om du vill välja en datauppsättning väljer du **+**) bredvid datauppsättningsnamnet eller markera kryssrutan för att lägga till flera datauppsättningar samtidigt. Du kan också använda sökalternativet för att snabbt hitta de datauppsättningar du är intresserad av.

När du har valt de datauppsättningar du vill använda väljer du **[!UICONTROL Add]** om du vill lägga till datauppsättningarna i förhandsgranskningsfönstret för datauppsättningar.

![Välj datauppsättningar](./images/user-guide/select-datasets.png)

Välja informationsikonen ![informationsikon](./images/user-guide/info-icon.png) bredvid en datauppsättning öppnar förhandsvisningsprogramdrivrutinen för datauppsättningen.

![Välj och söka efter datauppsättning](./images/user-guide/dataset-preview.png)

Förhandsgranskningen av datauppsättningen innehåller data som senaste uppdateringstid, källschema och en förhandsgranskning av de första tio kolumnerna.

Välj **[!UICONTROL Save]** om du vill spara dina utkast när du går vidare i arbetsflödet. Du kan också spara utkastmodellkonfigurationer och gå vidare till nästa steg i arbetsflödet. Använd **[!UICONTROL Save and continue]** för att skapa och spara utkast under modellkonfigurationer. Med den här funktionen kan du skapa och spara utkast av modellkonfigurationen och den är särskilt användbar när du måste definiera många fält i konfigurationsarbetsflödet.

![Arbetsflödet Skapa på fliken Data Science Services-Attribution AI med Spara och Spara och fortsätt markerat.](./images/user-guide/aai-save-save-&-exit.png)

### Fullständighet för datauppsättning {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

I datauppsättningsförhandsvisningen är ett procentvärde för datauppsättningens fullständighet. Det här värdet ger en snabb ögonblicksbild av hur många kolumner i datauppsättningen som är tomma/null. Om en datauppsättning innehåller många värden som saknas och dessa värden hämtas någon annanstans rekommenderar vi att du inkluderar datauppsättningen som innehåller de värden som saknas.

>[!NOTE]
>
>Datauppsättningens fullständighet beräknas med hjälp av det maximala utbildningsfönstret för Attribution AI (ett år). Detta innebär att data som är äldre än ett år inte beaktas när datamängdens fullständighetsvärde visas.

![Fullständighet för datauppsättning](./images/user-guide/dataset-completeness.png)

### Välj en identitet {#identity}

Nu kan du koppla flera datauppsättningar till varandra baserat på identitetskartan (fältet). Du måste välja en identitetstyp (kallas även&quot;id namespace&quot;) och ett identitetsvärde i det namnutrymmet. Om du har tilldelat mer än ett fält som en identitet i ditt schema under samma namnutrymme, visas alla tilldelade identitetsvärden i den listruta för identitet som föregås av namnutrymmet, till exempel `EMAIL (personalEmail.address)` eller `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>Samma identitetstyp (namnutrymme) måste användas för varje datamängd som du väljer. En grön bock visas bredvid identitetstypen i identitetskolumnen som anger att datauppsättningarna är kompatibla. Om du till exempel använder namnutrymmet Telefon `mobilePhone.number` som identifierare måste alla identifierare för de återstående datauppsättningarna innehålla och använda namnutrymmet Telefon.

Markera en identitet genom att markera det understrukna värdet i identitetskolumnen. Välj en identitetsleverantör.

![välj samma namnutrymme](./images/user-guide/aai-identity-map-save-and-exit.png)

Om fler än en identitet är tillgänglig i ett namnutrymme måste du välja rätt identitetsfält för ditt användningsfall. Det finns till exempel två e-postidentiteter tillgängliga i e-postnamnutrymmet, ett arbete och en personlig e-postadress. Beroende på användningsfallet är det troligare att ett personligt e-postmeddelande fylls i och är mer användbart i individuella prognoser. Det innebär att du måste välja `EMAIL (personalEmail.address)` som din identitet.

![Datauppsättningsnyckeln är inte markerad](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> Om det inte finns någon giltig identitetstyp (namnutrymme) för en datauppsättning måste du ange en primär identitet och tilldela den till ett identitetsnamnutrymme med hjälp av [schemaredigerare](../../xdm/schema/composition.md#identity). Mer information om namnutrymmen och identiteter finns på [Namnutrymmen för identitetstjänst](../../identity-service/namespaces.md) dokumentation.

## Mappa mediekanal- och kampanjfält {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

När du har valt och lagt till datauppsättningar **Karta** konfigurationssteget visas. Attribution AI kräver att du mappar mediekanalsfältet för varje datauppsättning som du valde i föregående steg. Detta beror på att utan mediekanalmappningen mellan datauppsättningar kanske insikter som härletts från Attribution AI inte visas korrekt, vilket gör det svårt att tolka insikter. Även om bara mediekanalen krävs rekommenderar vi att du mappar några av de valfria fälten, som Media-åtgärd, Campaign-namn, Campaign-grupp och Campaign-tagg. På så sätt kan Attribution AI få tydligare insikter och optimala resultat.

![mappning](./images/user-guide/mapping-save-&-exit.png)

## Definiera händelser {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

Det finns tre olika typer av indata som används för att definiera händelser:

- **Konverteringshändelser:** Verksamhetsmål som identifierar effekten av marknadsföringsaktiviteter, t.ex. e-handelsorder, butiksköp och webbplatsbesök.
- **Fönstret Lookback:** Anger en tidsram som anger hur många dagar före kontaktytorna för konverteringshändelsen som ska inkluderas.
- **Pekpunkter:** marknadsföringshändelser på mottagarnivå, individ- och cookie-nivå som används för att utvärdera den numeriska eller intäktsbaserade effekten av konverteringar.

### Definiera konverteringshändelser {#define-conversion-events}

Om du vill definiera en konverteringshändelse måste du ge händelsen ett namn och välja händelsetyp genom att välja datauppsättningen och fältet i **Välj en datauppsättning och ett fält** listrutemeny.

![ja, listruta](./images/user-guide/define-conversion-events.png)

När en händelse har valts visas en ny listruta till höger om händelsen. Den andra listrutan används för att ge ytterligare kontext till händelsen genom att åtgärder används. Standardåtgärden för den här konverteringshändelsen *exists* används.

>[!NOTE]
>
>En sträng under *konverteringsnamn* uppdateras när du definierar händelsen.

![ingen listruta](./images/user-guide/conversion_event_1.png)

Därefter kan du välja en kombinerad datauppsättning som genereras genom att kombinera alla indatauppsättningar i föregående steg. Du kan också välja en kolumn baserad på enskilda datauppsättningar i **Välj en datauppsättning och ett fält** listrutemeny.

The **[!UICONTROL Add event]** och **[!UICONTROL Add Group]** -knappar används för att ytterligare definiera konverteringen. Beroende på vilken konvertering du definierar kan du behöva använda **[!UICONTROL Add event]** och **[!UICONTROL Add group]** knappar som ger ytterligare kontext.

![add, händelse](./images/user-guide/add_event.png)

Markera **[!UICONTROL Add event]** skapar ytterligare fält som kan fyllas i med samma metod som beskrivs ovan. När du gör det läggs en AND-sats till i strängdefinitionen under konverteringsnamnet. Välj **x** för att ta bort en händelse som har lagts till.

![lägg till händelsemeny](./images/user-guide/add_event_result.png)

Markera **[!UICONTROL Add Group]** ger möjlighet att skapa ytterligare fält som är åtskilda från originalet. Med tillägg av grupper är *Och* visas. Markera **Och** ger ett alternativ att ändra parametern så att den innehåller &quot;Eller&quot;. &quot;Eller&quot; används för att definiera flera lyckade konverteringssökvägar. &quot;And&quot; utökar konverteringssökvägen så att den innehåller ytterligare villkor.

![använder och](./images/user-guide/and_or.png)

Om du behöver mer än en konvertering väljer du **Lägg till konvertering** för att skapa ett nytt konverteringskort. Du kan upprepa processen ovan om du vill definiera flera konverteringar.

![konvertera](./images/user-guide/add_conversion.png)

### Definiera uppslagsfönster {#lookback-window}

När du har definierat konverteringen måste du bekräfta uppslagsfönstret. Använd piltangenterna eller genom att välja standardvärdet (56), och ange hur många dagar före konverteringshändelsen du vill ta med kontaktytor från. Pekpunkter definieras i nästa steg.

![uppslag](./images/user-guide/lookback_window.png)

### Definiera kontaktytor

När du definierar kontaktytor följer du ett arbetsflöde som liknar [definiera konverteringar](#define-conversion-events). Först måste du namnge kontaktytan och välja ett kontaktytpunktsvärde på menyn *Ange fältnamn* listrutemeny. När du har valt operatorlistrutan visas standardvärdet &quot;exists&quot;. Markera listrutan för att visa en lista med operatorer.

![operatorer](./images/user-guide/operators.png)

För denna kontaktyta väljer du **är lika med**.

![steg 1](./images/user-guide/touchpoint_step1.png)

När en operator för en kontaktyta har valts, *Ange fältvärde* är tillgänglig. Värdena i listrutan för *Ange fältvärde* fylls i baserat på den operator och det slutpunktsvärde som du valde tidigare. Om ett värde inte fylls i i listrutan kan du skriva värdet i manuellt. Välj listrutan och välj **KLICKA**.

>[!NOTE]
>
>Operatorerna &quot;exists&quot; och &quot;not exists&quot; har inga fältvärden kopplade till sig.

![listruta med kontaktyta](./images/user-guide/touchpoint_dropdown.png)

The **Lägg till händelse** och **Lägg till grupp** -knappar används för att ytterligare definiera din kontaktyta. På grund av den komplexa beskaffenheten kring kontaktytor är det inte ovanligt att ha flera händelser och grupper för en enda kontaktyta.

När du har valt **Lägg till händelse** tillåter att ytterligare fält läggs till. välj **x** för att ta bort en händelse som har lagts till.

![add, händelse](./images/user-guide/touchpoint_add_event.png)

Markera **Lägg till grupp** ger dig möjlighet att skapa ytterligare fält som är åtskilda från originalet. Med tillägg av grupper är *Och* visas. Välj **Och** Om du vill ändra parametern används den nya parametern &quot;Or&quot; för att definiera flera lyckade sökvägar. Den här kontaktytan har bara en lyckad bana och därför behövs inte &quot;Eller&quot;.

![översikt över kontaktyta](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Använd strängen under *Kontaktpunktsnamn* om du vill få en snabb översikt över din kontaktyta. Observera att strängen matchar namnet på kontaktytan.

![](./images/user-guide/touchpoint_string.png)

Du kan lägga till fler kontaktytor genom att välja **Lägg till kontaktyta** och upprepa processen ovan.

![lägg till kontaktyta](./images/user-guide/add_touchpoint.png)

När du har definierat alla nödvändiga kontaktytor rullar du uppåt och väljer **Nästa** i det övre högra hörnet för att fortsätta till det sista steget.

![färdig definition](./images/user-guide/define_event_save_and_exit.png)

## Avancerad utbildning och poängsättning

Den sista sidan i Attribution AI är **[!UICONTROL Advanced]** sida som används för att ställa in utbildning och poängsättning.

![nya alternativ för siduppsättning](./images/user-guide/advanced_settings_set_options.png)

### Schemalägg utbildning

Använda *Schema* kan du välja vilken dag och tid i veckan du vill att poängsättningen ska äga rum.

Välj listrutan under *Värderingsfrekvens* för att välja mellan poängsättning varje dag, vecka och månad. Välj sedan de veckodagar du vill att poängsättningen ska äga rum. Du kan välja flera dagar. Om du väljer samma dag igen avmarkeras den.

![Schemalägg utbildning](./images/user-guide/schedule_training.png)

Om du vill ändra tiden på dagen som du vill att poängsättningen ska göras väljer du klockikonen. I den nya övertäckning som visas anger du den tid på dagen som du vill att poängsättningen ska göras. Stäng övertäckningen genom att markera den utanför den.

>[!NOTE]
>
>Det kan ta upp till 24 timmar för varje poängprocess att slutföra.

![klockikon](./images/user-guide/time_of_day.png)

### Kolumner för extra poängdatauppsättning (valfritt)

Som standard skapas en poängdatauppsättning för varje tjänstmodell i ett standardschema. Du kan välja att lägga till ytterligare kolumner baserat på dina Conversion Event- och Touchpoint-konfigurationer i resultatmängden. Börja med att välja kolumner från indatauppsättningen. Du kan sedan dra och släppa dem för att ändra ordningen genom att hålla ned vänster musknapp över hamburgikonen.

![kolumntillägg för stackdata](./images/user-guide/Add-score-dataset.png)

### Regionbaserad modellering (valfritt) {#region-based-modeling-optional}

Kundernas beteenden kan skilja sig avsevärt mellan olika länder och geografiska regioner. För globala företag kan användning av landsbaserade eller regionbaserade modeller öka attribueringsnoggrannheten. Varje region som läggs till skapar en ny modell med den regionens data.

Om du vill definiera en ny region börjar du med att välja **[!UICONTROL Add region]**. Ange ett namn för regionen i behållaren som visas. Endast ett värde (&quot;placeContext.geo.countryCode&quot;) fylls i från **[!UICONTROL Enter Field Name]** nedrullningsbar meny. Välj det här värdet.

![Välj region att](./images/user-guide/select_region_att.png)

Välj sedan en operator.

![operatorn region](./images/user-guide/region_operators.png)

Skriv till sist in landskoden i **[!UICONTROL Enter Field Value]** nedrullningsbar meny.

>[!NOTE]
>
>Landskoderna är två tecken långa. En fullständig lista finns här [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![region](./images/user-guide/region-based.png)

### Utbildningsfönster {#training-window}

För att säkerställa att ni får den mest korrekta modellen är det viktigt att utbilda modellen med historiska data som representerar ert företag. Som standard används två fjärdedelar (6 månader) av konverteringshändelsedata för modellen. Välj listrutan för att ändra standardinställningen. Du kan välja att utbilda med en till fyra fjärdedelar av data (3-12 månader).

>[!NOTE]
>
>Ett kortare utbildningsfönster är mer känsligt för de senaste trenderna, medan ett längre utbildningsfönster skapar en mer robust modell och är mindre känsligt för de senaste trenderna.

![utbildningsfönster](./images/user-guide/training_window.png)

När du har valt kursfönster väljer du **[!UICONTROL Finish]** längst upp till höger. Ge databearbetningen lite tid. När du är klar visas en dialogruta som bekräftar att instansinställningarna är klara. Välj **[!UICONTROL Ok]** omdirigeras till **[!UICONTROL Service instances]** sida där du kan se tjänstinstansen.

![installationen slutförd](./images/user-guide/instance_setup_complete.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en tjänstinstans i Attribution AI. När instansen är klar med poängsättningen (upp till 24 timmar) är du redo att [identifiera insikter om Attribution AI](./discover-insights.md). Om du vill ladda ned dina poängresultat går du till [ladda ned bakgrundsmusik](./download-scores.md) dokumentation.

## Ytterligare resurser

I följande video visas ett arbetsflöde från början till slut som du kan använda för att skapa en ny instans i Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
