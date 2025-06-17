---
title: Information om AI-betygsmodell för kund
description: Lär dig mer om AI-modellen som används för kundens AI.
source-git-commit: 6fe2041c0dc5f7f4b98dee00d3a793469b5f64db
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Information om AI-betygsmodell för kund

## Modellöversikt {#model-overview}

* **Modellnamn och version**: Kundens AI-prioritetsbedömningsmodell
* **Modellsyfte**: Modellen är utformad för att ge marknadsförare och kundinteraktionsteam åtgärdbara insikter genom att förutsäga sannolikheten för att en konsument kommer att utföra en viss åtgärd, till exempel göra ett köp, registrera sig för en prenumeration eller engagera sig i en e-postkampanj. Tack vare resultaten kan företag optimera målgruppssegmentering och personalisera konsumentinteraktioner baserat på förutsedda beteenden.
* **Avsedda användare**: De primära användarna i den här modellen är marknadsförare, dataanalytiker och kundinteraktionsteam som utnyttjar [Real-Time CDP](../../rtcdp/home.md) för att driva datadrivna marknadsföringsstrategier.
* **Användningsfall**: Den här modellen används främst för konsumentsegmentering, riktad marknadsföring och bortfallsprognoser. Företagen utnyttjar den här modellen för att förutsäga kundernas inköpsavsikt, optimera marknadsföringskampanjer och förbättra personaliseringen. Ett e-handelsföretag kan till exempel använda modellen för att identifiera kunder med hög återgivning och erbjuda dem exklusiva erbjudanden.
* **Smärta punkter**: Marknadsförare kämpar ofta med att identifiera rätt konsumenter för att målinrikta och optimera engagemanget. Den här modellen minskar gissningsarbetet genom att tillhandahålla en datadriven metod för målgruppsanpassning, vilket säkerställer att marknadsföringsresurserna fördelas effektivt.
* **Potentiell felaktig användning**: Modellen ska inte användas för högriskfall, t.ex. finansiell kreditbedömning, medicinsk diagnostik eller juridiska bedömningar. Dessutom bör modellen inte användas för att förutsäga personligt känsliga beteenden (t.ex. hälsoförhållanden, politiska preferenser).

## Modellinformation {#model-details}

* **Modelltyp**: Det här är en övervakad inlärningsklassificeringsmodell som förutser sannolikheten för en händelse som inträffar (till exempel köp, köp, engagemang) utifrån historiska konsumentdata. Den har tränats med hjälp av övertoningsstartsbeslutsträd (GBDT) med logistisk regression för att modellera benägenhetspoäng.
* **Indata**: Modellen behandlar konsumentbeteendedata, demografiska attribut och historiska interaktioner. Detta inkluderar data som besöksfrekvens på webbplatser, inköpshistorik, engagemang med marknadsföringsmejl och demografiska uppgifter.
* **Utdata**: Modellen returnerar en poäng mellan 0 och 100, där högre värden anger en större sannolikhet för den förväntade händelsen i den poängsatta populationskohorten. Dessutom ger den funktionens prioritet och gör det möjligt för marknadsförarna att förstå vilka faktorer som påverkade förutsägbarheten.

**Exempelindata**

```json
{ 
  "customer_id": 12345, 
  "past_purchases": 3, 
  "last_visit_days": 7,
  "email_click_rate": 0.4 
}
```

**Exempelutdata**

```json
{ 
  "customer_id": 12345,
  "SCORE": 89 
}
```

## Modellutbildning {#model-training}

* **Utbildningsdata och förbehandling**: Utbildningsdata för varje kund hämtas direkt från deras egna data i Adobe Experience Platform. Detta omfattar kundens historiska interaktioner, transaktionsregister, beteendeloggar och demografiska uppgifter som samlats in och lagrats i Adobe Experience Platform-instansen. Datauppsättningen utnyttjar kundspecifika data över den valda tidsramen och fångar upp deras unika säsongstrender och engagemangsmönster. Innan de används genomgår varje kunds datauppsättning en förbearbetning som är anpassad efter deras dataegenskaper, inklusive hantering av saknade värden, kategorisisk kodning, funktionens skalning, avkänning av tidigare versioner och funktionsteknik för att säkerställa optimal kvalitet och användbarhet för just deras användningsfall.
   * Konsumentdata som används för utbildning används inte för kunder.
