---
keywords: Experience Platform;hem;populära ämnen;Azure Blob;azure blob;Azure blob connector
solution: Experience Platform
title: Skapa en Azure Blob Source-anslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Blob-källanslutning med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---


# Skapa en [!DNL Azure Blob]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Blob] (kallas nedan [!DNL Blob]) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Blob]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

[!DNL Experience Platform] har stöd för följande filformat som ska importeras från externa lagringsplatser:

- Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
- JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
- Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Blob]-lagringsutrymme på plattformen måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En sträng som innehåller den auktoriseringsinformation som krävs för att autentisera [!DNL Blob] till Experience Platform. Anslutningssträngsmönstret [!DNL Blob] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i det här [!DNL Blob]-dokumentet om [konfigurering av anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt [!DNL Blob]-konto. SAS-URI-mönstret [!DNL Blob] är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i det här [!DNL Blob]-dokumentet på [URI:er för delad åtkomst](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Anslut ditt [!DNL Blob]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Blob]-konto till Platform.

I [Plattformsgränssnittet](https://platform.adobe.com) väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Azure Blob Storage]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/blob/catalog.png)

Sidan **[!UICONTROL Connect to Azure Blob Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Blob]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/blob/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en alternativbeskrivning för ditt nya [!DNL Blob]-konto.

**Autentisera med en anslutningssträng**

[!DNL Blob]-anslutningen ger dig olika autentiseringstyper för åtkomst. Under [!UICONTROL Account authentication] väljer du **[!UICONTROL ConnectionString]** om du vill använda anslutningssträngsbaserade autentiseringsuppgifter.

![anslutningssträng](../../../../images/tutorials/create/blob/connectionstring.png)

**Autentisera med en URI för delad åtkomst**

En SAS-URI (Shared Access Signature) möjliggör säker delegerad auktorisering till ditt [!DNL Blob]-konto. Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Välj **[!UICONTROL SasURIAuthentication]** och ange sedan din [!DNL Blob] SAS-URI. Välj **[!UICONTROL Connect to source]** för att fortsätta.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Blob]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
