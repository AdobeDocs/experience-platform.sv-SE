---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: Upptäck insikter inom Attribution AI
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Upptäck insikter inom Attribution AI

Attribution AI Service-instanser ger insikter som kan användas för att fatta och mäta marknadsföringsbeslut som rör marknadsföringens resultat och avkastningen på investeringen. Genom att välja en tjänstinstans får ni visualiseringar och filter som hjälper er att förstå effekten av varje kundinteraktion i varje fas av kundresan.

Det här dokumentet är en guide för interaktion med Service Instance-insikter i användargränssnittet för Adobe Intelligent Services.

## Komma igång

För att kunna utnyttja insikter om Attribution AI måste du ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [Attribution AI användargränssnittshandbok](./user-guide.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

## Översikt över insikter om tjänstinstans

Klicka på [!DNL Adobe Experience Platform] Tjänster **i den vänstra navigeringen i** användargränssnittet. Webbläsaren *Services* visas och visar tillgängliga Adobe Intelligent Services. Klicka på **Öppna** i behållaren för Attribution AI.

![Åtkomst till din instans](./images/insights/open_Attribution_ai.png)

Attribution AI tjänstsida visas. På den här sidan visas tjänstinstanser av Attribution AI och information om dem, inklusive namnet på instansen, konverteringshändelser, hur ofta instansen körs och status för den senaste uppdateringen. Klicka på ett tjänstinstansnamn för att börja.

>[!NOTE]
>
>Det går endast att välja tjänstinstanser som har slutfört betygskörningar.

![Skapa instans](./images/insights/select-service-instance.png)

Därefter visas informationssidan för den aktuella tjänstinstansen, där du får visualiseringar och ett antal filter för att interagera med dina data. Visualiseringar och filter förklaras mer ingående i den här guiden.

![konfigurationssida](./images/insights/landing-page.png)

### Information om tjänstinstans

Om du vill visa mer information om en tjänstinstans klickar du på **Visa mer** i det övre högra hörnet.

![visa mer](./images/insights/show-more.png)

En detaljerad lista visas. Mer information om egenskaperna finns i användarhandboken för [Attribution AI](./user-guide.md).

![visa detaljer](./images/insights/advanced-details.png)

### Redigera en instans

Om du vill redigera en instans klickar du på *Redigera* i den övre högra navigeringen.
![klicka på redigeringsknappen](./images/insights/edit-button.png)

Dialogrutan Redigera visas. Du kan redigera beskrivningen och bedömningsfrekvensen för instansen. Om du vill bekräfta ändringarna och stänga dialogrutan klickar du på *Redigera* längst ned till höger.

![redigera poesi](./images/insights/edit-popover.png)

### Fler åtgärder {#more-actions}

Knappen *Fler åtgärder* finns i den övre högra navigeringen bredvid *Redigera*. Om du klickar på **Fler åtgärder** öppnas en listruta där du kan välja någon av följande åtgärder:

- **Ta bort**: Tar bort instansen.
- **Hämta sammanfattningsdata**: Hämtar en CSV-fil som innehåller sammanfattningsdata.
- **Åtkomstpoäng**: Om du klickar på *Åtkomstpoäng* omdirigeras du till [åtkomstpoängen för självstudiekursen](./download-scores.md).
- **Visa körningshistorik**: En pover som innehåller en lista över alla poäng som är associerade med tjänstinstansen visas.

![fler åtgärder](./images/insights/more-actions.png)

## Filtrera data

Med hjälp av Attribution AI kan du filtrera data och automatiskt uppdatera gränssnittets visuella information baserat på dina valda filter.

>[!NOTE]
>
>Som standard är alla filter inställda på &quot;Alla&quot; förutom filtret *Attribution model* , som är inställt på &quot;Inkrementella och påverkade attributkonverteringar&quot;.

### Konverteringshändelse

När du skapar en ny instans i Attribution AI är ett av de obligatoriska fälten&quot;Conversion events&quot;. Konverteringshändelser är affärsmål som identifierar effekten av marknadsföringsaktiviteter, som e-handelsorder, butiksköp och webbplatsbesök.

I listrutan *Conversion Events* kan du välja någon av de händelser som är definierade för instansen för att filtrera data. Om du väljer specifika händelser ändras visualiseringarna av användargränssnittet så att endast konverteringar som tillhör dessa händelser fylls i.

![konverteringshändelse](./images/insights/conversion-event.png)

### Attributionsmodell

När du klickar på *Attribution Model* öppnas en listruta med alla olika attribueringsmodeller. Du kan välja flera modeller för att jämföra resultaten. Mer information om de olika attribueringsmodellerna och hur de fungerar finns i översikten över [Attribution AI](./overview.md) , som innehåller en tabell med information om varje modell.

![attribueringsmodell](./images/insights/attribution-model.png)

### Produkt

Med *produktfiltret* kan du välja bland de produkter som ursprungligen var inkapslade när du skapade instansen. Klicka på listrutan och använd sökfunktionen för att snabbt välja alla produkter du vill jämföra.

![produktfilter](./images/insights/product-filter.png)

### Geografi

Filtret *Geografi* fyller i landskoder som baseras på regionsbaserade modeller. Beroende på dina data kan det här filtret finnas eller inte finnas.

>[!NOTE]
>
>Landskoderna är två tecken långa. En fullständig lista finns här: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

### Län

>[!NOTE]
>
>Det här filtret finns bara om du utförde den valfria [regionbaserade modelleringen](./user-guide.md#region-based-modeling-optional) i användargränssnittsguiden för Attribution AI när du skapade tjänstinstansen.

Med det här filtret kan du markera alla områden som du har konfigurerat när du skapar instansen.

### Kanal

När du klickar på *kanalfiltret* visas en listruta med alla tillgängliga marknadsföringskanaler. Du kan välja flera kanaler för att jämföra dem.

![Kanal](./images/insights/channel.png)

### Datumintervall

Klicka på kalenderikonen för att öppna datumintervallposeraren. Början- och slutkonverteringshändelsedatumen avgör mängden data som fylls i i användargränssnittet. Du kan välja att begränsa eller utöka datumintervallet för att kunna fokusera eller utöka mängden data som fylls i.

![datumintervall](./images/insights/display-date-range.png)

## Översikt över era data

På *översiktskortet* visas det totala antalet konverteringar per attribueringsmodell. Det totala antalet ändras baserat på hur specifik sökningen är med hjälp av de filter som beskrivs tidigare i det här dokumentet. Om du väljer flera modeller läggs ytterligare cirklar till i översikten, där var och en har en egen färg som motsvarar teckenförklaringen.

![översikt](./images/insights/Overview.png)

## Trender varje vecka

Kortet *för veckotrender* delar upp din totala konvertering med det datumintervall du anger under filtreringsprocessen.

![trender](./images/insights/weekly-trends.png)

Om du klickar på ellipserna i det övre högra hörnet av ** veckostyrningskortet visas en listruta där du kan välja trender varje dag, vecka eller månad.

När du hovrar över dataraden för en viss attribueringsmodell skapas en pover som visar det totala antalet konverteringar för det datumet.

![hovringstrender](./images/insights/weekly-trend-hover.png)

## Uppdelning efter kanal

Uppdelningen *per kanal* används för att bestämma det totala antalet konverteringar i förhållande till varje kanal. Detta kort kan användas för att fatta beslut om varje kanals effektivitet och avkastningen på investeringen.

![fördelningskanal](./images/insights/channel-breakdown.png)

Om du klickar på ellipserna i det övre högra hörnet av *kortet för uppdelning efter kanal* öppnas en listruta där du kan fylla i data baserat på kontaktytor.

![kontaktytor](./images/insights/breakdown-by-touchpoints.png)

## Populära kampanjer

Kortet *Top campaign* visar en översikt över era kampanjer och hur kampanjen fungerar i varje kanal. Kortet kan hjälpa ditt team att informera om hur effektiv en viss kampanj är för en viss kanal och ge insikt i var ytterligare investeringar ska göras.

![toppkampanjer](./images/insights/top-campaigns.png)

## Nästa steg

När du är klar med filtreringen av data och kan visa lämplig information kan du välja att få åtkomst till poängen. Om du vill ha en detaljerad guide om hur du får tillgång till dina poäng kan du gå till [självstudiekursen i Attribution AI](./download-scores.md) . Dessutom kan du hämta sammanfattningsdata enligt [fler åtgärder](#more-actions). Om du väljer Hämta sammanfattningsdata hämtas sammanfattningsdata som aggregerats efter datum.

## Ytterligare resurser

Följande videofilm är utformad för att hjälpa dig att lära dig hur ni kan använda sidan med insikter om Attribution AI för att förstå avkastningen på marknadsföringskanaler och kampanjer.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)