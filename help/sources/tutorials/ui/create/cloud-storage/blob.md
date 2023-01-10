---
keywords: Experience Platform;hem;populära ämnen;Azure Blob;azure blob;Azure blob connector
solution: Experience Platform
title: Skapa en Azure Blob Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Azure Blob-källanslutning med hjälp av användargränssnittet för plattformen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Skapa en [!DNL Azure Blob] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Azure Blob] (nedan kallad[!DNL Blob]&quot;) med användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Blob] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

[!DNL Experience Platform] har stöd för följande filformat som ska importeras från externa lagringsplatser:

- Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
- JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
- Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Blob] på Platform måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En sträng som innehåller den auktoriseringsinformation som krävs för att autentisera [!DNL Blob] till Experience Platform. The [!DNL Blob] anslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i [!DNL Blob] dokument på [konfigurera anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som alternativ autentiseringstyp för att ansluta [!DNL Blob] konto. The [!DNL Blob] SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i [!DNL Blob] dokument på [URI:er för delad åtkomstsignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Koppla samman [!DNL Blob] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Blob] konto till plattform.

I [Plattformsgränssnitt](https://platform.adobe.com), markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Azure Blob Storage]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/blob/catalog.png)

The **[!UICONTROL Connect to Azure Blob Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL Blob] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/blob/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en alternativbeskrivning för ditt nya [!DNL Blob] konto.

**Autentisera med en anslutningssträng**

The [!DNL Blob] med en koppling får du olika typer av autentisering för åtkomst. Under [!UICONTROL Account authentication] välj **[!UICONTROL ConnectionString]** om du vill använda anslutningssträngsbaserade autentiseringsuppgifter.

![anslutningssträng](../../../../images/tutorials/create/blob/connectionstring.png)

**Autentisera med en URI för delad åtkomst**

En SAS-URI (Shared Access Signature) ger säker delegerad behörighet till din [!DNL Blob] konto. Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Välj **[!UICONTROL SasURIAuthentication]** och sedan [!DNL Blob] SAS-URI. Välj **[!UICONTROL Connect to source]** för att fortsätta.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Blob] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
