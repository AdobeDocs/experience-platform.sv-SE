---
keywords: Experience Platform;hem;populära ämnen;felsökning av sandlådor
solution: Experience Platform
title: Felsökningsguide för sandlådor
description: Det här dokumentet innehåller svar på vanliga frågor om sandlådor i Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Felsökningsguide för sandlådor

Det här dokumentet innehåller svar på vanliga frågor om sandlådor i Adobe Experience Platform. För frågor och felsökning som rör andra Experience Platform-tjänster, se [Experience Platform felsökningsguide](../landing/troubleshooting.md).

Sandlådor delar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser. Se [översikten över sandlådor](home.md) för mer information.

## Vad är en sandlåda?

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje sandlåda har ett eget oberoende bibliotek med Experience Platform-resurser (inklusive scheman, datauppsättningar, profiler och så vidare). Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor. Se [översikten över sandlådor](home.md) för mer information.

## Vilka typer av sandlådor är tillgängliga och vilka är skillnaderna? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Sandlådetyp"
>abstract="Sandlådetypen anger om det här är en produktions- eller utvecklingssandlåda. Produktionssandlådor innehåller livedata och utvecklingssandlådor som används för testning och utveckling."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Skapa en sandlåda i användargränssnittet"

Det finns två typer av sandlådor i Experience Platform:

* **Produktionssandlåda**: En produktionssandlåda är avsedd att användas med profiler i din produktionsmiljö. Med Experience Platform kan du skapa flera produktionssandlådor för att tillhandahålla rätt funktionalitet för data samtidigt som du behåller driftisoleringen. Med den här funktionen kan du dedikera specifika produktionssandlådor till olika affärsområden, varumärken, projekt eller regioner. Produktionssandlådor har stöd för en mängd produktionsprofiler upp till ditt licensierade [!DNL Profile]-åtagande (uppmätt kumulativt i alla dina auktoriserade produktionssandlådor). Du har rätt att använda hela den licensierade totala datavolymen (uppmätt kumulativt i alla dina godkända produktionssandlådor).

* **Utvecklingssandlåda**: En utvecklingssandlåda är en sandlåda som endast kan användas för utveckling och testning med icke-produktionsprofiler. Utvecklingssandlådor har stöd för en mängd icke-produktionsprofiler på upp till 10 % av ditt licensierade [!DNL Profile]-åtagande (uppmätt kumulativt i alla dina auktoriserade utvecklingssandlådor). Du har rätt till upp till
   * Ett batchsegmenteringsjobb per dag, per utvecklingssandlåda.
   * Ett genomsnitt på 120 [!DNL Profile] API-anrop, per [!DNL Profile], per år (mäts kumulativt i alla dina auktoriserade utvecklingssandlådor.

Se [översikten över sandlådor](./home.md) för mer information.

## Kan jag få åtkomst till en resurs från mer än en sandlåda?

Sandlådor är isolerade partitioner av en enda Experience Platform-instans, där varje sandlåda underhåller ett eget oberoende resursbibliotek. En resurs som finns i en sandlåda kan inte nås från någon annan sandlåda, oavsett sandlådetyp (produktion eller icke-produktion).

## Vilken är standardproduktionssandlådan?

Standardproduktionssandlådan är den första produktionssandlådan som skapas när en organisation etableras första gången. Med standardproduktionssandlådan kan du importera eller använda data från Experience Platform, samt acceptera begäranden som inte innehåller värden för ett sandlådenamn eller ett sandbox-ID. Standardproduktionssandlådan kan återställas men inte tas bort.

## Hur många produktionssandlådor kan jag ha?

En Experience Platform-instans har stöd för flera produktions- och utvecklingssandlådor, där varje sandlåda har ett eget oberoende bibliotek med Experience Platform-resurser (inklusive scheman, datamängder och profiler).

En Experience Platform-standardlicens ger dig totalt fem sandlådor, som du kan klassificera som produktion eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor.

Produktionssandlådor kan återställas eller tas bort, förutom för produktionssandlådor som också används av Adobe Analytics för funktionen [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=sv) eller om identitetsdiagrammet som finns i det också används av Adobe Audience Manager för funktionen [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=sv) .

Du kan uppdatera titeln för en produktionssandlåda. En produktionssandlåda kan dock inte byta namn.

>[!NOTE]
>
>Sandlådans namn används för uppslagssyften i API-anrop, medan sandlådans titel används som visningsnamn.

## Hur många utvecklingssandlådor kan jag ha?

Experience Platform tillåter för närvarande att maximalt 75 sandlådor (produktion och utveckling) är aktiva i en enda organisation.

Utvecklingssandlådor har stöd för både återställnings- och borttagningsfunktioner.

## Jag har just skapat en sandlåda. Hur anger jag behörigheter för de användare som ska arbeta med den här sandlådan?

Adobe Admin Console länkar användare till sandlådor och behörigheter genom att använda produktprofiler. När du har skapat en ny sandlåda går du till fliken **Behörigheter** i produktprofilen som du vill ge åtkomst till och klickar sedan på **Sandlådor**. Härifrån kan du lägga till eller ta bort åtkomst till den nya sandlådan på samma sätt som andra behörigheter.

Om du vill lägga till unika behörigheter för användare av en viss sandlåda kan du behöva skapa en ny produktprofil med rätt sandlådor och behörigheter tillämpade, och tilldela dessa användare till den profilen.

Mer information om hur du hanterar sandlådor och behörigheter i Admin Console finns i användarhandboken för [åtkomstkontrollen](../access-control/ui/overview.md) .
