---
title: AI Assistant i Adobe Experience Platform - översikt
description: Lär dig mer om AI Assistant, dess nyanser och användningsexempel, och hur du kan använda det för att snabba upp arbetsflödet med Adobe Experience Platform och Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e8939132c1508e1dfc4028e6c8ff23662d6c2b2b
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# AI Assistant i Adobe Experience Platform

Läs det här dokumentet om du vill veta mer om AI Assistant i Adobe Experience Platform.

AI Assistant i Adobe Experience Platform är en samtalsupplevelse som du kan använda för att snabba upp arbetsflödena i Adobe-program. Du kan använda AI Assistant för att få en bättre förståelse för produktkunskaper, felsöka problem eller söka i information och hitta operativa insikter. AI Assistant har stöd för Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

![AI Assistant-gränssnittet med förstagångsupplevelsen aktiveras.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Du måste godkänna [användaravtal](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) innan du kan använda AI-assistenten. Användaravtalet innehåller även det allmänna betaavtalet. Detta gör att du kan använda ytterligare AI Assistant-funktioner när de lanseras i en betapacitet.

+++Välj för att visa användaravtalsgränssnittet

![Användaravtalets första sida.](./images/user-agreement-1.png)

![Användaravtalets sista sida.](./images/user-agreement-2.png)

+++

## Förstå AI-assistenten {#understanding-ai-assistant}

AI Assistant besvarar dina inskickade frågor genom att fråga en databas och sedan omvandla data från databasen till ett läsbart svar.

Denna interna representation av underliggande data kallas också **[!DNL Knowledge Graph]** - en omfattande webbplats med koncept, data och metadata för ett givet svar.

The [!DNL Knowledge Graph] består av deldiagram som refereras när frågor skickas:

* Kundens operativa insikter.
* Kundens operativa insikter i olika metabutiker.
* Experience League dokumentation.

Det finns två frågeklasser att tänka på innan du frågar AI Assistant:

### Produktkunskap {#product-knowledge}

Produktkännedom avser begrepp och ämnen som anges i Experience League dokumentation. Produktkunskapsfrågor kan specificeras ytterligare i följande undergrupper:

| Produktkunskap | Exempel |
| --- | --- |
| Undervisning | <ul><li>Vad är skillnaden mellan en identitet och en primär eller extern nyckel?</li><li>Hur beräknas profilrikedomen?</li></ul> |
| Öppna identifiering | <ul><li>Hur exporterar jag den här datauppsättningen?</li><li>Finns det scheman för vårdkunder?</li></ul> |
| Felsökning | <ul><li>Varför kan jag inte aktivera ett schema som ägs av Adobe för en profil?</li><li>Varför kan jag inte ta bort ett segment?</li></ul> |

{style="table-layout:auto"}

### Driftsinsikter {#operational-insights}

>[!IMPORTANT]
>
>Svar på frågor om driftsinsikter finns i betaversionen. Alla som har åtkomst till **Visa användningsinformation** behörighet får tillgång till svar på driftsinsikter.

Användningsinsikter hänvisar till svar på AI Assistant genererar om dina metadata-objekt (attribut, målgrupper, dataflöden, datauppsättningar, destinationer, resor, scheman och källor), inklusive antal, sökningar och linjepåverkan. Den tittar inte på några data i sandlådan.

* Hur många datauppsättningar har jag?
* Hur många schemaattribut har aldrig använts?
* Vilka målgrupper har aktiverats?

Du kan ställa frågor till AI Assistant om dina operativa insikter i följande domäner:

| Domän | Metadata som stöds |
| --- | --- |
| Attribut | <ul><li>Attributnamn söker upp</li><li>Attribut - schemarelation</li><li>Attribut - datauppsättningsrelation</li><li>Attribut - målgruppsrelation</li><li>Attribut - målrelation</li><li>Oanvända attribut</li></ul> |
| Målgrupper | <ul><li>Antal målgrupper</li><li>Målgruppstyp (direktuppspelning eller batch)</li><li>Skapande-/ändringsdatum</li><li>Aktiveringsstatus</li><li>Profilantal</li><li>Duplicera målgrupper</li><li>Målgruppsdefinitionssökningar</li><li>Målgrupp - attributrelation</li><li>Målgrupp - datauppsättningsrelation</li><li>Målgrupp - målrelation</li><li>InSegment-regler</li><li>Namnsökningar</li><li>Namn- och ID-sökningar |
| Dataflöden | <ul><li>Antal dataflöden</li><li>Dataflödesstatus</li><li>Dataflöde - Datauppsättningsrelation</li><li>Dataflöd - källrelation</li></ul> |
| Datauppsättningar | <ul><li>Antal data</li><li>Aktivera profilstatus</li><li>Skapad/ändrad den</li><li>Datauppsättning - schemarelation</li><li>Datauppsättning - målgruppsrelation</li><li>Datauppsättning - attributrelation</li><li>Datauppsättning - dataflödesrelation</li><li>Namnsökningar </li><li>Namn- och ID-sökningar</li></ul> |
| Mål  | <ul><li>Konfigurerade destinationsantal</li><li>Mål - målgruppsrelation</li><li>Destinationsattributrelation</li></ul> |
| Resor | <ul><li>Antal</li><li>Namnsökningar</li><li>Namn- och ID-sökningar</li><li>Resestatus</li><li>Utlöst status (målgrupp kontra händelse)</li><li>Skapande-/ändringsdatum</li><li>Återkommande frekvens</li></ul> |
| Scheman | <ul><li>Antal scheman</li><li>Skapad/ändrad den</li><li>Typ av schemaklass</li><li>Schema - attributrelation</li><li>Schema - datauppsättningsrelation</li><li>Schema - målgruppsrelation</li><li>Aktivera profilstatus</li><li>Namnsökningar</li><li>Namn- och ID-sökningar</li></ul> |
| Källor | <ul><li>Konton</li><li>Kontostatus</li><li>Aktiva/inaktiva dataflöden för varje konto</li><li>Källkoppling - dataflödesrelation</li><li>Källkonto - dataflödesrelation</li></ul> |

{style="table-layout:auto"}

När det gäller frågor om driftsinsikter kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som stödjer dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Du måste logga in i en sandlåda för att få veta mer om specifika data som är relaterade till objekt.

### Funktionsomfång {#feature-scope}

För närvarande har AI Assistant följande omfattning:

* [Produktkunskap](./home.md#product-knowledge): AI Assistant kan besvara produktkunskapsfrågor för Experience Platform, Real-time Customer Data Platform och Adobe Journey Optimizer. Du kan också gå in i produktinformationsämnen för Customer Journey Analytics, men bara via användargränssnittet i Customer Journey Analytics.
* [Driftsinsikter](./home.md#operational-insights): Du kan ställa frågor till AI Assistant om driftsinsikter för följande dataobjekt: attribut, målgrupper, dataflöden, datauppsättningar, destinationer, resor, scheman och källor.

## Nästa steg

Nu när du har en allmän förståelse för AI Assistant kan du fortsätta använda AI Assistant under arbetsflödena. Mer information finns i följande dokumentation:

* [Användargränssnittshandbok för AI Assistant](./ui-guide.md)
* [Funktionsåtkomst](./access.md)
* [Frågeguide](./questions.md)
* [Integritet, säkerhet och styrning i AI Assistant](./privacy.md)
* [Vanliga frågor och svar](./faq.md)
