---
keywords: Experience Platform;product purchase recept;Data Science Workspace;populära topics;recipes;prebuild recept
solution: Experience Platform
title: Produktinköpsförutsägelsekvitto
description: Med recept för produktinköpsförutsägelse kan du förutsäga sannolikheten för en viss typ av kundinköpshändelse, till exempel ett produktköp.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Produktinköpsprognosrecept

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Med recept för produktinköpsförutsägelse kan du förutsäga sannolikheten för en viss typ av kundinköpshändelse, till exempel ett produktköp.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Följande dokument kommer att svara på frågor som:
* Vem är receptet avsett för?
* Vad gör det här receptet?

## Vem är receptet avsett för?

Varumärket vill öka försäljningen varje kvartal för er produktlinje genom effektiva och målinriktade kampanjer till era kunder. Alla kunder är dock inte likadana och ni vill ha pengarna till godo. Vem riktar du dig till? Vilka av era kunder är mest benägna att svara utan att stöta på er kampanj? Hur anpassar ni era kampanjer till varje kund? Vilka kanaler ska ni förlita er på och när ska ni skicka ut kampanjer?

## Vad gör det här receptet?

recept på produktinköpsförutsägelse använder maskininlärning för att förutsäga kundens köpbeteende. Det gör man genom att använda en anpassad slumpmässig skogsklassificerare och en XDM-modell (Experience Data Model) med två nivåer för att förutsäga sannolikheten för en köphändelse. Modellen använder indata som innehåller information om kundprofiler och tidigare inköpshistorik, och som standard används förbestämda konfigurationsparametrar som våra datavetare fastställer för att förbättra förutsägbarheten.

## Datamodell

I det här receptet används [XDM-scheman](../../xdm/home.md) för att modellera data. Schemat som används för det här receptet visas nedan:

| Fältnamn | Typ |
| --- | --- |
| userId | Sträng |
| könRatio | Nummer |
| ageY | Nummer |
| ageM | Nummer |
| optinEmail | Boolean |
| optinMobile | Boolean |
| optinAddress | Boolean |
| skapad | Heltal |
| totalOrders | Nummer |
| totalItems | Nummer |
| orderDate1 | Nummer |
| shippingDate1 | Nummer |
| totalPrice1 | Nummer |
| tax1 | Nummer |
| orderDate2 | Nummer |
| shippingDate2 | Nummer |
| totalPrice2 | Nummer |


## Algoritm

Först läses utbildningsdatauppsättningen i *ProductPredication* -schemat in. Härifrån utbildas modellen med en [slumpmässig skogsklassificerare](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Slumpmässig skogsklassificerare är en typ av ensemberad algoritm som refererar till en algoritm som kombinerar flera algoritmer för att få bättre prediktiva prestanda. Tanken bakom algoritmen är att den slumpmässiga skogsklassificeraren bygger flera beslutsträd och sammanfogar dem för att skapa en mer korrekt och stabil förutsägelse.

Denna process börjar med att skapa en uppsättning beslutsträd som slumpvis väljer ut undergrupper av utbildningsdata. Därefter beräknas medelvärdet för resultaten av varje beslutsträd.
