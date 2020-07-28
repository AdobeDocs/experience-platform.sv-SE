---
keywords: Experience Platform;user guide;attribution ai;popular topics
solution: Experience Platform
title: Användarhandbok för Attribution AI
topic: User guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# Användarhandbok för Attribution AI

Attribution AI, som en del av Intelligent Services är en flerkanalig algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner i förhållande till angivna resultat. Med Attribution AI kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion i varje fas av kundresan.

Det här dokumentet är en guide för interaktion med Attribution AI i användargränssnittet för intelligenta tjänster.

## Skapa en instans

Klicka på [!DNL Adobe Experience Platform] Tjänster **i den vänstra navigeringen i** användargränssnittet. Webbläsaren *Services* visas och visar tillgängliga smarta Adobe-tjänster. Klicka på **Öppna** i behållaren för Attribution AI.

![Åtkomst till din instans](./images/user-guide/open_Attribution_ai.png)

Attribution AI tjänstsida visas. På den här sidan visas tjänstinstanser av Attribution AI och information om dem, inklusive namnet på instansen, konverteringshändelser, hur ofta instansen körs och status för den senaste uppdateringen. Klicka på **Skapa instans** för att börja.

![Skapa instans](./images/user-guide/landing_page.png)

Därefter visas konfigurationssidan för Attribution AI, där du kan ange grundläggande information och en datauppsättning för instansen.

![konfigurationssida](./images/user-guide/setup_attribution.png)

### Namnge instansen

Ange ett namn och en valfri beskrivning av tjänstinstansen under *Grundläggande information*.

![namnge en instans](./images/user-guide/naming_instance.png)

### Välj en datauppsättning

När du har fyllt i den grundläggande informationen klickar du på listrutan **Välj datauppsättning** för att välja datauppsättningen. Datauppsättningen används för att träna modellen och poängsätta efterföljande data som den skapar. När du väljer en datauppsättning i listruteväljaren visas endast de som är kompatibla med Attribution AI och som följer XDM-schemat (Experience Data Model). När du har valt en datauppsättning klickar du på **Nästa** i det övre högra hörnet för att fortsätta till sidan för att definiera händelser.

![konfigurationssida](./images/user-guide/initial_creation_attribution.png)

## Definiera händelser

Det finns tre olika typer av indata som används för att definiera händelser:

- **Konverteringshändelser:** Verksamhetsmål som identifierar effekten av marknadsföringsaktiviteter, t.ex. e-handelsorder, butiksköp och webbplatsbesök.
- **Fönstret Lookback:** Anger en tidsram som anger hur många dagar före kontaktytorna för konverteringshändelsen som ska inkluderas.
- **Pekpunkter:** marknadsföringshändelser på mottagarnivå, individ- och cookie-nivå som används för att utvärdera den numeriska eller intäktsbaserade effekten av konverteringar.

### Definiera konverteringshändelser {#define-conversion-events}

Om du vill definiera en konverteringshändelse måste du ge händelsen ett namn och välja händelsetyp genom att klicka på **listrutan Ange fältnamn** .

![ja, listruta](./images/user-guide/conversion_event_2.png)

När en händelse har valts visas en ny listruta till höger om händelsen. Den andra listrutan används för att ge ytterligare kontext till händelsen genom att åtgärder används. Standardåtgärden *finns* för den här konverteringshändelsen.

>[!NOTE]
>
>En sträng under ditt *konverteringsnamn* uppdateras när du definierar händelsen.

![ingen listruta](./images/user-guide/conversion_event_1.png)

Knapparna *Lägg till händelse* och *Lägg till grupp* används för att ytterligare definiera konverteringen. Beroende på vilken konvertering du definierar kan du behöva använda knapparna *Lägg till händelse* och *Lägg till grupp* för att få ytterligare kontext.

![add, händelse](./images/user-guide/add_event.png)

