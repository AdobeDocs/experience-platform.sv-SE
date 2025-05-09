---
title: AI Assistant Natural Language to SQL Model Card
description: Lär dig mer om AI Assistant Natural Language i SQL AI-modellen.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AI Assistant Operational Insights Natural Language to SQL Model Card

## Modellöversikt {#model-overview}

* Modellens officiella namn är AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) och släpptes i den senaste GA-versionen i februari 2025.
* Modellen är utformad för att översätta kundernas naturliga språkfrågor om driftsinsikter till SQL-frågor. Dessa SQL-frågor körs via Adobe Experience Platform kunskapsdiagram, som innehåller metadata om kundens Experience Platform-enheter, som scheman, datamängder, målgrupper, mål och resor. Resultatet av SQL-frågorna används sedan för att generera svar på kundernas frågor om det naturliga språket.
* De främsta användarna i den här modellen är marknadsförare, dataanalytiker eller kundreseansvariga, som vill förstå och agera utifrån driftinsikter inom Experience Platform med hjälp av naturligt språk. De kanske inte är experter på SQL eller datateknik, men behöver snabba, korrekta svar om sina Experience Platform-enheter för att fatta välgrundade beslut och optimera kundupplevelserna.
* Den här modellen är en del av AI Assistant för Operational Insights, där den hjälper användare att få tillgång till metadata om sina Experience Platform-enheter som målgrupper, resor, scheman, attribut, datamängder och destinationer. Användare kan ställa frågor på ett naturligt språk, som vilka målgrupper som är aktiverade eller vilka målgrupper som använder ett specifikt schema, och modellen översätter dessa till SQL-frågor via Experience Platform kunskapsdiagram. Detta gör att användarna snabbt kan få insyn i driften och fatta välgrundade beslut utan att behöva utforska eller fråga systemet manuellt.
* Den här modellen åtgärdar problem som affärsanvändare och analytiker som arbetar med Experience Platform ställs inför, till exempel komplexiteten i navigeringen i stora volymer sammankopplade metadata, behovet av att skriva SQL-frågor manuellt för att få operativa insikter och osynlighet i hur Experience Platform enheter som målgrupper, datauppsättningar och resor är sammankopplade eller fungerar. Genom att ge naturligt språk tillgång till metadata och automatisera SQL-genereringen minskar modellen beroendet av tekniska resurser, förkortar insiktstiderna och ger användarna möjlighet att fatta snabbare, datadrivna beslut.
* Modellen får inte användas för att komma åt eller härleda personligt identifierbar information (PII), t.ex. kundnamn, e-postadresser eller telefonnummer, även om sådana data finns på plattformen.
* Dessutom bör den inte förlitas för efterlevnads- eller styrningskontroller, t.ex. validering av datalagringspolicyer, regler för åtkomstkontroll eller godkännandestatus. Dessa uppgifter kräver specialsystem och strategier.

## Modellinformation {#model-details}

* Modelltypen är LLM Prompt med Dynamic In-Context Learning.
* Modellindata är användares naturliga språkfrågor.
* Modellen matar ut SQL-frågor i syntaxen [!DNL Snowflake], som körs över Experience Platform Knowledge Graph.

**Exempelindata**

```console
How many datasets were created within the last 10 days?
```

**Exempelutdata**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Modellutbildning {#model-training}

* [!DNL NL2SQL] använde [!DNL OpenAI] GPT-baserade modeller för kontextinlärning.
* Frågebanken [!DNL NL2SQL] innehåller 428 frågor från [!DNL Operational Insights]-teamet och 524 externa team för alfavärden.

## Modellutvärdering {#model-evaluation}

* Modellen utvärderas med hjälp av noggrannhet. Hur många av förfrågningarna som genererar rätt SQL-resultat, till exempel av alla [!DNL NL2SQL]-begäranden.
* Utvärderingsprocessen är en kombination av regelbaserad matchning (SQL-standardisering och sedan direkt SQL-strängmatchning), LLM-baserad SQL-lösare och mänsklig utvärdering
* Öppna uppsättningar används för regressionstestning och anteckningsprojekt varje vecka övervakar modellens prestanda genom att ta prov på verklig kundtrafik.
* När det gäller konsariell utvärdering finns det en separat modell inom och utanför omfånget som fungerar som en garanti för [!DNL NL2SQL].

## Modelldistribution {#model-deployment}

* LLM-modellen är en GPT-baserad modell som hanteras av [!DNL Azure OpenAI] API:er.
* Basmodellen är värd för [!DNL Azure].
* Modellen uppdateras regelbundet, varje vecka, genom att banken utökar sin verksamhet. Lägeslistan uppdateras även via nya strategier och instruktioner vid behov.

## Förklaring {#explainability}

I modellen används en separat förklaringsmodell för SQL.

## Fairness and bias {#fairness-and-bias}

* För att säkerställa att modelltolkningarna och genererar frågor på ett enhetligt sätt i olika användarsyften och språkvarianter utan att införa avvikelser eller förstärkande stereotyper använder Adobe snabb granskning, förklaringsfunktion och skydd mot att generera partiska eller oetiska resultat.
* Modellutdata påverkas av exemplen för In-Context Learning och vad som hämtas i uppmaningen. Frågebanksexemplen innehåller exempel som bedöms vara representativa ur PM:s perspektiv, och vi utökar också frågebankerna baserat på den faktiska kundtrafiken.

## Robusitet {#robustness}

Eftersom de flesta av de frågor som tas emot inte täcks av frågebanken, återspeglar exaktheten i produktionstrafiken modellens tillförlitlighet.

## Sekretess och säkerhet {#privacy-and-security-considerations}

Modellen bearbetar inte eller behåller ingen personligt identifierbar information (PII), och den informationen maskeras ut för SQL-generering. För attributbaserad behörighetskontroll bearbetas den genererade SQL-filen ytterligare av Experience Platform Knowledge Graph-teamet för att säkerställa styrningskvaliteten.

## Etiska överväganden {#ethical-considerations}

För att undvika att exponera PII-attribut eller känsliga attribut har modellen utformats för att stödja sekretess, undvika att förstärka befintliga dataavvikelser och respektera gränserna för åtkomstkontroll. Detta inkluderar filtrering, taggning och granskning av schemafält för ansvarsfull användning.

