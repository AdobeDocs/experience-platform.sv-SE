---
title: Hantera TTL för datauppsättning
description: Lär dig hur du schemalägger en TTL-tid (time to live) för en datauppsättning i Adobe Experience Platform-gränssnittet.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Hantera TTL för datamängd

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt Adobe Shield for Healthcare.

The [[!UICONTROL Data Hygiene] arbetsyta](./overview.md) i Adobe Experience Platform UI kan du schemalägga en TTL-tid (time to live) för en datauppsättning.

Det här dokumentet beskriver hur du schemalägger och hanterar TTL-värden för datauppsättningar i plattformsgränssnittet.

## Schemalägg en TTL

Om du vill skapa en ny begäran väljer du **[!UICONTROL Create request]** från huvudsidan på arbetsytan.

![Bilden visar [!UICONTROL Create request] knappen markeras](../images/ui/ttl/create-request-button.png)

Dialogrutan där begäran skapas visas. Under **[!UICONTROL Action]** avsnitt, markera **[!UICONTROL Dataset]** för att uppdatera de tillgängliga kontrollerna för TTL-schemaläggning.

![Bilden visar [!UICONTROL Dataset] valt alternativ](../images/ui/ttl/create-request-button.png)

### Välj ett datum och en datauppsättning

Under **[!UICONTROL Action]** väljer du ett datum som du vill att datauppsättningen ska tas bort av. Du kan ange datumet manuellt (i formatet `mm/dd/yyyy`) eller välj kalenderikonen (![Bild på kalenderikonen](../images/ui/ttl/calendar-icon.png)) för att välja datumet i en dialogruta.

![Bild som visar ett förfallodatum som anges för TTL](../images/ui/ttl/select-date.png)

Nästa, under **[!UICONTROL Dataset Details]**, markerar du databasikonen (![Bild på databasikonen](../images/ui/ttl/database-icon.png)) för att öppna en dialogruta för val av datauppsättning. Välj en datauppsättning från listan som du vill använda TTL-värdet på och välj sedan **[!UICONTROL Done]**.

![Bild som visar vilken datauppsättning som väljs](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Endast datauppsättningar som tillhör den aktuella sandlådan visas.

### Skicka begäran

När du har valt en datauppsättning och ett TTL-datum väljer du **[!UICONTROL Submit]**.

![Bilden visar [!UICONTROL Submit] knappen markeras](../images/ui/ttl/select-dataset.png)

Du ombeds bekräfta datumet då datauppsättningen ska tas bort senast. Välj **[!UICONTROL Submit]** för att fortsätta.

När begäran har skickats skapas en arbetsorder och visas på [!UICONTROL Consumer] -fliken i [!UICONTROL Data Hygiene] arbetsyta. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

## Redigera eller avbryta en TTL

Om du vill redigera eller avbryta en TTL-fil väljer du **[!UICONTROL Dataset]** på arbetsytans huvudsida och välj TTL i listan.

På informationssidan i TTL-listan visas kontroller för att redigera eller avbryta den schemalagda borttagningen.

## Nästa steg

I det här dokumentet beskrivs hur du schemalägger TTL-värden för datauppsättningar i användargränssnittet för Experience Platform. Mer information om hur du utför andra datahygienuppgifter i användargränssnittet finns i [översikt över användargränssnittet för datahygien](./overview.md).

Mer information om hur du schemalägger TTL-värden för datauppsättningar med API:t för datahygien finns i [TTL-slutpunktshandbok för datauppsättning](../api/ttl.md).
