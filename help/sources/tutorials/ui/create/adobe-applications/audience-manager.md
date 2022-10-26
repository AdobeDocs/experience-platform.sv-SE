---
keywords: Experience Platform;hem;populära ämnen;Målgruppshanterarens källkontakt;Audience Manager;målgruppshanterarens koppling
title: Skapa en Adobe Audience Manager Source Connection i användargränssnittet
description: I den här självstudiekursen får du hjälp med att skapa en källanslutning för Adobe Audience Manager så att du kan hämta data om konsumentupplevelsehändelser till plattformen med hjälp av användargränssnittet.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 9cdb8933d166445bf41ed314d7ffc7d5762e1adb
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Skapa en Adobe Audience Manager-källanslutning i användargränssnittet

I den här självstudiekursen får du hjälp med att skapa en källanslutning för Adobe Audience Manager för att hämta data om konsumentupplevelsehändelser till plattformen med hjälp av användargränssnittet.

## Skapa en källanslutning med Adobe Audience Manager

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Adobe Application], markera **[!UICONTROL Adobe Audience Manager]** och sedan markera **[!UICONTROL Set up]**.

![katalog](../../../../images/tutorials/create/aam/catalog.png)

### Markera egenskaper och segment

>[!NOTE]
>
>Du kan inte importera regionala data från Audience Manager-källan till Experience Platform. Om ni har användningsfall för Analytics som kräver regionala data kan ni använda [Källanslutning för analyser](../adobe-applications/analytics.md).

The [!UICONTROL Select traits and segments] visas så att du får ett interaktivt gränssnitt där du kan utforska och välja egenskaper, segment och data.

* Den vänstra panelen i gränssnittet innehåller [!UICONTROL Select traits and segments] samt en hierarkisk katalog över alla segment som är tillgängliga för dig.
* Den högra delen av gränssnittet gör att du kan interagera med valda segment och välja bland specifika data som du vill använda.

![tilläggsdata](../../../../images/tutorials/create/aam/add-data.png)

Om du vill navigera bland tillgängliga segment väljer du den mapp du vill komma åt på menyn [!UICONTROL All Segments] -panelen. Om du väljer en mapp kan du gå igenom mappens hierarki och visa en lista med segment som du kan filtrera igenom.

![segment-mapp](../../../../images/tutorials/create/aam/segment-folder.png)

När du har identifierat och markerat de segment som du vill använda visas en ny panel till höger med listan över valda objekt. Du kan fortsätta använda olika mappar och välja olika segment för anslutningen. Om du markerar fler segment uppdateras panelen till höger.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Du kan också välja **[!UICONTROL Select all segments]** och **[!UICONTROL Select all traits]** rutor. Om du markerar alla segment kommer Audience Manager segment att få plats på plattformen, och om du väljer alla egenskaper aktiveras alla egenskaper från Audience Manager.

>[!WARNING]
>
>Intag av stora Audience Manager-segmentpopulationer har en direkt inverkan på det totala antalet profiler när du för första gången skickar ett Audience Manager-segment till plattformen via Audience Manager. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Granska [användningsutrymme för licens](../../../../../dashboards/guides/license-usage.md) innan du fortsätter.

När du är klar väljer du **[!UICONTROL Next]**

![helsegmentering](../../../../images/tutorials/create/aam/all-segments.png)

The [!UICONTROL Review] visas så att du kan granska de valda egenskaperna och segmenten innan de är anslutna till plattformen. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Selected data]**: Visar antalet markerade segment och aktiverade egenskaper.

![recension](../../../../images/tutorials/create/aam/review.png)

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** så att dataflödet kan skapas.

## Nästa steg

När ett dataflöde i Audience Manager är aktivt hämtas inkommande data automatiskt till kundprofiler i realtid. Du kan nu använda dessa inkommande data och skapa målgruppssegment med hjälp av plattformssegmenteringstjänsten. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../../profile/home.md)
* [Översikt över segmenteringstjänsten](../../../../../segmentation/home.md)
