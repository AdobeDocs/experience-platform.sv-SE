---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics;recipes;pre build recipe
solution: Experience Platform
title: Produktinköpsrecept
topic: overview
description: Med recept för produktinköpsförutsägelse kan du förutsäga sannolikheten för en viss typ av kundinköpshändelse, till exempel ett produktköp.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 5%

---


# Produktinköpsrecept

## Översikt

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
--- | ---
| userId | Sträng |
| könRatio | Siffra |
| ageY | Siffra |
| ageM | Siffra |
| optinEmail | Boolean |
| optinMobile | Boolean |
| optinAddress | Boolean |
| skapad | Heltal |
| totalOrders | Siffra |
| totalItems | Siffra |
| orderDate1 | Siffra |
| shippingDate1 | Siffra |
| totalPrice1 | Siffra |
| tax1 | Siffra |
| orderDate2 | Siffra |
| shippingDate2 | Siffra |
| totalPrice2 | Siffra |


## Algoritm

Först läses utbildningsdatauppsättningen i *ProductPredication* -schemat in. Härifrån utbildas modellen med en [slumpmässig skogsklassificerare](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Slumpmässig skogsklassificerare är en typ av ensemberad algoritm som refererar till en algoritm som kombinerar flera algoritmer för att få bättre prediktiva prestanda. Tanken bakom algoritmen är att den slumpmässiga skogsklassificeraren bygger flera beslutsträd och sammanfogar dem för att skapa en mer korrekt och stabil förutsägelse.

Denna process börjar med att skapa en uppsättning beslutsträd som slumpvis väljer ut undergrupper av utbildningsdata. Därefter beräknas medelvärdet för resultaten av varje beslutsträd.