Om du klickar på **Lägg till händelse** skapas ytterligare fält som kan fyllas i med samma metod som beskrivs ovan. Då läggs en *AND* -sats till i strängdefinitionen nedanför *konverteringsnamnet*. Klicka på **x** för att ta bort en händelse som har lagts till.

![lägg till händelsemeny](./images/user-guide/add_event_result.png)

Om du klickar på **Lägg till grupp** kan du skapa ytterligare fält som är åtskilda från originalet. När du lägger till grupper visas en blå *Och* -knapp. Om du klickar på **Och** får du ett alternativ för att ändra parametern så att den innehåller &quot;Eller&quot;. &quot;Eller&quot; används för att definiera flera lyckade konverteringssökvägar. &quot;And&quot; utökar konverteringssökvägen så att den innehåller ytterligare villkor.

![använder och](./images/user-guide/and_or.png)

Om du behöver mer än en konvertering klickar du på **Lägg till konvertering** för att skapa ett nytt konverteringskort. Du kan upprepa processen ovan om du vill definiera flera konverteringar.

![konvertera](./images/user-guide/add_conversion.png)

### Definiera uppslagsfönster

När du har definierat konverteringen måste du bekräfta uppslagsfönstret. Ange med piltangenterna eller genom att klicka på standardvärdet (56) hur många dagar före konverteringshändelsen som du vill ta med kontaktytor från. Pekpunkter definieras i nästa steg.

![uppslag](./images/user-guide/lookback_window.png)

### Definiera kontaktytor

