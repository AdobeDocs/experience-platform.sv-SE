---
title: Skapa en Azure Synapse Analytics Source Connection i användargränssnittet
description: Lär dig hur du skapar en källanslutning för Azure Synapse Analytics (nedan kallad Synapse) med hjälp av Adobe Experience Platform användargränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Skapa en [!DNL Azure Synapse Analytics]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Azure Synapse Analytics] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Azure Synapse Analytics]-konto till Adobe Experience Platform med hjälp av källarbetsytan i användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Azure Synapse Analytics]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Azure Synapse Analytics] översikten](../../../../connectors/databases/synapse-analytics.md#prerequisites) om du vill ha information om autentisering.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Azure Synapse Analytics] går du till kategorin *[!UICONTROL Databases]*, markerar **[!UICONTROL Azure Synapse analytics]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med &quot;Azure Synapse Analytics&quot; har valts.](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Azure Synapse Analytics]-konto som du vill använda.

![Källarbetsflödets befintliga kontogränssnitt.](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Skapa ett nytt konto {#new}

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och kan lägga till en beskrivning för ditt konto.

![Källarbetsflödets nya kontogränssnitt.](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Anslut till Experience Platform

Du kan ansluta ditt [!DNL Azure Synapse Analytics]-konto till Experience Platform med autentisering av kontonycklar eller tjänstens huvudnamn och nyckelautentisering.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Om du vill använda kontonyckelautentisering väljer du **[!UICONTROL Account key authentication]**, anger din [anslutningssträng](../../../../connectors/databases/synapse-analytics.md#prerequisites) och väljer sedan **[!UICONTROL Connect to source]**.

![Stegen &quot;Skapa nytt konto&quot; i källarbetsflödet med &quot;verifiering av kontonyckel vald.](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

Du kan också välja **[!UICONTROL Service principal and key authentication]**, ange värden för dina [autentiseringsuppgifter](../../../../connectors/databases/synapse-analytics.md#prerequisites) och sedan välja **[!UICONTROL Connect to source]**.

![Steget Skapa nytt konto i källarbetsflödet med autentisering av tjänstens huvudnamn och nyckel markerat.](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## Skapa ett dataflöde för [!DNL Azure Synapse Analytics] data

Nu när du har anslutit din [!DNL Azure Synapse Analytics]-databas kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../dataflow/databases.md).
