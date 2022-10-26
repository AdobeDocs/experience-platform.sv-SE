---
keywords: Översikt över mätvärden. Översikt över rtcdp-mått
title: Real-time Customer Data Platform hemsida och Dashboards
description: Kontrollpaneler, startsidan och förstagångsupplevelsen av Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] hemsida och kontrollpaneler

Hemsidan för Adobe Real-time Customer Data Platform (Real-Time CDP), som innehåller en mätinstrumentpanel, visas när du loggar in på Real-Time CDP.

Hemsidan är bara en av platserna där metriska kort visas. Real-Time CDP tillhandahåller mätkort genom hela upplevelsen. Dessa mätvärden ger information om data, profiler och målgrupper i systemet.

![bild](assets/home.png)

Om det inte finns några data i systemet när du loggar in på Real-Time CDP visas inte instrumentpanelen på startsidan. I det här fallet innehåller startsidan utbildningsmaterial för en förstagångsupplevelse. Som data samlas in, med andra ord som <!--sources-->datauppsättningar, profiler, segment och mål skapas och dataflöden in i systemet - instrumentpanelen uppdateras automatiskt för att visa information om dessa data<!-- in metric cards-->.

## Instrumentpanelsvy för hemsidan

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Kontrollpanelen är uppdelad i<!-- two areas.-->:

* **The leaderboard** visas längst upp på kontrollpanelen. I resultatlistan visas antalet datauppsättningar, profiler, segment och mål i systemet.

   ![bild](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Senaste objekt** innehåller de fem senaste datauppsättningarna, källorna, segmenten och destinationerna som lagts till i systemet.

   ![bild](assets/recent.png)

Ytterligare mätvärden - till exempel för profiler och segment - finns i andra delar av Real-time Customer Data Platform.

### Datauppsättningar

The **[!UICONTROL Datasets]** räknaren visar antalet datauppsättningar i systemet och mängden data i [!DNL Platform]. Den här räknaren uppdateras när en datauppsättning skapas.

Mer information om datauppsättningar finns i [datauppsättningar, översikt](../catalog/datasets/overview.md).

### Profiler

The **[!UICONTROL Profiles]** antal visar det totala antalet personer med profiler i [!DNL Real-time Customer Profile]. Det innehåller inte profilfragment. Det här är er totala adresserbara målgrupp.

Det här antalet använder standardvärdet [sammanfogningsprincip](profile/merge-policies.md) enligt konfigurationen för sammanfogningsprincipen i Unified Profile.

Antalet profiler uppdateras en gång var 24:e timme.

Mer information om profiler finns i [En enhetlig bild av era kunder i Real-Time CDP](profile/profile-overview.md).

### Segment

**[!UICONTROL Segments]** visar det totala antalet segment som skapats för organisationen. Numret uppdateras när nya segment skapas.

Mer information om segment finns i [Översikt över segmenteringstjänsten](segmentation/segmentation-overview.md).

### Mål 

**[!UICONTROL Destinations]** visar det totala antalet destinationer som skapats för organisationen. Numret uppdateras när nya mål skapas.

Mer information om destinationer finns i [Översikt över destinationer](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Senaste datauppsättningar

The **[!UICONTROL Recent datasets]** visar de fem senaste datauppsättningarna som skapats inom organisationen. Listan uppdateras när en ny datauppsättning skapas.

Välj en datauppsättning för att visa information om objektet, eller **[!UICONTROL View all]** för att se en lista över datauppsättningar. Därifrån kan du välja en specifik källa för information.

Mer information om datauppsättningar finns i [datauppsättningar, översikt](../catalog/datasets/overview.md).

### Senaste källor

The **[!UICONTROL Recent sources]** med ett metriskt kort visas de fem senaste källorna som skapats inom organisationen. Listan uppdateras när en ny källa skapas.

Välj en källa för att visa information om objektet, eller **[!UICONTROL View all]** för att se en lista över källor. Därifrån kan du välja en specifik källa för information.

Mer information om källor finns i [Översikt över källor](sources/sources-overview.md).

### Senaste segment

The **[!UICONTROL Recent segments]** med ett metriskt kort visas de fem senaste segmenten som har skapats inom organisationen. Listan uppdateras när ett nytt segment skapas.

Markera ett segment om du vill visa information om det objektet, eller **[!UICONTROL View all]** om du vill ha information om fler segment.

Mer information om segment finns i [Översikt över segmenteringstjänsten](segmentation/segmentation-overview.md).

### Senaste destinationer

The **[!UICONTROL Recent destinations]** med ett metriskt kort visas de fem senaste destinationerna som skapats inom organisationen. Listan uppdateras när ett nytt mål skapas.

Välj ett mål om du vill visa information om det objektet, eller **[!UICONTROL View all]** för att se information om fler destinationer.

Mer information om destinationer finns i [Översikt över destinationer](destinations/overview.md).
