---
title: AI Assistant i Adobe Experience Platform - översikt
description: Lär dig mer om AI Assistant, dess nyanser och användningsexempel, och hur du kan använda det för att snabba upp arbetsflödet med Adobe Experience Platform och Real-time Customer Data Platform.
hide: true
hidefromtoc: true
source-git-commit: fe87a487079f5154f238b2d425cdd249a4724762
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 0%

---

# AI Assistant i Adobe Experience Platform

Läs det här dokumentet om du vill veta mer om AI Assistant i Adobe Experience Platform.

AI Assistant i Adobe Experience Platform är en samtalsupplevelse som du kan använda för att snabba upp arbetsflödena i Adobe-program. Du kan använda AI Assistant för att få en bättre förståelse för produktkunskaper, felsöka problem eller söka i information och hitta operativa insikter. AI Assistant har stöd för Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

>[!IMPORTANT]
>
>* Du måste godkänna [ett användaravtal](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) innan du kan använda AI-assistenten. Användaravtalet innehåller även det allmänna betaavtalet. Detta gör att du kan använda ytterligare AI Assistant-funktioner när de lanseras i en betapacitet.

![AI Assistant-gränssnittet med förstagångsupplevelsen aktiveras.](./images/blank.png)

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

* Attribut
* Målgrupper
* Dataflöden
* Datauppsättningar
* Destinationer _(Frågor om konton och vissa frågor om dataflöde kan inte besvaras just nu.)_
* Resor
* Scheman _(Frågor om fältgrupper kan inte besvaras just nu.)_
* Källor _(Frågor om konton kan inte besvaras just nu.)_

När det gäller frågor om driftsinsikter kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som stödjer dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Du måste logga in i en sandlåda för att få veta mer om specifika data som är relaterade till objekt.

## Funktionsåtkomst {#feature-access}

Åtkomst till AI Assistant styrs av följande parametrar:

