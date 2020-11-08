---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Översikt över åtkomstkontroll
description: Åtkomstkontroll för Adobe Experience Platform tillhandahålls via Adobe Admin Console. Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.
translation-type: tm+mt
source-git-commit: ccb7286e47aa4cf6356d22f84111b0c0fb30dfa8
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---


# Översikt över åtkomstkontroll

Åtkomstkontroll för [!DNL Experience Platform] tillhandahålls via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i [!DNL Admin Console], som länkar användare med behörigheter och sandlådor.

## Åtkomststyrningshierarki och arbetsflöde

Om du vill konfigurera åtkomstkontroll för [!DNL Experience Platform]måste du ha administratörsbehörighet för en organisation som har en [!DNL Experience Platform] produktintegrering. Den minsta rollen som beviljar eller återkallar behörigheter är en administratör för produktprofilen. Andra administratörsroller som kan hantera behörigheter är produktadministratörer (kan hantera alla profiler i en produkt) och systemadministratörer (utan begränsningar). Mer information finns i Adobe Help Center artikel om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) .

>[!NOTE]
>
>Från och med nu avser alla omnämnanden av&quot;administratör&quot; i det här dokumentet en administratör för en produktprofil eller en senare (enligt ovan).

Ett arbetsflöde på hög nivå för att hämta och tilldela åtkomstbehörigheter kan sammanfattas på följande sätt:

