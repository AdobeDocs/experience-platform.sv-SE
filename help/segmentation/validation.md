---
title: Audience Validation
description: Läs om hur Experience Platform validerar era målgrupper för att säkerställa att de presterar bättre längre fram i kedjan.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 0%

---


# Målgruppsvalidering

När ni skriver en målgruppsdefinition i Adobe Experience Platform ger målgruppsvalideringen inbyggda valideringar och skyddsprofiler som säkerställer att målgrupperna inte bara är korrekta, utan även stabila och skalbara.

Genom att följa vedertagna standarder för målgruppsdefinition kan ni se till att era målgrupper kan utvärdera snabbare, säkerställa att logiken förblir effektiv även när målgruppens storlek ökar och minska risken för misslyckade utvärderingar under högtrafikperioder. Optimerade målgrupper förbättrar också aktiveringshastigheten för destinationer, minskar personaliseringsfördröjningen i realtid och bibehåller den övergripande sandlådestabiliteten.

Experience Platform kör dessa valideringar i realtid när ni bygger er målgrupp i Segment Builder. När du lägger till händelser eller attribut som överskrider valideringströsklarna får du omedelbar feedback i gränssnittet i Segment Builder.

## Valideringstyper {#validation-types}

När målgruppsvalideringen körs på målgrupperna finns det två olika typer av konstruktioner som kan överträdas: Kritisk validering och prestandaoptimering.

Om en viktig valideringskonstruktion överträds förhindrar systemet att du sparar din målgrupp för att skydda sandlådans stabilitet. Om en prestandaoptimeringskonstruktion överträds kan du spara din målgrupp, men det *rekommenderas varmt* att du uppdaterar din målgruppsdefinition för att undvika prestandaproblem.

## Valideringskontroller {#validation-checks}

Följande valideringar stöds för närvarande:

| Valideringskontroll | Typ | Tröskelvärde |
| ---------------- | ---- | --------- |
| Logisk komplexitet | Kritisk validering | Målgruppsdefinitionen innehåller för många frågor, vilket resulterar i onödig logisk komplexitet. |
| Sekventiella händelser | Kritisk validering | Det finns mer än 6 sekventiella händelser i en målgruppsdefinition. |
| Sammanlagt antal | Prestandaoptimering | Det finns mer än tre aggregeringsfunktioner i en publikdefinition. |
| Kapslade data | Prestandaoptimering | Det finns mer än två nivåer av kapslade data (datatyperna array eller map) i en målgruppsdefinition. |
| Målgruppsstorlek | Prestandaoptimering | Storleken på målgruppens kvalificering är större än 30 % av det totala antalet profiler i sandlådan. |

### [!BADGE Kritisk validering]{type=Negative} Logisk komplexitet {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Fråga om effektivitet"
>abstract="Din målgrupp innehåller för många frågor, vilket leder till onödig logisk komplexitet. Förenkla målgruppsdefinitionen innan du fortsätter."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Logikkomplexitet"
>abstract="Din målgrupp innehåller för många frågor, vilket leder till onödig logisk komplexitet. Förenkla målgruppsdefinitionen innan du fortsätter."

Valideringen av logisk komplexitet analyserar strukturen för dina logiska satser (AND, OR, NOT) inom målgruppsdefinitionen. Det letar efter målgruppsdefinitioner som tvingar systemet att utföra ett stort antal jämförelser per profil.

Om er målgruppsdefinition har ett stort antal jämförelser per profil leder den här komplexiteten till en långsammare utvärdering per profil. Detta medför att den totala tiden för målgruppsutvärdering ökar.

Undvik att aktivera den här valideringen genom att göra målgruppsdefinitionen enkel. Om ni inte förstår er egen målgruppsdefinition är den för komplicerad och Experience Platform kan ta längre tid att utvärdera målgruppen.

**Exempel**

Säg att ni vill hitta kunder som bor i vissa delstater. Du _kan_ skriva det här ineffektivt genom att kontrollera om profilen har värdet för ett läge som matchar ett av de 45 listade värdena enligt följande:

+++ Ineffektiv målgruppsdefinition

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Om du använder en&quot;inte&quot;-kontroll behöver du bara kontrollera om profilen inte har något av de 5 listade värdena, vilket ger en mycket effektivare fråga.

+++ Effektiv målgruppsdefinition

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Eller säg att du vill hitta kunder som är kanadensare i testversionen. Ett mindre effektivt sätt vore att leta efter kanadensare på din testversion genom att manuellt utesluta alla andra planer, en efter en, och kontrollera att profilen inte finns i någon av dem.

+++ Ineffektiv målgruppsdefinition

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

I stället bör du vara direkt och ange den specifika plan som du vill inkludera som mål.

+++ Effektiv målgruppsdefinition

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Kritisk validering]{type=Negative} Sekventiell händelsekomplexitet {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Gräns för händelsesekvens"
>abstract="Din målgrupp innehåller för många sekventiella händelser. Du kan bara ha högst sex sekventiella händelser inom målgruppsdefinitionen. Ta bort några sekventiella händelser från målgruppsdefinitionen innan du fortsätter."

Den sekventiella valideringen av händelsekomplexitet begränsar antalet sekventiella händelser i en sekvens till 6 händelser.

Sekventiell segmentering är en av de mest beräkningsmässigt komplicerade åtgärderna i Experience Platform, eftersom systemet måste skanna in en kunds hela historik med Experience Events, sortera dem efter tidsstämpel och verifiera om den angivna ordningen matchar din fråga. När kedjan växer ökar därför antalet permutationer som systemet behöver för att kunna beräkna drastiskt.

För att undvika att utlösa den här valideringen kan du fokusera på grunderna i den sekventiella kedjan genom att definiera början, mitten och slutet av resan. Omedelbara steg är ofta underförstådda inom den slutliga konverteringen.

**Exempel**

Säg att du vill rikta in dig på användare som har tittat på en produkt, lagt till den i kundvagnen och köpt den. Ett mindre effektivt tillvägagångssätt skulle kontrollera alla enskilda tillstånd i användarens sökväg. Följande fråga går till exempel igenom den här händelsesekvensen: Loggar in på webbplatsen -> Söker efter produkt -> Visar en produktsida -> Lägger till i kundvagn -> Navigerar till kassan -> Köphändelse

+++ Ineffektiv målgruppsdefinition

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Om du reducerar sekvensen till början, mitten och slutet behöver du bara ha en sekvens med händelser som är 3 händelser långa, vilket ger en mer effektiv fråga. Följande fråga går till exempel igenom den här händelsesekvensen: Visar en produktsida -> Lägger till i kundvagnen -> Inköpshändelse

+++ Effektiv målgruppsdefinition

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Prestandaoptimering]{type=Caution} Sammanlagt antal {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Filtervarning för antal"
>abstract="Din publik har för många aggregeringshändelser. Ni bör använda maximalt 3 aggregeringshändelser inom er målgrupp. För att undvika prestandaproblem bör du ta bort vissa aggregeringshändelser från målgruppsdefinitionen."

Kontrollen av aggregerat antal begränsar antalet aggregeringshändelser som används inom målgruppen till tre villkor.

En standardhändelse behöver bara hitta en enda matchande händelse för att kvalificera en användare. En aggregeringshändelse måste dock läsa och analysera en användares **hela historik** innan den kan fatta ett beslut, vilket leder till långsammare bearbetningstider med fler aggregeringshändelser som används.

För att undvika att utlösa den här valideringen bör du bara använda specifika räkningar när det är absolut nödvändigt för målgruppsdefinitionen. Om du bara behöver veta om en användare har engagerat sig en gång, kan du till exempel använda standardlogiken&quot;Exists&quot; i stället för att använda händelsen&quot;Count > 0&quot;.

### [!BADGE Prestandaoptimering]{type=Caution} Komplexitet för kapslade data {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Varning för kapslade data"
>abstract="Din målgrupp har för många kapslade datalager. Ni bör använda maximalt två lager data inom er målgrupp. För att undvika prestandaproblem bör du förenkla målgruppsdefinitionen."

Den kapslade valideringen av datakomplexitet begränsar antalet kapslade data inom en målgruppsdefinition till två lager.

Experience Platform stöder användning av array- och mappobjekt för lagring av komplexa datatyper, men uppackning av kapslade strukturer för att hitta ett värde kräver mer komplex genomgångslogik. Djupa data kapslas i en array, ju längre det tar att hämta dem för validering.

Om du ofta utför segmentering på ett djupt inkapslat attribut kan du behöva kontakta ditt datateknikteam för att kopiera attributet till en högre nivå i profilschemat för att få enklare åtkomst.

### [!BADGE Prestandaoptimering]{type=Caution} Målgrupp {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Varning om målgruppsstorlek"
>abstract="Din målgrupp är skriven för brett. Du bör undvika att skriva en målgruppsdefinition som kvalificerar mer än 30 % av det totala antalet profiler i sandlådan. För att undvika prestandaproblem bör du göra målgruppsdefinitionen tätare."

Valideringen av målgruppsstorlek kontrollerar om målgruppsdefinitionen är så bred att mer än 30 % av det totala antalet profiler i din sandlåda kvalificerar sig för målgruppen.

Även om Experience Platform kan hantera stora målgrupper kan en för otydlig målgruppsdefinition (till exempel Alla aktiva kunder) öka utvärderingstiden och aktiveringstiden.

Om ni behöver skapa en målgrupp som kvalificerar mer än 30 % av er profilbutik måste ni se till att målgruppens första utvärdering görs med hjälp av flexibel målgruppsutvärdering. Genom att utvärdera målgruppen med en on-demand-utvärdering kan man minska den övergripande effekten av en stor publik på det dagliga segmenteringsjobbet.

## Nästa steg

När du har läst den här guiden får du en bättre förståelse för hur Experience Platform kör automatiska valideringar för att förbättra utvärderingen, stabiliteten och skalbarheten. Mer information om hur du skapar målgrupper med användargränssnittet finns i [dokumentationen för segmentbyggaren](./ui/segment-builder.md).

## Bilaga

I följande bilaga visas vanliga frågor om målgruppsvalidering i Experience Platform.

### Vanliga frågor och svar {#faq}

**Vad händer om jag ignorerar varningarna och sparar publiken?**

+++ Svar

För prestandaoptimeringsvarningar sparas målgruppen och systemet försöker utvärdera den. Det kan dock ta betydligt längre tid att bearbeta. I extrema situationer, om datavolymen är tillräckligt hög, kan segmenteringsjobbet misslyckas eller ta slut, vilket tvingar dig att designa om publiken.

Vid kritiska valideringsfel kan du inte spara på publiken.

+++

**Kan jag begära en ökning av gränsen för sekventiell händelse?**

+++ Svar

Nej, det kan du inte. Detta är ett hårt skyddsräcke som utformats för att skydda stabiliteten i hela Experience Platform-miljön. Om din sekvens kräver mer än sex steg är det en stark indikator på att logiken antingen ska förenklas eller delas upp i två olika målgrupper (till exempel en&quot;engagerande&quot; målgrupp och en&quot;konverteringsgrupp&quot;).

+++

**Kommer dessa nya valideringar att bryta ned mina befintliga målgrupper?**

+++ Svar

Dessa valideringar körs vid redigering av **&#x200B;**. Därför kommer era befintliga målgrupper att fortsätta att fungera som de är. Om du försöker redigera en befintlig målgrupp som bryter mot dessa regler måste du optimera den innan du kan spara ändringarna.

+++

**Jag har komplexa datakrav. Hur undviker jag varningen om kapslade data?**

+++ Svar

Det är bäst att undvika varningen om kapslade data i datamodelleringslagret. Några tips är att arbeta med ditt datateknikteam för att förenkla XDM-schemat och placera viktiga attribut (som `subscriptionStatus` och `loyaltyTier`) på den översta profilnivån.

+++

**Gäller de här kontrollerna både Utkast- och Publicerad-målgrupper?**

+++ Svar

Ja, de här kontrollerna gäller för *alla* målgrupper som utvärderas i Experience Platform.

+++