* **Åtkomst till programmet:** Du kan öppna AI Assistant i Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer och [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Kontraktsåtkomst:** Ditt företag måste godkänna vissa [!DNL GenAI]-relaterade juridiska villkor innan din organisation kan använda AI Assistant. Kontakta din organisations administratör eller ditt Adobe-kontoteam om du inte kan komma åt AI Assistant.
* **Behörigheter:** Använd [Behörighetsgränssnitt](../access-control/abac/ui/permissions.md) för att bevilja eller återkalla åtkomst till AI Assistant i din organisation. För att kunna använda AI Assistant måste en viss användare tillhöra en roll som har etablerats med **Aktivera AI-assistenten** och **Visa användningsinformation** behörigheter.
   * Som administratör kan du lägga till **Aktivera AI-assistenten** till en viss roll och lägga till en användare till den rollen så att de kan komma åt AI-assistenten i organisationen.
   * Som administratör kan du lägga till **Visa användningsinformation** till en viss roll och lägga till en användare till den rollen, så att de kan använda AI Assistants funktionsinsikter. Driftsinsikter är för närvarande i betaversion.

![Behörighetsgränssnittssidan med behörigheterna Aktivera AI-assistenten och Visa driftsinsikter som ingår i en viss roll.](./images/permissions.png)

## Exempelfrågor {#example-questions}

I det här avsnittet beskrivs exempelfrågor som du kan referera till under dina arbetsflöden. Frågorna är uppdelade i tre avsnitt: operativa insikter, mål och föremål.

### Exempelfrågor grupperade efter operativa insikter {#operational-insights-questions}

+++Välj för att visa exempel på frågor om driftsinsikt och deras respektive användningsfall:

| Frågetyp | Använd skiftläge | Exempel |
| --- | --- | --- | 
| Datalinje | Spåra användningen av ett eller flera objekt över andra Experience Platform-objekt | <ul><li>Vilka datauppsättningar använder schemat &quot;ACME schema&quot;?</li><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilka datauppsättningar har använts i aktiverade målgrupper?</li><li>Lista scheman som har attribut som används i aktiverade målgrupper.</li><li>Visa vilka målgrupper som är aktiverade för&quot;ACME Destinations&quot; och som har fler än 1 000 profiler.</li><li>Visa vilka attribut som används i de aktiverade målgrupperna som har ändrats efter januari 2023.</li><li>Vilka datauppsättningar hämtas via källan&quot;ACME Amazon S3&quot;?</li><li>Vilka dataflöden är kopplade till&quot;ACME Loyalty Dataflow&quot;?</li><li>Lista scheman som är relaterade till aktiverade målgrupper och som skapades under det senaste året.</li></ul> |
| Distribution och aggregering | Sammanfattningsbaserade frågor om objektanvändning i Experience Platform | <ul><li>Hur många procent av de aktiva målgrupperna?</li><li>Hur många fält används vid segmentering?</li><li>Vilka målgrupper aktiveras för det största antalet destinationer?</li><li>Lista duplicerade målgrupper.</li><li>Visa vilka målgrupper som är aktiverade för&quot;ACME-mål&quot; och rangordna dem efter profilstorlek.</li><li>Vad är procentandelen av de målgrupper som inte har aktiverats men som har fler än 100 profiler. Visa mig deras namn.</li><li>Lista de tre källanslutningarna som samlar in data i mina datauppsättningar.</li><li>Ange de fem vanligaste attributen som används i aktiverade målgrupper baserat på deras förekomst.</li></ul> |
| Objektsökning | Hämta eller få åtkomst till ett Experience Platform-objekt eller dess egenskaper. | <ul><li>Vilka datamängder har inget associerat schema</li><li>Vill du lista attributen som används för&quot;ACME Audience&quot;?</li><li>Ge mig listan över scheman som är aktiverade för profiler, men som inte har ändrats sedan de skapades.</li><li>Vilka målgrupper har ändrats den senaste veckan?</li><li>Ange de målgrupper som har samma segmentdefinitioner tillsammans med deras skapandedatum.</li><li>Vilka datauppsättningar är profilaktiverade och innehåller även hur många målgrupper som har skapats från varje datauppsättning.</li><li>Vilka källkonton är associerade med datauppsättningen XYZ?</li><li>Visa segmentdefinitionen och ändringsdatumet för &quot;ACME Audience&quot;.</li></ul> |
| Objektjämförelse | Identifiera duplicerade målgrupper. | <ul><li>Baserat på segmentdefinitionen kan du lista de målgrupper som är dubbletter.</li><li>Vilka duplicerade målgrupper som aktiveras för &quot;ACME Destinations&quot;.</li></ul> |

{style="table-layout:auto"}

+++

### Exempelfrågor grupperade efter mål {#objectives-questions}

+++Välj för att visa en lista med mål som du kan uppnå med AI Assistant

| Syfte | Beskrivning | Exempel |
| --- | --- | --- |
| Utbildningsbegrepp och fortsatta arbetsflöden | <ul><li>Som nybörjare kan du använda AI Assistant för att lära dig Real-Time CDP- och Adobe Journey Optimizer-koncept och själv ta till vara produkter och funktioner som du inte känner till.</li><li>Som erfaren användare kan du använda AI Assistant för att lösa ett edge-fall som kan blockera ditt arbetsflöde. | <ul><li>Hur skapar jag en kontrollpanel i Journey Analytics?</li><li>Berätta några användningsfall för Real-Time CDP.</li></ul> |
| Felsökning | Använd AI Assistant för att lära dig hur du felsöker grundläggande fel som kan uppstå i arbetsflödet. | <ul><li>Vad är felet? {ERROR_MESSAGE} menar du?</li><li>Varför kan jag inte ta bort målgruppen Luma: Email Audience?</li></ul> |
| Sandlådehygien | Använd AI Assistant för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan underhålla sandlådan. | <ul><li>Kan ni visa mig målgrupper som är lika?</li><li>Finns det några scheman som inte har någon associerad datauppsättning?</li></ul> |
| Värdeanalys | Använd AI Assistant för att identifiera dina mest använda dataobjekt och utvärdera eventuella prestandaindikatorer eller hitta de värdefullaste dataobjekten. | <ul><li>Hur många profiler finns i segmentdefinitionen&quot;Luma: Email Audience&quot;?</li><li>När aktiverades målgrupper för målgrupper i Experience Cloud?</li></ul> |
| Sök | Använd AI Assistant för att hitta Experience Platform-objekt som stöds, som målgrupper, datauppsättningar, destinationer, scheman och källor. | <ul><li>Visa en lista över målgrupper som innehåller&quot;Luma&quot; i namnet som skapades under det senaste kvartalet.</li><li>Vilka attribut finns i XDM-schemat&quot;Luma: Custom Actions&quot;?</li></ul> |
| Effektanalys | Använd AI Assistant för att identifiera dataobjekt som har använts i vissa arbetsflöden, så att du kan bedöma effekten av eventuella ändringar. | <ul><li>Vilka målgrupper använder `homeAddress.city` i schemat &quot;Luma: PersonProfiles&quot;?</li><li>Vilka datamängder är `consents.marketing.push.val` vilket profilattribut som lagras i?</li></ul> |

{style="table-layout:auto"}

+++

### Exempelfrågor grupperade efter objekt {#objects-questions}

+++Välj för att visa en lista med exempelfrågor som AI Assistant kan hjälpa dig med:

| Objekt | Beskrivning |
| --- | --- |
| Målgrupper - operativa insikter | <ul><li>Vilka målgrupper använder andra målgrupper?</li><li>Vilken är fördelningen av antalet profiler mellan olika målgrupper?</li><li>Visa vilka målgrupper som senast ändrades innan {RELATIVE_DATE}.</li><li>Vilka målgrupper har 0 profiler?</li><li>Är {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} används i andra målgrupper?</li></ul> |
| Attribut - driftsinsikter | <ul><li>Vilka målgrupper som har XDM-attribut {ATTRIBUTE_PATH} i segmentdefinitionen?</li><li>Hur många XDM-schemaattribut används inte i någon målgrupp?</li><li>Vilka scheman har XDM-attribut {ATTRIBUTE_PATH} i dem?</li><li>Vilka XDM-attribut aktiveras?</li><li>Vilka XDM-attribut som används i målgrupper med fler än 10 profiler</li></ul> |
| Dataflöden - driftsinsikter | <ul><li>Vilka dataflöden bidrar till {DATASET_NAME} datauppsättning?</li><li>Vilka källdataflöden används inte eller har inga data längre?</li><li> |
| Datauppsättningar - driftsinsikter | <ul><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilken källkoppling är associerad med {DATASET_NAME} datauppsättning></li><li>Vilka datauppsättningar används för varje målgrupp?</li><li>Vilka scheman används inte i några datauppsättningar?</li><li>Hur många datauppsättningar har jag?</li></ul> |
| Destinationer - driftsinsikter | <ul><li>Vilka destinationer befinner sig i ett aktivt läge?</li><li>Vilka målkonton har 0 målgrupper aktiverade?</li><li> |
| Resor - operativa insikter | <ul><li>Hur många resor har jag?</li><li>Vilka resor som har skapats i {RELATIVE_DATE} (t.ex. förra veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?</li><li>Visa listan över resor som har ändrats i {RELATIVE_DATE} (t.ex. förra veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?</li><li>Lista de resor jag har.</li><li>Ange de målgrupper som används i direktresor.</li></ul> |
| Scheman - operativa insikter | <ul><li>Vilka schemafält har bidragit till de flesta målgrupper?</li><li>Hur många scheman är profiler aktiverade?</li><li>Visa alla scheman som har ändrats under den senaste veckan.</li><li>Vilka scheman används inte i några datauppsättningar?</li><li>Visa alla scheman som skapats den senaste veckan.</li></ul> |
| Källor - driftsinsikter | <ul><li>Vilka källor är i ett aktivt läge?</li><li>Vilken källanslutning som är associerad med datauppsättningen {DATASET_NAME}?</li><li>Vilken källanslutning har det högsta antalet associerade konton?</li><li>Visa dataflödena och tillhörande källanslutningar.</li></ul> |
| Lär dig mer - Produktkunskap (Real-Time CDP och Journey Optimizer) | <ul><li>Vad kan AI Assistant hjälpa till med?</li><li>Vad är lookalike-målgrupper?</li><li>Hur är användargrupper relaterade till roller?</li><li>När ska jag använda en datatyp jämfört med en fältgrupp?</li><li>Vad är skillnaden mellan en identitet och en primär eller extern nyckel?</li><li>Hur beräknas profilrikedomen?</li></ul> |
| Felsökning - produktkunskap (Real-Time CDP och Journey Optimizer) | <ul><li>Vad kan AI Assistant hjälpa till med?</li><li>Kan jag ta bort ett profilaktiverat schema efter att data har importerats?</li><li>Varför kan jag inte ta bort en publik?</li><li>Hur lång tid tar det för målgrupperna att utvärderas och för att resultaten ska vara tillgängliga för målinriktning?</li></ul> |

{style="table-layout:auto"}

+++

## Tar hand om dina frågor {#phrasing-your-questions}

Du måste ge AI Assistant tydliga och kontextuella uppgifter för att få ett så korrekt svar som möjligt. Se följande lista med tips om hur du ställer en tydlig fråga i sitt sammanhang:

* Ange din uppgift och/eller fråga kortfattat.
* Undvik tvetydigt språk och alltför komplex syntax för att underlätta förståelsen.
* Ange relevant sammanhang för dina uppgifter och/eller frågor eftersom kontexten kan hjälpa AI Assistant att generera mer relevanta svar.

Läs tabellerna nedan för mer information om de effektivaste strategierna när du ställer frågor till AI Assistant.

+++Välj om du vill se exempel på bästa praxis när du formulerar dina frågor

| Gör | Exempel |
| --- | --- |
| <ul><li>Var tydlig med objektet eller informationen som du vill hämta eller analysera.</li><li>Försök att ange dataobjektens namn inom citattecken. Om du bara känner till en del av objektnamnet kan du även ange det i frågan.</li><li>Använd [objekt som slutförs automatiskt](./ui-guide.md#use-auto-complete) för att hjälpa AI Assistant att bättre förstå sammanhanget i din fråga.</li></ul> | <ul><li>Vilka datauppsättningar använder schemat&quot;Luma - Loyalty&quot;?</li><li>Visa de aktiverade segmenten som har &quot;Luma&quot; i sina namn. Rangordna dem efter antal profiler.</li></ul> |
| <ul><li>Undvik tvetydighet och använd tydligt språk</li><li>Använd exakt terminologi för att få bättre tydlighet i frågan.</li><li>När du ställer frågor om Adobe Experience Platform kan du försöka använda terminologi som är specifik för Experience Platform för att förbättra relevansen i svaren.</li></ul> | <ul><li>Hur många profiler har jag i&quot;ACME Audience&quot;.</li><li>Visa de fem främsta XDM-attributen som används i aktiverade målgrupper.</li></ul> |
| <ul><li>Ange sammanhang eller ange ett villkor för att filtrera resultaten.</li><li>Använd ett filtervillkor i frågorna för att begränsa mängden data i svaret.</li></ul> | <ul><li>Visa målgrupper som inte har aktiverats och skapats för mer än sex månader sedan och som aldrig har ändrats.</li><li>Visa att målgrupper är aktiverade för&quot;ACME Destination&quot; och har fler än 10 000 profiler.</li></ul> |

{style="table-layout:auto"}

| Gör det inte | Exempel |
| --- | --- |
| Använd oklart eller tvetydigt språk. | <ul><li>Ge mig information om datauppsättningar.</li><li>Hur många användare har jag i&quot;ACME Audience&quot;?</li><li>Visa segment.</li><li>Listattribut.</li></ul> |
| Gör ofullständiga förfrågningar. | &quot;Luma - lojalitetsdatauppsättning&quot; |
| Anta kunskap utan kontext. | <ul><li>Målgrupper de senaste sex månaderna.</li><li>Bygg en fråga åt mig.</li></ul> |
| Formge alltför komplexa frågor. | Gör en omfattande analys av datalinjer för alla objekt och deras beroenden. |
| Utelämna villkor eller parametrar. | Visa datauppsättningar. |

{style="table-layout:auto"}

+++

## Nästa steg

Nu när du har en allmän förståelse för AI Assistant kan du fortsätta använda AI Assistant under arbetsflödena. Mer information finns i följande dokumentation:

* [Användargränssnittshandbok för AI Assistant](./ui-guide.md)
* [Integritet, säkerhet och styrning i AI Assistant](./privacy.md)
* [Vanliga frågor och svar](./faq.md)