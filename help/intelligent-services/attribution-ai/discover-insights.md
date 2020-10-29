---
keywords: Experience Platform;insights;attribution ai;popular topics;attribution ai insights
solution: Experience Platform
title: Upptäck insikter inom Attribution AI
topic: Attribution AI insights
description: Det här dokumentet är en guide för interaktion med Service Instance-insikter i användargränssnittet för Adobe Intelligent Services.
translation-type: tm+mt
source-git-commit: 69c27fc45aa9d9acaaed29c2324d02ebd471d63d
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---


# Upptäck insikter inom Attribution AI

Attribution AI Service-instanser ger insikter som kan användas för att fatta och mäta marknadsföringsbeslut som rör marknadsföringens resultat och avkastningen på investeringen. Genom att välja en tjänstinstans får ni visualiseringar och filter som hjälper er att förstå effekten av varje kundinteraktion i varje fas av kundresan.

Det här dokumentet är en guide för interaktion med Service Instance-insikter i användargränssnittet för Adobe Intelligent Services.

## Komma igång

För att kunna utnyttja insikter om Attribution AI måste du ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [Attribution AI användargränssnittshandbok](./user-guide.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

## Översikt över insikter om tjänstinstans

In the [!DNL Adobe Experience Platform] UI, select **[!UICONTROL Services]** in the left navigation. Webbläsaren visas och visar tillgängliga Adobe Intelligent Services. **[!UICONTROL Services]** I behållaren för Attribution AI väljer du **[!UICONTROL Open]**.

![Åtkomst till din instans](./images/insights/open_Attribution_ai.png)

Attribution AI tjänstsida visas. På den här sidan visas tjänstinstanser av Attribution AI och information om dem, inklusive namnet på instansen, konverteringshändelser, hur ofta instansen körs och status för den senaste uppdateringen. Välj ett tjänstinstansnamn som ska börja.

>[!NOTE]
>
>Det går endast att välja tjänstinstanser som har slutfört betygskörningar.

![Skapa instans](./images/insights/select-service-instance.png)

Därefter visas informationssidan för den aktuella tjänstinstansen, där du får visualiseringar och ett antal filter för att interagera med dina data. Visualiseringar och filter förklaras mer ingående i den här guiden.

![konfigurationssida](./images/insights/landing-page.png)

### Information om tjänstinstans

Om du vill visa mer information om en tjänstinstans väljer du **[!UICONTROL Show more]** i det övre högra hörnet.

![visa mer](./images/insights/show-more.png)

En detaljerad lista visas. Mer information om egenskaperna finns i användarhandboken för [Attribution AI](./user-guide.md).

![visa detaljer](./images/insights/advanced-details.png)

### Redigera en instans

Om du vill redigera en instans väljer du **[!UICONTROL Edit]** i den övre högra navigeringen.
![klicka på redigeringsknappen](./images/insights/edit-button.png)

Dialogrutan Redigera visas. Du kan redigera instansens namn, beskrivning och bedömningsfrekvens. Om instansstatusen är inaktiverad går det inte att redigera bedömningsfrekvensen. Om du vill bekräfta ändringarna och stänga dialogrutan väljer du **[!UICONTROL Save]** i det nedre högra hörnet.

![redigera poesi](./images/insights/edit-popover.png)

### Fler åtgärder {#more-actions}

Knappen finns i den övre högra navigeringen bredvid **[!UICONTROL More actions]** **[!UICONTROL Edit]**. Om du väljer **[!UICONTROL More actions]** det här alternativet öppnas en listruta där du kan välja någon av följande åtgärder:

- **[!UICONTROL Clone]**: Klonar instansen.
- **[!UICONTROL Delete]**: Tar bort instansen.
- **[!UICONTROL Download summary data]**: Hämtar en CSV-fil som innehåller sammanfattningsdata.
- **[!UICONTROL Access scores]**: Om du väljer **[!UICONTROL Access scores]** Omdirigeras du till [åtkomstpoängen för självstudiekursen](./download-scores.md)om.
- **[!UICONTROL View run history]**: En pover som innehåller en lista över alla poäng som är associerade med tjänstinstansen visas.

![fler åtgärder](./images/insights/more-actions.png)

## Filtrera data

Med hjälp av Attribution AI kan du filtrera data och automatiskt uppdatera gränssnittets visuella information baserat på dina valda filter.

### Konverteringshändelse

När du skapar en ny instans i Attribution AI är ett av de obligatoriska fälten&quot;Conversion events&quot;. Konverteringshändelser är affärsmål som identifierar effekten av marknadsföringsaktiviteter, som e-handelsorder, butiksköp och webbplatsbesök.

I **[!UICONTROL Conversion events]** listrutan kan du välja någon av de händelser som är definierade för instansen för att filtrera data. Om du väljer specifika händelser ändras visualiseringarna av användargränssnittet så att endast konverteringar som tillhör dessa händelser fylls i.

![konverteringshändelse](./images/insights/conversion-event.png)

### Attributionsmodell

Om du väljer **[!UICONTROL Attribution Model]** det här alternativet öppnas en listruta med alla olika attribueringsmodeller tillgängliga. Du kan välja flera modeller för att jämföra resultaten. Mer information om de olika attribueringsmodellerna och hur de fungerar finns i översikten över [Attribution AI](./overview.md) , som innehåller en tabell med information om varje modell.

![attribueringsmodell](./images/insights/attribution-model.png)

### Län

>[!NOTE]
>
>Det här filtret finns bara om du utförde den valfria [regionbaserade modelleringen](./user-guide.md#region-based-modeling-optional) i användargränssnittsguiden för Attribution AI när du skapade tjänstinstansen.

Med det här filtret kan du markera alla områden som du har konfigurerat när du skapar instansen.

### Lägg till filter

Du kan lägga till fler filter genom att välja **filterikonen** för att öppna **[!UICONTROL Add filters]** pekaren. Med **[!UICONTROL Add filters]** povern kan du filtrera efter kanal, geografi, medietyp och produkt. Endast tillämpliga filter för en tjänstinstans fylls i av povern. Om du till exempel inte angav geografiska data eller en medietyp kommer dessa filterattribut inte att vara tillgängliga för din instans.

![extra filter](./images/insights/additional-filters.png)

![filterpotens](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** Om du väljer kanalattributet kan du filtrera alla tillgängliga marknadsföringskanaler. Du kan välja flera kanaler för att jämföra dem.
- **[!UICONTROL Geography]:** Om du väljer attributet geography kan du filtrera landskoder baserat på regionsbaserade modeller. Beroende på vilka data du har kan det här filtret finnas eller inte finnas. Landskoderna är två tecken långa. Se den fullständiga landskodslistan [här](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** Om du väljer medietypsattribut kan du filtrera alla definierade medietyper.
- **[!UICONTROL Product]:** Om du väljer produktattributet kan du filtrera från alla produkter som ursprungligen var inkapslade när du skapade instansen.

### Datumintervall

Välj kalenderikonen för att öppna datumintervallposeraren. Början- och slutkonverteringshändelsedatumen avgör mängden data som fylls i i användargränssnittet. Du kan välja att begränsa eller utöka datumintervallet för att kunna fokusera eller utöka mängden data som fylls i.

![datumintervall](./images/insights/display-date-range.png)

## Översikt över era data

På **[!UICONTROL Overview]** kortet visas det totala antalet konverteringar per attribueringsmodell. Det totala antalet ändras baserat på hur specifik sökningen är med hjälp av de filter som beskrivs tidigare i det här dokumentet. Om du väljer flera modeller läggs ytterligare cirklar till i översikten, där var och en har en egen färg som motsvarar teckenförklaringen.

![översikt](./images/insights/Overview.png)

## Trender varje vecka

Kortet **[!UICONTROL Weekly trends]** delar upp den totala konverteringen enligt det datumintervall du anger under filtreringsprocessen.

Om du väljer ellipserna i det övre högra hörnet av **veckotrendkortet** visas en listruta där du kan välja trender varje dag, vecka eller månad.

När du hovrar över dataraden för en viss attribueringsmodell skapas en pover som visar det totala antalet konverteringar för det datumet.

![trender](./images/insights/weekly-trends.png)

## Uppdelning efter kanal

Kortet används för att bestämma det totala antalet konverteringar i förhållande till varje kanal. **[!UICONTROL Breakdown by channel]** Detta kort kan användas för att fatta beslut om varje kanals effektivitet och avkastningen på investeringen.

Om du markerar ellipserna i det övre högra hörnet av **[!UICONTROL Breakdown by channel]** kortet öppnas en listruta där du kan fylla i data baserat på kontaktytor.

![fördelningskanal](./images/insights/channel-breakdown.png)

## Populära kampanjer

Kortet visar en översikt över era kampanjer och hur kampanjen fungerar i varje kanal. **[!UICONTROL Top campaigns]** Med det här kortet kan ni informera teamet om hur effektiv en viss kampanj är för en viss kanal och ge er insikter om vilka kampanjer ni bör investera i ytterligare.

![toppkampanjer](./images/insights/top-campaigns.png)

## Uppdelning efter kontaktytsposition

När du väljer **[!UICONTROL Path Analysis]** tabb läses diagrammen **[!UICONTROL Breakdown by touchpoint position]** och **[!UICONTROL Top conversion paths]** diagrammen in.

Diagrammet **[!UICONTROL Breakdown by touchpoint position]** är en fördelning av konverteringar utifrån kontaktytans position jämfört med alla konverteringsbanor. Det här diagrammet hjälper dig att förstå vilka kontaktytor som är mer effektiva i olika faser av konverteringsbanan. Stegen är starter, spelare och närmare.

- **Starter:** Anger att kontaktytan var den första beröringen i en konverteringsbana.
- **Spelare:** Anger att kontaktytan inte var den första eller sista beröringen som ledde till en konvertering.
- **Closer:** Anger att kontaktytan var den sista kontakten före en konvertering.

>!![NOTE]
Summan av procentandelen för en attribueringsmodell för alla kontaktytor och positioner ska vara lika med 100.

![kontaktyta för nedbrytning av användarväg](./images/insights/user-paths.png)

## De vanligaste konverteringsbanorna

I diagrammet visas de påverkade och algoritmiska poängen på de översta konverteringsbanorna i de valda områdena. **[!UICONTROL Top conversion paths]** I det här diagrammet kan du se vilka kontaktytor som bidrar till konverteringarna och vad attribueringspoängen är för varje kontaktyta. Du kan använda den här informationen för att visa de mest frekventa banorna i ett visst område och se om det uppstår några mönster mellan de olika uppsättningarna med kontaktytor.

![De vanligaste användarsökvägarna](./images/insights/Touchpoint-paths.png)

## Pekpunktseffektivitet

Om du väljer **[!UICONTROL Touchpoint Effectiveness]** fliken läses **[!UICONTROL Touchpoint effectiveness]** kortet in. Det här kortet använder Attribution AI datadistribution för att visa information för varje kontaktyta. Data för den här tabellen genereras endast för specifika tidsperioder enligt datumet i kortets övre högra **[!UICONTROL As of]** hörn.

![val av kontaktyteffekt](./images/insights/Touchpoint-effectiveness.png)

Du kan använda **[!UICONTROL Touchpoint effectiveness]** kortinformationen för att förstå hur en kontaktyta bidrar till en konvertering. Du kan också se hur effektiv varje kontaktyta är med följande prestandamått:

**Perfekta** banor: Det här måttet visar en procentandel av banorna som uppnår eller inte uppnår konvertering för kontaktytan. Du ser högre konverteringar om förhållandet mellan banor (i procent) som uppnår konvertering till banor som inte uppnår konvertering är högt.

![Banor rörde vid mått](./images/insights/Touchpoint-metrics.png)

**Effektivitetsmått**: Det här måttet visar stjärnor på en skala från ett till fem. Skalan anger den relativa vikten av en kontaktyta för att göra en konvertering.

>[!NOTE]
Högre kontaktytvolym garanterar inte högre effektivitetsmått.

**Total volym**: Det sammanlagda antalet gånger en kontaktyta berördes av en användare. Detta inkluderar alla kontaktytor som visas på en bana som uppnår konvertering samt banor som inte leder till konvertering.

## Nästa steg

När du är klar med filtreringen av data och kan visa lämplig information kan du välja att få åtkomst till poängen. Om du vill ha en detaljerad guide om hur du får tillgång till dina poäng kan du gå till [självstudiekursen i Attribution AI](./download-scores.md) . Dessutom kan du hämta sammanfattningsdata enligt [fler åtgärder](#more-actions). Om du väljer Hämta sammanfattningsdata hämtas sammanfattningsdata som aggregerats efter datum.

## Ytterligare resurser

Följande videofilm är utformad för att hjälpa dig att lära dig hur du använder informationssidan för Attribution AI för att förstå avkastningen på marknadsföringskanaler och kampanjer.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)