---
title: Fliken Nätverk
description: Lär dig hur du använder fliken Nätverk i Adobe Experience Platform Debugger.
keywords: felsökning;Experience Platform Debugger extension;chrome;extension;network;information
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Fliken Nätverk

Fliken **Nätverk** samlar alla Adobe Experience Cloud-lösningsanrop som gjorts på sidan och visar dem i ordning från vänster till höger. Standardparametrar etiketteras automatiskt med egna namn och ordnas för att gruppera gemensamma parametrar i samma roll.

![](images/network.jpg)

Den här skärmen är användbar när du vill jämföra nyckelvärdepar i olika träffar. Du kan bekräfta att de parametrar som används för integreringar, till exempel Experience Cloud Visitor-ID eller Kompletterande data-ID, är konsekventa för alla integreringar.

>[!NOTE]
>
>I nuläget visas inte alla parametrar som skickas i lösningsanrop (till exempel kontextvariabler för Analytics, anpassade målparametrar eller kundID:n för Experience Cloud ID-tjänsten) på nätverksskärmen.

Om du vill ändra information per lösning väljer du den lösning du vill visa i listan i det vänstra navigeringsfältet. Följande exempel filtreras så att endast Analytics visas:

![](images/network-analytics.jpg)

Om du vill återgå till att visa alla lösningar väljer du **[!UICONTROL Network]**

Markera ett objekt i nätverksvyn om du vill visa en utökad vy. I det utökade visningsfönstret kan du kopiera den information som visas till Urklipp.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Om du vill rensa listan väljer du **[!UICONTROL Remove Events]**.

Om du vill hämta en Excel-fil som innehåller informationen på den här skärmen väljer du **[!UICONTROL Download]**.
