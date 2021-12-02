---
keywords: Experience Platform;luma web data;Data Science Workspace;populära topics;recipes;demo data;demo web data;luma data
solution: Experience Platform
title: Skapa webbscheman och datauppsättningar för Luma
topic-legacy: tutorial
type: Tutorial
description: I den här självstudiekursen får du tillgång till de förutsättningar och resurser som krävs för Lumas modell för benägenhet för demo.
source-git-commit: fd0f6aa2ac73bdc0a5413c437d091df6bb5d38a6
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Skapa Luma-profilmodellscheman och datauppsättningar

I den här självstudiekursen får du de krav och resurser som krävs för alla andra [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] självstudiekurser. När detta är klart är följande scheman och datauppsättningar tillgängliga för dig och din IMS-organisation.

**Scheman:**

- Luma-webbdataschema
- Resultatschema för poängsättningsmodell för benägenhetsmodell

**Datauppsättningar:**

- Luma web dataset
- Utbildningsdata för modell av benägenhet
- Datauppsättning för bedömning av sannolikhetsmodell
- Resultatdatauppsättning för bedömning av sannolikhetsmodell

## Hämta resurserna {#assets}

I följande självstudie används en anpassad Luma-modell för köpbenägenhet. Innan du fortsätter [hämta nödvändiga resurser](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip-mapp. Mappen innehåller:

- Modell för inköpsbenägenhet
- En anteckningsbok som används för att importera data till en utbildnings- och bedömningsdatauppsättning (en deluppsättning av Lumas webbdata)
- En demo-JSON-fil som innehåller webbdata för 730 000 Luma-användare
- En bärbar dator med Python 3 EDA (explorativ dataanalys) som kan användas som tillval för att förstå webbdata och webbmodell.

>[!NOTE]
>
> Du kan använda ditt eget schema och data för alla självstudiekurser. Demomodellen som finns i resurserna fungerar dock inte om den inte innehåller rätt konfigurationsfiler och kravfil. Denna demobenägenhetsmodell har utformats för att fungera med Lumas webbdata.

### Skapa Luma-webbdataramat och importera data

För att kunna skapa en modell måste du ha en datauppsättning i Platform som används för att utbilda och bedöma modellen. Följande videosjälvstudiekurs från [Utbildning i datavetenskap](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) leder dig igenom hur du skapar Luma-schemat och importerar de data som används av modellen för inköpsbenägenhet.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Skapa datauppsättningar för kurser, poängsättning och poängsättning

Om du vill köra den bärbara datorn för recept builder eller använda API:t för att utbilda och klassificera en modell måste du ange de datamängder och scheman som används för utbildning/poängsättning. I följande videofilm får du hjälp med att konfigurera datamängder för utbildning, poängsättning och poängsättning samt det poängresultatschema som används i Lumas modell för köpbenägenhet.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Nästa steg

I den här självstudiekursen har du skapat de scheman och datamängder som krävs för Luma-benägenhetsmodellen. Nu kan du fortsätta med nästa självstudiekurs och skapa modellen med [recept builder bärbar dator](../jupyterlab/create-a-model.md) självstudiekurs.

Dessutom kan du utforska data med den medföljande EDA-anteckningsboken (Exploratory Data Analysis). Den här anteckningsboken kan användas för att förstå mönster i Luma-data, kontrollera datavården och sammanfattar relevanta data för den prediktiva benägenhetsmodellen. Mer information om dataanalys finns på [EDA-dokumentation](../jupyterlab/eda-notebook.md).