---
keywords: Experience Platform;home;Data Science Workspace;populära topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;Intelligence;aep Intelligence package
solution: Experience Platform
title: Data Science Workspace Access and Features
topic-legacy: Access and features for data science workspace
description: I följande dokument beskrivs behörigheter och åtkomst till funktioner i arbetsytan Data Science.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 319cdb13c965010062aa9179b197d6f5b6a20287
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---

# Åtkomst och funktioner till arbetsytan Data Science

I följande dokument beskrivs behörigheter och åtkomst till funktioner i arbetsytan Data Science.

![DSW-flikar](./images/access/platform-tabs.png)

- **bärbara datorer:** Innehåller en interaktiv utvecklingsmiljö ([JupyterLab](./jupyterlab/overview.md)) för att utforska, analysera och modellera data på Experience Platform.
- **Modeller:** innehåller verktyg för att skapa, publicera och lagra avancerade maskininlärningsrecept och modeller. Mer information finns i [skapa och publicera en maskininlärningsmodell](./models-recipes/create-publish-model.md) självstudiekurs.
- **Tjänster:** Innehåller både tjänster som tillhandahålls av Adobe, t.ex.  [AI/ML-](../intelligent-services/home.md) tjänster och anpassade tjänster som du har skapat med Data Science Workspace.

Varför visas bara fliken Tjänster?

- Din organisation kan endast vara berättigad till kunddataplattform i realtid (RTCDP) som innehåller kundens AI/ML-tjänst.

Om du inte kan se någon av flikarna **Datavetenskap** och vill använda funktioner i Datavetenskapen, kontaktar du företagets administratör för att kontrollera om du har en Adobe Experience Platform Intelligence-licens.

## Data Science Workspace-paketering

Data Science Workspace-funktionerna finns i Adobe Experience Platform Intelligence-paketet och Advanced Intelligence Pack-tillägget

I följande tabell beskrivs några av de viktigaste skillnaderna för Data Science Workspace-berättiganden med och utan tillägget Advanced Intelligence Pack:

>[!NOTE]
>
>Du kan licensiera mer än ett tillägg till Advanced Intelligence Pack och den utökade kapaciteten läggs till i det totala berättigandet. Om du t.ex. har licensierat 2 Adobe Experience Platform Advanced Intelligence Pack-tillägg har du rätt till totalt 20 samtidiga användare av bärbara datorer.

| Tillstånd för datavetenskap | Endast Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence plus Advanced Intelligence Pack Add-on |
| --- | :---: | :---: |
| Antal anteckningsboksanvändare som stöds. | 5 samtidiga användare | Första paketet innehåller 5 samtidiga användare och ytterligare köp ger 10 samtidiga användare per paket. |
| Tillåter integrerade Jupyter-anteckningsböcker för utforskande dataanalys och modellutveckling. | X (Stöder R R-, Python- och Scala-bibliotek) | X (Lägger till PySpark- och Spark ML-bibliotek) |
| Inbyggd integrering med Query Service. Möjlighet att utforska och forma datauppsättningar med SQL i bärbara datorer. | X | X |
| Tillgång till fördefinierade mallar för bärbara datorer för prediktiv analys. | X | X |
| Utbilda och poängsätta modeller manuellt med Jupyter Notebooks. | X | X |
| Driftsätt och driftsätt modeller med möjlighet att boka utbildning och instuderingsjobb. |  | X |
| Recipe framework to easily configure, evaluate, training, score, and publish models into production. |  | X |
| UI-driven modellexperimenterande och utvärdering. |  | X |
| Stöd för djupgående inlärning i Tensorflow-modeller (GPU Compute). |  | X |
| Spark-baserad distribuerad beräkning för att träna och poängsätta mot stora datamängder (10 MM + rader). |  | X |

## Åtkomstkontroll

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor. Mer information finns i [översikten över åtkomstkontroll](../access-control/home.md).

För att kunna använda arbetsytan Datavetenskap måste behörigheten Hantera datavetenskapen aktiveras. I följande tabell visas effekterna av att ha den här behörigheten aktiverad eller inaktiverad:

| Behörighet | Aktiverad | Handikappade |
|---|---|---|
| Hantera arbetsytan Datavetenskap | Ger tillgång till alla tjänster i arbetsytan Datavetenskap. | API- och gränssnittsåtkomst till alla tjänster i Data Science Workspace är inaktiverat. När du är inaktiverad går det inte att välja sidorna **Anteckningsböcker**, **Models** och **Tjänster**. <li>Åtkomst till **tjänster** kan fortfarande vara tillgänglig via kunddataplattformen i realtid (RTCDP).</li> |

## Stöd för sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje Plattformsinstans har stöd för flera produktionssandlådor och icke-produktionssandlådor, där var och en har ett eget bibliotek med plattformsresurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka dina produktionssandlådor. Mer information om sandlådor finns i [översikten över sandlådor](../sandboxes/home.md).

För närvarande har Data Science Workspace följande sandlådebegränsning:

- Beräkningsresurser delas mellan sandlådor för produktion och icke-produktion.

## Nästa steg

I det här dokumentet beskrivs de olika typerna av åtkomst och funktioner som finns i arbetsytan Data Science.

Om du vill veta mer om arbetsytan Data Science Workspace, t.ex. ett komplett arbetsflöde, kan du börja med att läsa igenom [Data Science Workspace-genomgången](./walkthrough.md)-dokumentationen. Mer allmän information finns på [Översikt över arbetsytan Datavetenskap](./home.md).
