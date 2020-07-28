---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Adobe Audience Manager-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 2%

---


# Skapa en Adobe Audience Manager-källanslutning i användargränssnittet

I den här självstudiekursen får du hjälp med att skapa en källanslutning som Adobe Audience Manager kan använda för att hämta data om konsumentupplevelsehändelser till Platform via användargränssnittet.

## Skapa en källanslutning med Adobe Audience Manager

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På *katalogskärmen* visas ett antal olika källor som du kan skapa källanslutningar med, och varje källa visar antalet befintliga anslutningar som är kopplade till dem.

Under programkategorin *Adobe väljer du* Adobe Audience Manager **** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att visa dess dokumentation eller ansluta till källan.

Om du vill skapa en ny källanslutning för Adobe Audience Manager klickar du på **Anslut källa**.

![](../../../../images/tutorials/create/aam/aam_catalog.png)

En dialogruta visas. Klicka på **Anslut** för att skapa anslutningen.

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

Om en källanslutning till Adobe Audience Manager upprättas visas *källaktivitetssidan* för Audience Manager-anslutningen.

![](../../../../images/tutorials/create/aam/aam_flow.png)

Om du vill pausa inkommande Audience Manager-data kan du göra det genom att klicka på dataflödeslistan och växla dess *status* från den högra *egenskapskolumnen* .

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## Nästa steg

När ett dataflöde i Audience Manager är aktivt hämtas inkommande data automatiskt till kundprofiler i realtid. Du kan nu använda dessa inkommande data och skapa målgruppssegment med Platform segmenteringstjänst. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../../profile/home.md)
- [Översikt över segmenteringstjänsten](../../../../../segmentation/home.md)