---
keywords: visa profiler rtcdp;rtcdp profilvy;rtcdp-profiler
title: Bläddra bland profiler i Real-Time Customer Data Platform
description: Med Adobe Real-Time Customer Data Platform kan du bläddra bland kundprofildata i realtid med Adobe Experience Platform användargränssnitt.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Bläddra bland profiler i Real-Time Customer Data Platform

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. När individuella profiler sammanställs baserat på data som hämtas in till systemet från olika källor blir varje profil en användbar, tidsstämplad redovisning av varje interaktion som kunden har med ert varumärke.

I Adobe Experience Platform användargränssnitt kan du visa dessa skrivskyddade profiler och se viktig information om var och en av dina enskilda kunder, inklusive deras preferenser, tidigare händelser, interaktioner och vilka målgrupper personen tillhör.

Adobe Real-Time Customer Data Platform är byggt på Adobe Experience Platform och kan därmed utnyttja profilvisningsfunktionerna i Experience Platform användargränssnitt. En detaljerad guide till hur du visar kundprofiler i Experience Platform användargränssnitt finns i användarhandboken för [kundprofilen i realtid](../../profile/ui/user-guide.md).

## Profilförbättringar för Real-Time CDP, B2B edition

Förutom profilbläddringsfunktionerna som stöds av Adobe Experience Platform, Real-Time CDP, kan B2B edition-användare komma åt B2B-attribut och händelser i kundprofilen på flikarna [!UICONTROL Attributes] och [!UICONTROL Events]. B2B-data kan också användas för att utföra segmentering, där de målgrupperna visas under kundens [!UICONTROL Audience membership]-flik tillsammans med målgrupper som inte är B2B.

Real-Time CDP, B2B edition gör det även möjligt att bläddra bland [!UICONTROL Accounts], [!UICONTROL Opportunities] och [!UICONTROL Source records] från olika företagskällor som är kopplade till en enskild kund.

Om du vill utforska de här förbättringarna börjar du med att följa de steg som beskrivs i användarhandboken för [kundprofilen i realtid](../../profile/ui/user-guide.md) och bläddra i en profil genom att sammanfoga princip eller identitetsnamnområde.

![](images/b2b-browse-profile.png)

Profilinformationen omfattar åtkomst till flikarna [!UICONTROL Accounts], [!UICONTROL Opportunities] och [!UICONTROL Source records] utöver den standardinformation som anges i kundprofilen, som också har förbättrats med B2B-händelser och -attribut.

![](images/b2b-profile-detail.png)

Mer information om profilinformationen i Experience Platform-gränssnittet finns i avsnittet [information i dokumentationen för kontrollpanelen för profiler](../../dashboards/guides/profiles.md#browse-profiles).

### Fliken Konton

Välj **[!UICONTROL Accounts]** om du vill visa en lista över konton som är relaterade till profilen. Den här listan innehåller grundläggande information från kontoprofilen, t.ex. namn, webbplats och bransch för kontot, samt en länk till kontoprofilen.

Mer information om hur du visar och utforskar kontoprofiler får du om du börjar med att läsa översikten över [kontoprofiler](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Fliken Affärsmöjligheter

Fliken **[!UICONTROL Opportunities]** innehåller information om öppna och stängda affärsmöjligheter som är relaterade till kontot. Dessa möjligheter kan förtäras i Experience Platform från flera olika källor, men med Real-Time CDP är det enkelt för marknadsförarna att se alla dessa möjligheter på ett och samma ställe.

Varje affärsmöjlighet innehåller information som namn på affärsmöjligheten, belopp, fas och huruvida affärsmöjligheten är öppen, stängd, vunnen eller förlorad.

![](images/b2b-profile-opportunities.png)

### Fliken Source records

På fliken **[!UICONTROL Source records]** kan du enkelt se flera källposter från dina företagskällor som bidrar till den enskilda kundprofilen. Förutom e-postadressen [!UICONTROL Person source key] och e-postadressen, innehåller varje källpost också posttyp (till exempel en kontakt- eller lead-post) samt källan.

![](images/b2b-profile-source-records.png)
