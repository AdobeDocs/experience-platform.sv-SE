---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilpanel;instrumentpanel
title: Instrumentpanelshandbok för profiler
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid för din organisation.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: a28c1c00fd0b33af3b797ecf2b4d45154dedc823
workflow-type: tm+mt
source-wordcount: '3166'
ht-degree: 0%

---

# [!UICONTROL Profiles] kontrollpanel

I Adobe Experience Platform användargränssnitt finns en kontrollpanel där du kan visa viktig information om ditt [!DNL Real-Time Customer Profile] data, enligt vad som tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med profilkontrollpanelen i användargränssnittet, och den innehåller information om de mått som visas på kontrollpanelen.

En översikt över alla profilfunktioner i användargränssnittet i Experience Platform finns i [Användargränssnittsguide för kundprofil i realtid](../../profile/ui/user-guide.md).

## Data för kontrollpanel för profil

På profilpanelen visas en ögonblicksbild av attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för profiler uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen Profiler

Om du vill navigera till profilkontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra listen väljer du **[!UICONTROL Overview]** för att visa kontrollpanelen.

>[!NOTE]
>
>Om din organisation inte har använt plattformen tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanslagningsprinciper skapade, visas inte instrumentpanelen för profiler. I stället [!UICONTROL Overview] På fliken visas länkar och dokumentation som hjälper dig att komma igång med kundprofilen i realtid.

![Kontrollpanelen för profiler i Experience Platform med profiler och översikt markerad.](../images/profiles/dashboard-overview.png)

### Ändra kontrollpanelen för profiler

Du kan ändra utseendet på profilkontrollpanelen genom att välja **[!UICONTROL Modify dashboard]**. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt få tillgång till **[!UICONTROL Widget library]** för att utforska tillgängliga widgetar och skapa anpassade widgetar för din organisation.

Se [ändra kontrollpaneler](../customize/modify.md) och [Översikt över widgetbiblioteket](../customize/widget-library.md) dokumentation som lär dig mer.

### Lägg till widgetar {#add-widget}

Välj **[!UICONTROL Add widget]** för att navigera till widgetbiblioteket och se en lista över tillgängliga widgetar att lägga till på din instrumentpanel.

![Panelen Profiler med widgeten markerad.](../images/profiles/profiles-overview-add-widget.png)

