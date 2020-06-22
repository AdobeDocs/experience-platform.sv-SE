---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform datastyrning
topic: overview
translation-type: tm+mt
source-git-commit: 42d4fe7eecf1f64fab1c9554cfdc4bfeb42ffdeb
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---


# Datastyrning - översikt

En av kärnfunktionerna i Adobe Experience Platform är att sammanföra data från olika affärssystem så att marknadsförarna bättre kan identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Det är därför viktigt att se till att dataåtgärderna i Platform är kompatibla med dataanvändningspolicyer.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och se till att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en nyckelroll på olika nivåer inom Experience Platform, bland annat för katalogisering, datalinje, märkning av dataanvändning, dataanvändningspolicyer och kontroll av användningen av data för marknadsföringsåtgärder.

## Datastyrningsroller

Som begrepp är datastyrning varken automatisk eller sker i ett vakuum. Det som började som en roll för en individ, som vanligen kallas **dataförvaltare**, har ökat avsevärt i takt med att ekosystemet för datastyrning har expanderat. Idag kräver datastyrning kontinuerlig hantering och övervakning för att bli framgångsrik och bygger på datahanteringar med verktyg som data kan märkas med, användarprofiler kan skapas och regelefterlevnaden kan upprätthållas.

Även om datastyrning bör vara ansvaret för varje enskild person i organisationen finns det några av de viktigaste rollerna inom datastyrningscykeln:

![Roller för datastyrning](./images/overview/roles.png)

### Dataförvaltare

Datastyrning är kärnan i datastyrningen. Denna roll ansvarar för att tolka förordningar, avtalsbegränsningar och policyer och tillämpa dem direkt på data. Som informerats av deras förståelse för dessa regler, begränsningar och policyer omfattar rollen som datastyrning följande:

* Granska data, datauppsättningar och dataexempel för att använda och hantera etiketter för metadataanvändning.
* Skapa dataprofiler och tillämpa dem på datauppsättningar och fält.
* kommunicera dataprofiler till organisationen,

### Marknadsförare

Marknadsförarna är slutpunkten för datastyrning. De begär data från den infrastruktur för datastyrning som har skapats av dataansvariga, forskare och ingenjörer. Marknadsförarna omfattar ett antal olika specialiteter inom ramen för marknadsföringsparaplyet, bland annat följande:

* Marknadsföringsanalytiker begär data för att kunna förstå kunderna, både individer och grupper (kallas även segment).
* Marknadsföringsspecialister och Experience Designers använder data för att utforma nya kundupplevelser.


## DULE-ramverk

Varumärkning och verkställighet av dataanvändning (DULE) är grundramverket för datastyrning i Experience Platform. DULE förenklar och effektiviserar arbetet med att kategorisera data och skapa principer för dataanvändning. När dataetiketter har tillämpats och dataanvändningspolicyer har införts kan marknadsföringsåtgärder utvärderas för att säkerställa korrekt dataanvändning.

DULE-ramverket består av tre nyckelelement: Etiketter, profiler och verkställighet.

1. **Etiketter:** Klassificera data som återspeglar integritetsrelaterade överväganden och avtalsvillkor så att de överensstämmer med regler och organisationsprofiler.
1. **Profiler:** Beskriv vilka typer av marknadsföringsåtgärder som är tillåtna eller inte får vidtas på specifika data.
1. **Tvingande:** Använder policyramverket för att ge råd och tillämpa policyer för olika dataåtkomstmönster.

## Dataanvändningsetiketter

Med datastyrning kan datasegmentering tillämpa användningsetiketter på datauppsättnings- och fältnivå för att kategorisera data efter vilken typ av profiler som används.

DULE-ramverket innehåller fördefinierade etiketter för dataanvändning som kan användas för att kategorisera data på tre sätt:

![Etikettkategorier för dataanvändning](./images/overview/label-categories.png)

* **Kontraktets&quot;C&quot;-dataetiketter:** Märk och kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till policyer för styrning av kunddata.
* **Identitet&quot;I&quot;-dataetiketter:** Märk och kategorisera data som kan identifiera eller kontakta en viss person.
* **Känsliga&quot;S&quot;-dataetiketter:** Märk och kategorisera data relaterade till känsliga data, t.ex. geografiska data.

>[!NOTE] I guiden om [dataanvändningsetiketter](labels/reference.md) som stöds finns en fullständig lista över tillgängliga etiketter samt definitioner för varje etiketttyp.

Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa praxis uppmuntrar till märkning av data så snart de har importerats till Experience Platform, eller så snart data blir tillgängliga i Platform.

Mer information finns i översikten över [dataanvändningsetiketter](./labels/overview.md) .

## Dataanvändningspolicyer

För att dataanvändningsetiketter effektivt ska stödja regelefterlevnad måste dataanvändningsprinciper implementeras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom Experience Platform.

Ett exempel på en marknadsföringsåtgärd kan vara en önskan att exportera en datauppsättning till en tredjepartstjänst. Om det finns en policy som säger att vissa typer av data, t.ex. PII (Personally Identiitable Information), inte kan exporteras och att ID-etiketten (Identity data) har tillämpats på datauppsättningen, får du ett svar från principtjänsten som säger att en dataanvändningspolicy har överträtts.

