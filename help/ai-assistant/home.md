---
title: AI Assistant (äldre) i Adobe Experience Platform Overview
description: Lär dig mer om AI Assistant (äldre), dess nyanser och användningsexempel, och hur du kan använda det för att snabba upp arbetsflödet med Adobe Experience Platform och Real-Time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 68c55e370cab58ce5c93359520bf4ce671282a1b
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# AI Assistant (äldre) i Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet gäller för AI Assistant (äldre). Mer information om AI Assistant (Next-Gen) finns i [gränssnittsguiden för AI-assistenten](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) i [AI-dokumentationen i Experience Cloud](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/home).

I följande tabell finns en jämförelse mellan AI Assistant (äldre) och AI Assistant (nästa generation):

| Funktionsområde | AI Assistant (äldre) | AI Assistant (nästa generation) |
| --- | --- | --- |
| Användarupplevelse | AI Assistant (äldre) är endast tillgängligt på en panel på den högra listen. | AI Assistant (Next-Gen) finns både på den högra panelen och i en engagerande helskärmsupplevelse. |
| Funktionens omfattning | Du kan använda AI Assistant (äldre) för både produktkunskap och driftsinsikter. | Du kan använda AI Assistant (Next-Gen) för produktkunskap, driftsinsikter samt avancerade agetiska färdigheter och körning av uppgifter i flera steg. |
| Plattformsarkitektur | AI Assistant (äldre) är inte byggt på Agent Orchestrator-stacken. | AI Assistant (Next-Gen) drivs av [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) vilket möjliggör utbyggbarhet och avancerad samordning mellan funktioner. |
| Programtäckning | AI Assistant (äldre) är en programspecifik implementering. | Du kan använda AI Assistant (Next-Gen) för en enhetlig AI Assistant-upplevelse i alla Adobe Experience Cloud-program. |
| Åtkomst och behörighetsmodell | Åtkomstmodell som omfattas av programmet och som anpassas efter enskilda produktgränser. | Alla användare har tillgång till AI Assistant (Next-Gen) och tillhörande Experience Platform-agenter. **Obs!**: <ul><li>**Adobe Experience Manager**: Din administratör måste ge dig behörighet att komma åt AI Assistant (Next-Gen) via [Adobe Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics**: Din administratör måste ge dig behörighet att komma åt AI Assistant via [Customer Journey Analytics Access Control](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/technotes/access-control?lang=en). På så sätt kan du ställa frågor om produktkunskap och datainsikter. |

Följande video är avsedd att ge stöd för din förståelse av AI Assistant.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Läs det här dokumentet om du vill veta mer om AI Assistant (äldre) i Adobe Experience Platform.

AI Assistant (äldre) i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att snabba upp arbetsflödena i Adobe-program. Du kan använda AI Assistant (äldre) för att bättre förstå produktkunskap, felsöka problem eller söka genom information och hitta operativa insikter. AI Assistant (äldre) stöder Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

![AI Assistant-gränssnittet med förstagångsupplevelsen har utlösts.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Du måste godkänna ett [användaravtal](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) innan du kan använda AI Assistant (äldre). Användaravtalet innehåller även det allmänna betaavtalet. Detta gör att du kan använda ytterligare AI Assistant-funktioner (äldre) när de lanseras i en betapacitet.

+++Välj om du vill visa användaravtalsgränssnittet

![Användaravtalets första sida.](./images/user-agreement-1.png)

![Den sista sidan i användaravtalet.](./images/user-agreement-2.png)

+++

## Förstå AI-assistenten {#understanding-ai-assistant}

AI Assistant (äldre) svarar på dina inskickade frågor genom att fråga en databas och sedan omvandla data från databasen till ett läsbart svar.

Den här interna representationen av underliggande data kallas också **[!DNL Knowledge Graph]** - en omfattande webbplats med koncept, data och metadata för ett givet svar.

[!DNL Knowledge Graph] består av deldiagram som refereras till när frågor skickas:

* Kundens operativa insikter.
* Kundens operativa insikter i olika metabutiker.
* Experience League dokumentation.

Det finns två typer av frågor att tänka på innan du frågar AI Assistant (äldre):

### Produktkunskap {#product-knowledge}

Produktkännedom avser begrepp och ämnen som beskrivs i Experience League dokumentation. Produktkunskapsfrågor kan specificeras ytterligare i följande undergrupper:

| Produktkunskap | Exempel |
| --- | --- |
| Undervisning | <ul><li>Vad är skillnaden mellan en identitet och en primär eller extern nyckel?</li><li>Vad är lookalike-målgrupper?</li></ul> |
| Öppna identifiering | <ul><li>Hur exporterar jag den här datauppsättningen?</li><li>Finns det scheman för vårdkunder?</li></ul> |
| Felsökning | <ul><li>Varför kan jag inte aktivera ett schema som ägs av Adobe för en profil?</li><li>Varför kan jag inte ta bort ett segment?</li></ul> |

{style="table-layout:auto"}

Titta på följande video för mer information om AI Assistant-produktkunskap (äldre):

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### Driftsinsikter {#operational-insights}

Användningsinsikter hänvisar till svar AI Assistant (äldre) genererar om dina metadata-objekt (attribut, målgrupper, dataflöden, datauppsättningar, destinationer, resor, scheman och källor), inklusive antal, sökningar och linjepåverkan. Den tittar inte på några data i sandlådan.

* Hur många datauppsättningar har jag?
* Hur många schemaattribut har aldrig använts?
* Vilka målgrupper har aktiverats?

Du kan ställa frågor om AI Assistant (äldre) om dina operativa insikter i följande domäner:

| Domän | Metadata som stöds | Metadata som inte stöds |
| --- | --- | --- |
| Attribut | <ul><li>Sök attributnamn</li><li>Attribut - schemarelation</li><li>Attribut - datauppsättningsrelation</li><li>Attribut - målgruppsrelation</li><li>Attribut - målrelation</li></ul> | <ul><li>Klassen Attribute</li><li>Granskning</li><li>Föråldringsstatus</li><li>Etiketter</li><li>Värde lagrat i attribut</li></ul> |
| Målgrupper | <ul><li>Antal målgrupper</li><li>Målgruppstyp (direktuppspelning eller batch)</li><li>Skapande-/ändringsdatum</li><li>Aktiveringsstatus</li><li>Profilantal</li><li>Duplicera målgrupper</li><li>Sök efter målgruppsdefinition</li><li>Målgrupp - målgruppsrelation</li><li>Målgrupp - attributrelation</li><li>Målgrupp - datauppsättningsrelation</li><li>Målgrupp - målrelation</li><li>Namnsökning</li><li>Sök namn och ID | <ul><li>Målgruppsöverlappningar</li><li>Målgruppsaktivering</li><li>Målgrupp - kampanjrelationer</li><li>Granskning</li><li>Skapa/ändra</li><li>Etiketter</li><li>Profilkvalificeringstrender</li></ul> |
| Dataflöden | <ul><li>Antal dataflöden</li><li>Dataflödesstatus</li><li>Dataflöde - Datauppsättningsrelation</li><li>Dataflöd - källrelation</li></ul> | <ul><li>Skapande/ändring</li><li>Dataflödesbatchrelationer</li><li>Antal infogningsprofiler</li></ul> |
| Datauppsättningar | <ul><li>Antal data</li><li>Aktivera profilstatus</li><li>Skapad/ändrad den</li><li>Datauppsättning - schemarelation</li><li>Datauppsättning - målgruppsrelation</li><li>Datauppsättning - attributrelation</li><li>Datauppsättning - dataflödesrelation</li><li>Datauppsättningsstorlek</li><li>Antal rader</li><li>Namnsökning </li><li>Sök namn och ID</li></ul> | <ul><li>Granskning</li><li>Skapad av</li><li>Datauppsättning - batchrelation</li><li>Skapa/ändra datauppsättning</li><li>Antal profiler</li><li>Värdesökning</li></ul> |
| Mål | <ul><li>Konfigurerade destinationsantal</li><li>Mål - målgruppsrelation</li><li>Destinationsattributrelation</li></ul> | <ul><li>Kontoinställning</li><li>Autentiseringsinformation för konto</li><li>Unika profiler har aktiverats</li></ul> |
| Resor | <ul><li>Antal</li><li>Namnsökning</li><li>Sök namn och ID</li><li>Resestatus</li><li>Utlöst status (målgrupp kontra händelse)</li><li>Skapande-/ändringsdatum</li><li>Återkommande frekvens</li></ul> | <ul><li>Attribut - reserelationer</li><li>Granskning</li><li>Skapande/ändring</li><li>Skapad av</li><li>Händelser</li><li>Resa - datauppsättning</li><li>Resa - schema</li><li>Erbjudanden</li><li>Profilkvalificeringstrender</li><li>Steg för händelser</li></ul> |
| Scheman | <ul><li>Antal scheman</li><li>Skapad/ändrad den</li><li>Schema - attributrelation</li><li>Schema - datauppsättningsrelation</li><li>Schema - målgruppsrelation</li><li>Aktivera profilstatus</li><li>Namnsökning</li><li>Sök namn och ID</li></ul> | <ul><li>Granskning</li><li>Skapande/ändring</li><li>Skapad av</li><li>Fältgrupper</li><li>Identiteter</li><li>Identitetsnamnutrymmen</li><li>Etiketter</li><li>Antal profiler</li></ul> |
| Källor | <ul><li>Konton</li><li>Kontostatus</li><li>Aktiva/inaktiva dataflöden för varje konto</li><li>Source-anslutning - dataflödesrelation</li><li>Source-konto - dataflödesrelation</li></ul> | <ul><li>Information om kontoautentiseringsuppgifter</li><li>Kontoinställning</li><li>Mätvärden för dataöverföring</li><li>Antal profiler</li><li>Source - batchrelationer</li></ul> |

{style="table-layout:auto"}

När det gäller frågor om driftsinsikter kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som stödjer dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Du måste logga in i en sandlåda för att få veta mer om specifika data som är relaterade till objekt.

Titta på följande video för mer information om AI Assistant (äldre) driftsinsikter:

>[!VIDEO](https://video.tv.adobe.com/v/3444031?learn=on&enablevpops)

### Funktionsomfång {#feature-scope}

För närvarande har AI Assistant följande omfattning (äldre):

* [Produktkunskap](./home.md#product-knowledge): AI Assistant (äldre) kan besvara produktkunskapsfrågor för Experience Platform, Real-Time Customer Data Platform och Adobe Journey Optimizer. Du kan också gå in i produktinformationsämnen för Customer Journey Analytics, men bara via Customer Journey Analytics användargränssnitt.
* [Driftsinsikter](./home.md#operational-insights): Du kan ställa frågor till AI Assistant (äldre) om driftsinsikter för följande dataobjekt: attribut, målgrupper, dataflöden, datauppsättningar, destinationer, resor, scheman och källor.

## Nästa steg

Nu när du har en allmän förståelse för AI Assistant (äldre) kan du fortsätta och använda AI Assistant (äldre) under arbetsflödena. Mer information finns i följande dokumentation:

* [Användargränssnittshandbok för AI Assistant (äldre)](./ui-guide.md)
* [Funktionsåtkomst](./access.md)
* [Frågeguide](./questions.md)
* [Integritet, säkerhet och styrning i AI Assistant (äldre)](./privacy.md)
* [Vanliga frågor och svar](./faq.md)