I widgetbiblioteket kan du bläddra genom urvalet av standardwidgetar och anpassade segmentwidgetar.Mer information om hur du lägger till widgetar finns i dokumentationen för widgetbiblioteket. [lägga till en widget](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Bläddra bland profiler {#browse-profiles}

The [!UICONTROL Browse] Med -fliken kan du söka efter och visa de skrivskyddade profiler som är inkapslade i din organisation. Härifrån kan du se viktig information som hör till profilen om deras inställningar, tidigare händelser, interaktioner och segment

Mer information om profilvisningsfunktionerna i plattformsgränssnittet finns i dokumentationen om [webbläsarprofiler i Adobe Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Sammanfoga profiler {#merge-policies}

De mätvärden som visas på profilpanelen baseras på sammanslagningsprinciper som tillämpas på dina kundprofildata i realtid. När data samlas in från flera källor för att skapa kundprofilen kan data innehålla värden som är i konflikt. En datauppsättning kan till exempel visa en kund som&quot;enkel&quot; medan en annan datauppsättning kan visa kunden som&quot;gift&quot;. Det är huvudsyftet med sammanfogningsprincipen att avgöra vilka data som ska prioriteras och visas som en del av profilen.

Mer information om kopplingsprofiler, inklusive hur du skapar, redigerar och deklarerar en standardkopplingsprofil för din organisation, finns i [sammanfogningsprinciper - översikt](../../profile/merge-policies/overview.md).

Kontrollpanelen väljer automatiskt vilken sammanfogningsprincip som ska användas. Den tillämpade sammanfogningsprincipen kan ändras med hjälp av listrutan bredvid sammanfogningsprincipens namn.

>[!NOTE]
>
>I listrutan visas endast sammanfogningsprinciper som använder `_xdm.context.profile` schema. Om din organisation har skapat flera sammanfogningsprinciper kan det dock innebära att du måste rulla för att kunna visa den fullständiga listan över tillgängliga sammanfogningsprinciper.

![Fliken Profiler - översikt med listrutan Sammanslagningsprincip markerad.](../images/profiles/select-merge-policy.png)

## Unionens system

The [!UICONTROL Union Schema] På kontrollpanelen visas unionsschemat för en viss XDM-klass. Genom att välja **[!UICONTROL Class]** kan du visa föreningsscheman för olika XDM-klasser.

Unionsscheman består av flera scheman som delar samma klass och har aktiverats för profilen. Med dem kan du i en enda vy se en sammanslagning av alla fält i varje schema som delar samma klass.

Läs användargränssnittsguiden för unionsschemat om du vill veta mer om [visa fackscheman i plattformsgränssnittet](../../profile/ui/union-schema.md#view-union-schemas).

## Widgetar och mätvärden

Kontrollpanelen består av widgetar, som är skrivskyddade mått som ger viktig information om dina profildata.

Datum och tid för den senaste ögonblicksbilden visas högst upp i [!UICONTROL Overview] bredvid listrutan för sammanfogningsprinciper. Alla widgetdata är korrekta från och med det datumet och den tidpunkten. Tidsstämpeln för ögonblicksbilden anges i UTC. det ligger inte i den enskilda användarens eller organisationens tidszon.

![På fliken Profiles dashboard overview med den senaste tidsstämpeln för ögonblicksbilder markerad.](../images/profiles/snapshot-timestamp.png)

## Standardwidgetar {#standard-widgets}

Adobe tillhandahåller flera standardwidgetar som du kan använda för att visualisera olika mått som relaterar till dina profildata. Du kan också skapa anpassade widgetar som ska delas med din organisation med hjälp av [!UICONTROL Widget library]. Om du vill veta mer om hur du skapar anpassade widgetar börjar du med att läsa [Översikt över widgetbiblioteket](../customize/widget-library.md).

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profile count trend]](#profile-count-trend)
* [[!UICONTROL Profile count change]](#profile-count-change)
* [[!UICONTROL Profiles count change trend]](#profiles-count-change-trend)
* [[!UICONTROL Profiles count change trend by identity]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Single identity profiles]](#single-identity-profiles)
* [[!UICONTROL Single identity profiles by identity]](#single-identity-profiles-by-identity)
* [[!UICONTROL Unsegmented profiles]](#unsegmented-profiles)
* [[!UICONTROL Unsegmented profiles change trend]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Unsegmented profiles by identity]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiences]](#audiences)
* [[!UICONTROL Audiences mapped to destination status]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Audiences size]](#audiences-size)
* [[!UICONTROL Audience overlap by merge policy]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Audience overlap report]](#audience-overlap-report)

### [!UICONTROL Profile count] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Profilantal"
>abstract="Den här widgeten visar det totala antalet sammanfogade profiler i profilarkivet när ögonblicksbilden togs. Numret beror på den valda sammanfogningsprincipen som tillämpas på dina profildata."

The **[!UICONTROL Profile count]** visar det totala antalet sammanfogade profiler i profilarkivet när ögonblicksbilden togs. Det här numret är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

>[!NOTE]
>
>The [!UICONTROL Profile count] widgeten kan visa ett annat nummer än det antal profiler som visas på [!UICONTROL Browse] i [!UICONTROL Profiles] av flera anledningar. Den vanligaste orsaken till detta är att [!UICONTROL Browse] -fliken refererar till det totala antalet sammanfogade profiler baserat på organisationens standardpolicy för sammanfogning, medan [!UICONTROL Profile count] widgeten refererar till det totala antalet sammanfogade profiler baserat på den sammanfogningsprincip som du har valt att visa på kontrollpanelen.
>
>En annan vanlig orsak är att det finns skillnader mellan tidpunkten då instrumentpanelsögonblicksbilden tas och tidpunkten då exempeljobbet körs för [!UICONTROL Browse] -fliken. Du kan se när [!UICONTROL Profile count] widgeten uppdaterades senast genom att titta på tidsstämpeln i widgeten. Om du vill veta mer om hur exempeljobbet aktiveras på [!UICONTROL Browse] -fliken finns i [profilräknaren i användargränssnittsguiden för kundprofiler i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![Kontrollpanelen för profiler i Experience Platform med widgeten Profilantal markerad.](../images/profiles/profile-count.png)

### [!UICONTROL Profile count trend] {#profile-count-trend}

The [!UICONTROL Profile count trend] används ett linjediagram för att illustrera trenden i det totala antalet profiler i systemet över tiden. Det totala antalet inkluderar alla profiler som importerats till systemet sedan den senaste ögonblicksbilden. Data kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten.

![Trendwidgeten Profilantal.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profile count change] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Ändring av antal profiler"
>abstract="Den här widgeten visar totalt antal sammanfogade profiler **tillagd** till profilarkivet vid tidpunkten för den senaste ögonblicksbilden. Numret beror på den valda sammanfogningsprincipen som tillämpas på dina profildata."

The **[!UICONTROL Profile count change]** visar antalet sammanfogade profiler som lagts till i profilarkivet sedan föregående ögonblicksbild. Det här numret är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person. Du kan använda listruteväljaren för att visa antalet profiler som lagts till under de senaste 30 dagarna, 90 dagarna eller 12 månaderna.

>[!NOTE]
>
>The [!UICONTROL Profile count change] widgeten visar antalet tillagda profiler **efter** det första profilintaget och konfigurationen av profilarkivet. Med andra ord: om din organisation konfigurerade profilarkivet och importerade 4 000 000 Dag 1 är kontrollpanelen tillgänglig inom 24 timmar, men [!UICONTROL Profile count change] widgeten ställs in på 0. Detta görs för att undvika en topp som uppstår i samband med det initiala intaget av profiler i systemet. Under de kommande 30 dagarna har din organisation importerat ytterligare 1 000 000 profiler till Profilarkivet. När nästa ögonblicksbild tagits visas [!UICONTROL Profile count change] visar totalt 1 000 000 profiler, medan [!UICONTROL Profile count] widgeten visar totalt 5 000 000 profiler.

![Kontrollpanelen för användargränssnittsprofiler för plattformen med widgeten för ändring av profilantal markerad.](../images/profiles/profile-count-change.png)

### [!UICONTROL Profiles count change trend] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="trender för antal profiler"
>abstract="Den här widgeten visar antalet sammanfogade profiler som har lagts till i profilarkivet dagligen under de senaste 30 dagarna, 90 dagar eller 12 månaderna. Talet beror också på vilken sammanfogningsprincip som används för profildata."

The **[!UICONTROL Profiles count change trend]** visar det totala antalet sammanfogade profiler som har lagts till i profilarkivet dagligen de senaste 30 dagarna, 90 dagar eller 12 månaderna. Detta nummer uppdateras varje dag som ögonblicksbilden tas, och om du vill importera profiler till Platform kommer antalet profiler inte att visas förrän nästa ögonblicksbild tas. Antalet tillagda profiler är resultatet av att den valda sammanfogningsprincipen tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

The **[!UICONTROL Profiles count change trend]** widgeten visar en knapp för bildtexter i widgetens övre högra hörn. Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![Fliken Profilöversikt som visar widgeten Antal profiler ändrar trend med bildtextknappen markerad.](../images/profiles/profiles-count-change-trend-captions.png)

En maskininlärningsmodell genererar automatiskt beskrivningar av viktiga trender och viktiga händelser genom att analysera diagrammet och data. Anteckningar läggs till i diagrammet baserat på bildtexterna. Välj en bildtext som ska fokuseras på motsvarande anteckning.

![Dialogrutan med automatiska bildtexter för widgeten Antal profiler ändrar trendvändning.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Profiles count change trend by identity] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Den här widgeten filtrerar profilantalet baserat på en vald källidentitet och sammanfogningsprincip, och visar sedan ändringen av antalet för en rad punkter med hjälp av ett linjediagram. Sammanslagningsprincipen väljs i översiktslistrutan högst upp på sidan och källans identitet och tidsperiod väljs i widgetens listruta. Trenden kan visualiseras under 30 dagar, 90 dagar och 12 månader.

Denna widget hjälper dig att hantera dina behov av målaktivering genom att visa tillväxtmönstret för profiler som filtrerats med en obligatorisk identitet.

![Profilerna räknar en trend som ändras efter identitetswidget.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profiler efter identitet"
>abstract="Den här widgeten visar en uppdelning av alla sammanfogade profiler i din profilbutik efter identiteter."

The **[!UICONTROL Profiles by identity]** widgeten visar en beskrivning av identiteterna för alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per identitet (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kan vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Se [avsnittet om sammanfogningsprinciper tidigare i det här dokumentet](#merge-policies) om du vill veta mer.

![Kontrollpanelen Profiler i översikt med widgeten Profiler per identitet markerad.](../images/profiles/profiles-by-identity.png)

Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![Dialogrutan Profiler efter identitetsteckningar.](../images/profiles/profiles-by-identity-captions.png)

En maskininlärningsmodell genererar automatiskt datainsikter genom att analysera den övergripande fördelningen och de viktigaste dimensionerna av data.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Identitetsöverlappning"
>abstract="Den här widgeten använder ett Venndiagram för att visa överlappningen mellan profiler i din profilbutik som innehåller de två valda identiteterna."

The **[!UICONTROL Identity overlap]** widgeten använder ett Venndiagram, eller ett angivet diagram, för att visa överlappningen mellan profiler i din profilbutik som innehåller de två valda identiteterna.

Använd widgetens listrutor för att välja de identiteter som du vill jämföra. Cirklar visar det relativa totala antalet profiler som innehåller varje identitet. Antalet profiler som innehåller båda identiteterna representeras av storleken på överlappningen mellan cirklarna. Om en kund interagerar med ert varumärke i mer än en kanal kopplas flera identiteter till den enskilda kunden, och därför är det troligt att organisationen har flera profiler som innehåller fragment från mer än en identitet.

Mer information om profilfragment finns i avsnittet om [profilfragment jämfört med sammanslagna profiler](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) i realtidsöversikten över kundprofilen.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Översikt över kontrollpanelen Profiler med widgeten Identitetsöverlappning markerad.](../images/profiles/identity-overlap.png)

### [!UICONTROL Single identity profiles] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Enstaka identitetsprofiler"
>abstract="Den här widgeten innehåller ett antal profiler för din organisation som bara har en typ av ID som skapar deras identitet. Den här ID-typen kan antingen vara ett e-postmeddelande eller ett ECID."

The [!UICONTROL Single Identity Profiles] widgeten innehåller ett antal profiler för din organisation som bara har en typ av ID-typ som skapar deras identitet. Den här ID-typen kan antingen vara ett e-postmeddelande eller ett ECID. Profilantalet genereras från data i den senaste ögonblicksbilden.

![Widgeten för profiler för en identitet.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Single identity profiles by identity] {#single-identity-profiles-by-identity}

Den här widgeten använder ett stapeldiagram för att illustrera det totala antalet profiler som identifieras med endast en unik identifierare. Widgeten stöder upp till fem av de vanligaste identiteterna.

Håll pekaren över enskilda fält för att visa en dialogruta med information om det totala antalet profiler för en identitet.

![The Single identity profiles by identity widget.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Unsegmented profiles] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Osegmenterade profiler"
>abstract="Den här widgeten visar det totala antalet profiler som inte är kopplade till något segment och representerar möjligheten till profilaktivering i hela organisationen."

The [!UICONTROL Unsegmented Profiles] innehåller det totala antalet profiler som inte är kopplade till något segment. Det genererade numret är korrekt vid den senaste ögonblicksbilden och representerar möjligheten till profilaktivering i hela organisationen. Det visar också möjligheten att utvinna profiler som inte ger tillräcklig avkastning.

![Widgeten Osegmenterade profiler.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Unsegmented profiles change trend] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Trend för osegmenterade profiler"
>abstract="Den här widgeten innehåller en illustration av linjediagram för antalet profiler som inte är kopplade till något segment under en viss tidsperiod. Trenden för profiler som inte är kopplade till något segment kan visas under perioderna 30 dagar, 90 dagar och 12 månader."

The [!UICONTROL Unsegmented profiles change trend] i en widget används ett linjediagram för att illustrera antalet profiler som har lagts till sedan den senaste ögonblicksbilden som inte är kopplade till något segment. Ändringstrenden för profiler som inte är kopplade till något segment kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten. Profilantalet återspeglas på y-axeln och tiden på x-axeln.

![De osegmenterade profilerna ändrar trendwidgeten.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Unsegmented profiles by identity] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>De osegmenterade profilerna efter identitetswidget har tagits bort från oktober 2022 och är inte längre tillgängliga.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Audiences] {#audiences}

Den här widgeten visar det totala antalet segment som är klara att aktiveras enligt den valda sammanfogningsprincipen som tillämpas på dina profildata.

Välj **[!UICONTROL Audiences]** för att navigera till [!UICONTROL Segments] kontrollpanel [!UICONTROL Browse] -fliken. Därifrån visas en lista med alla segmentdefinitioner för din organisation.

![Widgeten Publiker.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Audience overlap report] {#audience-overlap-report}

Den här widgeten gör att målgruppen överlappar data från alla tillgängliga segment som filtreras efter sammanfogningsprincip. En lista med fem målgrupper som rangordnas mellan de högsta och de lägsta procentsatserna för överlappning finns för den sammanslagningsprincip som väljs i listrutan högst upp på skärmen. De två analyserade segmenten listas i [!UICONTROL SEGMENT A NAME] och [!UICONTROL SEGMENT B NAME] kolumner. Procentöverlappningen anges i den tredje kolumnen med 12 decimaler.

Rapporten om publiköverlappning hjälper er att skapa nya högpresterande segment. Genom att observera hög procentuell överlappning kan ni hindra målgrupper och förhindra att samma målgrupp skickas till olika destinationer. De hjälper er också att identifiera dolda insikter som kan bidra till bättre segmentering. Låg procentuell överlappning hjälper till att hitta unika profiler att eftersträva.

Välj **[!UICONTROL View more]** om du vill öppna en dialogruta i helskärmsläge som innehåller fler överlappande data.

![Målgruppen överlappar rapportwidgeten med Visa mer markerat .](../images/profiles/profiles-audience-overlap-report.png)

The [!UICONTROL Audience overlap report] visas. Den här dialogrutan kan innehålla upp till 50 rader med målgrupper som överlappar analyser uppdelade i sex kolumner. Välj inställningsikonen (![Inställningsikonen.](../images/profiles/settings-icon.png)) för att ta bort eller lägga till kolumner från tabellen.

![Dialogrutan för publiköverlappande rapporter.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Välj **[!UICONTROL Overlapping]** kolumnrubrik om du vill ändra resultatens rangordning mellan högsta och lägsta respektive högsta.

Om du vill hämta hela rapporten i PDF-format väljer du Alternativ-menyn (**`...`**) följt av **[!UICONTROL Download]**.

![Dialogrutan för publiköverlappningsrapport med ellipserna och nedladdningsalternativet markerat.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Välj en rad i rapporten för att öppna ett Venndiagram över överlappningsanalysen. Håll pekaren över ett avsnitt i Venndiagrammet för att visa antalet profiler i en dialogruta.

![Dialogrutan för målgruppsöverlappning med ett Venndiagram och en rad markerad.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Välj **[!UICONTROL Close]** för att gå tillbaka till [!UICONTROL Profiles] kontrollpanel.

### [!UICONTROL Audiences mapped to destination status] {#audiences-mapped-to-destination-status}

The [!UICONTROL Audiences mapped to destination status] widgeten visar det totala antalet både mappade och omappade målgrupper i ett enda mätresultat och använder ett ringdiagram för att illustrera den proportionella skillnaden mellan deras summor. Beräknade tal är beroende av den valda sammanfogningsprincipen.

Individuella värden för antingen mappade eller omappade målgrupper visas i en dialogruta när markören hålls över respektive avsnitt i donatdiagrammet.

![De målgrupper som är mappade till målstatuswidgeten.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Audiences size] {#audiences-size}

The [!UICONTROL Audiences size] widgeten innehåller en tabell med två kolumner som visar upp till 20 segment och det totala antalet målgrupper i varje segment. Listan ordnas från hög till låg enligt det totala antalet målgrupper. Det totala antalet målgrupper beror på vilken sammanfogningsprincip som används.

![Storlekswidgeten för publiker.](../images/profiles/audiences-size.png)

Om du vill visa omfattande information om ett segment väljer du ett segmentnamn i listan för att navigera till [!UICONTROL Segments] [!UICONTROL Detail] sida. Genom att markera **[!UICONTROL View all segments]** från slutet av widgeten kan du navigera till [!UICONTROL Segments] [!UICONTROL Browse] för att hitta ett befintligt segment.

![Widgeten Publikens storlek med ett segmentnamn och visa all segmenttext markerad.](../images/profiles/audiences-size-view-all-segments.png)

Mer information om [[!UICONTROL Segments] [!UICONTROL  Browse] tab](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Audience overlap by merge policy] {#audience-overlap-by-merge-policy}

Den här widgeten använder ett Venndiagram för att visa överlappningen mellan två markerade segment. Sammanslagningsprincipen väljs i översiktslistrutan högst upp på sidan och segmenten för analys väljs från två listrutor i widgeten. Det totala antalet profiler i den relevanta segmentdefinitionen kan du se genom att hålla markören över en cirkel eller skärningspunkten.

När widgeten visar den visuella överlappningen av segmentdefinitioner kan du optimera segmenteringsstrategin genom att studera likheter mellan segmentdefinitionerna.

![Kontrollpanelen Plattformsgränssnittsprofiler med listrutan för sammanslagningsprinciper och listrutorna för widgetsegment markerade.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta profilkontrollpanelen och förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om att arbeta med [!DNL Profile] data i användargränssnittet för Experience Platform, se [Användargränssnittsguide för kundprofil i realtid](../../profile/ui/user-guide.md).
