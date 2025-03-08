---
title: Inmatning on demand för källdataflöden i användargränssnittet
description: Lär dig hur du skapar dataflöden on demand för dina källanslutningar med Experience Platform användargränssnitt.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: 7a287c8de3c3fd0670cbdf29cd58558b30982122
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# On-demand-inmatning för källdataflöden i användargränssnittet

Du kan använda on-demand-inmatning för att utlösa en flödeskörning av ett befintligt dataflöde med hjälp av källarbetsytan i Adobe Experience Platform användargränssnitt.

I det här dokumentet får du information om hur du skapar dataflöden på begäran för källor samt hur du försöker återanvända flödeskörningar som har bearbetats eller misslyckats.

>[!BEGINSHADEBOX]

**Vad är en flödeskörning?**

Flödeskörningar är en instans av körning av dataflöde. Om ett dataflöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

>[!ENDSHADEBOX]

## Komma igång

>[!NOTE]
>
>För att kunna skapa en flödeskörning måste du först ha flödes-ID:t för ett dataflöde som är schemalagt för engångsinmatning.

Dokumentet kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Dataflöden](../../../dataflows/home.md): Ett dataflöde är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källkopplingar till måldatauppsättningar, till identitetstjänsten och kundprofilen i realtid samt till destinationer.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

## Skapa ett dataflöde on demand {#create-a-dataflow-on-demand}

Navigera till fliken *[!UICONTROL Dataflows]* på källarbetsytan. Härifrån söker du efter det dataflöde som du vill köra på begäran och väljer sedan ellipserna (**`...`**) bredvid dataflödets namn.

![En lista med dataflöden på källarbetsytan.](../../images/tutorials/on-demand/select-dataflow.png)

Välj sedan **[!UICONTROL Run on-demand]** i listrutan som visas.

![En listruta med alternativet Kör på begäran markerat.](../../images/tutorials/on-demand/run-on-demand.png)

Konfigurera schemat för on demand-intaget. Markera **[!UICONTROL Ingestion start time]**, **[!UICONTROL Date range start time]** och **[!UICONTROL Date range end time]**.

| Schemaläggningskonfiguration | Beskrivning |
| --- | --- |
| [!UICONTROL Ingestion start time] | Den schemalagda tiden då flödeskörningen på begäran börjar. |
| [!UICONTROL Date range start time] | Det tidigaste datum och den tidigaste tid som data hämtas från. |
| [!UICONTROL Date range end time] | Datum och tid då data hämtas fram till. |

Välj **[!UICONTROL Schedule]** och tillåt ett par stunder så att dataflödet på begäran kan utlösas.

![Schemaläggningskonfigurationsfönstret för on demand-inmatning.](../../images/tutorials/on-demand/configure-schedule.png)

Välj dataflödets namn för att visa dataflödesaktiviteten. Här visas en lista över dataflödeskörningar som har bearbetats. Du kan köra enskilda versioner av ditt dataflöde på nytt oavsett om de har misslyckats eller slutförts. För körningsiterationer som har misslyckats kan du använda **[!UICONTROL Retry]** för att starta körningen igen efter att ha diagnostiserat och åtgärdat eventuella fel som kan ha påträffats under skapandeprocessen.

![En lista över bearbetade flödeskörningar för ett valt dataflöde.](../../images/tutorials/on-demand/processed.png)

Välj **[!UICONTROL Scheduled]** om du vill se en lista över dataflödeskörningar som är schemalagda för framtida förtäring.

![En lista över schemalagda flöden för ett valt dataflöde.](../../images/tutorials/on-demand/scheduled.png)

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig hur du skapar flöden på begäran för befintliga källfilsdataflöden. Mer information om källor finns i [Källöversikt](../../home.md)
