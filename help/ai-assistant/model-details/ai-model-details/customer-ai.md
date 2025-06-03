---
title: Kort för AI-poängsättningsmodell för kund
description: Lär dig mer om AI-modellen som används för kundens AI.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: dddd699f231d54ee44b33f86a5c9e59c0aedc30c
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Kort för AI-poängsättningsmodell för kund

## Modellöversikt {#model-overview}

* Kundens AI-poängsättningsmodell är utformad för att ge marknadsförare och kundinteraktionsteam åtgärdbara insikter genom att förutsäga sannolikheten för att en kund kommer att utföra en viss åtgärd, som att göra ett köp, registrera sig för en prenumeration eller engagera sig i en e-postkampanj. Tack vare resultaten kan företag optimera målgruppssegmentering och personalisera kundinteraktioner baserat på förutsedda beteenden.
* De främsta användarna i den här modellen är marknadsförare, dataanalytiker och kundinteraktionsteam som utnyttjar [Real-Time CDP](../../../rtcdp/home.md) för att driva datadrivna marknadsföringsstrategier.
* Den här modellen används främst för kundsegmentering, riktad marknadsföring och bortfallsprognoser. Företagen använder den här modellen för att förutsäga kundens inköpsavsikt, optimera marknadsföringskampanjer och förbättra personaliseringen. Ett e-handelsföretag kan till exempel använda modellen för att identifiera kunder med hög återgivning och erbjuda dem exklusiva erbjudanden.
* Marknadsförare kämpar ofta med att identifiera rätt kunder för att målinrikta och optimera engagemanget. Den här modellen minskar gissningsarbetet genom att tillhandahålla en datadriven metod för kundanpassning, vilket säkerställer att marknadsföringsresurserna fördelas effektivt.
* Modellen bör inte användas för beslutsfattande med hög risk, t.ex. bedömning av finansiella krediter, medicinsk diagnostik eller rättsliga bedömningar. Dessutom är det inte avsett att användas för att förutsäga personligt känsliga beteenden (t.ex. hälsoförhållanden, politiska preferenser) på grund av potentiella etiska frågor.

## Modellinformation {#model-details}

* Det här är en modell för inlärningsklassificering som övervakar sannolikheten för att en händelse inträffar (inköp, bortfall, engagemang) utifrån historiska kunddata. Den har tränats med hjälp av övertoningsstartsbeslutsträd (GBDT) med logistisk regression för att modellera benägenhetspoäng.
* Modellen behandlar kundbeteendedata, demografiska attribut och historiska interaktioner. Detta inkluderar data som besöksfrekvens på webbplatser, inköpshistorik, engagemang med marknadsföringsmejl och demografiska uppgifter.
* Modellen ger en poäng mellan 0 och 100, där högre värden anger en större sannolikhet för den förväntade händelsen bland den poängsatta populationskohorten. Dessutom ger det funktionens prioritet och gör det möjligt för användarna att förstå vilka faktorer som påverkade förutsägelsen.

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

* Utbildningsdata för varje kund hämtas direkt från deras egna data inom Experience Platform. Detta inkluderar kundens historiska interaktioner, transaktionsregister, beteendeloggar och demografiska uppgifter som samlats in och lagrats i Experience Platform-instansen. Datauppsättningen utnyttjar kundspecifika data över den valda tidsramen och fångar upp deras unika säsongstrender och engagemangsmönster. Innan de används genomgår varje kunds datauppsättning en förbearbetning som är anpassad efter deras dataegenskaper, inklusive hantering av saknade värden, kategorisisk kodning, funktionens skalning, avkänning av tidigare versioner och funktionsteknik för att säkerställa optimal kvalitet och användbarhet för just deras användningsfall.
* Modellen utnyttjar [!DNL LightGBM] med [!DNL GBM], optimerad för strukturerade data. Det har utbildats på historiska kundhändelsesekvenser för att identifiera prediktiva beteendemönster.
* Modellen har utvecklats med [!DNL LightGBM] och [!DNL scikit-learn] och har tränats i Adobe AI-molninfrastruktur.
* Datorresurserna som används för modellutbildningen är [!DNL Databricks] kluster.

## Modellutvärdering {#model-evaluation}

