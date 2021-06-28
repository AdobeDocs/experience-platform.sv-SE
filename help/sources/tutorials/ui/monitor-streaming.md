---
keywords: Experience Platform;startsida;populära ämnen;bildskärmskonton;bildskärmsdataflöden;dataflöden
description: Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du övervakar direktuppspelade dataflöden från arbetsytan Källor.
solution: Experience Platform
title: Övervaka dataflöden för strömningskällor i användargränssnittet
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Övervaka dataflöden för strömningskällor i användargränssnittet

I den här självstudiekursen beskrivs stegen för att övervaka dataflöden för direktuppspelningskällor med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Dataflöden](../../../dataflows/home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] och till [!DNL Destinations].
   * [Dataflödet körs](../../notifications.md): Dataflödeskörningar är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Övervaka dataflöden för strömningskällor

Välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Om du vill visa befintliga dataflöden för direktuppspelningskällor väljer du **[!UICONTROL Dataflows]** i den övre rubriken.

![katalog](../../images/tutorials/monitor-streaming/catalog.png)

Sidan [!UICONTROL Dataflows] innehåller en lista med alla befintliga dataflöden i organisationen, inklusive information om deras källdata, kontonamn och körningsstatus för dataflöd.

Välj namnet på det dataflöde som du vill visa.

![dataflöden](../../images/tutorials/monitor-streaming/dataflows.png)

Följande tabell innehåller mer information om status för dataflödeskörning:

| Status | Beskrivning |
| ------ | ----------- |
| Slutförd | Statusen `Completed` anger att alla poster för motsvarande dataflödeskörning bearbetades inom en timmes period. En `Completed`-status kan fortfarande innehålla fel i dataflödeskörningar. |
| Bearbetar | Statusen `Processing` anger att ett dataflöde ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` anger att aktiveringsprocessen för ett dataflöde har avbrutits. |

Sidan [!UICONTROL Dataflow Activity] visar specifik information om ditt dataflöde för direktuppspelning. Den översta banderollen innehåller det kumulativa antalet poster som importerats och poster som misslyckats för alla strömmande dataflöden i det valda datumintervallet.

Den nedre halvan av sidan visar information om antalet poster som tagits emot, importerats och misslyckats, per flödeskörning. Varje flödeskörning registreras i ett timfönster.

![dataflödesaktivitet](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Varje enskild dataflödeskörning visar följande information:

* **[!UICONTROL Dataflow run start]**: Den tid som dataflödet körs vid.
* **[!UICONTROL Processing time]**: Den tid det tog för dataflödet att bearbeta.
* **[!UICONTROL Records Received]**: Det totala antalet poster som tagits emot i dataflödet från en källkoppling.
* **[!UICONTROL Records Ingested]**: Det totala antalet poster som har importerats till  [!DNL Data Lake].
* **[!UICONTROL Records Failed]**: Antalet poster som inte har inhämtats  [!DNL Data Lake] på grund av datafel.
* **[!UICONTROL Ingestion Rate]**: Hur många poster som har importerats till  [!DNL Data Lake]. Det här måttet används när [!UICONTROL Partial Ingestion] är aktiverat.
* **[!UICONTROL Status]**: Representerar läget för dataflödet: antingen  [!UICONTROL Completed] eller  [!UICONTROL Processing]. [!UICONTROL Completed] innebär att alla poster för motsvarande dataflödeskörning har bearbetats inom en timma. [!UICONTROL Processing] betyder att dataflödeskörningen inte har slutförts ännu.

Som standard innehåller de data som visas mängder av konsumtion från de senaste sju dagarna. Välj **[!UICONTROL Last 7 days]** om du vill justera tidsramen för de poster som visas.

![change-time](../../images/tutorials/monitor-streaming/change-time.png)

Ett kalender-popup-fönster visas med alternativ för alternativa tidsramar för inmatning. Välj **[!UICONTROL Last 30 days]** och sedan **[!UICONTROL Apply]**.

![kalender](../../images/tutorials/monitor-streaming/calendar.png)

Om du vill visa information om ett visst dataflöde, inklusive fel, väljer du körningens starttid i listan.

![välj-fel](../../images/tutorials/monitor-streaming/select-fail.png)

Sidan [!UICONTROL Dataflow run overview] innehåller ytterligare information om dataflödet, till exempel motsvarande ID för dataflöde, måldatauppsättning och ID för IMS-organisation.

En flödeskörning med fel innehåller även panelen [!UICONTROL Dataflow run errors], som visar det specifika fel som ledde till att körningen misslyckades samt det totala antalet poster som misslyckades.

![fel](../../images/tutorials/monitor-streaming/failure.png)

## Nästa steg

I den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att övervaka dataflödena för direktuppspelning och identifiera de fel som ledde till eventuella felaktiga dataflöden. Mer information finns i följande dokument:

* [Översikt över källor](../../home.md)
* [Översikt över dataflöden](../../../dataflows/home.md)