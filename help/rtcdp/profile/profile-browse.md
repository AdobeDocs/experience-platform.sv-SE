---
keywords: visa profiler rtcdp;rtcdp profilvy;rtcdp-profiler
title: Bläddra bland profiler i Real-time Customer Data Platform
description: Med Adobe Real-time Customer Data Platform kan du bläddra bland kundprofildata i realtid med Adobe Experience Platform användargränssnitt.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Bläddra bland profiler i Real-time Customer Data Platform

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. När individuella profiler sammanställs baserat på data som hämtas in till systemet från olika källor blir varje profil en användbar, tidsstämplad redovisning av varje interaktion som kunden har med ert varumärke.

I Adobe Experience Platform användargränssnitt kan du visa dessa skrivskyddade profiler och se viktig information om var och en av dina enskilda kunder, inklusive deras preferenser, tidigare händelser, interaktioner och vilka målgrupper personen tillhör.

Adobe Real-time Customer Data Platform är byggt på Adobe Experience Platform och kan därmed utnyttja profilvisningsfunktionerna i användargränssnittet i Experience Platform. En detaljerad guide till hur du visar kundprofiler i användargränssnittet för plattformen finns i [Användarhandbok för kundprofil i realtid](../../profile/ui/user-guide.md).

## Profilförbättringar för Real-Time CDP, B2B Edition

Förutom profilbläddringsfunktionerna som stöds av Adobe Experience Platform har Real-Time CDP, B2B Edition-användare tillgång till B2B-attribut och -händelser i kundprofilen på [!UICONTROL Attributes] och [!UICONTROL Events] tabbar. B2B-data kan också användas för att utföra segmentering, där målgrupperna visas under kundens [!UICONTROL Audience membership] jämför icke-B2B-målgrupper.

Med Real-Time CDP, B2B Edition kan du även bläddra [!UICONTROL Accounts], [!UICONTROL Opportunities]och [!UICONTROL Source records] från alla era företagskällor som är kopplade till en enskild kund.

Om du vill utforska dessa förbättringar börjar du med att följa stegen som beskrivs i [Användarhandbok för kundprofil i realtid](../../profile/ui/user-guide.md) om du vill bläddra i en profil genom en sammanfogningsprincip eller ett identitetsnamnutrymme.

![](images/b2b-browse-profile.png)

Profilinformationen innehåller åtkomst till [!UICONTROL Accounts], [!UICONTROL Opportunities]och [!UICONTROL Source records] utöver standardinformationen i kundprofilen, som också har förbättrats med B2B-händelser och -attribut.

![](images/b2b-profile-detail.png)

### Fliken Konton

Välj **[!UICONTROL Accounts]** om du vill visa en lista med konton som hör till profilen. Den här listan innehåller grundläggande information från kontoprofilen, till exempel namn, webbplats och bransch för kontot, samt en länk till kontoprofilen.

Mer information om att visa och utforska kontoprofiler finns i [kontoprofilöversikt](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Fliken Affärsmöjligheter

The **[!UICONTROL Opportunities]** -fliken innehåller information om öppna och stängda affärsmöjligheter som är relaterade till kontot. Dessa möjligheter kan förtäras i Experience Platform från flera olika källor, men Real-Time CDP B2B Edition gör det enkelt för marknadsförarna att se alla dessa möjligheter på ett och samma ställe.

Varje affärsmöjlighet innehåller information som namn på affärsmöjligheten, belopp, fas och huruvida affärsmöjligheten är öppen, stängd, vunnen eller förlorad.

![](images/b2b-profile-opportunities.png)

### Fliken Källposter

The **[!UICONTROL Source records]** Med -fliken kan du enkelt se de poster från olika källor i företaget som bidrar till en enda kundprofil. Förutom [!UICONTROL Person source key] och e-postadressen, innehåller varje källpost också posttyp (t.ex. en&quot;kontakt&quot;- eller&quot;lead&quot;-post) samt källan.

![](images/b2b-profile-source-records.png)
