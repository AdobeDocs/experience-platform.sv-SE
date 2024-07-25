---
keywords: Experience Platform;insikter;kundinformation;populära ämnen;kundinsikter
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Identifiera insikter med kundens AI
description: Det här dokumentet är en guide för interaktion med Service Instance Insights i användargränssnittet för AI för Intelligent Services.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 1%

---

# Upptäck insikter med kundens AI

Kundens AI, som en del av de intelligenta tjänsterna, ger marknadsförarna möjlighet att utnyttja Adobe Sensei för att förutse vad kunderna kommer att göra härnäst. Kund-AI används för att generera anpassade benägenhetspoäng som omsättning och konvertering för enskilda profiler i stor skala. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbildning eller driftsättning.

Det här dokumentet är en guide för interaktion med Service Instance Insights i användargränssnittet för AI för Intelligent Services.

## Komma igång

För att kunna utnyttja insikter om kundens AI måste du ha en tjänstinstans med status lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [Konfigurera en AI-instans för kund](./configure.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

## Översikt över tjänstinstans

I användargränssnittet för [!DNL Adobe Experience Platform] väljer du **[!UICONTROL Services]** i den vänstra navigeringen. Webbläsaren *Services* visas och visar tillgängliga intelligenta tjänster. Välj **[!UICONTROL Open]** i behållaren för kund-AI.

![Åtkomst till din instans](../images/insights/navigate-to-service.png)

Kundens AI-tjänstsida visas. På den här sidan visas tjänstinstanser för kundens AI och information om dem, inklusive namnet på instansen, typ av benägenhet, hur ofta instansen körs och status för den senaste uppdateringen.

>[!NOTE]
>
>Det är bara tjänstinstanser som har slutfört poängsättningen som har insikter.

![Skapa instans](../images/insights/dashboard.png)

Välj ett tjänstinstansnamn som ska börja.

![Skapa instans](../images/insights/click-the-name.png)

Därefter visas informationssidan för den tjänstinstansen med alternativet att välja **[!UICONTROL Latest scores]** eller **[!UICONTROL Performance summary]**. Standardfliken **[!UICONTROL Latest scores]** innehåller visualiseringar av dina data. Visualiseringarna och vad du kan göra med data beskrivs mer ingående i den här handboken.

Fliken **[!UICONTROL Performance summary]** visar de faktiska bortfall- eller konverteringsfrekvenserna för varje prioritetsbucket. Mer information finns i avsnittet [sammanfattningsmått för prestanda](#performance-metrics).

![installationssida](../images/insights/landing_page_insights.png)

## Information om tjänstinstans

Det finns två sätt att visa tjänstinstansinformation: från kontrollpanelen eller i tjänstinstansen.

### Instrumentpanel för tjänstinstans

Om du vill visa en översikt över tjänstinstansinformationen på kontrollpanelen väljer du en tjänstinstansbehållare och undviker hyperlänken som är kopplad till namnet. Då öppnas en högerrät som innehåller ytterligare information. Kontrollerna innehåller följande:

- **[!UICONTROL Edit]**: Om du väljer **[!UICONTROL Edit]** kan du ändra en befintlig tjänstinstans. Du kan redigera instansens namn, beskrivning och bedömningsfrekvens.
- **[!UICONTROL Clone]**: Om du väljer **[!UICONTROL Clone]** kopieras den valda tjänstinstansen. Du kan sedan ändra arbetsflödet för att göra mindre ändringar och byta namn på det som en ny instans.
- **[!UICONTROL Delete]**: Du kan ta bort en tjänstinstans, inklusive eventuella tidigare körningar.
- **[!UICONTROL Data source]**: En länk till datauppsättningen som används av den här instansen.
- **[!UICONTROL Run Frequency]**: Hur ofta en poängsättning utförs och när.
- **[!UICONTROL Score definition]**: En snabb översikt över målet som du konfigurerade för den här instansen.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>Om en poängkörning misslyckas visas ett felmeddelande. Felmeddelandet visas under **Information om senaste körning** i den högra listen, som bara är synlig för misslyckade körningar.

![kunde inte köra meddelandet](../images/insights/failed-run.png)

### Visa fler insikter i listrutan

Det andra sättet att visa ytterligare information för en tjänstinstans finns på sidan med insikter. Välj **[!UICONTROL Show more]** i det övre högra hörnet för att fylla i en listruta. Detaljer visas, till exempel poängdefinitionen, när den skapades, typ av benägenhet och vilka datamängder som används. Mer information om de angivna egenskaperna finns på [Konfigurera en AI-instans](./configure.md).

![visa mer](../images/insights/landing-show-more.png)

### Förhandsgranskning av AI-datauppsättning för kund

Om mer än en datauppsättning används av kundens AI anges en hyperlänk med namnet **[!UICONTROL Multiple]** följt av antalet datauppsättningar inom hakparenteser `()`.

![flera datauppsättningar](../images/insights/insights-multi-datasets.png)

Om du väljer länken för flera datauppsättningar öppnas förhandsvisningsprogrammet för kundens AI-datauppsättning. Varje färg i förhandsvisningen representerar en datauppsättning som visas av färgnyckeln till vänster om datauppsättningens kolumner. I det här exemplet ser du att bara **datauppsättningen** innehåller kolumnen `PROP1`.

![visa mer](../images/insights/dataset-preview.png)

### Redigera en instans

Om du vill redigera en instans väljer du **[!UICONTROL Edit]** i den övre högra navigeringen.

![klicka på redigeringsknappen](../images/insights/edit-button.png)

Dialogrutan Redigera visas. Du kan redigera instansens namn, beskrivning, status och bedömningsfrekvens. Om du vill bekräfta ändringarna och stänga dialogrutan väljer du **[!UICONTROL Save]** i det nedre högra hörnet.

![redigera pover](../images/insights/edit-instance.png)

### Fler åtgärder

Knappen **[!UICONTROL More actions]** finns i den övre högra navigeringen bredvid **[!UICONTROL Edit]**. Om du väljer **[!UICONTROL More actions]** öppnas en listruta där du kan välja någon av följande åtgärder:

- **[!UICONTROL Clone]**: Om du väljer **[!UICONTROL Clone]** kopieras tjänstinstansen som har konfigurerats. Du kan sedan ändra arbetsflödet för att göra mindre ändringar och byta namn på det som en ny instans.
- **[!UICONTROL Delete]**: Tar bort instansen.
- **[!UICONTROL Access scores]**: Om du väljer **[!UICONTROL Access scores]** öppnas en dialogruta med en länk till självstudiekursen [Hämta bakgrundsmusik för kund-AI](./download-scores.md). Dialogrutan innehåller även det datauppsättnings-ID som krävs för att göra API-anrop.
- **[!UICONTROL View run history]**: En dialogruta med en lista över alla poängkörningar som är associerade med tjänstinstansen visas.

![fler åtgärder](../images/insights/more-actions.png)

## Sammanfattning av poäng {#scoring-summary}

Bedömningssammanfattning visar det totala antalet profiler som poängsatts och kategoriserar dem i grupper som innehåller hög, medelhög och låg benägenhet. Propensitetsbucketerna baseras på poängintervall, låg är mindre än 24, medel är 25 till 74 och hög är över 74. Varje hink har en färg som motsvarar teckenförklaringen.

>[!NOTE]
>
>Om det är en konverteringsbenägenhetspoäng visas de höga poängen i grönt och de låga poängen i rött. Om du förutser kurvbenägenheten att detta vänds är de höga poängen röda och de låga poängen gröna. Mediefiltret förblir gult oavsett vilken typ av benägenhet du väljer.

![poängsammanfattning](../images/insights/scoring-summary.png)

Du kan hovra över en färg i ringen om du vill visa ytterligare information, till exempel ett procenttal och det totala antalet profiler som tillhör en hink.

![](../images/insights/scoring-ring.png)

## Distribution av bakgrundsmusik

Kortet **[!UICONTROL Distribution of Scores]** ger dig en visuell sammanfattning av populationen baserat på poängen. Färgerna som visas på kortet [!UICONTROL Distribution of Scores] representerar den typ av prioritetsskala som genereras. Genom att hovra över någon av poängfördelningarna får du det exakta antal som hör till den fördelningen.

![fördelning av poäng](../images/insights/distribution-of-scores.png)

## Influensafaktorer

För varje poänggrupp skapas ett kort som visar de tio viktigaste inflytelserika faktorerna för den aktuella bucket. Inflytelserika faktorer ger er ytterligare information om varför era kunder tillhör olika poänggrupper.

![Influensafaktorer](../images/insights/influential-factors.png)

### Influentiella faktornivåreglagen

När du hovrar över någon av de viktigaste inflytelserika faktorerna bryts data ytterligare. Du får en översikt över varför vissa profiler tillhör en benägenhetsklocka. Beroende på faktorn kan du få tal, kategoriserade värden eller booleska värden. I exemplet nedan visas kategoriska värden per region.

![detaljbild, bild](../images/insights/drilldown.png)

Dessutom kan du använda drolldowns för att jämföra en fördelningsfaktor om den förekommer i två eller flera benägenhetsintervall och skapa mer specifika segment med dessa värden. I följande exempel visas det första användningsfallet:

![](../images/insights/drilldown-compare.png)

Du ser att det är mindre troligt att profiler med låg benägenhet att konvertera har gjort ett besök på adobe.com webbsidor nyligen. Faktorn&quot;Dagar sedan senaste webVisit&quot; har bara 8 % täckning jämfört med 26 % i medelstora prioritetsprofiler. Med hjälp av dessa tal kan du jämföra fördelningen inom varje hink för faktorn. Den här informationen kan användas för att dra slutsatsen att den senaste webbbesöket inte har lika stor inverkan på den låga benägenhetsknappen som den är i en större benägenhetsklocka.

### Skapa ett segment

Om du väljer knappen **[!UICONTROL Create Segment]** i någon av bucketerna för låg, medelhög och hög benägenhet omdirigeras du till segmentbyggaren.

>[!NOTE]
>
>Knappen **[!UICONTROL Create Segment]** är bara tillgänglig om kundprofilen i realtid är aktiverad för datauppsättningen. Mer information om hur du aktiverar kundprofilen i realtid finns i [Översikt över kundprofilen i realtid](../../../rtcdp/overview.md).

![Klicka på Skapa segment](../images/insights/influential-factors-create-segment.png)

![Skapa ett segment](../images/insights/create-segment.png)

Segmentverktyget används för att definiera ett segment. När du väljer **[!UICONTROL Create Segment]** från Insights-sidan lägger Customer AI automatiskt till den valda bucketinformationen i segmentet. Fyll i behållarna **Namn** och **Beskrivning** som finns till höger i segmentbyggarens användargränssnitt för att slutföra segmentskapandet. När du har gett segmentet ett namn och en beskrivning väljer du **[!UICONTROL Save]** längst upp till höger.

>[!NOTE]
>
>Eftersom benägenhetspoängen skrivs till den enskilda profilen är de tillgängliga i segmentbyggaren som andra profilattribut. När du navigerar till segmentbyggaren för att skapa nya segment kan du se alla olika benägenhetspoäng under din namnområdes-AI för kunder.

![Segmentfyllning i](../images/insights/segment-saving.png)

Om du vill visa det nya segmentet i plattformsgränssnittet väljer du **[!UICONTROL Segments]** i den vänstra navigeringen. Sidan **[!UICONTROL Browse]** visas och visar alla tillgängliga segment.

![Alla dina segment](../images/insights/Segments-dashboard.png)

## Historiska prestanda {#historical-performance}

Fliken **[!UICONTROL Performance summary]** visar de faktiska bortfall- eller konverteringsfrekvenserna, indelade i de olika benägenhetsintervall som anges av kundens AI.

![Fliken Resultatsammanfattning](../images/insights/summary_tab.png)

Inledningsvis visas bara förväntade frekvenser (prickade linjer). Förväntade hastigheter visas när en poängkörning inte har utförts och data ännu inte är tillgängliga. När ett resultatfönster har passerat ersätts den förväntade hastigheten med en faktisk hastighet (heldragen linje).

När du hovrar över raderna visas datumet och den faktiska/förväntade frekvensen för den dagen i den hakparken.

![Exempel på pyts](../images/insights/churn_tab.png)

Du kan filtrera tidsramen för de förväntade och faktiska frekvenserna som visas. Välj **kalenderikonen** ![ikonen](/help/images/icons/calendar.png)och välj sedan ett nytt datumintervall. Resultaten i varje bucket uppdateras för att visas inom det nya datumintervallet.

![Datumväljare](../images/insights/date_selector.png)

### Enskilda poängsättningsgrader

I den nedre halvan av fliken **[!UICONTROL Performance summary]** visas resultatet för varje enskild poängkörning. Välj listdatumet i det övre högra hörnet om du vill visa resultat för en annan poängkörning.

Beroende på om du förutser kurvor eller konverteringar visar diagrammet [!UICONTROL Distribution of Scores] fördelningen av profiler som kurvats/konverterats och inte kurvkonverterats/inte konverterats i varje steg.

![individuell poängsättning](../images/insights/scoring_tab.png)

## Modellutvärdering {#model-evaluation}

Förutom att följa upp de förväntade och faktiska resultaten över tid på fliken Historiska prestanda har marknadsförarna ännu större transparens över modellkvalitet på fliken Modellutvärdering. Du kan använda diagrammen Lyft och Vinst för att avgöra skillnaderna när det gäller att använda en prediktiv modell jämfört med målinriktning slumpmässigt. Dessutom kan du bestämma hur många positiva utfall som ska tas vid varje poängutfall. Detta är användbart för segmentering och för att anpassa avkastningen på investeringar till marknadsföringsåtgärder.

### Lyft diagram

![lyfta diagram](../images/user-guide/lift-chart.png)

Lyftdiagrammet mäter förbättringen av användningen av en prediktiv modell i stället för slumpmässig målinriktning.

Exempel på indikatorer för högkvalitetsmodeller är:

- Höga höjdvärden i de första decimalerna. Det innebär att modellen är bra på att identifiera de användare som har störst benägenhet att vidta intressanta åtgärder.
- Fallande lyftvärden. Det innebär att kunder med högre poäng är mer benägna att vidta intressanta åtgärder än personer med lägre poäng.

### Vinster

![vinstdiagram](../images/user-guide/gains-chart.png)

Diagrammet över kumulativa vinster mäter andelen positiva resultat som erhållits genom målresultat över ett visst tröskelvärde. Efter att ha sorterat kunderna efter benägenhetspoäng från hög till låg delas populationen in i deciler - 10 lika stora grupper. En perfekt modell skulle fånga alla positiva utfall i de högsta poängdecimalerna. En målinriktningsmetod som baslinje hämtar positiva resultat proportionellt mot gruppens storlek - 30 % av användarna fångar 30 % av resultaten.

Exempel på indikatorer för högkvalitetsmodeller är:

- De kumulativa vinsterna når upp till 100 % snabbt.
- Den kumulativa kurvan för modellen ligger närmare diagrammets övre vänstra hörn.
- Diagrammet över kumulativa vinster kan användas för att fastställa poängbortfall för segmentering och målinriktning. Om modellen till exempel fångar 70 % av de positiva resultaten i de två första poängen kommer målgruppsanvändare med PercentileScore > 80 att förväntas fånga upp cirka 70 % av de positiva resultaten.

### AUC (yta under kurvan)

AUC återspeglar styrkan i relationen mellan rangordningen efter poäng och förekomsten av det förväntade målet. En **AUC** på 0,5 betyder att modellen inte är bättre än en slumpmässig gissning. En **AUC** på 1 innebär att modellen kan förutsäga exakt vem som ska utföra den relevanta åtgärden.

## Nästa steg

I det här dokumentet beskrevs de insikter som en kundens AI-tjänstinstans har gett. Du kan nu fortsätta med självstudiekursen om att [hämta poäng i kundens AI](./download-scores.md) eller gå till de andra [Adobe Intelligent Services](../../home.md)-guiderna som erbjuds.

## Ytterligare resurser

I följande videofilm visas hur du använder AI från kunder för att se resultatet av modellerna och de inflytelserika faktorerna.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
