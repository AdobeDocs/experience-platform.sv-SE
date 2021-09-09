---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;adobe admin admin console
solution: Experience Platform
topic-legacy: overview
title: Översikt över åtkomstkontroll
description: Åtkomstkontroll för Adobe Experience Platform tillhandahålls via Adobe Admin Console. Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88593d921d6ad97fc4dfb059f0272817caee06c7
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 0%

---

# Översikt över åtkomstkontroll

Åtkomstkontroll för [!DNL Experience Platform] tillhandahålls via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i [!DNL Admin Console], som länkar användare med behörigheter och sandlådor.

## Åtkomststyrningshierarki och arbetsflöde

Om du vill konfigurera åtkomstkontroll för [!DNL Experience Platform] måste du ha administratörsbehörighet för en organisation som har en [!DNL Experience Platform]-produktintegrering. Den minsta rollen som beviljar eller återkallar behörigheter är en administratör för produktprofilen. Andra administratörsroller som kan hantera behörigheter är produktadministratörer (kan hantera alla profiler i en produkt) och systemadministratörer (utan begränsningar). Mer information finns i Adobe Help Center-artikeln [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html).

>[!NOTE]
>
>Från och med nu avser alla omnämnanden av&quot;administratör&quot; i det här dokumentet en administratör för en produktprofil eller en senare (enligt ovan).

Ett arbetsflöde på hög nivå för att hämta och tilldela åtkomstbehörigheter kan sammanfattas på följande sätt:

