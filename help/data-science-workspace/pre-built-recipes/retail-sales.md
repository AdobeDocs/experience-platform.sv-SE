---
keywords: Experience Platform;recept;data Science Workspace;populära topics;recipes;prebuild recept
solution: Experience Platform
title: Butiksförs.mottagare
topic: overview
description: Med butiksförsäljningsreceptet kan du förutsäga försäljningsprognos för alla butiker som behövs under en viss tidsperiod. Med en korrekt prognosmodell skulle handlaren kunna hitta förhållandet mellan efterfrågan och prispolitiken och fatta optimerade prissättningsbeslut för att maximera försäljningen och intäkterna.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 1%

---


# Butiksförsäljningsrecept

Med butiksförsäljningsreceptet kan du förutsäga försäljningsprognos för alla butiker som behövs under en viss tidsperiod. Med en korrekt prognosmodell skulle handlaren kunna hitta förhållandet mellan efterfrågan och prispolitiken och fatta optimerade prissättningsbeslut för att maximera försäljningen och intäkterna.

Följande dokument kommer att svara på frågor som:
* Vem är receptet avsett för?
* Vad gör det här receptet?
* Hur kommer jag igång?

## Vem är receptet avsett för?

En återförsäljare står inför många utmaningar när det gäller att vara konkurrenskraftiga på den nuvarande marknaden. Varumärket vill öka den årliga försäljningen för ert varumärke, men det finns många beslut att fatta för att minimera era driftskostnader. För mycket leverans ökar lagerkostnaderna samtidigt som för lite tillgång ökar risken för att förlora kunder till andra varumärken. Behöver ni beställa mer för de kommande månaderna? Hur bestämmer ni er för optimala priser för era produkter för att uppnå era försäljningsmål varje vecka?

## Vad gör det här receptet?

I recept på försäljningsprognos används maskininlärning för att förutse försäljningstrender. receptet gör detta genom att utnyttja det stora utbudet av historiska detaljhandelsdata och en anpassad algoritm för att öka övertoningen, vilket gör att maskininlärningsalgoritmen kan förutse försäljningen en vecka i förväg. Modellen utnyttjar tidigare inköpshistorik och använder som standard förbestämda konfigurationsparametrar som fastställts av våra datavetare för att förbättra förutsägbarheten.

## Hur kommer jag igång?

Du kan komma igång genom att följa den här [självstudiekursen](../jupyterlab/create-a-recipe.md).

I den här självstudiekursen går vi vidare med att skapa säljrecept i en Jupyter-anteckningsbok och använda anteckningsboken för att hämta arbetsflöden för att skapa recept i Adobe Experience Platform.

## Datamodell

I det här receptet används [XDM-scheman](../../xdm/schema/field-dictionary.md) för att modellera data. Schemat som används för det här receptet visas nedan:

| Fältnamn | Typ |
--- | ---
| datum | Sträng |
| store | Heltal |
| storeType | Sträng |
| weekSales | Siffra |
| storeSize | Heltal |
| temperatur | Siffra |
| regionalFuelPrice | Siffra |
| markering | Siffra |
| cpi | Siffra |
| arbetslöshet | Siffra |
| isHoliday | Boolean |


## Algoritm

Först läses utbildningsdatauppsättningen i schemat *DSWRetailSales* in. Härifrån utbildas modellen med en [övertoningsförstärkningsalgoritm](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). För övertoningsförbättringar används idén att svaga studerande (en som är minst något bättre än en slumpmässig chans) kan bilda en rad olika studerande som fokuserar på att förbättra den tidigare elevens svagheter. Tillsammans kan de användas för att skapa en kraftfull prediktiv modell.

Processen består av tre delar: en förlustfunktion, en svag kursledare och en additiv modell.

Förlustfunktionen avser ett mått på hur bra en förutsägelsemodell gör när det gäller att kunna förutsäga det förväntade resultatet - regression på minst fyrkanter används i detta recept.

Vid övertoningsförbättring används ett beslutsträd som den svaga läraren. Vanligtvis används träd med ett begränsat antal lager, noder och delningar för att säkerställa att eleven förblir svag.

Slutligen används en additiv modell. Efter beräkning av förlusten med förlustfunktionen väljs det träd som minskar förlusten och viktas för att förbättra modelleringen av de svåraste observationerna. Resultatet av det viktade trädet läggs sedan till i den befintliga trädsekvensen för att förbättra slutresultatet av modellen - kvantitet för framtida försäljning.