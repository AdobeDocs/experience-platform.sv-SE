---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;kampanj;kampanjhanterade tjänster
title: Skapa en källanslutning till Adobe Campaign Managed Services med hjälp av plattformsgränssnittet
description: Lär dig hur du ansluter Adobe Experience Platform till Adobe Campaign Managed Services med hjälp av plattformsgränssnittet.
hide: true
hidefromtoc: true
source-git-commit: 57a34b10e40dee80638392477d49c21e107c491f
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Skapa en källanslutning till Adobe Campaign Managed Services med hjälp av plattformsgränssnittet

I den här självstudiekursen beskrivs hur du skapar en källanslutning för att överföra dina Adobe Campaign Managed Services-data till Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Plattformen gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Plattformen innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Anslut Adobe Campaign Managed Services till plattformen

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka källor som visas.

Under **[!UICONTROL Adobe applications]** kategori, välj **[!UICONTROL Adobe Campaign Managed Services]** och sedan markera **[!UICONTROL Add data]**.

### Markera data {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="ACC-instans"
>abstract="Namnet på den Adobe Campaign Classic-miljö som du vill använda."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Målmappning"
>abstract="Målmappningar är tekniska objekt som används av Campaign för att leverera meddelanden och innehåller alla tekniska inställningar som krävs för att skicka leveranser (adresser, telefonnummer, anmälningsindikatorer, ytterligare identifierare..)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Schemanamn"
>abstract="Namnet på entiteten som definieras i Adobe Campaign-databasen."
>text="Learn more in documentation"

The [!UICONTROL Select data] visas, där du får ett gränssnitt för att konfigurera värden för [!UICONTROL Adobe Campaign instance], [!UICONTROL Target mapping]och [!UICONTROL Schema name].
