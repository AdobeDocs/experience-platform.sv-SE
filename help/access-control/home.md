---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över åtkomstkontroll
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# Översikt över åtkomstkontroll

Åtkomstkontroll för Experience Platform tillhandahålls via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.

## Åtkomststyrningshierarki och arbetsflöde

Om du vill konfigurera åtkomstkontroll för Experience Platform måste du ha administratörsbehörighet för en organisation som har en produktintegrering med Experience Platform. Den minsta rollen som beviljar eller återkallar behörigheter är en **produktprofiladministratör**. Andra administratörsroller som kan hantera behörigheter är **produktadministratörer** (kan hantera alla profiler i en produkt) och **systemadministratörer** (utan begränsningar). Mer information finns i Adobe Help Center-artikeln om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) .

>[!NOTE]
>
>Från och med nu avser alla omnämnanden av&quot;administratör&quot; i det här dokumentet en administratör för en produktprofil eller en senare (enligt ovan).

Ett arbetsflöde på hög nivå för att hämta och tilldela åtkomstbehörigheter kan sammanfattas på följande sätt:

- När du prenumererar på Adobe Experience Platform skickas ett e-postmeddelande till administratören som anges i registreringsformuläret.
- Administratören loggar in på [Adobe Admin Console](#adobe-admin-console) och väljer **Adobe Experience Platform** i produktlistan på översiktssidan.
- Administratören kan visa [standardproduktprofilerna](#product-profiles) eller skapa nya kundproduktprofiler efter behov.
- Administratören kan redigera behörigheter och användare för befintliga produktprofiler.
- När du skapar eller redigerar en produktprofil lägger administratören till användare i profilen på fliken **Användare** och tilldelar behörigheter till dessa användare (till exempel Läs datauppsättningar eller Hantera schema) genom att gå till fliken **Behörigheter** . På samma sätt kan administratören tilldela åtkomst till sandlådor med samma behörighetsflik.
- När användare loggar in i användargränssnittet i Experience Platform styrs deras åtkomst till Platform-funktioner av de behörigheter som de har fått från steg 2. Om en användare t.ex. inte har behörigheten Visa datauppsättningar kommer fliken *Datauppsättningar* på sidomenyn inte att vara synlig för användaren.

Mer information om hur du hanterar åtkomstkontroll i Experience Platform finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

Alla anrop till Experience Platform API:er valideras för behörigheter och returnerar fel om lämpliga behörigheter inte hittas i den aktuella användarkontexten. Elementen döljs eller ändras i användargränssnittet beroende på vilka behörigheter den aktuella användaren har.

## Adobe Admin Console

Adobe Admin Console är en central plats för hantering av berättiganden och åtkomst för Adobe-produkter. Via konsolen kan du ge användargrupper åtkomstbehörigheter för olika Platform-funktioner, t.ex.&quot;Hantera datauppsättningar&quot;,&quot;Visa datauppsättningar&quot; eller&quot;Hantera profiler&quot;.

### Produktprofiler

I Admin Console tilldelas användare behörigheter genom användning av **produktprofiler**. Med produktprofiler kan du bevilja behörigheter till en eller flera användare, och de kan även innehålla deras åtkomst till omfattningen av de sandlådor som de har tilldelats via produktprofiler. Användare kan tilldelas till en eller flera produktprofiler som tillhör din organisation.

### Standardproduktprofiler

Experience Platform levereras med två förkonfigurerade standardproduktprofiler. Följande tabell visar vad som anges i respektive standardprofil, inklusive vilken sandlåda de beviljar åtkomst till samt de behörigheter de ger inom den sandlådans omfång.

| Produktprofil | Sandlådeåtkomst | Behörigheter |
| --- | --- | --- |
| Standardproduktion - Alla åtkomst | Produktion | Alla behörigheter som gäller för Experience Platform, förutom sandlådeadministration. |
| Förvald sandlådeadministration | Ej tillämpligt | Ger endast åtkomst till sandlådeadministrationsbehörigheter. |

## Sandlådor och behörigheter

Experience Platform ger åtkomst till en produktionssandlåda och gör att du kan skapa **icke-produktionssandlådor**. Sandlådor som inte är produktionssandlådor är en form av datavirtualisering som gör att du kan isolera data från andra sandlådor och som vanligtvis används för utvecklingsexperiment, testning och testning. En produktprofils **behörigheter** ger profilens användare tillgång till Platform-funktioner i sandlådemiljöer som de har beviljats åtkomst till.

Mer information om sandlådor i Experience Platform finns i översikten över [sandlådor](../sandboxes/home.md).

### Åtkomst till sandlådor

Åtkomst till sandlådor hanteras via produktprofiler. Detaljerade steg om hur du aktiverar åtkomst till en sandlåda för en produktprofil finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

Användare kan beviljas åtkomst till en eller flera sandlådor i en produktprofil. Om en användare ingår i två eller flera produktprofiler får den användaren tillgång till alla sandlådor som ingår i de profilerna.

Med behörigheten&quot;Sandlådehantering&quot; kan användare hantera, visa och återställa sandlådor.

### Behörigheter

På fliken **Behörigheter** i en produktprofil visas de sandlådor och behörigheter som är aktiva för den profilen:

![](./images/permissions-overview.png)

Behörigheter som beviljas via Admin Console sorteras efter kategori, med vissa behörigheter som ger åtkomst till flera lågnivåfunktioner.

Följande tabell visar vilka behörigheter som är tillgängliga för Experience Platform i Admin Console, med beskrivningar av de specifika Platform-funktioner som de ger åtkomst till. Detaljerade anvisningar om hur du lägger till behörigheter i en produktprofil finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| Datamodellering | Hantera scheman | Åtkomst för att läsa, skapa, redigera och ta bort scheman och relaterade resurser. |
| Datamodellering | Visa scheman | Skrivskyddad åtkomst till scheman och relaterade resurser. |
| Datahantering | Hantera datauppsättningar | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar. Skrivskyddad åtkomst för scheman. |
| Datahantering | Visa datauppsättningar | Skrivskyddad åtkomst för datauppsättningar och scheman. |
| Datahantering | Dataövervakning | Skrivskyddad åtkomst till övervakning av datauppsättningar och strömmar. |
| Profilhantering | Hantera profiler | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar som används för kundprofiler. Skrivskyddad åtkomst till tillgängliga profiler. |
| Profilhantering | Visa profiler | Skrivskyddad åtkomst till tillgängliga profiler. |
| Profilhantering | Exportera målgrupp för segment | Möjlighet att exportera ett utvärderat målgruppssegment till en datauppsättning. |
| Identiteter | Hantera identitetsnamnutrymmen | Åtkomst för att läsa, skapa, redigera och ta bort identitetsnamnutrymmen. |
| Identiteter | Visa identitetsnamnutrymmen | Skrivskyddad åtkomst för identitetsnamnutrymmen. |
| Sandlådeadministration | Hantera sandlådor | Åtkomst för att läsa, skapa, redigera och ta bort sandlådor. |
| Sandlådeadministration | Visa sandlådor | Skrivskyddad åtkomst för sandlådor som tillhör din organisation. |
| Sandlådeadministration | Återställ en sandlåda | Möjlighet att återställa en sandlåda. |
| Mål  | Hantera mål | Åtkomst för att läsa, skapa, redigera och inaktivera mål.* |
| Mål  | Visa mål | Skrivskyddad åtkomst till tillgängliga mål på fliken *Katalog* och autentiserade mål på fliken *Bläddra* .* |
| Mål  | Aktivera destinationer | Möjlighet att aktivera data till aktiva destinationer som har skapats. Den här behörigheten kräver att antingen Visa destinationer eller Hantera destinationer beviljas den användare som ska aktivera destinationer.* |
| Dataintag | Hantera källor | Tillgång till att läsa, skapa, redigera och inaktivera källor. |
| Dataintag | Visa källor | Skrivskyddad åtkomst till tillgängliga källor på fliken *Katalog* och autentiserade källor på fliken *Bläddra* . |
| Datavetenskapens arbetsyta | Hantera arbetsytan Datavetenskap | Åtkomst att läsa, skapa, redigera och ta bort i arbetsytan Data Science. |

_(*) Detta tillstånd kräver att man reserverar sig för Real-time Customer Data Platform. Mer information om CDP i realtid finns i[realtidsöversikten](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)._

## Nästa steg

Genom att läsa den här guiden har du lagts till i huvudprinciperna för åtkomstkontroll i Experience Platform. Du kan nu fortsätta till användarhandboken [för](./ui/overview.md) åtkomstkontroll och få detaljerade anvisningar om hur du använder Admin Console för att skapa produktprofiler och tilldela behörigheter för Platform.