---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilpanel;instrumentpanel
title: Kontrollpanel för profiler
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid för din organisation.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 7ca40776747541615e1a1d717aae8d48bed27a74
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 0%

---

# [!UICONTROL Profiles] kontrollpanel

I Adobe Experience Platform användargränssnitt finns en kontrollpanel där du kan visa viktig information om ditt [!DNL Real-time Customer Profile] data, enligt vad som tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med [!UICONTROL Profiles] kontrollpanelen i användargränssnittet och ger information om de mått som visas på kontrollpanelen.

En översikt över alla profilfunktioner i användargränssnittet i Experience Platform finns på [Användargränssnittsguide för kundprofiler i realtid](../../profile/ui/user-guide.md).

## Data för kontrollpanel för profil

The [!UICONTROL Profiles] På kontrollpanelen visas en ögonblicksbild av de attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för profiler uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska [!UICONTROL Profiles] kontrollpanel

Navigera till [!UICONTROL Profiles] kontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra listen väljer du **[!UICONTROL Overview]** för att visa kontrollpanelen.

>[!NOTE]
>
>Om din organisation inte har använt Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanfogningsprinciper har skapats kan [!UICONTROL Profiles] Kontrollpanelen visas inte. I stället [!UICONTROL Overview] På fliken visas länkar och dokumentation som hjälper dig att komma igång med kundprofilen i realtid.

![](../images/profiles/dashboard-overview.png)

### Ändra [!UICONTROL Profiles] kontrollpanel

Du kan ändra utseendet på [!UICONTROL Profiles] kontrollpanel genom att välja **[!UICONTROL Modify dashboard]**. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt få tillgång till **[!UICONTROL Widget library]** för att utforska tillgängliga widgetar och skapa anpassade widgetar för din organisation.

Se [ändra kontrollpaneler](../customize/modify.md) och [widgetbibliotek - översikt](../customize/widget-library.md) dokumentation som lär dig mer.

## (Beta) Profileffektivitetsinsikter {#profile-efficacy-insights}

>[!IMPORTANT]
>
>Profilens insiktsfunktion finns för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

The [!UICONTROL Efficacy] på fliken finns mått på kvaliteten och fullständigheten hos dina profildata som grundligt bygger på widgetar för profileffektivitet. De här widgetarna visar i korthet hur profilerna är uppbyggda, trender för fullständighet över tiden och bedömningar av kvaliteten på profildata.

![Kontrollpanelen för profileffektivitet.](../images/profiles/attributes-quality-assessment.png)

