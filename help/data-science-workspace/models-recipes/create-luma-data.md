---
keywords: Experience Platform;luma web data;Data Science Workspace;populära topics;recipes;demo data;demo web data;luma data
solution: Experience Platform
title: Skapa webbscheman och datauppsättningar för Luma
type: Tutorial
description: I den här självstudiekursen får du tillgång till de förutsättningar och resurser som krävs för Lumas modell för benägenhet för demo.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Skapa scheman och datauppsättningar för Luma-benägenhetsmodellen

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I den här självstudiekursen får du de krav och resurser som krävs för alla andra [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] självstudiekurser. När detta är klart är följande scheman och datauppsättningar tillgängliga för dig och din organisation.

**Scheman:**

- Luma-webbdataschema
- Resultatschema för poängsättningsmodell för benägenhetsmodell

**Datauppsättningar:**

- Luma web dataset
- Utbildningsdata för modell av benägenhet
- Datauppsättning för bedömning av sannolikhetsmodell
- Resultatdatauppsättning för bedömning av sannolikhetsmodell

## Hämta resurserna {#assets}

I följande självstudie används en anpassad Luma-modell för köpbenägenhet. [Ladda ned zip-mappen för nödvändiga resurser](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) innan du fortsätter. Mappen innehåller:

- Modell för inköpsbenägenhet
- En anteckningsbok som används för att importera data till en utbildnings- och bedömningsdatauppsättning (en deluppsättning av Lumas webbdata)
- En demo-JSON-fil som innehåller webbdata för 730 000 Luma-användare
- En bärbar dator med Python 3 EDA (explorativ dataanalys) som kan användas som tillval för att förstå webbdata och webbmodell.

>[!NOTE]
>
> Du kan använda ditt eget schema och data för alla självstudiekurser. Demomodellen som finns i resurserna fungerar dock inte om den inte innehåller rätt konfigurationsfiler och kravfil. Denna demobenägenhetsmodell har utformats för att fungera med Lumas webbdata.

### Skapa Luma-webbdataramat och importera data

För att kunna skapa en modell måste du ha en datauppsättning i Experience Platform som används för att utbilda och bedöma din modell. I följande videofilm från [Data Science Workspace-kursen](https://experienceleague.adobe.com/?lang=sv&recommended=ExperiencePlatform-U-1-2021.1.dsw) får du hjälp med att skapa Luma-schemat och inhämta data som används av inköpsbenägenhetsmodellen.

>[!VIDEO](https://video.tv.adobe.com/v/3447158?captions=swe)

### Skapa datauppsättningar för kurser, poängsättning och poängsättning

Om du vill köra den bärbara datorn för recept builder eller använda API:t för att utbilda och klassificera en modell måste du ange de datamängder och scheman som används för utbildning/poängsättning. I följande videofilm får du hjälp med att konfigurera datamängder för utbildning, poängsättning och poängsättning samt det poängresultatschema som används i Lumas modell för köpbenägenhet.

>[!VIDEO](https://video.tv.adobe.com/v/3447425?captions=swe)

## Nästa steg

I den här självstudiekursen har du skapat de scheman och datamängder som krävs för Luma-benägenhetsmodellen. Du kan nu fortsätta med nästa självstudiekurs och skapa modellen med självstudiekursen [recept builder för anteckningsbok](../jupyterlab/create-a-model.md).

Dessutom kan du utforska data med den medföljande EDA-anteckningsboken (Exploratory Data Analysis). Den här anteckningsboken kan användas för att förstå mönster i Luma-data, kontrollera datavården och sammanfattar relevanta data för den prediktiva benägenhetsmodellen. Om du vill veta mer om Analys av experimentella data kan du gå till [EDA-dokumentationen](../jupyterlab/eda-notebook.md).
