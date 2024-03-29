---
title: Inmatning on demand för källdataflöden i användargränssnittet
description: Lär dig hur du skapar dataflöden on demand för dina källanslutningar med användargränssnittet i Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: 38da1c1d5e563ea3f66cc25a69ad726f709784d0
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# On-demand-inmatning för källdataflöden i användargränssnittet

Du kan använda on-demand-inmatning för att utlösa en flödeskörning av ett befintligt dataflöde med hjälp av källarbetsytan i Adobe Experience Platform användargränssnitt.

I det här dokumentet får du information om hur du skapar dataflöden på begäran för källor samt hur du försöker återanvända flödeskörningar som har bearbetats eller misslyckats.

>[!BEGINSHADEBOX]

**Vad är ett flöde?**

Flödeskörningar är en instans av körning av dataflöde. Om ett dataflöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

>[!ENDSHADEBOX]

## Komma igång

>[!NOTE]
>
>För att kunna skapa en flödeskörning måste du först ha flödes-ID:t för ett dataflöde som är schemalagt för engångsinmatning.

Dokumentet kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Dataflöden](../../../dataflows/home.md): Ett dataflöde är en representation av datajobb som flyttar data över plattformen. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källkopplingar till måldatauppsättningar, till identitetstjänsten och kundprofilen i realtid samt till destinationer.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Skapa ett dataflöde on demand {#create-a-dataflow-on-demand}

Navigera till *[!UICONTROL Dataflows]* -fliken i källarbetsytan. Här hittar du det dataflöde som du vill köra on demand och väljer ellipserna (**`...`**) bredvid ditt dataflödesnamn.

![En lista med dataflöden i källarbetsytan.](../../images/tutorials/on-demand/select-dataflow.png)

Nästa, välj **[!UICONTROL Run on-demand]** i listrutan som visas.

![En rullgardinsmeny med alternativet Kör på begäran markerat.](../../images/tutorials/on-demand/run-on-demand.png)

Konfigurera schemat för on demand-intaget. Välj **[!UICONTROL Ingestion start time]**, **[!UICONTROL Date range start time]** och **[!UICONTROL Date range end time]**.

| Schemaläggningskonfiguration | Beskrivning |
| --- | --- |
| [!UICONTROL Ingestion start time] | Den schemalagda tiden då flödeskörningen på begäran börjar. |
| [!UICONTROL Date range start time] | Det tidigaste datum och den tidigaste tid som data hämtas från. |
| [!UICONTROL Date range end time] | Datum och tid då data hämtas fram till. |

Välj **[!UICONTROL Schedule]** och ge ett par minuter så att dataflödet kan utlösas när det behövs.

![Schemaläggningskonfigurationsfönstret för on demand-inmatning.](../../images/tutorials/on-demand/configure-schedule.png)

Välj dataflödets namn för att visa dataflödesaktiviteten. Här visas en lista över dataflödeskörningar som har bearbetats. Välj ett dataflöde och välj sedan **[!UICONTROL Retry]** från den högra listen för att försöka lägga på igen för ett valt dataflöde som körs.

![En lista över bearbetade flödeskörningar för ett valt dataflöde.](../../images/tutorials/on-demand/processed.png)

Välj **[!UICONTROL Scheduled]** för att se en lista över dataflödeskörningar som är schemalagda för framtida intag.

![En lista över schemalagda flöden för ett valt dataflöde.](../../images/tutorials/on-demand/scheduled.png)

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig hur du skapar flöden på begäran för befintliga källfilsdataflöden. Mer information om källor finns i [källöversikt](../../home.md)
