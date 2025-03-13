---
keywords: Experience Platform;home;populära topics;access control;adobe admin console
solution: Experience Platform
title: Översikt över åtkomstkontroll
description: Åtkomstkontroll för Adobe Experience Platform tillhandahålls via Adobe Admin Console. Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 50d768eeb0dc8fa85af113db7790ad3e3258ea64
workflow-type: tm+mt
source-wordcount: '3222'
ht-degree: 0%

---

# Översikt över åtkomstkontroll

Åtkomstkontroll för Adobe Experience Platform tillhandahålls via **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/). Den här funktionen utnyttjar roller och principer som länkar användare med behörigheter och sandlådor.

## Åtkomststyrningshierarki och arbetsflöde

För att kunna konfigurera åtkomstkontroll för Experience Platform måste du ha system- eller produktadministratörsbehörighet för en organisation som har en Experience Platform-produkt. Minimirollen som kan bevilja eller återkalla behörigheter är en produktadministratör. Andra administratörsroller som kan hantera behörigheter är systemadministratörer (inga begränsningar). Mer information finns i Adobe Help Center-artikeln om [administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html).

>[!NOTE]
>
>Från och med nu avser alla omnämnanden av&quot;administratör&quot; i det här dokumentet en produktadministratör eller en senare (enligt ovan).

Ett arbetsflöde på hög nivå för att hämta och tilldela åtkomstbehörigheter kan sammanfattas på följande sätt:

- När du har licensierat Adobe Experience Platform, eller en program-/apptjänst som använder Experience Platform, skickas ett e-postmeddelande till administratören som anges under licensieringen.
- Administratören loggar in på [Adobe Admin Console](#adobe-admin-console) och väljer **Adobe Experience Platform** i produktlistan på översiktssidan.
- Om du vill ge åtkomst till Experience Platform rekommenderar vi att administratören lägger till användare i standardproduktprofilen: `AEP-Default-All-Users`.
- I Experience Platform Permissions kan administratören skapa nya roller eller redigera behörigheter och användare för befintliga roller.
- När en roll skapas eller redigeras lägger administratören till användare i rollen med fliken **[!UICONTROL users]** och tilldelar behörigheter till dessa användare (till exempel [!UICONTROL Read Datasets] eller [!UICONTROL Manage Schemas]) genom att redigera rollens behörigheter. På samma sätt kan administratören tilldela åtkomst till sandlådor med samma redigeringsalternativ.
- När användare loggar in på Experience Platform användargränssnitt styrs deras åtkomst till Experience Platform-funktioner av de behörigheter de fått från föregående steg. Om en användare t.ex. inte har behörigheten [!UICONTROL View Datasets] kommer fliken **[!UICONTROL Datasets]** på sidomenyn inte att vara synlig för användaren.

Mer detaljerad information om hur du hanterar åtkomstkontroll i Experience Platform finns i användarhandboken för [åtkomstkontroll](./ui/overview.md).

Alla anrop till Experience Platform API:er valideras för behörigheter och returnerar fel om lämpliga behörigheter inte hittas i den aktuella användarkontexten. Elementen döljs eller ändras i användargränssnittet beroende på vilka behörigheter den aktuella användaren har.

## Behörigheter {#platform-permissions}

[!UICONTROL Permissions] är en central plats för hantering av Experience Platform-åtkomst för din organisation. Genom [!UICONTROL Permissions] kan du ge användargrupper åtkomstbehörigheter för olika Experience Platform-funktioner, som [!UICONTROL Manage Datasets], [!UICONTROL View Datasets] eller [!UICONTROL Manage Profiles].

### Roller

I avsnittet [!UICONTROL Roles] tilldelas användare behörigheter genom användning av roller. Med roller kan du tilldela behörigheter till en eller flera användare, och de kan även innehålla deras åtkomst till omfattningen av de sandlådor som tilldelats dem via roller. Användare kan tilldelas till en eller flera roller som tillhör din organisation.

### Standardroller

Experience Platform har två förkonfigurerade standardroller. Följande tabell visar vad som anges i respektive standardprofil, inklusive vilken sandlåda de beviljar åtkomst till samt de behörigheter de ger inom den sandlådans omfång.

| Roll | Sandlådeåtkomst | Behörigheter |
| --- | --- | --- |
| Standardproduktion, all åtkomst | Prod | Alla behörigheter som gäller för Experience Platform, förutom sandlådeadministration. |
| Sandlådeadministratörer | N/A | Ger åtkomst till sandlådan `Prod` och till administratörsbehörigheter för sandlådan. |

## Sandlådor och behörigheter

Sandlådor som inte är produktionssandlådor är en form av datavirtualisering som gör att du kan isolera data från andra sandlådor och som vanligtvis används för utvecklingsexperiment, testning och testning. En rolls behörigheter ger rollens användare åtkomst till Experience Platform-funktioner i sandlådemiljöer som de har beviljats åtkomst till. En standardlicens för Experience Platform ger dig fem sandlådor (en produktion och fyra icke-produktioner). Du kan lägga till paket med tio icke-produktionssandlådor, upp till totalt högst 75 sandlådor. Kontakta din organisations administratör eller din Adobe-säljare för mer information.

Mer information om sandlådor i Experience Platform finns i [översikten över sandlådor](../sandboxes/home.md).

### Åtkomst till sandlådor

Åtkomst till sandlådor hanteras via roller. Detaljerade steg om hur du aktiverar åtkomst till en sandlåda för en roll finns i handboken [för attributbaserade åtkomstkontrollsroller](./abac/ui/roles.md).

Användare kan beviljas åtkomst till en eller flera sandlådor i en roll. Om en användare ingår i två eller flera roller får den användaren åtkomst till alla sandlådor som ingår i de rollerna.

Med behörigheten&quot;Sandlådehantering&quot; kan användare hantera, visa och återställa sandlådor.

### Resursbehörigheter {#permissions}

Resursbehörigheter ger åtkomst till specifika Experience Platform-funktioner. Resurserna är indelade i kategorier som innehåller en uppsättning relevanta behörigheter, som kan tilldelas roller individuellt.

I [!UICONTROL Permissions] visar en rolls resurarbetsyta de sandlådor och behörigheter som är aktiva för den rollen:

![En rolls arbetsyta för resurser med en lista över valda kategorier och behörigheter.](./images/permissions.png)

I följande tabell visas de tillgängliga resurskategorierna för både Experience Platform och program som hanteras via behörigheter:

| Kategori | Beskrivning |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Konfigurera, hantera och visa behörigheter för [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Konfigurera behörigheter för [!DNL AI Assistant]. |
| [!DNL Alerts] | Konfigurera hantera, lösa och visa behörigheter för aviseringar och aviseringshistorik. |
| [!DNL B2B Account Lists] | Konfigurera hanterings-, vy- och publiceringsbehörigheter för B2B-kontolistor, inklusive åtgärder som att lägga till, ta bort, importera och ta bort konton från kontolistor. |
| [!DNL B2B Admin Configurations] | Konfigurera hanterings- och visningsbehörigheter för B2B-administratörskonfigurationer, inklusive anslutningar för digital resurshantering, resursarkiv och händelser. |
| [!DNL B2B Assets] | Konfigurera hanterings- och visningsbehörigheter för B2B-resurser, inklusive e-post, SMS, landningssidor, fragment, mallar och bilder. |
| [!DNL B2B Buying Groups] | Konfigurera hanterings- och visningsbehörigheter för B2B-inköpsgrupper, inklusive funktioner som lösningsintressen, rollmallar och inköpsgruppsstatus. |
| [!DNL B2B Channel Configurations] | Konfigurera hanterings- och visningsbehörigheter för B2B-kanalkonfigurationer, inklusive inställningar som kommunikationsbegränsningar, API-autentiseringsuppgifter och säkerhetsinställningar. |
| [!DNL B2B Dashboards] | Konfigurera visningsbehörigheter för B2B-instrumentpaneler, inklusive funktioner som kontoengagemang, inköpsgruppsfaser, surging-konton och kontakttäckning. |
| [!DNL B2B Journeys] | Konfigurera hanterings-, vy- och publiceringsbehörigheter för B2B-resor, inklusive funktioner som konto- och personåtgärder, händelseavlyssnare och delade sökvägar. |
| [!DNL Campaigns] | Konfigurera hantera, publicera och visa behörigheter för kampanjer i Journey Optimizer. |
| [!DNL Channel Configurations] | Konfigurera funktioner för hantering, visning och export av kanalkonfigurationer, till exempel underdomäner, IP-pooler, meddelandeförinställningar, PTR-poster, undertryckslistor, inställningar för landningssidor, SMS-inställningar och filroutning. |
| [!DNL Collaborations] | Konfigurera hanterings- och visningsbehörigheter för Collaboration-funktioner för kunddataprofiler i realtid. |
| [!DNL Computed Attributes] | Konfigurera hanterings- och visningsbehörigheter för utkast eller publicerade beräknade attribut. |
| [!DNL Customer Managed Keys] | Konfigurera hantera behörigheter för kundhanterade nycklar. |
| [!DNL Dashboards] | Konfigurera hanterings- och visningsbehörigheter för standardkontrollpaneler, anpassade kontrollpaneler och licensierade paneler. |
| [!DNL Data Collection] | Konfigurera hanterings- och visningsbehörigheter för datastreams. |
| [!DNL Data Governance] | Konfigurera hanterings-, tillämpnings- och visningsbehörigheter för datastyrningsfunktioner som etiketter, principer och aktivitetsloggar. |
| [!DNL Data Ingestion] | Konfigurera hanterings- och visningsbehörigheter för dataöverföringsfunktioner som källor och målgruppsresurser. |
| [!DNL Data Lifecycle] | Konfigurera hanterings- och visningsbehörigheter för datahygien. |
| [!DNL Data Management] | Konfigurera hanterings- och visningsbehörigheter för datahanteringsfunktioner som datauppsättningar och övervakning av datauppsättningar och strömmar. |
| [!DNL Data Modeling] | Konfigurera hanterings- och visningsbehörigheter för datamodelleringsfunktioner som scheman, relationer och identitetsmetadata. |
| [!DNL Data Science Workspace] | Konfigurera hantera behörigheter för [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Konfigurera hanterings- och visningsbehörigheter för beslut, erbjudanden och rankningsstrategier i beslutsprocessen. |
| [!DNL Destinations] | Konfigurera hanterings- och visningsbehörigheter för mål, inklusive funktioner som aktivering och redigering med Destinations SDK. |
| [!DNL Federated Data] | Konfigurera hanterings- och visningsbehörigheter för federerade datafunktioner. |
| [!DNL Identity Management] | Konfigurera hanterings- och visningsbehörigheter för identitetstjänstfunktioner som identitetsnamnutrymmen och identitetsdiagram. |
| [!DNL Intelligent Service] | Konfigurera hanterings- och visningsbehörigheter för attribuering av AI och kundens AI i intelligent service. |
| [!DNL IP Warmup Configurations] | Konfigurera hanterings- och visningsbehörigheter för IP-uppvärmningsplaner och visa behörigheter för att visa IP-värmerapporter. |
| [!DNL Journey Optimizer Library] | Konfigurera hantering av behörigheter för biblioteksobjekt i Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Konfigurera hanterings- och visningsbehörigheter för frekvensregler i Adobe Journey Optimizer. |
| [!DNL Journeys] | Konfigurera hanterings-, publicerings- och visningsbehörigheter för resor, inklusive funktioner som reserapporter, händelser, datakällor och åtgärder. |
| [!DNL Messages] | Konfigurera behörighet att hantera, publicera och visa meddelanden, inklusive funktioner som förhandsgranskning och test av meddelanden. |
| [!DNL Privacy Service] | Konfigurera hanterings- och visningsbehörigheter för Privacy Service-funktioner. |
| [!DNL Profile Management] | Konfigurera behörighet att hantera, visa, exportera och utvärdera till profiltjänster som målgrupper, profiler och sammanfogningsprinciper. |
| [!DNL Prospects] | Konfigurera hantering och visning av behörigheter till scheman, profiler och målgrupper för potentiella kunder, inklusive funktioner som att se dragspelspanelen för potentiella kunder. |
| [!DNL Query Service] | Konfigurera behörighetshantering för att fråga efter tjänstfunktioner som t.ex. ej förfallande autentiseringsuppgifter och strukturerade SQL-frågor. |
| [!DNL Reports] | Konfigurera visningsbehörigheter för att kanalisera rapporter. |
| [!DNL Sandbox Administration] | Konfigurera behörighet att hantera, visa och återställa när sandlådor administreras. |
| [!DNL Traits Configuration] | Konfigurera hantera och visa egenskaper via det beräknade attributgränssnittet. |
| [!DNL Translation Services] | Konfigurera hanterings- och visningsbehörigheter för översättningstjänster för projekt, uppgifter, granskningar, intern information, inställningar och leverantörer. |

I följande tabell visas de behörigheter som är tillgängliga för Experience Platform i rollen, med beskrivningar av de specifika Experience Platform-funktioner som de ger åtkomst till. Detaljerade anvisningar om hur du lägger till behörigheter i en roll finns i handboken [om attributbaserade åtkomstkontrollsroller](./abac/ui/roles.md).

| Kategori | Behörighet | Beskrivning |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | Möjlighet att visa och ändra harmoniserade data. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | Skrivskyddad åtkomst till harmoniserade data. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | Möjlighet att visa och ändra modellkonfigurationer. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | Skrivskyddad åtkomst till modellkonfigurationer. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | Möjlighet att visa och ändra plankonfigurationer. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | Skrivskyddad åtkomst till plankonfigurationer. |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | Möjlighet att ställa [!DNL [AI assistant]](../ai-assistant/access.md) frågor. |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | Åtkomst att få svar på [operativa insikter](../ai-assistant/home.md##operational-insights)-frågor. |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | Gör det möjligt för användare att generera innehåll med [!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | Gör det möjligt för användare att skapa varumärkesriktlinjer med [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | Skrivskyddad åtkomst för aviseringshistorik. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | Tillgång till att läsa, redigera och ta bort aviseringar. |
| [!DNL Alerts] | [!UICONTROL View Alerts] | Skrivskyddad åtkomst för aviseringar. |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | Åtkomst för att läsa, skapa, redigera och ta bort aviseringar. |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | Möjlighet att visa och komma åt **[!UICONTROL Account Lists]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Account Lists]** bör ha åtkomst till alla CRUD-funktioner för kontolistor: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | Möjlighet att visa och komma åt **[!UICONTROL B2B Admin Configurations]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL B2B Admin Configurations]** bör ha åtkomst till alla CRUD-funktioner för SMS API-autentiseringsuppgifter: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | Möjlighet att visa och komma åt **[!UICONTROL Assets]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Assets]** bör ha åtkomst till alla Assets CRUD-funktioner: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | Möjlighet att visa och komma åt **[!UICONTROL Templates]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Templates]** bör ha åtkomst till alla Templates CRUD-funktioner: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | Möjlighet att visa och komma åt **[!UICONTROL Fragments]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Fragments]** bör ha åtkomst till alla Fragments CRUD-funktioner: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | Möjlighet att visa och komma åt **[!UICONTROL Buying Groups]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Buying Groups]** bör ha åtkomst till alla inköpsgruppers CRUD-funktioner: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | Möjlighet att visa och komma åt **[!UICONTROL Dashboard]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Dashboards]** bör ha åtkomst till alla CRUD-funktioner för instrumentpaneler: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | Möjlighet att visa och komma åt **[!UICONTROL Channels]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Channels]** bör ha åtkomst till alla Channel CRUD-funktioner: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | Möjlighet att visa och komma åt **[!UICONTROL Account Journeys]** i den vänstra navigeringen. Användare med åtkomst till **[!UICONTROL Account Journeys]** bör ha åtkomst till alla CRUD-funktioner för kontoresor: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | Tillgång till att läsa, skapa, redigera och ta bort kampanjer. |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | Möjlighet att godkänna och publicera kampanjer. |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | Publicera kampanjer. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | Skrivskyddad åtkomst till kampanjer. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | Skrivskyddad åtkomst till kampanjrapporter. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | Skrivskyddad åtkomst till allmänna inställningar för meddelanden. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | Åtkomst att läsa, skapa, redigera och ta bort underdomänsdelegeringar. |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | Åtkomst för att läsa, skapa och redigera IP-pooler. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | Åtkomst att läsa, skapa, redigera och ta bort meddelanden med allmänna inställningar. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | Åtkomst för att läsa, skapa, redigera och ta bort meddelandeförinställningar. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | Skrivskyddad åtkomst till meddelandeförinställningar. |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | Åtkomst att läsa och redigera PTR-poster. |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | Skrivskyddad åtkomst till PTR-poster. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | Åtkomst för att läsa, skapa, redigera och ta bort undertryckningsregler. |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | Skrivskyddad åtkomst till suppressionslistan. |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | Åtkomst till export av undertryckningslistan som en CSV-fil. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | Åtkomst för att läsa, skapa, redigera och ta bort inställningar för landningssidor. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | Åtkomst för att läsa, skapa, redigera och ta bort SMS-inställningar. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | Åtkomst att läsa, skapa, redigera och ta bort SMS-underdomäner. |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | Åtkomst för att läsa, skapa, redigera och ta bort filroutningar. |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | Skrivskyddad åtkomst till filroutningar. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | Möjlighet att skapa och redigera Seed-listan. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | Möjlighet att skapa och redigera språkinställningarna. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | Möjlighet att skapa och redigera CJM-webbunderdomäner. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | Möjlighet att skapa, redigera och ta bort push-referenser. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | Visa, skapa, uppdatera och ta bort en organisations samarbetsinstanser. Upptäck hur andra organisationer samarbetar. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | Läs en organisations samarbetsinstanser och se andra organisationers samarbetsinstanser. |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | Visa, skapa och ta bort anslutningsinbjudningar som initierats av din organisation. Acceptera och avböj inbjudan om anslutning som initierats av andra organisationer. |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | Skrivskyddad åtkomst till anslutningsinbjudningar. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | En annonsör kan visa, skapa och uppdatera inställningar samt skicka och ta bort anslutningar. En utgivare kan visa, acceptera eller neka anslutningar. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | Skrivskyddad åtkomst till anslutningar. |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | Anlita och identifiera målgrupper. Uppdatera publika, privata och anpassade målgrupper och hantera metadatainställningar för Audience Inventory. |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | Läs och identifiera målgrupper. |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | Lägg in, uppdatera och ta bort mätdata. |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | Skrivskyddad åtkomst till mätdata. |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | Visa, skapa, uppdatera och ta bort projekt för någon av aktiviteterna för upptäckt, delning, aktivering och mätning. |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | Visa projekt för någon av aktiviteterna för upptäckt, delning, aktivering och mätning. |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | Skrivskyddad åtkomst till användaraktiviteter. |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | Exportera användaraktiviteter. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | Kreditövervakning på organisations- och instansnivå. |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | Skrivskyddad åtkomst för fliken, lagret och informationen för beräknade attribut. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | Åtkomst för att läsa, skapa, ta bort utkast och inaktivera beräknade attribut. |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | Tillgång till att visa och konfigurera kundhanterade nycklar. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Skrivskyddad åtkomst för att visa kontrollpanelen för licensanvändning. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Lägg till anpassade attribut som ännu inte finns i datalagret. |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | Skrivskyddad åtkomst för att visa kontrollpanelen för licensanvändning. |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | Åtkomst för att skapa eller redigera en kontrollpanel. |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | Skrivskyddad åtkomst till användardefinierade instrumentpaneler. |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | Möjlighet att skapa scheman. |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | Åtkomst för att läsa, skapa och redigera datastreams. |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | Skrivskyddad åtkomst till datastreams. |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | Åtkomst att läsa, skapa och ta bort användningsetiketter. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Åtkomst att läsa, skapa, redigera och ta bort dataanvändningsprinciper. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Skrivskyddad åtkomst till dataanvändningsprinciper som tillhör din organisation. |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | Skrivskyddad åtkomst för att visa inspelade [granskningsloggar](../landing/governance-privacy-security/audit-logs/overview.md) för plattformsaktiviteter. |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | Skrivskyddad åtkomst till sekretesskonsoler. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Tillgång till att läsa, skapa, redigera och inaktivera källor. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Skrivskyddad åtkomst till tillgängliga källor på fliken **[!UICONTROL Catalog]** och autentiserade källor på fliken **[!UICONTROL Browse]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Åtkomst att skapa, acceptera och avböja partnerdelning för att ansluta två organisationer och aktivera [!DNL Segment Match]-flöden. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Åtkomst att läsa, skapa, redigera och publicera [!DNL Segment Match]-feeds med aktiva partners. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | Skrivskyddad åtkomst för datalängd. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | Tillgång till att läsa, skapa, redigera och ta bort livscykeln för data. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Åtkomst för att läsa, skapa, redigera och ta bort scheman och relaterade resurser. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Skrivskyddad åtkomst till scheman och relaterade resurser. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Åtkomst för att läsa, skapa, redigera och ta bort schemarelationer. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Åtkomst för att läsa, skapa, redigera och ta bort identitetsmetadata för scheman. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar. Skrivskyddad åtkomst för scheman. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Skrivskyddad åtkomst för datauppsättningar och scheman. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Skrivskyddad åtkomst till övervakning av datauppsättningar och strömmar. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Åtkomst att läsa, skapa, redigera och ta bort i [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | Möjlighet att hantera enheter för upplevelsebeslut. |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | Skrivskyddad åtkomst till enheter för upplevelsebeslut. |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | Åtkomst för att läsa, skapa, redigera och ta bort beslutsenheter. |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | Skrivskyddad åtkomst till beslutsenheter. |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | Tillgång att läsa, skapa, redigera och ta bort alla erbjudanden och komponenter. Skrivskyddad åtkomst till beslut och samlingar. |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | Tillgång till att läsa, skapa, redigera och ta bort anpassade rapporter och använda åtgärdsfunktioner. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Skrivskyddad åtkomst för att visa tillgängliga mål på fliken **[!UICONTROL Catalog]** och autentiserade mål på fliken **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Åtkomst för att läsa, skapa och ta bort målanslutningar och destinationskonton. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Möjlighet att aktivera data till aktiva destinationer som har skapats. Den här behörigheten kräver också att antingen [!UICONTROL View Destinations] eller [!UICONTROL Manage Destinations] beviljas den användare som ska aktivera destinationer. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | Möjlighet att aktivera målgrupper till befintliga mål utan att visa [mappningssteget](../destinations/ui/activate-batch-profile-destinations.md#mapping). Användare kan lägga till och ta bort målgrupper i aktiveringsarbetsflöden, men kan inte lägga till eller ta bort mappade attribut eller identiteter. Den här behörigheten kräver även att behörigheten [!UICONTROL View Destinations] beviljas den användare som ska aktivera data till mål. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | Möjlighet att läsa, skapa, redigera och inaktivera datauppsättningsexportflöden. Möjlighet att även aktivera data till aktiva datauppsättningar som har skapats. Den här behörigheten kräver även att behörigheten [!UICONTROL View Destinations] beviljas den användare som ska aktivera data till mål. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Möjlighet att skapa mål med [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | Möjlighet att få tillgång till alla federerade datafunktioner som att skapa scheman, modeller och kompositioner. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | Åtkomst för att läsa, skapa, redigera och ta bort identitetsnamnutrymmen. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | Skrivskyddad åtkomst för identitetsnamnutrymmen. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | Skrivskyddad åtkomst för identitetsdiagram. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | Åtkomst för att läsa, skapa och redigera identitetsinställningar. |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | Skrivskyddad åtkomst till identitetsinställningar. |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | Skrivskyddad åtkomst för AI-inställningar och insikter för attribuering. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | Åtkomst för att läsa, skapa, redigera och ta bort AI-modeller för attribut. |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | Tillgång till att läsa eller visa kundens AI-modeller. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | Tillgång till att skapa, uppdatera, ta bort, aktivera eller inaktivera kundens AI-modeller. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | Skrivskyddad åtkomst till IP-beredskapsplaner. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | Möjlighet att hantera IP-uppvärmningsplaner. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | Skrivskyddad åtkomst till rapporter om IP-värmare. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | Tillgång att läsa, skapa, redigera och ta bort resor. |
| [!DNL Journeys] | [!UICONTROL View Journeys] | Skrivskyddad åtkomst till resor. |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | Skrivskyddad åtkomst till reserapport. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | Åtkomst för att läsa, skapa, redigera och ta bort händelser, datakällor eller åtgärder. |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | Skrivskyddad åtkomst till händelser, datakällor eller åtgärder. |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | Möjlighet att godkänna och publicera resor när en policy tillämpas. |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | Möjlighet att publicera resor. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | Möjlighet att lägga till och ta bort sparade uttryck. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | Möjlighet att publicera innehållsfragment. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | Tillgång till alternativet för att simulera innehåll för förhandsgranskning och korrektur. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | Skrivskyddad åtkomst till frekvensregler. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | Åtkomst för att läsa, skapa, redigera eller ta bort frekvensregler. |
| [!DNL Messages] | [!UICONTROL Manage Messages] | Åtkomst för att läsa, skapa, redigera och ta bort meddelanden. |
| [!DNL Messages] | [!UICONTROL View Messages] | Skrivskyddad åtkomst till meddelanden. |
| [!DNL Messages] | [!UICONTROL View Messages Report] | Åtkomst att läsa och redigera meddelanderapporter. |
| [!DNL Messages] | [!UICONTROL Publish Messages] | Möjlighet att publicera meddelanden. |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | Möjlighet att godkänna och publicera meddelanden när en policy tillämpas. |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | Tillgång till arbetsflöden för läs- och skrivsekretess. |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | Skrivskyddad åtkomst till arbetsflöden för sekretess. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Åtkomst för att läsa, skapa, redigera och ta bort datauppsättningar som används för kundprofiler. Skrivskyddad åtkomst till tillgängliga profiler. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Skrivskyddad åtkomst till tillgängliga profiler. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Tillgång till att läsa, skapa, redigera och ta bort målgrupper. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Skrivskyddad åtkomst till tillgängliga målgrupper. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Åtkomst för att läsa, skapa, redigera och ta bort sammanfogningsprinciper. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Skrivskyddad åtkomst till tillgängliga kopplingsprofiler. |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | Möjlighet att använda arbetsflödet för CSV-överföring för att importera nya målgrupper. |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | Möjlighet att exportera en utvärderad målgrupp till en datauppsättning. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Möjlighet att generera profiler för en viss målgrupp genom att utvärdera en segmentdefinition. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | Skrivskyddad åtkomst till inställningar och konfigurationer för alla B2B AI/ML-tjänster. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | Åtkomst att läsa, skapa, redigera och ta bort inställningar och konfigurationer för alla B2B AI/ML-tjänster. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | Skrivskyddad åtkomst till B2B-entitetsprofiler (som Konto, Möjligheter och så vidare), inställningar och konfigurationer för alla B2B AI/ML-tjänster och B2B-instrumentpanelswidgetar. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | Åtkomst för att läsa, skapa, redigera och ta bort B2B-enhetsprofiler (t.ex. konto, säljprojekt). Skrivskyddad åtkomst för inställningar och konfigurationer för alla B2B AI/ML-tjänster och B2B-instrumentpanelswidgetar. |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | Möjlighet att skapa eller ta bort lookalike-målgrupper. |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | Möjlighet att visa B2B-profiler och attribut. |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | Skrivskyddad åtkomst till alla profilinställningar. |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | Åtkomst för att läsa och redigera alla profilinställningar. |
| [!DNL Prospects] | [!UICONTROL View Prospects] | Skrivskyddad åtkomst till scheman, profiler, målgrupper och dragspelspanelen för potentiella kunder. |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | Möjlighet att skapa och hantera scheman, profiler och målgrupper för potentiella kunder. Skrivskyddad åtkomst till den potentiella kundens dragspelspanel. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Åtkomst att läsa, skapa, redigera och ta bort strukturerade SQL-frågor för plattformsdata. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Åtkomst för att skapa, uppdatera och ta bort ej förfallande autentiseringsuppgifter för åtkomst till frågetjänsten. |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | Möjlighet att avlägsna befintliga sessioner. |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | Möjlighet att hantera IP-begränsningar för din organisation. |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | Möjlighet att visa och ändra kanalrapporter. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Åtkomst för att läsa, skapa, redigera och ta bort sandlådor. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Skrivskyddad åtkomst för sandlådor som tillhör din organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Möjlighet att återställa en sandlåda. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | Åtkomst för att skapa, importera och exportera paket. |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | Åtkomst att dela paket mellan olika organisationer. |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | Skrivskyddad åtkomst för egenskaper. |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | Tillgång till att hantera egenskaper. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | Möjlighet att hantera översättningsprojekt. |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | Skrivskyddad åtkomst till översättningsprojekt. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | Möjlighet att hantera översättningsuppgifter. |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | Skrivskyddad åtkomst till översättningsuppgifter. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | Möjlighet att hantera översättningsgranskningar. |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | Skrivskyddad åtkomst till översättningsgranskningar. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | Möjlighet att hantera intern översättning. |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | Skrivskyddad åtkomst till intern översättning. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | Administratörer kan hantera översättningsinställningar. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | Möjlighet att hantera översättningsleverantörer. |

## Nästa steg

Genom att läsa den här guiden har du lagts till de viktigaste principerna för åtkomstkontroll i Experience Platform. Du kan nu fortsätta till den [attributbaserade användarhandboken för åtkomstkontroll](./abac/overview.md) för detaljerade steg om hur du använder Experience Cloud för att skapa roller och tilldela behörigheter för Experience Platform.
