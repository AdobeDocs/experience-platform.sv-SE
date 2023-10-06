---
title: Användargränssnittshandbok för datalivscykel
description: Lär dig hur du hanterar livscykeluppgifter för data i Adobe Experience Platform användargränssnitt.
exl-id: 7199151a-5390-4150-8a1d-daf53b7a1f5b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Användargränssnittshandbok för datalängd {#lifecycle-ui-guide}

>[!CONTEXTUALHELP]
>id="platform_hygiene_privacyconsole_consumer"
>title="Status för datalivscykel"
>abstract="Den här widgeten visar det totala antalet postborttagningsjobb för skapad, misslyckad och slutförd datalängd. Om du vill ha mer information om dina datalivscykler väljer du **Datas livscykel** i den vänstra navigeringen."

>[!CONTEXTUALHELP]
>id="platform_hygiene_privacyconsole_recents"
>title="Senaste arbetsorder för livscykel"
>abstract="Den här widgeten visar de fem senast skapade eller uppdaterade arbetsordningarna för livscykeln för data, beroende på vilket alternativ du väljer högst upp till höger. Om du vill ha mer information om dina datalivscykler väljer du **Datas livscykel** i den vänstra navigeringen."

The **[!UICONTROL Data Lifecycle]** Med arbetsytan i Adobe Experience Platform UI kan du skapa och övervaka olika livscykelhanteringsuppgifter för data, inklusive att ta bort poster och schemalägga förfallotider för datauppsättningar.

Den här guiden beskriver hur du hanterar livscykelaktiviteter för data i plattformens användargränssnitt. Information om hur du utför dessa åtgärder med API-anrop finns i [API-guide för datahygien](../api/overview.md).

Om du vill komma åt arbetsytan väljer du **Datas livscykel** i den vänstra navigeringen.

![The [!UICONTROL Data Lifecycle] arbetsytan i plattformsgränssnittet med [!UICONTROL Data Lifecycle] markerat i den vänstra navigeringen.](../images/ui/overview/home.png)

Härifrån kan du bläddra bland befintliga arbetsorder och konfigurera nya livscykelåtgärder för data. Läs mer i följande avsnitt i den här handboken:

* [Bläddra bland befintliga arbetsorder](./browse.md)
* [Skapa en förfallobegäran för datauppsättning](./dataset-expiration.md)
* [Skapa en begäran om postborttagning](./record-delete.md)
