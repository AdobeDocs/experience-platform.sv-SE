---
title: Anslut Oracle DB till Experience Platform med användargränssnittet
description: Lär dig hur du ansluter Oracle DB-instansen till Experience Platform med användargränssnittet.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Anslut [!DNL Oracle DB] till Experience Platform med användargränssnittet

Läs den här vägledningen när du vill lära dig hur du ansluter [!DNL Oracle DB]-instansen till Adobe Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Oracle DB]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Oracle DB] översikten](../../../../connectors/databases/oracle.md#prerequisites) om du vill ha information om autentisering.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Oracle DB] går du till kategorin *[!UICONTROL Databases]*, markerar **[!UICONTROL Oracle DB]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor visar **[!UICONTROL Set up]** för nya anslutningar och **[!UICONTROL Add data]** om ett konto redan finns.

![Källkatalogen med &quot;Oracle DB&quot; har valts.](../../../../images/tutorials/create/oracle/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Oracle DB]-konto som du vill använda.

![Det befintliga kontogränssnittet i källarbetsflödet med &quot;Befintligt konto&quot; valt.](../../../../images/tutorials/create/oracle/existing.png)

## Skapa ett nytt konto {#new}

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och kan lägga till en beskrivning för ditt konto.

### Anslut till Experience Platform på Azure {#azure}

Du kan ansluta din [!DNL Oracle DB]-databas till Experience Platform på Azure med en anslutningssträng.

Om du vill använda autentisering av anslutningssträngar anger du din [anslutningssträng](../../../../connectors/databases/oracle.md#azure) och väljer **[!UICONTROL Connect to source]**.

![Det nya kontogränssnittet i källarbetsflödet med autentiseringen av anslutningssträngar markerat.](../../../../images/tutorials/create/oracle/azure.png)

### Ansluta till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Om du vill skapa ett nytt [!DNL Oracle DB]-konto och ansluta till Experience Platform på AWS kontrollerar du att du befinner dig i en VA6-sandlåda och anger sedan de [autentiseringsuppgifter som krävs för autentisering](../../../../connectors/databases/oracle.md#aws).

![Det nya kontogränssnittet i källarbetsflödet som ska anslutas till AWS.](../../../../images/tutorials/create/oracle/aws.png)

## Skapa ett dataflöde för [!DNL Oracle DB] data

Nu när du har anslutit din [!DNL Oracle DB]-databas kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../dataflow/databases.md).
