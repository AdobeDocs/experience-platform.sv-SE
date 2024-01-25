---
keywords: Experience Platform;hem;populära ämnen;DULE;Schedule
solution: Experience Platform
title: Datastyrning - översikt
description: Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en nyckelroll på olika nivåer inom Experience Platform, bland annat för katalogisering, datalinje, märkning av dataanvändning, dataanvändningspolicyer och kontroll av användningen av data för marknadsföringsåtgärder.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 1a050cfb41a28053606f07931c7c97d15989ac3e
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 0%

---

# Datastyrning - översikt {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Datastyrningsskyldighet"
>abstract="Kom ihåg att det är ditt enda ansvar att följa din organisations policyer för datastyrning och uppfylla dina lagstadgade krav. Experience Platform tillhandahåller datastyrningsverktyg som du kan använda för att hantera dina dataanvändningsskyldigheter. Använd lämpliga etiketter för dataanvändning innan du frågar eller bearbetar data. Läs dokumentationen om du vill veta mer om verktyg för datastyrning och metodtips."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html" text="Datastyrning - översikt"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html" text="Översikt över etiketter för datastyrning"

En av de viktigaste funktionerna i Adobe Experience Platform är att samla data från olika affärssystem så att marknadsförarna bättre kan identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Det är därför viktigt att se till att era dataåtgärder inom [!DNL Platform] är kompatibla med dataanvändningsprinciper.

Hantera kunddata och säkerställ att regler, begränsningar och regler som gäller för dataanvändning följs med Adobe Experience Platform Data Governance. Datastyrning spelar en viktig roll inom Experience Platform på olika nivåer, inklusive katalogisering, datalinje, etikettering av dataanvändning, dataanvändningspolicyer och kontroll av användningen av data för marknadsföringsåtgärder.

>[!NOTE]
>
>I Experience Platform gäller datastyrning endast hur data används eller aktiveras, oavsett vilken användare som utför åtgärden. Mer information om hur du styr åtkomsten till specifika datafält för vissa plattformsanvändare i organisationen finns i dokumentationen om [attributbaserad åtkomstkontroll](../access-control/abac/overview.md) i stället.

## Datastyrningsroller {#data-governance-roles}

Som begrepp är datastyrning varken automatisk eller sker i ett vakuum. Det som började som en roll för en individ, vanligen erkänd som en dataförvaltare, har ökat avsevärt i takt med att ekosystemet för datastyrning har expanderat. Idag kräver datastyrning kontinuerlig hantering och övervakning för att lyckas. Effektiv datastyrning bygger på datastyrningar med verktyg med vilka data kan märkas på rätt sätt, användarprofiler kan skapas och regelefterlevnaden kan upprätthållas.

Även om datastyrning bör vara ansvaret för varje enskild person i organisationen finns det några av de viktigaste rollerna inom datastyrningscykeln:

![Grafik för att förmedla de fyra rollerna för datastyrning, med citat om respektive rolls arbetsuppgifter.](./images/overview/roles.png)

### Stegvis data {#data-steward}

Datastyrning är kärnan i datastyrningen. Denna roll ansvarar för att tolka förordningar, avtalsbegränsningar och policyer och tillämpa dem direkt på data. Som informerats av deras förståelse för dessa regler, begränsningar och policyer omfattar rollen som datastyrning följande:

* Granska data, datauppsättningar och dataexempel för att använda och hantera etiketter för metadataanvändning.
* Skapa dataprofiler och tillämpa dem på datauppsättningar och fält.
* kommunicera dataprofiler till organisationen,

### Marknadsförare {#marketer}

Marknadsförarna är slutpunkten för datastyrning. De begär data från den infrastruktur för datastyrning som har skapats av dataansvariga, forskare och ingenjörer. Marknadsförarna omfattar ett antal olika specialiteter inom ramen för marknadsföringsparaplyet, bland annat följande:

* Marknadsföringsanalytiker begär data för att kunna förstå kunderna, både individer och grupper (kallas även segment).
* Marknadsföringsspecialister och Experience Designers använder data för att utforma nya kundupplevelser.

## Ramverk för datastyrning {#data-governance-framework}

Datastyrningsramverket förenklar och effektiviserar processen att kategorisera data och skapa policyer för dataanvändning. När dataetiketter har tillämpats och dataanvändningspolicyer har införts kan marknadsföringsåtgärder utvärderas för att säkerställa korrekt dataanvändning.

Det finns tre viktiga element i ramverket för datastyrning: etiketter, policyer och verkställighet.

1. **Etiketter:** Klassificera data som återspeglar integritetsrelaterade överväganden och avtalsvillkor så att de överensstämmer med regler och organisationsprofiler.
1. **Profiler:** Beskriv vilka typer av marknadsföringsåtgärder som är tillåtna eller inte får vidtas på specifika data.
1. **Tvingande:** Använder policyramverket för att ge råd och tillämpa policyer för olika dataåtkomstmönster.

## Dataanvändningsetiketter {#data-usage-labels}

Med Datastyrning kan datasegmentering tillämpa användningsetiketter på schemafältnivå för att kategorisera data efter den typ av principer som gäller.

Ramverket för datastyrning innehåller fördefinierade etiketter för dataanvändning som kan användas för att kategorisera data på tre sätt:

![De tre kategorierna för dataanvändningsetiketter.](./images/overview/label-categories.png)

* **Kontraktets&quot;C&quot;-dataetiketter:** Märk och kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till policyer för styrning av kunddata.
* **Identitet&quot;I&quot;-dataetiketter:** Märk och kategorisera data som kan identifiera eller kontakta en viss person.
* **Känsliga&quot;S&quot;-dataetiketter:** Märk och kategorisera data relaterade till känsliga data, t.ex. geografiska data.

>[!NOTE]
>
>Se guiden på [etiketter för dataanvändning](labels/reference.md) för en fullständig lista över tillgängliga etiketter och definitioner för varje etiketttyp.

Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa praxis uppmuntrar till etikettdata när de hämtas till Experience Platform, eller så snart data blir tillgängliga i [!DNL Platform].

Se översikten på [etiketter för dataanvändning](./labels/overview.md) om du vill ha mer information om hur dataanvändningsetiketter används för att säkerställa regelefterlevnad för datastyrning.

## Dataanvändningspolicyer {#data-usage-policies}

För att dataanvändningsetiketter effektivt ska stödja regelefterlevnad måste dataanvändningsprinciper implementeras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom Experience Platform.

Ett exempel på en marknadsföringsåtgärd kan vara en önskan att exportera en datauppsättning till en tredjepartstjänst. Om det finns en princip som anger att personligt identifierbar information (PII) inte kan exporteras och en I-etikett (identitetsdata) har tillämpats på fältnivån från dess schema. Policy Service förhindrar sedan alla åtgärder som skulle kunna exportera den här datauppsättningen till ett mål från en annan leverantör. Om någon av dessa åtgärder skulle utföras skickar Policy Service ett meddelande om att en dataanvändningsprincip har överträtts.


Det finns två typer av principer:

* **[!UICONTROL Data governance policy]**: Begränsa dataaktiveringen baserat på den marknadsföringsåtgärd som utförs och de dataanvändningsetiketter som medföljer data i fråga.
* **[!UICONTROL Consent policy]**: Filtrera de profiler som kan aktiveras för [mål](../destinations/home.md) baserat på kundernas samtycke eller önskemål.

När dataanvändningsetiketterna har tillämpats kan datafördelare skapa principer med hjälp av principtjänstens API eller användargränssnittet i Experience Platform. Mer information om dataanvändningspolicyer och marknadsföringsåtgärder finns i [profiler, översikt](./policies/overview.md).