När du definierar kontaktytor följer du ett arbetsflöde som liknar det som används för att [definiera konverteringar](#define-conversion-events). Först måste du namnge kontaktytan och välja ett kontaktytpunktsvärde i listrutan *Ange fältnamn* . När du har valt operatorlistrutan visas standardvärdet &quot;exists&quot;. Klicka på listrutan för att visa en lista med operatorer.

![operatorer](./images/user-guide/operators.png)

För den här kontaktytan väljer du **lika med**.

![steg 1](./images/user-guide/touchpoint_step1.png)

När du har valt en operator för en kontaktyta blir *Ange fältvärde* tillgängligt. Värdena för listrutan för *Ange fältvärde* fylls i baserat på operatorn och det kontaktpunktsvärde som du valde tidigare. Om ett värde inte fylls i i listrutan kan du skriva värdet i manuellt. Klicka på listrutan och välj **KLICKA**.

>[!NOTE]
>
>Operatorerna &quot;exists&quot; och &quot;not exists&quot; har inga fältvärden kopplade till sig.

![listruta med kontaktyta](./images/user-guide/touchpoint_dropdown.png)

Knapparna *Lägg till händelse* och *Lägg till grupp* används för att ytterligare definiera din kontaktyta. På grund av den komplexa beskaffenheten kring kontaktytor är det inte ovanligt att ha flera händelser och grupper för en enda kontaktyta.

När du klickar på **Lägg till händelse** kan ytterligare fält läggas till. Klicka på **x** för att ta bort en händelse som har lagts till.

![add, händelse](./images/user-guide/touchpoint_add_event.png)

Om du klickar på **Lägg till grupp** kan du skapa ytterligare fält som är åtskilda från originalet. När du lägger till grupper visas en blå *Och* -knapp. Klicka på **Och** om du vill ändra parametern används den nya parametern &quot;Or&quot; för att definiera flera lyckade sökvägar. Den här kontaktytan har bara en lyckad bana och därför behövs inte &quot;Eller&quot;.

![översikt över kontaktyta](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Använd strängen under *Touchpoint-namnet* för att få en snabb översikt över din kontaktyta. Observera att strängen matchar namnet på kontaktytan.

![](./images/user-guide/touchpoint_string.png)

Du kan lägga till ytterligare kontaktytor genom att klicka på **Lägg till kontaktyta** och upprepa processen ovan.

![lägg till kontaktyta](./images/user-guide/add_touchpoint.png)

När du har definierat alla nödvändiga kontaktytor rullar du uppåt och klickar på **Nästa** i det övre högra hörnet för att fortsätta till det sista steget.

![färdig definition](./images/user-guide/define_event_next.png)

## Avancerad utbildning och poängsättning

Den sista sidan i Attribution AI är den *avancerade* sidan som används för att ställa in utbildning och poängsättning.

![ny sida avancerad](./images/user-guide/advanced_settings.png)

### Schemalägg utbildning

Med *Schemalägg* kan du välja vilken dag och tid i veckan du vill att poängsättningen ska äga rum.

Klicka på listrutan under *Betygsningsfrekvens* för att välja mellan betygsättning varje dag, vecka och månad. Välj sedan de veckodagar du vill att poängsättningen ska äga rum. Du kan välja flera dagar. Klicka en dag en gång till för att avmarkera den.

![Schemalägg utbildning](./images/user-guide/schedule_training.png)

Klicka på klockikonen om du vill ändra den tidpunkt på dagen som du vill att poängsättningen ska göras. I den nya övertäckning som visas anger du den tid på dagen som du vill att poängsättningen ska göras. Klicka utanför övertäckningen för att stänga den.

>[!NOTE]
>
>Det kan ta upp till 24 timmar för varje poängprocess att slutföra.

![klockikon](./images/user-guide/time_of_day.png)

### Regionbaserad modellering (valfritt) {#region-based-modeling-optional}

Kundernas beteenden kan skilja sig avsevärt mellan olika länder och geografiska regioner. För globala företag kan användning av landsbaserade eller regionbaserade modeller öka attribueringsnoggrannheten. Varje region som läggs till skapar en ny modell med den regionens data.

Om du vill definiera en ny region börjar du med att klicka på **Lägg till region**. Ange ett namn för regionen i behållaren som visas. Endast ett värde (&quot;placeContext.geo.countryCode&quot;) fylls i från listrutan *Ange fältnamn* . Välj det här värdet.

![Välj region att](./images/user-guide/select_region_att.png)

Välj sedan en operator.

![operatorn region](./images/user-guide/region_operators.png)

Skriv landskoden i listrutan *Ange fältvärde* .

>[!NOTE]
>
>Landskoderna är två tecken långa. En fullständig lista finns här: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![region](./images/user-guide/region-based.png)

### Utbildningsfönster

För att säkerställa att ni får den mest korrekta modellen är det viktigt att utbilda modellen med historiska data som representerar ert företag. Som standard används två fjärdedelar (6 månader) av data för att utbilda modellen. Välj listrutan för att ändra standardinställningen. Du kan välja att utbilda med en till fyra fjärdedelar av data (3-12 månader).

>[!NOTE]
>
>Ett kortare utbildningsfönster är mer känsligt för de senaste trenderna, medan ett längre utbildningsfönster skapar en mer robust modell och är mindre känsligt för de senaste trenderna.

![utbildningsfönster](./images/user-guide/training_window.png)

När du har valt utbildningsfönstret klickar du på **Slutför** i det övre högra hörnet. Ge databearbetningen lite tid. När du är klar visas en dialogruta som bekräftar att instansinställningarna är klara. Klicka på **OK** om du vill omdirigeras till sidan *Tjänstinstanser* där du kan se tjänstinstansen.

![installationen slutförd](./images/user-guide/instance_setup_complete.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en tjänstinstans i Attribution AI. När instansen är klar med poängsättningen (upp till 24 timmar) är du redo att [identifiera Attribution AI insikter](./discover-insights.md). Om du dessutom vill ladda ned dina poängresultat går du till [nedladdningsdokumentationen för](./download-scores.md) bakgrundsmusik.

## Ytterligare resurser

I följande video visas ett arbetsflöde från början till slut som du kan använda för att skapa en ny instans i Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)