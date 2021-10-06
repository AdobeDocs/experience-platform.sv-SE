---
keywords: visa profiler rtcdp;rtcdp profilvy;rtcdp-profiler
title: Bläddra bland profiler i Real-time Customer Data Platform
description: Med Real-time Customer Data Platform kan du bläddra bland kundprofildata i realtid med Adobe Experience Platform användargränssnitt.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 6579e371a8729e926b7061418c786150a27d4876
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Bläddra bland profiler i Real-time Customer Data Platform

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. När individuella profiler sammanställs baserat på data som hämtas in till systemet från olika källor blir varje profil en användbar, tidsstämplad redovisning av varje interaktion som kunden har med ert varumärke.

I Adobe Experience Platform användargränssnitt kan du visa dessa skrivskyddade profiler och se viktig information om var och en av dina enskilda kunder, inklusive deras preferenser, tidigare händelser, interaktioner och de segment som personen tillhör.

Real-time Customer Data Platform är byggt på Adobe Experience Platform och kan därmed utnyttja profilvisningsfunktionerna i användargränssnittet i Experience Platform. En detaljerad guide till hur du visar kundprofiler i användargränssnittet för plattformen finns i [Användarhandboken för kundprofilen i realtid](../../profile/ui/user-guide.md).

## Profilförbättringar för CDP, B2B Edition i realtid

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.

Förutom de profilbläddringsfunktioner som stöds av Adobe Experience Platform kan användare av CDP, B2B Edition i realtid komma åt B2B-attribut och händelser i kundprofilen på flikarna [!UICONTROL Attributes] och [!UICONTROL Events]. B2B-data kan också användas för att utföra segmentering, där segmenten visas under kundens [!UICONTROL Segment membership]-flik bredvid segment som inte är B2B-segment.

Med CDP, B2B Edition i realtid kan du även bläddra i [!UICONTROL Accounts], [!UICONTROL Opportunities] och [!UICONTROL Source records] från olika företagskällor som är kopplade till en enskild kund.

Om du vill utforska de här förbättringarna börjar du med att följa stegen som beskrivs i [Användarhandbok för kundprofil i realtid](../../profile/ui/user-guide.md) och bläddrar efter en profil genom en sammanfogningsprincip eller ett identitetsnamnområde.

![](images/b2b-browse-profile.png)

Profilinformationen omfattar åtkomst till flikarna [!UICONTROL Accounts], [!UICONTROL Opportunities] och [!UICONTROL Source records] förutom standardinformationen i kundprofilen som också har förbättrats med B2B-händelser och -attribut.

![](images/b2b-profile-detail.png)

### Fliken Konton

Välj **[!UICONTROL Accounts]** om du vill visa en lista över konton som är relaterade till profilen. Den här listan innehåller grundläggande information från kontoprofilen, till exempel namn, webbplats och bransch för kontot, samt en länk till kontoprofilen.

Mer information om att visa och utforska kontoprofiler får du om du börjar med att läsa översikten över [kontoprofiler](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Fliken Affärsmöjligheter

Fliken **[!UICONTROL Opportunities]** innehåller information om öppna och stängda affärsmöjligheter som är relaterade till kontot. Dessa möjligheter kan förtäras i Experience Platform från flera olika källor, men CDP, B2B Edition i realtid gör det enkelt för marknadsförarna att se alla dessa möjligheter på ett och samma ställe.

Varje affärsmöjlighet innehåller information som namn på affärsmöjligheten, belopp, fas och huruvida affärsmöjligheten är öppen, stängd, vunnen eller förlorad.

![](images/b2b-profile-opportunities.png)

### Fliken Källposter

På fliken **[!UICONTROL Source records]** kan du enkelt se de poster från olika källor i företaget som bidrar till den enskilda kundprofilen. Förutom [!UICONTROL Person source key] och e-postadressen innehåller varje källpost också posttyp (till exempel en kontakt- eller lead-post) samt källan.

![](images/b2b-profile-source-records.png)
