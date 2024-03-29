---
title: Kontrollpanelshandbok för kontoprofiler
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om din organisations B2B-kontoprofiler.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# [!UICONTROL Account Profiles] kontrollpanel

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om dina kontoprofiler, som de tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med [!UICONTROL Account Profiles] kontrollpanelen i användargränssnittet och ger mer information om de visualiseringar som visas på kontrollpanelen.

En översikt över alla funktioner i användargränssnittet för kontoprofilen finns på [gränssnittshandbok för kontoprofil](../../rtcdp/accounts/account-profile-ui-guide.md).

## Komma igång

Du måste ha rätt till [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) för att få tillgång till B2B [!UICONTROL Account Profiles] kontrollpanel.

## Data för kontoprofiler

The [!UICONTROL Account Profiles] På kontrollpanelen visas en ögonblicksbild av enhetlig kontoinformation från olika källor över alla era marknadsföringskanaler och de olika system som organisationen för närvarande använder för att lagra kundkontoinformation.

Profildata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Med andra ord är ögonblicksbilden inte en uppskattning eller ett urval av data, och [!UICONTROL Account Profiles] Kontrollpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska [!UICONTROL Account Profiles] kontrollpanel

Navigera till [!UICONTROL Account Profiles] kontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** under [!UICONTROL Accounts] i den vänstra navigeringspanelen.

![Plattformsgränssnittet med kontoprofiler i den vänstra navigeringen är markerat och fliken Översikt visas.](../images/account-profiles/account-profiles-dashboard.png)

Från [!UICONTROL Account Profiles] kontrollpanel kan du antingen [bläddra bland de kontoprofiler som är insamlade i din organisation](#browse-account-profiles), eller [visa alla dina kontouppgifter i en översikt med widgetar](#standard-widgets) som visualiserar olika aspekter av data.

## Bläddra bland kontoprofiler {#browse-account-profiles}

The [!UICONTROL Browse] Med -fliken kan du söka efter och visa de skrivskyddade kontoprofiler som har hämtats till din organisation med ett konto-ID från en ansluten företagskälla eller genom att ange källinformation direkt. Härifrån kan du se viktig information som hör till kontoprofilen, bland annat namn, bransch, intäkter och målgrupp.

Välj [!UICONTROL Profile ID] från resultaten som visas på [!UICONTROL Browse] för att öppna [!UICONTROL Details] för kontoprofilen.

![Fliken Kontoprofiler bläddrar med resultat visade och profil-ID markerat.](../images/account-profiles/account-profiles-browse-tab.png)

Kontoprofilinformationen som visas på [!UICONTROL Details] har sammanfogats från flera profilfragment till en enda vy av det enskilda kontot. Läs dokumentationen om [surfkontoprofiler i Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) om du vill veta mer om visningsfunktioner för kontoprofiler i användargränssnittet för plattformen.

## The [!UICONTROL Account Profiles] [!UICONTROL Overview] {#overview}

The [!UICONTROL Overview] -fliken består av widgetar som tillhandahåller skrivskyddade mätvärden för att förmedla viktig information om dina kontoprofiler. Välj **[!UICONTROL Modify dashboard]** för att ändra utseendet på [!UICONTROL Overview] genom att flytta och ändra storlek på widgetar.

![Fliken Översikt över kontoprofiler med kontrollpanelen Ändra markerad.](../images/account-profiles/modify-dashboard.png)

Se dokumentet på [ändra kontrollpaneler](../customize/modify.md) och [Översikt över widgetbiblioteket](../customize/widget-library.md) om du vill veta mer.

## Standardwidgetar {#standard-widgets}

Adobe tillhandahåller standardwidgetar som du kan använda för att visualisera olika mätvärden för dina kontoprofiler.

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [Totalt antal konton per bransch](#total-accounts-by-industry)
* [Kontoprofiler har lagts till](#account-profiles-added)
* [Förutsägbar poängfördelning](#predictive-scoring-distribution)
* [Prediktiv bedömning av viktiga faktorer](#predictive-scoring-top-influential-factors)

### Totalt antal konton per bransch {#total-accounts-by-industry}

Den här widgeten visar det totala antalet konton i ett enskilt mätresultat och använder ett dondiagram för att illustrera de proportionella räkningsstorlekarna för de branscher som utgör det totala antalet. Nyckeln ger färgkodningsinformation för de olika branscherna som donationsdiagrammet består av.

Individuella värden för de olika branscherna visas i en dialogruta när markören hålls över respektive avsnitt i mundiagrammet.

![Det totala antalet konton per bransch-widget.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Kontoprofiler har lagts till {#account-profiles-added}

Den här widgeten använder ett färgkodat stapeldiagram för att illustrera antalet profiler som lagts till i ett konto under en viss tidsperiod och andelen olika branscher som utgör de tillagda profilerna. Branscherna är färgkodade och en nyckel innehåller färgkodningsinformation för de olika branscherna som stapeldiagrammet består av. Analysperioden väljs i widgetens listruta. Du kan visualisera stapeldiagrammet över en 30-dagars, 90-dagars och en 12-månadersperiod.

>[!NOTE]
>
>Eftersom profiler bara läggs till i ett konto och aldrig tas bort är det lägsta möjliga antalet profiler som läggs till under en tidsperiod noll.

![Kontoprofilerna har lagt till widget.](../images/account-profiles/accounts-profiles-added-widget.png)

### Förutsägbar poängfördelning {#predictive-scoring-distribution}

The [!UICONTROL Predictive scoring distribution] widgeten visar poängdistributionen för alla kontoprofiler så att du snabbt kan förstå hur din säljpipeline mår. Poängdata förmedlas via ett mundiagram och ett kolumndiagram.

I donutdiagrammet visas andelen av dina totala kontoprofiler i var och en av de stora, medelstora och låga benägenheterna att köpa bucklar. Nyckeln ger mer information om de färgkodade avsnitten, inklusive poängintervallen och antalet kontoprofiler i intervallet.

Kolumndiagrammet ger en mer detaljerad resultatfördelning. Varje kolumn visar antalet kontoprofiler i var och en av de 20 fempunktsökningsgrupperna.

I listrutan i widgeten kan du välja kontobedömningsmodellen.

![Widgeten Predictive scoring distribution.](../images/account-profiles/predictive-scoring-distribution.png)

### Prediktiv bedömning av viktiga faktorer {#predictive-scoring-top-influential-factors}

The [!UICONTROL Predictive scoring top influential factors] widgeten hjälper dig att förstå de viktigaste faktorerna som driver poängen för varje benägenhetspyts.

Den här widgeten visar de viktigaste inflytelserika faktorerna för de stora, medelstora och låga benägenhetsintervallen. En stapel för varje inflytelserik faktor anger den procentandel av kontoprofilerna i den benägenhetspytsen som innehåller den specifika inflytelserika faktorn.

I listrutan i widgeten kan du välja kontobedömningsmodellen.

![Widgeten Predictive scoring top influential factor.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Nästa steg

Om du följer det här dokumentet bör du nu veta hur du hittar [!UICONTROL Account Profiles] kontrollpanel. Du bör också förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med kontoprofiler som en del av dina B2B-data i användargränssnittet för Experience Platform finns i [kontoprofilöversikt](../../rtcdp/accounts/account-profile-overview.md) för Adobe Real-Time CDP, B2B Edition.
