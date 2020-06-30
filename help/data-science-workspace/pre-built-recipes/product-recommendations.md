---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Produktrekommendationsrecept
topic: overview
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---


# Produktrekommendationsrecept

Med recept för produktrekommendationer kan ni tillhandahålla personaliserade produktrekommendationer som är skräddarsydda efter kundens behov och intressen. Med en korrekt prognosmodell kan en kunds inköpshistorik ge er insikt i vilka produkter de kan vara intresserade av.

## Vem är receptet avsett för?

I dag kan en återförsäljare erbjuda ett stort antal produkter och ge sina kunder många valmöjligheter som även kan hindra deras kunder från att söka. På grund av tidsbegränsningar och begränsningar i ansträngningen kanske kunderna inte hittar den produkt de vill ha, vilket leder till köp med en hög nivå av kognitiv avståelse eller inga inköp alls.

## Vad gör det här receptet?

recept på produktrekommendationer använder maskininlärning för att analysera kundens interaktioner med produkter tidigare och generera en personlig lista med produktrekommendationer snabbt och enkelt. Detta optimerar processen för produktupptäckt och eliminerar långa, produktiva och irrelevanta sökningar för dina kunder. Resultatet blir att recept på produktrekommendationer kan förbättra en kunds totala inköpsupplevelse, vilket leder till större engagemang och ökad varumärkeslojalitet.

## Hur kommer jag igång?

Du kan komma igång genom att följa självstudiekursen för Adobe Experience Platform Lab (se Lab-länken nedan). I den här självstudiekursen visas hur du skapar recept för produktrekommendationer i en Jupyter-anteckningsbok genom att följa [anteckningsboken för att hämta](../jupyterlab/create-a-recipe.md) arbetsflödet och implementera receptet i [!DNL Experience Platform] [!DNL Data Science Workspace].

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

recept för produktrekommendationer använder samarbetsfiltrering för att generera en personlig lista med produktrekommendationer för dina kunder. I motsats till innehållsbaserad filtrering kräver inte samarbetsbaserad filtrering information om en viss produkt, utan snarare en kunds historiska preferenser för en uppsättning produkter. Denna kraftfulla rekommendationsteknik använder två enkla antaganden:
* Det finns kunder med liknande intressen, och de kan grupperas genom att jämföra sina köp- och surfbeteenden.
* Det är mer sannolikt att en kund är intresserad av en rekommendation baserad på liknande kunder vad gäller deras köp- och surfbeteende.

Denna process är uppdelad i två huvudsteg. Börja med att definiera en delmängd av liknande kunder. Identifiera sedan liknande funktioner bland kunderna i den uppsättningen för att returnera en rekommendation till målkunden.