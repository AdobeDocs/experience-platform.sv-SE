---
title: Hantera förfallodatum för datauppsättning
description: Lär dig hur du schemalägger en förfallotid för en datauppsättning i Adobe Experience Platform-gränssnittet.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 769c872d67141b4973b29a492e72c23491e2d1ae
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Hantera förfallodatum för datauppsättning

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt skölden.

The [[!UICONTROL Data Hygiene] arbetsyta](./overview.md) i Adobe Experience Platform UI kan du schemalägga en förfallotid för datauppsättningar. När en datauppsättning når sitt förfallodatum startar datasjön, identitetstjänsten och kundprofilen i realtid separata processer för att ta bort datauppsättningens innehåll från sina respektive tjänster. När data har tagits bort från alla tre tjänsterna markeras förfallotiden som slutförd.

Det här dokumentet beskriver hur du schemalägger och hanterar förfallodatum för datauppsättningar i plattformsgränssnittet.

## Schemalägg ett förfallodatum för datauppsättning

Om du vill skapa en ny begäran väljer du **[!UICONTROL Create request]** från huvudsidan på arbetsytan.

![Bilden visar [!UICONTROL Create request] knappen markeras](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for dataset expiration scheduling-->

### Välj ett datum och en datauppsättning

Dialogrutan där begäran skapas visas. Under **[!UICONTROL Action]** väljer du ett datum som du vill att datauppsättningen ska tas bort av. Du kan ange datumet manuellt (i formatet `mm/dd/yyyy`) eller välj kalenderikonen (![Bild på kalenderikonen](../images/ui/ttl/calendar-icon.png)) för att välja datumet i en dialogruta.

![Bild som visar ett förfallodatum som anges för datauppsättningen](../images/ui/ttl/select-date.png)

Nästa, under **[!UICONTROL Dataset Details]**, markerar du databasikonen (![Bild på databasikonen](../images/ui/ttl/database-icon.png)) för att öppna en dialogruta för val av datauppsättning. Välj en datauppsättning i listan som du vill tillämpa förfallodatumet på och välj sedan **[!UICONTROL Done]**.

![Bild som visar vilken datauppsättning som väljs](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Endast datauppsättningar som tillhör den aktuella sandlådan visas.

### Skicka begäran

När du har valt en datauppsättning och ett förfallodatum väljer du **[!UICONTROL Submit]**.

![Bilden visar [!UICONTROL Submit] knappen markeras](../images/ui/ttl/submit.png)

Du ombeds bekräfta datumet då datauppsättningen ska tas bort senast. Välj **[!UICONTROL Submit]** för att fortsätta.

När begäran har skickats skapas en arbetsorder och visas på huvudfliken i [!UICONTROL Data Hygiene] arbetsyta. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

## Redigera eller avbryta en förfallotid för en datauppsättning

Om du vill redigera eller avbryta en förfallotid för en datauppsättning väljer du **[!UICONTROL Dataset]** på arbetsytans huvudsida och välj datauppsättningens förfallodatum i listan.

På informationssidan om datauppsättningens förfallodatum, visar den högra listen kontroller för att redigera eller avbryta den schemalagda borttagningen.

## Nästa steg

I det här dokumentet beskrivs hur du schemalägger förfallodatum för datauppsättningar i användargränssnittet i Experience Platform. Om du vill lära dig hur du schemalägger förfallodatum för datauppsättningar med hjälp av API:t för datahygien kan du läsa [Slutpunktshandbok för datauppsättningens förfallodatum](../api/dataset-expiration.md).