Se [profileffektwidgetar](#profile-efficacy-widgets) om du vill ha mer information om de widgetar som är tillgängliga just nu.

Layouten på den här instrumentpanelen kan även anpassas genom att välja [**[!UICONTROL Modify dashboard]**](../customize/modify.md) från [!UICONTROL Overview] -fliken.

## Bläddra bland profiler {#browse-profiles}

The [!UICONTROL Browse] kan du söka efter och visa de skrivskyddade profiler som har importerats till din IMS-organisation. Härifrån kan du se viktig information som hör till profilen om deras inställningar, tidigare händelser, interaktioner och segment

Mer information om profilvisningsfunktionerna i plattformsgränssnittet finns i dokumentationen om [webbläsarprofiler i Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Sammanfoga profiler {#merge-policies}

De mått som visas i [!UICONTROL Profiles] Instrumentpanelen baseras på sammanslagningsprinciper som tillämpas på dina kundprofildata i realtid. När data samlas in från flera olika källor för att skapa kundprofilen är det möjligt att data innehåller motstridiga värden (en datauppsättning kan till exempel lista en kund som&quot;enkel&quot; medan en annan datauppsättning kan lista kunden som&quot;gift&quot;). Det är huvudsyftet med sammanfogningsprincipen att avgöra vilka data som ska prioriteras och visas som en del av profilen.

Mer information om kopplingsprofiler, inklusive hur du skapar, redigerar och deklarerar en standardkopplingsprofil för din organisation, får du genom att läsa [sammanfogningsprinciper - översikt](../../profile/merge-policies/overview.md).

The dashboard will automatically select a merge policy to display, but you can change the merge policy that is selected using the drop down menu. Om du vill välja en annan sammanfogningsprincip markerar du listrutan bredvid sammanfogningsprincipnamnet och väljer sedan den sammanfogningsprincip som du vill visa.

>[!NOTE]
>
>I listrutan visas endast sammanfogningsprinciper som är relaterade till den enskilda klassen för XDM-profiler, men om din organisation har skapat flera sammanfogningsprinciper kan det innebära att du måste rulla för att kunna visa den fullständiga listan över tillgängliga sammanfogningsprinciper.

![](../images/profiles/select-merge-policy.png)

## Union schemas

The [!UICONTROL Union Schema] På kontrollpanelen visas unionsschemat för en viss XDM-klass. Genom att välja [!UICONTROL **Klass**] kan du visa föreningsscheman för olika XDM-klasser.

Unionsscheman består av flera scheman som delar samma klass och har aktiverats för profilen. Med dem kan du i en enda vy se en sammanslagning av alla fält i varje schema som delar samma klass.

See the union schema UI guide to learn more about [viewing union schemas within the Platform UI](../../profile/ui/union-schema.md#view-union-schemas).

## Widgetar och mätvärden

The dashboard is composed of widgets, which are read-only metrics providing important information regarding your Profile data.

Datum och tid för den senaste uppdateringen av en widget visar när den senaste ögonblicksbilden av data togs. Datum och tid för ögonblicksbilden anges i UTC. den inte finns i den enskilda användarens eller IMS-organisationens tidszon.

## Standardwidgetar

Adobe tillhandahåller flera standardwidgetar som du kan använda för att visualisera olika mått som relaterar till dina profildata. Du kan också skapa anpassade widgetar som ska delas med din organisation med hjälp av [!UICONTROL Widget library]. Om du vill veta mer om hur du skapar anpassade widgetar börjar du med att läsa [widgetbibliotek - översikt](../customize/widget-library.md).

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles count trend]](#profiles-count-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Single Identity Profiles]](#single-identity-profiles)
* [[!UICONTROL Unsegmented Profiles]](#unsegmented-profiles)
* [[!UICONTROL Unsegmented Profiles] Trend](#unsegmented-profiles-trend)
* [[!UICONTROL Unsegmented Profiles by Identity]](#unsegmented-profiles-by-identity)

### [!UICONTROL Profile count] {#profile-count}

The **[!UICONTROL Profile count]** visar det totala antalet sammanfogade profiler i profilarkivet när ögonblicksbilden togs. Det här numret är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

>[!NOTE]
>
>The [!UICONTROL Profile count] widget may show a different number than the profile count shown on the [!UICONTROL Browse] tab in the [!UICONTROL Profiles] section of the UI for multiple reasons. Den vanligaste orsaken är att [!UICONTROL Browse] -fliken refererar till det totala antalet sammanfogade profiler baserat på organisationens standardpolicy för sammanfogning, medan [!UICONTROL Profile count] widgeten refererar till det totala antalet sammanfogade profiler baserat på den sammanfogningsprincip som du har valt att visa på kontrollpanelen.
>
>En annan vanlig orsak är att det finns skillnader mellan tidpunkten då instrumentpanelsögonblicksbilden tas och tidpunkten då exempeljobbet körs för [!UICONTROL Browse] -fliken. Du kan se när [!UICONTROL Profile count] widgeten uppdaterades senast genom att titta på tidsstämpeln i widgeten och lära dig mer om hur exempeljobbet utlöses på [!UICONTROL Browse] -fliken finns i [profilräknaren i användargränssnittsguiden för kundprofiler i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

The **[!UICONTROL Profiles added]** visar det totala antalet sammanfogade profiler som har lagts till i profilarkivet vid den senaste ögonblicksbilden som togs. This number is the result of the selected merge policy being applied to your Profile data in order to merge profile fragments together to form a single profile for each individual. You can use the dropdown selector to view the profiles added over the last 30 days, 90 days, or 12 months.

>[!NOTE]
>
>The [!UICONTROL Profiles added] widgeten visar antalet profiler som har lagts till efter att profilarkivet har konfigurerats och profiler har importerats. Med andra ord: om din organisation konfigurerade profilarkivet och importerade 4 000 000 Dag 1 är kontrollpanelen tillgänglig inom 24 timmar, men [!UICONTROL Profiles added] widgeten ställs in på 0. Detta görs för att undvika en topp som uppstår i samband med det initiala intaget av profiler i systemet. Under de kommande 30 dagarna har din organisation importerat ytterligare 1 000 000 profiler till Profilarkivet. När nästa ögonblicksbild tagits visas [!UICONTROL Profiles added] visar totalt 1 000 000 profiler, medan [!UICONTROL Profile count] widgeten visar totalt 5 000 000 profiler.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles count trend] {#profiles-count-trend}

The **[!UICONTROL Profiles count trend]** visar det totala antalet sammanfogade profiler som har lagts till i profilarkivet dagligen de senaste 30 dagarna, 90 dagar eller 12 månaderna. Detta nummer uppdateras varje dag som ögonblicksbilden tas, och om du vill importera profiler till Platform kommer antalet profiler inte att visas förrän nästa ögonblicksbild tas. Antalet tillagda profiler är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

The **[!UICONTROL Profile count trend]** widgeten visar en knapp för bildtexter i widgetens övre högra hörn. Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![The Profile overview tab displaying the Profiles count trend widget with the captions button highlighted.](../images/profiles/profile-count-trend-captions.png)

A machine learning model automatically generates captions for describing the key trends and important events by analyzing the chart and the data.

![The automatic captions dialog for the Profiles count trend widget.](../images/profiles/profiles-count-trends-automatic-captions-dialog.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

The **[!UICONTROL Profiles by identity]** widgeten visar en beskrivning av identiteterna för alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per identitet (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kan vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

The **[!UICONTROL Identity overlap]** widgeten visar ett Venndiagram, eller ett uppsättningsdiagram, som visar överlappningen mellan profiler i din profilbutik som innehåller flera identiteter.

När du har använt listrutemenyerna i widgeten för att markera de identiteter som du vill jämföra, visas cirklar med den relativa storleken för varje identitet. Antalet profiler som innehåller båda namnutrymmena representeras av storleken på överlappningen mellan cirklarna. Om en kund interagerar med ert varumärke i mer än en kanal kopplas flera identiteter till den enskilda kunden, och därför är det troligt att organisationen har flera profiler som innehåller fragment från mer än en identitet.

Mer information om profilfragment får du om du börjar med att läsa avsnittet om [profilfragment jämfört med sammanslagna profiler](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) i realtidsöversikten över kundprofiler.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

### [!UICONTROL Single Identity Profiles] {#single-identity-profiles}

The [!UICONTROL Single Identity Profiles] widgeten innehåller ett antal profiler för din organisation som bara har en typ av ID-typ som skapar deras identitet. Den här ID-typen kan antingen vara ett e-postmeddelande eller ett ECID. Profilantalet genereras från data i den senaste ögonblicksbilden.

![Widgeten för profiler för en identitet.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Unsegmented Profiles] {#unsegmented-profiles}

The [!UICONTROL Unsegmented Profiles] innehåller det totala antalet profiler som inte är kopplade till något segment. Det genererade numret är korrekt vid den senaste ögonblicksbilden och representerar möjligheten till profilaktivering i hela organisationen. Det visar också möjligheten att utvinna profiler som inte ger tillräcklig avkastning.

![Widgeten Osegmenterade profiler.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Unsegmented Profiles Trend] {#unsegmented-profiles-trend}

The [!UICONTROL Unsegmented Profiles Trend] innehåller en illustration av linjediagram för antalet profiler som inte är kopplade till något segment under en viss tidsperiod. The trend of profiles not attached to any segment can be visualized over 30 days, 90 days, and 12 month periods. Tidsperioden väljs i en listruta i widgeten. Profilantalet återspeglas i y-axeln och tiden på x-axeln.

![Widgeten Trend för osegmenterade profiler.](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL Unsegmented Profiles by Identity] (#unsegmented-profiles-by-identity)

The [!UICONTROL Unsegmented Profiles by Identity] widgeten kategoriserar det totala antalet osegmenterade profiler efter deras unika identifierare. Data visas i ett stapeldiagram för att underlätta jämförelse.

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png)

## (Beta) Profileffektwidgetar {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>Widgetarna för profileffekt finns för närvarande i Beta och är inte tillgängliga för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe tillhandahåller flera widgetar för att bedöma om de kapslade profilerna som finns tillgängliga för dataanalysen är fullständiga. Var och en av profilens effektwidgetar kan filtreras efter sammanfogningspolicy. Om du vill ändra kopplingsprofilfiltret väljer du[!UICONTROL Profiles using merge policy] och välj en lämplig profil i listan.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attribute-quality-assessment)
* [[!UICONTROL Profile completeness]](#profile-completeness)
* [[!UICONTROL Profile completeness trend]](#profile-completeness-trend)

### (Beta) [!UICONTROL Attribute quality assessment] {#attribute-quality-assessment}

Den här widgeten visar fullständigheten och kardinaliteten för varje profilattribut sedan det senaste bearbetningsdatumet. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Kolumn | Beskrivning |
|---|---|
| Attribut | The name of the attribute. |
| Profiler | The number of profiles that have this attribute and are filled with non-null values. |
| Fullständighet | Procentandelen bestäms av det totala antalet profiler som har det här attributet och som fylls med värden som inte är null. Talet beräknas genom att det totala antalet profiler divideras med det totala antalet icke-tomma värden i profilerna för det attributet. |
| Kardinalitet | Det totala antalet **unik** värden som inte är null för det här attributet. Den mäts över alla profiler. |

![Attribut för kvalitetsbedömningswidgeten](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profile-completeness}

This widget creates a circle chart of profile completeness since the last processing date. En profils fullständighet mäts av procentandelen attribut som är fyllda med värden som inte är null bland alla observerade attribut.

Den här widgeten visar andelen profiler som är av hög, medelhög eller låg fullständighet. By default, there are three levels of completeness configured:

* High completeness: Profiles have more than 70% of attributes filled.
* Medelfullständighet: Profiler har mindre än 70 % och mer än 30 % av attributen är ifyllda.
* Låg fullständighet: Profiler har mindre än 30 % av attributen ifyllda.

![Widgeten för profiler efter fullständighets](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profile completeness trend] {#profile-completeness-trend}

This widget creates a stacked column chart to depict the trend of profile completeness over time. Fullständigheten mäts i procent av attributen som fylls med värden som inte är null bland alla observerade attribut. Den klassar profilens fullständighet som hög, medelhög eller låg sedan det senaste bearbetningsdatumet.

X-axeln representerar tid, y-axeln representerar antalet profiler och färgerna representerar de tre nivåerna för profilens fullständighet.

De tre nivåerna av fullständighet är följande:

* Hög fullständighet: Profiler har mer än 70 % av attributen ifyllda.
* Medelfullständighet: Profiler har mindre än 70 % och mer än 30 % av attributen är ifyllda.
* Low completeness: Profiles have less than 30% of attributes filled.

![Trendwidgeten för profiler](../images/profiles/profiles-completeness-trend.png)

## Nästa steg

By following this document you should now be able to locate the Profiles dashboard and understand the metrics displayed in the available widgets. Mer information om att arbeta med [!DNL Profile] data i användargränssnittet för Experience Platform, se [Användargränssnittsguide för kundprofiler i realtid](../../profile/ui/user-guide.md).