* Modellens effektivitet mäts med [!DNL AUC-ROC]. Eftersom kundens AI är avsett för ett mycket brett spektrum av kundanvändningsfall är det inte känt hur stort operativsystemet är. Därför används måttet [!DNL AUC] eftersom det är oberoende av räckvidd och budget.
* Utvärderingsdata innehåller reserverade kundposter och är förbehandlade på liknande sätt som utbildningsdata med funktionsnormalisering, kodning och rengöringssteg för att matcha förväntningarna på indataformat. När resultatfönstret har passerat kan den slutliga prestandautvärderingen utföras.

## Modelldistribution {#model-deployment}

* Modellen ligger hos Experience Platform AI-tjänster och är integrerad med olika Adobe-program. Det är tillgängligt via API-slutpunkter, vilket ger smidig åtkomst för realtidspreditioner och batchbearbetning i arbetsflöden för marknadsföring och kundengagemang.
* Modellen övervakas kontinuerligt via modellövervakning för att se skillnaden från utbildningens uppbyggnad. Periodiska upptåg (en gång i 3 månader) körs automatiskt.
* Modellen omskolas en gång på flera månader (den bästa en gång på 6 månader) med uppdaterade data om kundinteraktionen för att säkerställa fortsatt relevans. Regelbunden omskolning bidrar till att minska dataavdrift och säsongsrelaterade fluktuationer som kan påverka prediktiv precision.

## Förklaring {#explainability}

Modellen använder [!DNL SHapley Additive Explanations] (SHAP) för att kvantifiera effekten av varje indatafunktion på dess prognoser, vilket ger transparens i hur kundattribut påverkar benägenhetspoängen. SHAP-värden möjliggör både global tolkning och identifierar de mest inflytelserika faktorerna i alla prognoser, samt lokal tolkning som förklarar individuella prognoser för specifika kunder. Modellen stöder även [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness and bias {#fairness-and-bias}

* Den här modellen är utbildad i anonyma beteendedata som är kopplade till cookie-ID:n, utan tillgång till skyddade demografiska attribut som ålder, kön eller etnicitet. Det är därför inte möjligt att direkt mäta rättvisa mellan känsliga grupper. Åtgärder för att minska bias är bland annat att normalisera användaraktivitetsfrekvensen, undertrycka överdrivet dominerande funktioner och genomföra kalibreringskontroller av poäng över kohorter.
* Modellen tar hänsyn till nybörjaravvikelser och övervakar exponeringsbias genom att utvärdera modellprognoser för randomiserad utelämningstrafik. Pågående utvärderingar finns på plats för att upptäcka och minska dubbelriktade förstärkningar och feedbackslingor under modelldriftsättningen.
* Datauppsättningen kommer huvudsakligen från engagerande användare, vilket kan innebära en förskjutning av urvalet. För att minska detta tillämpar modellen provtagningsstrategier.

## Robusitet {#robustness}

Modellen håller stor generalisering till nya kundregister. Prestandan är stabil för olika kundsegment men försämras något när användarbeteendet avviker avsevärt från historiska mönster.

## Sekretess och säkerhet {#privacy-and-security-considerations}

* Modellen behandlar inte eller bevarar någon personligt identifierbar information och alla data som används för utbildning anonymiseras och slås samman. Den uppfyller strikta krav på efterlevnad av GDPR, CCPA och Adobe interna integritetspolicyer. Modellen innehåller olika integritetstekniker, hashning, anonymisering och tokenisering för att säkerställa integriteten.
* Kunds-AI följer dina önskemål om samtycke. När du har [konfigurerat och aktiverat din medgivandeprincip](../../../data-governance/policies/user-guide.md#create-a-consent-policy) respekterar kundens AI de medgivandedata som samlats in från dig. Endast godkända data används för att bedöma modellen i efterföljande körningar av modellen. De nya poängen ersätter de gamla poängen och kan användas vid segmentering. Den här funktionen är för närvarande endast tillgänglig för kunder som har skölden för hälso- och sjukvård samt för kunder som har skölden för skydd av privatlivet och privatlivet.

## Etiska överväganden {#ethical-considerations}

Modellen skulle kunna ge upphov till partiskhet i beslutsfattandet. För att förhindra detta följer Experience Platform riktlinjer för ansvarsfull AI, som säkerställer att modellerna genomgår partiska revisioner, rimlighetstestning och mänsklig tillsyn före driftsättningen.
