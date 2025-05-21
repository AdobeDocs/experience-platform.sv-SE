---
title: Anslut MySQL till Experience Platform med användargränssnittet
description: Lär dig hur du ansluter MySQL-databasen till Experience Platform med användargränssnittet.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Anslut [!DNL MySQL] till Experience Platform med användargränssnittet

Läs den här vägledningen när du vill lära dig hur du ansluter din [!DNL MySQL]-databas till Adobe Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL MySQL]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL MySQL] översikten](../../../../connectors/databases/mysql.md#prerequisites) om du vill ha information om autentisering.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL MySQL] går du till kategorin *[!UICONTROL Databases]*, markerar **[!UICONTROL MySQL]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med källkortet MySQL markerat.](../../../../images/tutorials/create/my-sql/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL MySQL]-konto som du vill använda.

![Det befintliga kontogränssnittet i källarbetsflödet med &quot;Befintligt konto&quot; valt.](../../../../images/tutorials/create/my-sql/existing.png)

## Skapa ett nytt konto {#new}

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och kan lägga till en beskrivning för ditt konto.

![Det nya kontogränssnittet i källarbetsflödet med ett kontonamn och en valfri beskrivning har angetts.](../../../../images/tutorials/create/my-sql/new.png)

### Anslut till Experience Platform på Azure {#azure}

Du kan ansluta din [!DNL MySQL]-databas till Experience Platform på Azure med antingen kontonyckel eller grundläggande autentisering.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Om du vill använda kontonyckelautentisering väljer du **[!UICONTROL Account key authentication]**, anger din [anslutningssträng](../../../../connectors/databases/mysql.md#azure) och väljer sedan **[!UICONTROL Connect to source]**.

![Det nya kontogränssnittet i källarbetsflödet med autentiseringen av kontonyckeln markerat.](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB Grundläggande autentisering]

Om du vill använda grundläggande autentisering väljer du **[!UICONTROL Basic authentication]**, anger värden för dina [autentiseringsuppgifter](../../../../connectors/databases/mysql.md#azure) och väljer sedan **[!UICONTROL Connect to source]**.

![Det nya kontogränssnittet i källarbetsflödet med Grundläggande autentisering markerat.](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### Ansluta till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Om du vill skapa ett nytt [!DNL MySQL]-konto och ansluta till Experience Platform på AWS kontrollerar du att du befinner dig i en VA6-sandlåda och anger sedan de [autentiseringsuppgifter som krävs för autentisering](../../../../connectors/databases/mysql.md#aws).

![Det nya kontogränssnittet i källarbetsflödet som ska anslutas till AWS.](../../../../images/tutorials/create/my-sql/aws.png)

## Skapa ett dataflöde för [!DNL MySQL] data

Nu när du har anslutit din [!DNL MySQL]-databas kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../dataflow/databases.md).