- När du har licensierat Adobe Experience Platform, eller en program-/apptjänst som använder Experience Platform, skickas ett e-postmeddelande till administratören som anges under licensieringen.
- Administratören loggar in på [Adobe Admin Console](#adobe-admin-console) och väljer **Adobe Experience Platform** i produktlistan på översiktssidan.
- Administratören kan visa [standardproduktprofilerna](#product-profiles) eller skapa nya kundproduktprofiler efter behov.
- Administratören kan redigera behörigheter och användare för befintliga produktprofiler.
- När du skapar eller redigerar en produktprofil lägger administratören till användare i profilen med fliken **[!UICONTROL users]** och tilldelar behörigheter till dessa användare (till exempel [!UICONTROL Read Datasets] eller [!UICONTROL Manage Schemas]) med hjälp av fliken **[!UICONTROL permissions]**. På samma sätt kan administratören tilldela åtkomst till sandlådor med samma behörighetsflik.
- När användare loggar in på [!DNL Experience Platform]-användargränssnittet styrs deras åtkomst till [!DNL Platform]-funktioner av de behörigheter som de har fått från steg 2. Om en användare t.ex. inte har behörigheten [!UICONTROL View Datasets] kommer fliken **[!UICONTROL Datasets]** på sidomenyn inte att vara synlig för användaren.

Mer detaljerad information om hur du hanterar åtkomstkontroll i [!DNL Experience Platform] finns i [användarhandboken för åtkomstkontroll](./ui/overview.md).

Alla anrop till [!DNL Experience Platform] API:er valideras för behörigheter och returnerar fel om rätt behörighet(er) inte hittas i den aktuella användarkontexten. Elementen döljs eller ändras i användargränssnittet beroende på vilka behörigheter den aktuella användaren har.

## Adobe Admin Console

Adobe Admin Console är en central plats för hantering av Adobe produktberättiganden och åtkomst för din organisation. Via konsolen kan du ge användargrupper åtkomstbehörigheter för olika [!DNL Platform]-funktioner, till exempel &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot; eller &quot;[!UICONTROL Manage Profiles]&quot;.

### Produktprofiler

I [!DNL Admin Console] tilldelas användare behörigheter genom användning av produktprofiler. Med produktprofiler kan du bevilja behörigheter till en eller flera användare, och de kan även innehålla deras åtkomst till omfattningen av de sandlådor som de har tilldelats via produktprofiler. Användare kan tilldelas till en eller flera produktprofiler som tillhör din organisation.

### Standardproduktprofiler

[!DNL Experience Platform] levereras med två förkonfigurerade standardproduktprofiler. Följande tabell visar vad som anges i respektive standardprofil, inklusive vilken sandlåda de beviljar åtkomst till samt de behörigheter de ger inom den sandlådans omfång.

| Produktprofil | Sandlådeåtkomst | Behörigheter |
| --- | --- | --- |
| Standardproduktion, all åtkomst | Produktion | Alla behörigheter som gäller för [!DNL Experience Platform], förutom för administratörsbehörigheter för sandlådan. |
| Sandlådeadministratörer | Ej tillämpligt | Ger endast åtkomst till sandlådeadministrationsbehörigheter. |

## Sandlådor och behörigheter

Sandlådor som inte är produktionssandlådor är en form av datavirtualisering som gör att du kan isolera data från andra sandlådor och som vanligtvis används för utvecklingsexperiment, testning och testning. En produktprofils behörigheter ger profilens användare åtkomst till [!DNL Platform]-funktioner i sandlådemiljöer som de har beviljats åtkomst till. En standardlicens för Experience Platform ger dig fem sandlådor (en och fyra icke-produktioner). Du kan lägga till paket med tio icke-produktionssandlådor, upp till totalt högst 75 sandlådor. Kontakta din IMS-organisationsadministratör eller din Adobe-säljare om du vill ha mer information.

Mer information om sandlådor i [!DNL Experience Platform] finns i [översikten över sandlådor](../sandboxes/home.md).

### Åtkomst till sandlådor

Åtkomst till sandlådor hanteras via produktprofiler. Detaljerade steg om hur du aktiverar åtkomst till en sandlåda för en produktprofil finns i [användarhandboken för åtkomstkontroll](./ui/overview.md).

Användare kan beviljas åtkomst till en eller flera sandlådor i en produktprofil. Om en användare ingår i två eller flera produktprofiler får den användaren tillgång till alla sandlådor som ingår i de profilerna.

Med behörigheten&quot;Sandlådehantering&quot; kan användare hantera, visa och återställa sandlådor.

### Behörigheter {#permissions}

På fliken Behörigheter i en produktprofil visas de sandlådor och behörigheter som är aktiva för den profilen:

![permissions-overview](./images/permissions-overview.png)

Behörigheter som beviljas via [!DNL Admin Console] sorteras efter kategori, med vissa behörigheter som ger åtkomst till flera lågnivåfunktioner.

Följande tabell visar de tillgängliga behörigheterna för [!DNL Experience Platform] i [!DNL Admin Console], med beskrivningar av de specifika [!DNL Platform]-funktioner som de ger åtkomst till. Detaljerade anvisningar om hur du lägger till behörigheter i en produktprofil finns i [användarhandboken för åtkomstkontroll](./ui/overview.md).

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
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Åtkomst för att läsa, skapa, redigera och inaktivera mål. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Skrivskyddad åtkomst till tillgängliga mål på fliken **[!UICONTROL Catalog]** och autentiserade mål på fliken **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Möjlighet att aktivera data till aktiva destinationer som har skapats. Den här behörigheten kräver att antingen Visa mål eller Hantera [!UICONTROL Destinations”] beviljas den användare som ska aktivera mål. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Möjlighet att skapa mål med [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Tillgång till att läsa, skapa, redigera och inaktivera källor. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Skrivskyddad åtkomst till tillgängliga källor på fliken **[!UICONTROL Catalog]** och autentiserade källor på fliken **[!UICONTROL Browse]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Åtkomst att skapa, acceptera och avvisa partnerhandskakningar för att ansluta två IMS-organisationer och aktivera [!DNL Segment Match]-flöden. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Tillgång att läsa, skapa, redigera och publicera [!DNL Segment Match]-flöden med aktiva partners. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Åtkomst för att läsa, skapa, redigera och ta bort i [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Åtkomst att läsa, skapa och ta bort användningsetiketter. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Åtkomst att läsa, skapa, redigera och ta bort dataanvändningsprinciper. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Skrivskyddad åtkomst till dataanvändningsprinciper som tillhör din organisation. |
| [!DNL Data Governance] | [!UICONTROL View Audit Log] | Skrivskyddad åtkomst för att visa registrerade [granskningsloggar](../landing/governance-privacy-security/audit-logs/overview.md) för plattformsaktiviteter. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Skrivskyddad åtkomst för att visa kontrollpanelen för licensanvändning. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Lägg till anpassade attribut som ännu inte finns i data warehouse. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Åtkomst att läsa, skapa, redigera och ta bort strukturerade SQL-frågor för plattformsdata. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Åtkomst för att skapa, uppdatera och ta bort ej förfallande autentiseringsuppgifter för åtkomst till frågetjänsten. |

## Nästa steg

Genom att läsa den här guiden har du lagts till i huvudprinciperna för åtkomstkontroll i [!DNL Experience Platform]. Du kan nu fortsätta med användarhandboken för [åtkomstkontrollen](./ui/overview.md) för detaljerade steg om hur du använder [!DNL Admin Console] för att skapa produktprofiler och tilldela behörigheter för [!DNL Platform].