När dataanvändningsetiketterna har tillämpats kan datahanterarna skapa principer med DULE Policy Service API eller Experience Platform användargränssnitt.

>[!IMPORTANT] Alla dataanvändningspolicyer (inklusive kärnpolicyer från Adobe) är inaktiverade som standard. För att en enskild princip ska kunna användas för verkställighet måste du manuellt aktivera den principen.

Mer information om dataanvändningspolicyer och marknadsföringsåtgärder finns i [policyöversikten](./policies/overview.md).

## Framtida releaser

Datastyrning har för närvarande stöd för DULE-märkning på två nivåer (datamängd och fält). Datastyrning stöder också skapande och hantering av dataanvändningsprinciper och marknadsföringsåtgärder via DULE Policy Service API.

Efterföljande versioner innehåller följande funktioner:

* Etiketter för anpassad dataanvändning: Skapa nya etiketter och definitioner baserat på organisationens behov.
* Politiska åtgärder: Använd policyramverket för att ge råd om och tillämpa principer för olika dataåtkomstmönster.
* Granskning: Övervaka dataåtkomstaktiviteter och identifiera och rapportera om efterlevnadsproblem.

## Nästa steg

Detta dokument gav en introduktion på hög nivå till datastyrning och DULE-ramverket. Du kan nu fortsätta med användarhandboken för [dataanvändningsetiketter](labels/user-guide.md) och börja lägga till användningsetiketter till dina upplevelsedata.

## Bilaga

Följande avsnitt innehåller ytterligare information om datastyrning.

### Terminologi inom datastyrning

I följande tabell visas nyckeltermer för datastyrning och DULE-ramverket.

| Term | Definition |
|---|---|
| **Kontraktsetiketter** | Kontraktets&quot;C&quot;-etiketter används för att kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till organisationens policyer för datastyrning. |
| **Data för flera webbplatser** | Data på olika platser är en kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera externa källor. |
| **Datastyrning** | Datastyrning omfattar strategier och tekniker som används för att säkerställa att data överensstämmer med regler och företagspolicyer när det gäller dataanvändning. |
| **Dataförvaltare** | Dataförvaltningarna är den person som ansvarar för förvaltning, tillsyn och verkställighet av en organisations datatillgångar. En dataförvaltare säkerställer också att policyer för datastyrning skyddas och upprätthålls så att de följer myndighetsregler och organisationsregler. |
| **Dataanvändningsetiketter** | Etiketter för dataanvändning ger användarna möjlighet att kategorisera data som speglar integritetsrelaterade överväganden och avtalsvillkor så att de uppfyller regler och företagspolicyer. |
| **Datauppsättningsetiketter** | Etiketter kan läggas till i en datauppsättning. Alla fält i en datauppsättning ärver datauppsättningens etiketter. |
| **DULE** | DULE är en förkortning av&quot;Dataanvändningsetiketter och -verkställighet&quot;. DULE är en viktig del av datastyrningen och är en samling funktioner som gör det möjligt att sätta etiketter för dataanvändning och tillämpa policyer för dataåtkomst för styrningsbehov inom en organisation. |
| **Fältetiketter** | Fältetiketter är datastyrningsetiketter som antingen ärvs från en datamängd eller tillämpas direkt på ett fält.  Datastyrningsetiketter som används i ett fält ärvs inte upp till en datamängd. |
| **Geofence** | En geofence är en virtuell geografisk gräns, som definieras av GPS- eller RFID-teknik, som gör att programvara kan utlösa ett svar när en mobil enhet kommer in i eller lämnar ett visst område. |
| **Identitetsetiketter** | Identitet&quot;I&quot;-etiketter används för att kategorisera data som kan identifiera eller kontakta en viss person. |
| **Intressebaserad målinriktning** | Intressebaserad målinriktning, som också kallas personalisering, uppstår om följande tre villkor uppfylls: data som samlas in på webbplatsen används för att dra slutsatser om en användares intresse, i ett annat sammanhang, t.ex. på en annan webbplats eller i en app (utanför webbplatsen) och används för att välja vilket innehåll eller vilka annonser som ska hanteras baserat på dessa slutsatser. |
| **Marknadsföringsåtgärd** | En marknadsföringsåtgärd, inom ramen för datastyrningsramverket, är en åtgärd som en datakonsument i Experience Platform vidtar, där det finns ett behov av att kontrollera överträdelser av dataanvändningspolicyer |
| **Policy** | I ramverket för datastyrning är en regel som beskriver vilken typ av marknadsföringsåtgärder som tillåts eller inte tillåts att vidtas för specifika data. |
| **Känsliga etiketter** | Känsliga S-etiketter används för att kategorisera data som du, och din organisation, anser vara känsliga. |

## Ytterligare resurser

Följande video är avsedd att ge stöd för din förståelse av datastyrning och beskriver de viktigaste aspekterna i ramverket för märkning och verkställighet av dataanvändning (DULE).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