- När du har licensierat Adobe Experience Platform, eller en program-/apptjänst som använder Experience Platform, skickas ett e-postmeddelande till administratören som anges under licensieringen.
- Administratören loggar in på [Adobe Admin Console](#adobe-admin-console) och väljer **Adobe Experience Platform** i produktlistan på översiktssidan.
- Administratören kan visa [standardproduktprofilerna](#product-profiles) eller skapa nya kundproduktprofiler efter behov.
- Administratören kan redigera behörigheter och användare för befintliga produktprofiler.
- När du skapar eller redigerar en produktprofil lägger administratören till användare i profilen med hjälp av fliken **[!UICONTROL users]** och tilldelar behörigheter till dessa användare (till exempel&quot;[!UICONTROL Read Datasets]&quot; eller&quot;[!UICONTROL Manage Schemas]&quot;) med hjälp av **[!UICONTROL permissions]** fliken. På samma sätt kan administratören tilldela åtkomst till sandlådor med samma behörighetsflik.
- När användare loggar in på [!DNL Experience Platform] användargränssnittet styrs deras åtkomst till [!DNL Platform] funktioner av de behörigheter som de har fått från steg 2. Om en användare t.ex. inte har behörigheten &quot;[!UICONTROL View Datasets]&quot; kommer fliken på **[!UICONTROL Datasets]** sidomenyn inte att vara synlig för användaren.

Mer detaljerad information om hur du hanterar åtkomstkontroll i [!DNL Experience Platform]finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

Alla anrop till [!DNL Experience Platform] API:er valideras för behörigheter och returnerar fel om lämpliga behörigheter inte hittas i den aktuella användarkontexten. Elementen döljs eller ändras i användargränssnittet beroende på vilka behörigheter den aktuella användaren har.

## Adobe Admin Console

Adobe Admin Console är en central plats för hantering av Adobe produktberättiganden och åtkomst för din organisation. Via konsolen kan du ge grupper av användare åtkomstbehörigheter för olika [!DNL Platform] funktioner, till exempel&quot;[!UICONTROL Manage Datasets]&quot;,&quot;[!UICONTROL View Datasets]&quot; eller&quot;[!UICONTROL Manage Profiles]&quot;.

### Produktprofiler

I [!DNL Admin Console]tilldelas användare behörigheter genom användning av produktprofiler. Med produktprofiler kan du bevilja behörigheter till en eller flera användare, och de kan även innehålla deras åtkomst till omfattningen av de sandlådor som de har tilldelats via produktprofiler. Användare kan tilldelas till en eller flera produktprofiler som tillhör din organisation.

### Standardproduktprofiler

[!DNL Experience Platform] levereras med två förkonfigurerade standardproduktprofiler. Följande tabell visar vad som anges i respektive standardprofil, inklusive vilken sandlåda de beviljar åtkomst till samt de behörigheter de ger inom den sandlådans omfång.

| Produktprofil | Sandlådeåtkomst | Behörigheter |
| --- | --- | --- |
| Standardproduktion - Alla åtkomst | Produktion | Alla behörigheter som gäller för [!DNL Experience Platform], förutom sandlådeadministration. |
| Förvald sandlådeadministration | Ej tillämpligt | Ger endast åtkomst till sandlådeadministrationsbehörigheter. |

## Sandlådor och behörigheter

Sandlådor som inte är produktionssandlådor är en form av datavirtualisering som gör att du kan isolera data från andra sandlådor och som vanligtvis används för utvecklingsexperiment, testning och testning. En produktprofils behörigheter ger profilens användare åtkomst till [!DNL Platform] funktioner i sandlådemiljöer som de har beviljats åtkomst till. En standardlicens för Experience Platform ger dig fem sandlådor (en och fyra icke-produktioner). Du kan lägga till paket med tio icke-produktionssandlådor, upp till totalt högst 75 sandlådor. Kontakta din IMS-organisationsadministratör eller din Adobe-säljare om du vill ha mer information.

Mer information om sandlådor i finns i [!DNL Experience Platform]översikten över [sandlådor](../sandboxes/home.md).

### Åtkomst till sandlådor

Åtkomst till sandlådor hanteras via produktprofiler. Detaljerade steg om hur du aktiverar åtkomst till en sandlåda för en produktprofil finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

Användare kan beviljas åtkomst till en eller flera sandlådor i en produktprofil. Om en användare ingår i två eller flera produktprofiler får den användaren tillgång till alla sandlådor som ingår i de profilerna.

Med behörigheten&quot;Sandlådehantering&quot; kan användare hantera, visa och återställa sandlådor.

### Behörigheter

På fliken Behörigheter i en produktprofil visas de sandlådor och behörigheter som är aktiva för den profilen:

![permissions-overview](./images/permissions-overview.png)

Behörigheter som beviljas via [!DNL Admin Console] sorteras efter kategori, med vissa behörigheter som ger åtkomst till flera lågnivåfunktioner.

I följande tabell visas de tillgängliga behörigheterna för [!DNL Experience Platform] i [!DNL Admin Console], med beskrivningar av de specifika [!DNL Platform] funktioner som de ger åtkomst till. Detaljerade anvisningar om hur du lägger till behörigheter i en produktprofil finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Åtkomst för att läsa, skapa, redigera och ta bort scheman och relaterade resurser. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Skrivskyddad åtkomst till scheman och relaterade resurser. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Åtkomst för att läsa, skapa, redigera och ta bort schemarelationer. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Åtkomst för att läsa, skapa, redigera och ta bort identitetsmetadata för scheman. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar. Skrivskyddad åtkomst för scheman. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Skrivskyddad åtkomst för datauppsättningar och scheman. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Skrivskyddad åtkomst till övervakning av datauppsättningar och strömmar. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar som används för kundprofiler. Skrivskyddad åtkomst till tillgängliga profiler. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Skrivskyddad åtkomst till tillgängliga profiler. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Åtkomst för att läsa, skapa, redigera och ta bort segment. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Skrivskyddad åtkomst till tillgängliga segment. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Åtkomst för att läsa, skapa, redigera och ta bort sammanfogningsprinciper. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Skrivskyddad åtkomst till tillgängliga kopplingsprofiler. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Möjlighet att exportera ett utvärderat målgruppssegment till en datauppsättning. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Möjlighet att generera profiler för en viss målgrupp genom att utvärdera en segmentdefinition. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Åtkomst för att läsa, skapa, redigera och ta bort identitetsnamnutrymmen. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Skrivskyddad åtkomst för identitetsnamnutrymmen. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Åtkomst för att läsa, skapa, redigera och ta bort sandlådor. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Skrivskyddad åtkomst för sandlådor som tillhör din organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Möjlighet att återställa en sandlåda. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Åtkomst för att läsa, skapa, redigera och inaktivera mål.* |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Skrivskyddad åtkomst till tillgängliga destinationer på **[!UICONTROL Catalog]** fliken och autentiserade destinationer på **[!UICONTROL Browse]** fliken.* |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Möjlighet att aktivera data till aktiva destinationer som har skapats. Den här behörigheten kräver antingen Visa mål eller Hantera [!UICONTROL Destinations”] för den användare som ska aktivera mål.* |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Tillgång till att läsa, skapa, redigera och inaktivera källor. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Skrivskyddad åtkomst till tillgängliga källor på **[!UICONTROL Catalog]** fliken och autentiserade källor på **[!UICONTROL Browse]** fliken. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Åtkomst att läsa, skapa, redigera och ta bort i [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Åtkomst att läsa, skapa och ta bort användningsetiketter. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Åtkomst att läsa, skapa, redigera och ta bort dataanvändningsprinciper. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Skrivskyddad åtkomst till dataanvändningsprinciper som tillhör din organisation. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Åtkomst att läsa, skapa, redigera och ta bort strukturerade SQL-frågor för plattformsdata. |

_(*) Detta tillstånd kräver bestämmelser för [!DNL Real-time Customer Data Platform]. Mer information om CDP i realtid finns i [realtidsöversikten](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)._

## Nästa steg

Genom att läsa den här guiden har du lagts till i huvudprinciperna för åtkomstkontroll i [!DNL Experience Platform]. Du kan nu fortsätta till användarhandboken [för](./ui/overview.md) åtkomstkontroll och få detaljerade anvisningar om hur du använder [!DNL Admin Console] för att skapa produktprofiler och tilldela behörigheter för [!DNL Platform].