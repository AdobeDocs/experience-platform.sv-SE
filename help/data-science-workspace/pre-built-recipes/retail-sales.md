---
keywords: Experience Platform;recept;data Science Workspace;populära topics;recipes;prebuild recept
solution: Experience Platform
title: Butiksförs.mottagare
description: Med butiksförsäljningsreceptet kan du förutsäga försäljningsprognos för alla butiker som behövs under en viss tidsperiod. Med en korrekt prognosmodell skulle handlaren kunna hitta förhållandet mellan efterfrågan och prispolitiken och fatta optimerade prissättningsbeslut för att maximera försäljningen och intäkterna.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Butiksförsäljningsrecept

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Med butiksförsäljningsreceptet kan du förutsäga försäljningsprognos för alla butiker som behövs under en viss tidsperiod. Med en korrekt prognosmodell skulle handlaren kunna hitta förhållandet mellan efterfrågan och prispolitiken och fatta optimerade prissättningsbeslut för att maximera försäljningen och intäkterna.

Följande dokument kommer att svara på frågor som:
* Vem är det här receptet byggt för?
* Vad gör det här receptet?
* Hur kommer jag igång?

## Vem är receptet avsett för?

En återförsäljare står inför många utmaningar när det gäller att vara konkurrenskraftiga på den nuvarande marknaden. Varumärket vill öka den årliga försäljningen för ert varumärke, men det finns många beslut att fatta för att minimera era driftskostnader. För mycket leverans ökar lagerkostnaderna samtidigt som för lite tillgång ökar risken för att förlora kunder till andra varumärken. Behöver du beställa mer leverans för de kommande månaderna? Hur bestämmer du dig för optimala priser för dina produkter för att bibehålla försäljningsmål varje vecka?

## Vad gör det här receptet?

Receptet Retail Sales Forecasting använder maskininlärning för att förutsäga försäljningstrender. Receptet gör detta genom att utnyttja rikedomen av historiska detaljhandelsdata och anpassad övertoning öka regressor maskininlärningsalgoritm för att förutsäga försäljning en vecka i förväg. Modellen använder tidigare inköpshistorik och standardinställningar till förbestämda konfigurationsparametrar som bestäms av våra datalog för att förbättra den förutsägbara noggrannheten.

## Hur kommer jag igång?

Du kan komma igång genom att följa den här [självstudiekursen](../jupyterlab/create-a-model.md).

I den här självstudiekursen går vi vidare med att skapa säljrecept i en Jupyter-anteckningsbok och använda anteckningsboken för att hämta arbetsflöden för att skapa recept i Adobe Experience Platform.

## Datamodell

I det här receptet används [XDM-scheman](../../xdm/schema/field-dictionary.md) för att modellera data. Schemat som används för det här receptet visas nedan:

| Fältnamn | Typ |
| --- | --- |
| datum | Sträng |
| store | Heltal |
| storeType | Sträng |
| weekSales | Nummer |
| storeSize | Heltal |
| temperatur | Nummer |
| regionalFuelPrice | Nummer |
| prick | Nummer |
| cpi | Nummer |
| arbetslöshet | Nummer |
| isHoliday | Boolean |


## Algoritm

Först läses utbildningsdatauppsättningen i schemat *DSWRetailSales* in. Härifrån tränas modellen med en [övertoningsförstärkningsalgoritm](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). För övertoningsförbättringar används idén att svaga studerande (en som är minst något bättre än en slumpmässig chans) kan bilda en rad olika studerande som fokuserar på att förbättra den tidigare elevens svagheter. Tillsammans kan de användas för att skapa en kraftfull prediktiv modell.

Processen består av tre element: en förlustfunktion, en svag elev och en additiv modell.

Förlustfunktionen avser ett mått på hur bra en prognosmodell gör när det gäller att kunna förutsäga det förväntade resultatet - minsta kvadratregression används i detta recept.

Vid övertoningshöjning används ett beslutsträd som den svaga eleven. Vanligtvis används träd med ett begränsat antal lager, noder och delningar för att säkerställa att eleven förblir svag.

Slutligen används en additiv modell. Efter beräkning av förlusten med förlustfunktionen väljs trädet som minskar förlusten och viktas för att förbättra modelleringen av de svårare observationerna. Resultatet av det viktade trädet läggs sedan till den befintliga sekvensen av träd för att förbättra modellens slutliga produktion - kvantitet av framtida försäljning .