>[!IMPORTANT]
>
>Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen.

## Nästa steg

Detta dokument gav en introduktion på hög nivå till datastyrning och ramverket för datastyrning. Du kan nu fortsätta till [användarhandbok för dataanvändningsrubriker](labels/user-guide.md) och börja lägga till användningsetiketter i era upplevelsedata.

## Bilaga

Följande avsnitt innehåller ytterligare information om datastyrning.

### Terminologi inom datastyrning {#data-governance-terminology}

I följande tabell beskrivs nyckeltermer för datastyrning och ramverket för datastyrning.

| Term | Definition |
|---|---|
| **Kontraktsetiketter** | Kontraktets&quot;C&quot;-etiketter används för att kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till organisationens policyer för datastyrning. |
| **Data för flera webbplatser** | Data på olika platser är en kombination av data från flera platser. Data för olika webbplatser omfattar både data på plats och utanför platsen, eller en kombination av data från flera externa källor. |
| **Datastyrning** | Datastyrning omfattar strategier och tekniker som används för att säkerställa att data överensstämmer med regler och företagspolicyer när det gäller dataanvändning. |
| **Stegvis data** | Dataförvaltningarna är den person som ansvarar för förvaltning, tillsyn och verkställighet av en organisations datatillgångar. Ett dataflöde säkerställer också att policyer för datastyrning skyddas och upprätthålls så att de följer myndighetsregler och organisationsregler. |
| **Dataanvändningsetiketter** | Etiketter för dataanvändning ger användarna möjlighet att kategorisera data som speglar integritetsrelaterade överväganden och avtalsvillkor så att de uppfyller regler och företagspolicyer. |
| **Datauppsättningsetiketter** | Etiketter kan läggas till i ett schema. Alla fält i en datauppsättning ärver schemats etiketter. |
| **Fältetiketter** | Fältetiketter är datastyrningsetiketter som antingen ärvs från ett schema eller används direkt i ett fält. Datastyrningsetiketter som används i ett fält ärvs inte upp till schemanivå. |
| **Geofence** | En geofence är en virtuell geografisk gräns, som definieras av GPS- eller RFID-teknik, som gör att programvara kan utlösa ett svar när en mobil enhet kommer in i eller lämnar ett visst område. |
| **Identitetsetiketter** | Identitet&quot;I&quot;-etiketter används för att kategorisera data som kan identifiera eller kontakta en viss person. |
| **Intressebaserad målinriktning** | Intressebaserad målinriktning, som också kallas personalisering, uppstår om följande tre villkor uppfylls:<br>Data som samlas in på plats är<br><ul><li>Används för att dra slutsatser om en användares intresse,</li><li>Används i ett annat sammanhang, t.ex. på en annan webbplats eller i en annan app (utanför webbplatsen)</li><li>Används för att välja vilket innehåll eller vilka annonser som ska hanteras baserat på dessa slutsatser.</li></ul> |
| **Marknadsföringsåtgärd** | En marknadsföringsåtgärd, inom ramen för datastyrningsramverket, är en åtgärd som en datakonsument i Experience Platform vidtar, där det finns ett behov av att kontrollera överträdelser av dataanvändningspolicyer |
| **Policy** | I ramverket för datastyrning är en regel som beskriver vilka typer av marknadsföringsåtgärder som tillåts eller inte får vidtas för specifika data. |
| **Schemaetiketter** | Hantera etiketterna för datastyrning, samtycke och åtkomstkontroll på schemanivå. Detta sprider etiketterna till alla datauppsättningar som använder det schemat. |
| **Känsliga etiketter** | Känsliga S-etiketter används för att kategorisera data som du, och din organisation, anser vara känsliga. |

## Ytterligare resurser

Följande video är avsedd att ge stöd för din förståelse av ramverket för datastyrning.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

I följande videofilm visas hur du använder dataanvändningsetiketter på dina scheman eller på hela datauppsättningen i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
