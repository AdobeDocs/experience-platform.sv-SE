---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Åtkomst och funktioner till arbetsytan Data Science
topic: Access and features for data science workspace
description: 'I följande dokument beskrivs behörigheter och åtkomst till funktioner i arbetsytan Data Science. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 2%

---


# Åtkomst och funktioner till arbetsytan Data Science

I följande dokument beskrivs behörigheter och åtkomst till funktioner i arbetsytan Data Science.

![DSW-flikar](./images/access/platform-tabs.png)

- **Bärbara datorer:** Innehåller en interaktiv utvecklingsmiljö ([JupyterLab](./jupyterlab/overview.md)) för att utforska, analysera och modellera data på Experience Platform.
- **Modeller:** Innehåller verktyg för att skapa, publicera och lagra avancerade maskininlärningsrecept och modeller. Mer information finns i självstudiekursen [Skapa och publicera en maskininlärningsmodell](./models-recipes/create-publish-model.md) .
- **Tjänster:** Innehåller både tjänster som tillhandahålls av Adobe, t.ex. [intelligenta tjänster](../intelligent-services/home.md) , och alla anpassade tjänster som du har skapat med Data Science Workspace.

Varför visas bara fliken Tjänster?

- Din organisation kan endast ha rätt till RTCDP (Real-time Customer Data Platform) som innehåller AI för Intelligent Service.

Om du inte kan se någon av **datavetenskapliga** flikar och vill använda funktionerna i Datavetenskapen kontaktar du företagets administratör och kontrollerar om du har en Adobe Experience Platform Intelligence-licens.

## Adobe Experience Platform Intelligence-pakettillägg

I följande tabell beskrivs några viktiga skillnader för Data Science Workspace med och utan tillägget Adobe Experience Platform Intelligence:

>[!NOTE]
>
>Du kan licensiera mer än ett Intelligence-paket och den utökade kapaciteten läggs till i det övergripande berättigandet. Om du till exempel har licensierat 2 Adobe Experience Platform Intelligence-paket får du fler än 20 användare samtidigt.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] med Intelligence package addon |
| --- | :---: | :---: |
| Antal anteckningsboksanvändare som stöds. | 5 samtidiga användare | Första paketet innehåller 5 samtidiga användare och ytterligare köp ger 10 samtidiga användare per paket. |
| Tillåter integrerade Jupyter-anteckningsböcker för analys av data och modellutveckling (R, Python, Scala, PySpark) | X | X |
| Inbyggd integrering med Query Service. Möjlighet att utforska och forma datauppsättningar med SQL i bärbara datorer. | X | X |
| Tillgång till fördefinierade mallar för bärbara datorer för prediktiv analys. | X | X |
| Utbilda och poängsätta modeller manuellt med Jupyter Notebooks. | X | X |
| Driftsätt och driftsätt modeller med möjlighet att boka utbildning och instuderingsjobb. |  | X |
| Recipe framework to easily configure, evaluate, training, score, and publish models into production. |  | X |
| UI-driven modellexperimenterande och utvärdering. |  | X |
| Stöd för djupgående inlärning i Tensorflow-modeller (GPU Compute). |  | X |
| Spark-baserad distribuerad beräkning för att träna och poängsätta mot stora datamängder (10 MM + rader). |  | X |

## Åtkomstkontroll

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor. Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md) .

För att kunna använda arbetsytan Datavetenskap måste behörigheten Hantera datavetenskapen aktiveras. I följande tabell visas effekterna av att ha den här behörigheten aktiverad eller inaktiverad:

| Behörighet | Aktiverad | Handikappade |
|---|---|---|
| Hantera arbetsytan Datavetenskap | Ger tillgång till alla tjänster i arbetsytan Datavetenskap. | API- och gränssnittsåtkomst till alla tjänster i Data Science Workspace är inaktiverat. När du är inaktiverad går det inte att välja **sidor för bärbara datorer**, **modeller** och **tjänster** . <li>Tillgång till **tjänster** kan fortfarande vara tillgänglig via kunddataplattformen i realtid (RTCDP).</li> |

## Stöd för sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje plattformsinstans har stöd för en produktionssandlåda och flera icke-produktionssandlådor, där var och en har ett eget bibliotek med plattformsresurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. Mer information om sandlådor finns i översikten över [sandlådor](../sandboxes/home.md).

För närvarande har Data Science Workspace följande sandlådebegränsning:

- Beräkningsresurser delas mellan sandlådan för produktion och icke-produktionssandlådor.

## Nästa steg

I det här dokumentet beskrivs de olika typerna av åtkomst och funktioner som finns i arbetsytan Data Science.

Om du vill veta mer om arbetsytan Data Science Workspace, t.ex. ett komplett arbetsflöde, kan du börja med att läsa [dokumentationen från genomgången](./walkthrough.md) av datavetenskapen. Mer allmän information finns i översikten över arbetsytan för [datavetenskap](./home.md).