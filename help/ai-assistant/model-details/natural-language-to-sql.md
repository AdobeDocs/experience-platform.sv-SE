---
title: AI Assistant Natural Language to SQL Model Details
description: Lär dig mer om AI Assistant Natural Language i SQL AI-modellen.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 26d05e9519491ef2e8f239cba6a2cde43cff941c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# AI Assistant Operational Insights Naturliga språk för SQL-modellinformation

>[!IMPORTANT]
>
>Adobe publicerar aktivt mer modellinformation. Ytterligare dokumentation kommer att läggas till i Experience League när den blir tillgänglig.

## Modellöversikt {#model-overview}

* **Modellnamn och version**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]).
* **Modellreleasedatum**: februari 2025
* **Modellsyfte**: Modellen är utformad för att översätta kundernas naturliga språkfrågor om driftsinsikter till SQL-frågor. Dessa SQL-frågor körs via Adobe Experience Platform kunskapsdiagram, som innehåller metadata om kundens Experience Platform-enheter, som scheman, datamängder, målgrupper, mål och resor. Resultatet av SQL-frågorna används sedan för att generera svar på kundernas frågor om det naturliga språket.
* **Avsedda användare**: De primära användarna i den här modellen är marknadsförare, dataanalytiker eller kundreseansvariga som vill förstå och agera utifrån driftinsikter inom Experience Platform med hjälp av naturligt språk. De kanske inte är experter på SQL eller datateknik, men behöver snabba, korrekta svar om sina Experience Platform-enheter för att fatta välgrundade beslut och optimera kundupplevelserna.
* **Användningsfall**: Den här modellen hjälper användare att komma åt metadata om sina Experience Platform-enheter, som målgrupper, resor, scheman, attribut, datamängder och mål. Användare kan ställa frågor på ett naturligt språk, som vilka målgrupper som är aktiverade eller vilka målgrupper som använder ett specifikt schema, och modellen översätter dessa till SQL-frågor via Experience Platform kunskapsdiagram. Detta gör att användarna snabbt kan få insyn i driften och fatta välgrundade beslut utan att behöva utforska eller fråga systemet manuellt.
* **Smärta punkter**: Den här modellen åtgärdar viktiga problem som affärsanvändare och analytiker som arbetar med Experience Platform ställs inför, till exempel komplexiteten i navigeringen i stora volymer sammankopplade metadata, behovet av att skriva SQL-frågor manuellt för att få operativa insikter samt osynlighet i hur Experience Platform enheter som målgrupper, datauppsättningar och resor är sammankopplade eller fungerar. Genom att ge naturligt språk tillgång till metadata och automatisera SQL-genereringen minskar modellen beroendet av tekniska resurser, förkortar insiktstiderna och ger användarna möjlighet att fatta snabbare, datadrivna beslut.

## Modellinformation {#model-details}

* **Modelltyp**: LLM-fråga med dynamisk inlärning i kontext
* **Indata**: Användarens naturliga språkfrågor.
* **Utdata**: Modellen matar ut SQL-frågor i syntaxen [!DNL Snowflake] som körs över Experience Platform kunskapsdiagram.

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

## Modellutvärdering {#model-evaluation}

* **Mätvärden och procedurer för utvärdering**: Modellen utvärderas genom att undersöka [!DNL NL2SQL] -begäranden och utvärdera hur många av förfrågningarna som ger rätt SQL-resultat. Utvärderingsprocessen är en kombination av regelbaserad matchning (SQL-standardisering och sedan direkt SQL-strängmatchning), LLM-baserad SQL-lösare och mänsklig utvärdering.
* **Utvärderingsdata och förbearbetning**: Vi använder öppna uppsättningar för regressionstest och har också anteckningsprojekt varje vecka för att övervaka modellens prestanda genom provad verklig kundtrafik.

## Modelldistribution {#model-deployment}

* **Modellövervakning**: Basmodellen hanteras av [!DNL Azure].
* **Modelluppdatering**: Adobe Experience Platform AI Assistant Operational Insights Natural Language till SQL Model uppdateras regelbundet (varje vecka) genom frågebanksexpansion. Modellen uppdateras också med nya strategier och instruktioner vid behov.

## Fairness and bias {#fairness-and-bias}

* **Modellens rättvisa**: För att säkerställa att modellens tolkar och genererar frågor på ett konsekvent sätt i olika användarsyften och språkliga varianter utan att införa partiska eller förstärkande stereotyper använder Adobe snabb granskning, förklaring och skydd mot att generera partiska eller oetiska utdata.
* **Databiaser**: Modellutdata påverkas av exempel på In-Context Learning och vad hämtningarna väljer i uppmaningen. Frågebanksexemplen innehåller exempel som anses vara representativa för Product Management. Beroende på användningsfallet bör kunderna överväga hur potentiella avvikelser i modellutdata kan anpassas till eller påverka den avsedda tillämpningen.

## Etiska överväganden {#ethical-considerations}

**Etiska överväganden som är kopplade till modellen**: För att undvika att exponera PII-attribut eller känsliga attribut har modellen utformats för att undvika att förstärka befintliga dataavvikelser och respektera åtkomstkontrollsgränser. Detta inkluderar filtrering, taggning och granskning av schemafält för ansvarsfull användning.
