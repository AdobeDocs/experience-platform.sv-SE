---
keywords: Experience Platform;product recommendation recept;Data Science Workspace;populära topics;recipes;prebuild recept
solution: Experience Platform
title: Produktrekommendationsmottagare
topic: overview
description: Med Product Recommendations recept kan ni tillhandahålla personaliserade produktrekommendationer som är skräddarsydda efter kundens behov och intressen. Med en korrekt prognosmodell kan en kunds inköpshistorik ge er insikt i vilka produkter de kan vara intresserade av.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# Produktrekommendationsrecept

Med Product Recommendations recept kan ni tillhandahålla personaliserade produktrekommendationer som är skräddarsydda efter kundens behov och intressen. Med en korrekt prognosmodell kan en kunds inköpshistorik ge er insikt i vilka produkter de kan vara intresserade av.

## Vem är receptet avsett för?

I dag kan en återförsäljare erbjuda ett stort antal produkter och ge sina kunder många valmöjligheter som även kan hindra deras kunder från att söka. På grund av tidsbegränsningar och begränsningar i ansträngningen kanske kunderna inte hittar den produkt de vill ha, vilket leder till köp med en hög nivå av kognitiv avståelse eller inga inköp alls.

## Vad gör det här receptet?

Product Recommendations recept använder maskininlärning för att analysera kundens interaktioner med produkter tidigare och generera en personaliserad lista med produktrekommendationer snabbt och enkelt. Detta optimerar processen för produktupptäckt och eliminerar långa, produktiva och irrelevanta sökningar för dina kunder. Resultatet blir att recept på Product Recommendations kan förbättra kundens totala inköpsupplevelse, vilket leder till större engagemang och ökad varumärkeslojalitet.

## Hur kommer jag igång?

Du kan komma igång genom att följa självstudiekursen för Adobe Experience Platform Lab (se Lab-länken nedan). I den här självstudiekursen visas hur du skapar Product Recommendations-receptet i en Jupyter-anteckningsbok genom att följa [anteckningsboken för att hämta](../jupyterlab/create-a-recipe.md)-arbetsflödet och implementera receptet i [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: Förutse framtiden med datavetenskapen](https://expleague.azureedge.net/labs/L777/index.html)
* [Lab-resurser](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Datamodell

I det här receptet används anpassade [XDM-scheman](../../xdm/schema/field-dictionary.md) för att modellera in- och utdata:

### Schema för indatadata

| Fältnamn | Typ |
--- | ---
| itemId | Sträng |
| interactionType | Sträng |
| tidsstämpel | Sträng |
| userId | Sträng |

### Schema för utdata

| Fältnamn | Typ |
--- | ---
| rekommendationer | Sträng |
| userId | Heltal |

## Algoritm

Produktens Recommendations-recept använder samverkansfiltrering för att generera en personlig lista med produktrekommendationer för dina kunder. I motsats till innehållsbaserad filtrering kräver inte samarbetsbaserad filtrering information om en viss produkt, utan snarare en kunds historiska preferenser för en uppsättning produkter. Denna kraftfulla rekommendationsteknik använder två enkla antaganden:
* Det finns kunder med liknande intressen, och de kan grupperas genom att jämföra sina köp- och surfbeteenden.
* Det är mer sannolikt att en kund är intresserad av en rekommendation baserad på liknande kunder vad gäller deras köp- och surfbeteende.

Denna process är uppdelad i två huvudsteg. Börja med att definiera en delmängd av liknande kunder. Identifiera sedan liknande funktioner bland kunderna i den uppsättningen för att returnera en rekommendation till målkunden.