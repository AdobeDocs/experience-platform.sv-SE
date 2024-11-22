---
title: SQL-tillägg för funktionskonstruktion
description: Läs mer om SQL-tillägget Data Distiller för framtagning av data för avancerad statistisk modellering. Det täcker de tillgängliga teknikerna för extrahering, omformning och markering.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# SQL-tillägg för funktionsteknik

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

Använd SQL-transformatortillägget för att förenkla och automatisera förbearbetningen av data för att tillgodose dina behov inom funktionskonstruktion. Använd det här tillägget för att bygga funktioner och njuta av smidiga experiment med olika funktionstekniker, inklusive att koppla ihop dem med modeller. Utformad för distribuerad datoranvändning kan du utföra funktionsteknologi på stora datamängder parallellt och skalbart, vilket avsevärt minskar tiden för förbearbetning av data med Data Distiller SQL-tillägget för funktionsteknik.

## Teknik - översikt {#technique-overview}

Funktionsteknikfunktionerna omfattar tre huvudområden: Funktionsextraktion, Funktionsomvandling och Val av funktioner. Varje område innehåller specifika funktioner som är utformade för att extrahera, konvertera, fokusera och förbättra förbearbetningen av data.

### Funktionsextrahering {#feature-extraction}

Extrahera relevant information från era data, särskilt textdata, och konvertera den till ett numeriskt format som de modeller som stöds kan använda eller omvandla och härleda datauppsättningar. Använd följande funktioner för att extrahera funktioner:

- **[Textuell transformator](./feature-transformation.md#textual-transformations)**: Konvertera textdata till numeriska funktioner.
- **[Räkna vektorizer](./feature-transformation.md#countvectorizer)**: Omvandla en samling textdokument till vektorer med tokenantal.
- **[N-gram](./feature-transformation.md#ngram)**: Generera sekvenser av n-gram från textdata.
- **[Stoppord, påminnelse](./feature-transformation.md#stopwordsremover)**: Filtrera bort vanliga ord som inte har någon väsentlig betydelse.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Mät hur viktiga ord är i ett dokument i förhållande till ett corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: Dela upp text i enskilda termer (ord).
- **[Word2Vec](./feature-transformation.md#word2vec)**: Mappa ord till vektorer med fast storlek och skapa ordinbäddningar.

### Omvandling av funktioner {#feature-transformation}

Förutom extraheringsfunktioner använder du följande allmänna transformatorer för att förbereda dina funktioner för avancerade statistiska modeller och härledda datauppsättningar. Använd skalning, normalisering eller kodning för att säkerställa att funktionerna är i samma skala och har en liknande fördelning.

#### Allmänna transformatorer

Nedan finns en lista med verktyg för bearbetning av ett stort antal datatyper som förbättrar arbetsflödet för förbehandling av data.

- **[Numerisk import](./feature-transformation.md#numeric-imputer)**: Fyll i värden som saknas i numeriska kolumner med ett angivet värde, till exempel medelvärdet eller medianen.
- **[Strängimport](./feature-transformation.md#string-imputer)**: Ersätt saknade strängvärden med ett angivet värde, till exempel den mest frekventa strängen i kolumnen.
- **[Vector Assembler](./feature-transformation.md#vector-assembler)**: Kombinera flera kolumner till en enda vektorkolumn för att förbereda data för maskininlärningsmodeller.
- **[Boolean Imputer](./feature-transformation.md#boolean-imputer)**: Fyll i booleska värden som saknas med ett angivet värde, till exempel `true` eller `false`.

#### Numeriska omformare

Använd dessa tekniker för att effektivt bearbeta och skala numeriska data för bättre modellprestanda.

- **[Binarizer](./feature-transformation.md#binarizer)**: Konvertera kontinuerliga funktioner till binära värden baserat på ett tröskelvärde.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: Mappa kontinuerliga funktioner till diskreta behållare.
- **[Min-Max Scaler](./feature-transformation.md#minmaxscaler)**: Ändra skala på funktioner till ett angivet intervall, vanligtvis [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)**: Skala om funktioner till intervallet [-1, 1] utan att ändra ljusstyrkan.
- **[Normalisering](./feature-transformation.md#normalizer)**: Normalisera vektorer så att de har enhetsnorm.
- **[Kvantitet för diskretisering](./feature-transformation.md#quantilediscretizer)**: Konvertera kontinuerliga funktioner till kategoriserade funktioner genom att binda dem till kvantiteter.
- **[Standardskala](./feature-transformation.md#standardscaler)**: Normalisera funktioner så att de har en enhetsstandardavvikelse och/eller nollmedelvärde.

#### Kategoriserade transformatorer

Använd dessa transformers för att konvertera och koda kategoriserade data till format som passar för maskininlärningsmodeller.

- **[Strängindexerare](./feature-transformation.md#stringindexer)**: Konvertera kategoriserade strängdata till numeriska index.
- **[En Hot Encoder](./feature-transformation.md#onehotencoder)**: Mappa kategoriserade data till binära vektorer.

### Val av funktioner {#feature-selection}

Fokusera sedan på att välja en deluppsättning av de viktigaste funktionerna i den ursprungliga uppsättningen. Denna process hjälper till att minska dimensioneringen av dina data, vilket gör det enklare för dina modeller att bearbeta och förbättra den övergripande modellprestandan.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Implementera OPTIONS-satsen {#options-clause}

När du definierar modellen använder du `OPTIONS`-satsen för att ange algoritmen och dess parametrar. Börja med att ange parametern `type` för att ange den algoritm som du använder, till exempel `K-Means`. Definiera sedan de relevanta parametrarna i `OPTIONS`-satsen som nyckelvärdepar för att finjustera modellen. Om du väljer att inte anpassa vissa parametrar används standardinställningarna. Läs den relevanta dokumentationen för att förstå de olika parametrarnas funktion och standardvärden.

### Nästa steg

När du har lärt dig de funktionstekniker som beskrivs i det här dokumentet går du vidare till dokumentet [Models](./models.md). Här får du hjälp med att skapa, utbilda och hantera tillförlitliga modeller med hjälp av de funktioner du har skapat. När du har skapat dina modeller fortsätter du till dokumentet [Implementera avancerade statistiska modeller.](./implement-models/implement-models.md). Det här dokumentet fungerar som en översikt och länkar till djupgående guider för olika modelleringstekniker, inklusive klustring, klassificering och regression. Genom att följa dessa dokument får du lära dig hur du konfigurerar och implementerar olika betrodda modeller i dina SQL-arbetsflöden och optimerar dina modeller för avancerad dataanalys.