* **Utbildningsspecifikationer**: Modellen utnyttjar [!DNL LightGBM] med [!DNL GBM], optimerad för strukturerade data. Det har utbildats på historiska kundhändelsesekvenser för att identifiera prediktiva beteendemönster.
* **Utbildningsramverk**: Modellen har utvecklats med [!DNL LightGBM] och [!DNL scikit-learn] och finns på Adobe AI-molninfrastruktur.
* **Utbildningsinfrastruktur**: [!DNL Databricks] kluster.

## Modellutvärdering {#model-evaluation}

* **Mätvärden och procedurer för utvärdering**: Modellens effektivitet mäts med [!DNL AUC-ROC]. Eftersom kundens AI är avsett för ett mycket brett spektrum av kundanvändningsfall är det inte känt hur stort operativsystemet är. Därför använder vi måttet [!DNL AUC] som är oberoende av räckvidd och budget.
* **Utvärderingsdata och förbehandling**: Utvärderingsdata innehåller konsumentposter som är utelämnade och förbearbetas på liknande sätt som utbildningsdata med funktionsnormalisering, kodning och rengöringssteg för att matcha förväntningarna för indataformat. När resultatfönstret är passerat kan vi göra en slutlig utvärdering av prestanda.

## Modelldistribution {#model-deployment}

* **Modelldistribution**: Modellen finns på Adobe Experience Platform AI-tjänster och är integrerad med olika Adobe-program. Det är tillgängligt via API-slutpunkter, vilket ger smidig åtkomst för realtidspreditioner och batchbearbetning i arbetsflöden för marknadsföring och konsumentengagemang.
* **Modellövervakning**: Modellen övervakas kontinuerligt via modellövervakning för att se skillnaden från utbildningens inställning. Periodiska upptåg (en gång i tre månader) körs automatiskt.
* **Modelluppdatering**: Modellen omskolas en gång på flera månader (högst en gång på sex månader) med uppdaterade interaktionsdata för konsumenter för att säkerställa fortsatt relevans. Regelbunden omskolning bidrar till att minska dataavdrift och säsongsrelaterade fluktuationer som kan påverka prediktiv precision.

## Förklaring {#explainability}

**Modellförklaring**: Modellen använder [!DNL SHapley Additive Explanations] (SHAP) för att kvantifiera effekten av varje indatafunktion på sina prognoser, vilket ger transparens i hur konsumentattribut påverkar benägenhetspoängen. SHAP-värden möjliggör både global tolkning, och identifierar de mest inflytelserika faktorerna i alla prognoser, samt lokal tolkning som förklarar individuella prognoser för specifika konsumenter. Modellen stöder även [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness and bias {#fairness-and-bias}

* **Modellens rättvisa**: Den här modellen har tränats på anonyma beteendedata som är kopplade till cookie-ID:n, utan åtkomst till skyddade demografiska attribut som ålder, kön eller etnicitet. Det är därför inte möjligt att direkt mäta rättvisa mellan känsliga grupper. Åtgärder för att minska bias är bland annat att normalisera användaraktivitetsfrekvensen, undertrycka överdrivet dominerande funktioner och genomföra kalibreringskontroller av poäng över kohorter. Vi tar hänsyn till nyheten och övervakar exponeringsbias genom att utvärdera modellprognoser för randomiserad utelämningstrafik. Pågående utvärderingar finns på plats för att upptäcka och minska dubbelriktade förstärkningar och feedbackslingor under modelldriftsättningen.
* **Databitar**: Datauppsättningen kommer huvudsakligen från användare med högt engagemang, vilket kan innebära en förskjutning av urvalet. För att minska detta tillämpar modellen provtagningsstrategier. Beroende på användningsfallet bör kunderna överväga hur potentiella avvikelser i modellutdata kan anpassas till eller påverka den avsedda tillämpningen.

## Robusitet {#robustness}

**Modellens tillförlitlighet**: Modellen upprätthåller stark generalisering till nya konsumentposter. Prestandan är stabil för olika konsumentsegment men försämras något när användarbeteendet avviker avsevärt från historiska mönster.

## Etiska överväganden {#ethical-considerations}

**Etiska överväganden som är kopplade till modellen**: Den här modellen är avsedd för användning på marknaden, och kunderna bör iaktta större försiktighet om de tillämpar den på känsliga eller reglerade domäner som kredit eller anställning. Utdata är sannolika och härledda från beteendedata, som kan återspegla historiska eller representationsmässiga biaser. Kunderna uppmuntras att tillämpa mänsklig tillsyn. Adobe Experience Platform följer riktlinjerna för ansvarsfull AI och ser till att modellerna genomgår partiska revisioner, rimlighetstestning och mänsklig tillsyn före driftsättningen. Mer information finns i [Etiska principer för Adobe AI](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).