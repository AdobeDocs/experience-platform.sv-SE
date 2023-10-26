---
title: Skapa en Azure Blob Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en Azure Blob-källanslutning med hjälp av användargränssnittet för plattformen.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# Skapa en [!DNL Azure Blob] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Azure Blob] (nedan kallad[!DNL Blob]&quot;) källanslutning med användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket för att organisera kundupplevelsedata i Experience Platform.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Blob] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

Experience Platform stöder följande filformat som kan importeras från externa lagringsplatser:

* Avgränsaravgränsade värden (DSV): Du kan använda valfri enskild kolumnavgränsare, t.ex. tabb, komma, pipe, semikolon eller hash, för att samla in platta filer i vilket format som helst.
* JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Blob] lagringsutrymme i Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

>[!BEGINTABS]

>[!TAB Autentisering av anslutningssträng]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Anslutningssträng | En sträng som innehåller den auktoriseringsinformation som krävs för autentisering [!DNL Blob] till Experience Platform. The [!DNL Blob] anslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i [!DNL Blob] dokument på [konfigurera anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB SAS-URI-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-URI | Den URI för signatur för delad åtkomst som du kan använda som alternativ autentiseringstyp för att ansluta [!DNL Blob] konto. The [!DNL Blob] SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i [!DNL Blob] dokument på [URI:er för delad åtkomstsignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Behållare | Namnet på den behållare som du vill tilldela åtkomst till. När du skapar ett nytt konto med [!DNL Blob] kan du ange ett behållarnamn för att ange användaråtkomst till den undermapp du väljer. |
| Mappsökväg | Sökvägen till mappen som du vill ge åtkomst till. |

>[!ENDTABS]

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att ansluta [!DNL Blob] lagring i Experience Platform

## Koppla samman [!DNL Blob] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Azure Blob Storage]** och sedan markera **[!UICONTROL Add data]**.

![Experience Platform-källkatalogen med Azure Blob Storage-källan vald.](../../../../images/tutorials/create/blob/catalog.png)

The **[!UICONTROL Connect to Azure Blob Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Blob] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/blob/existing.png)

### Nytt konto

>[!TIP]
>
>När du har skapat en fil kan du inte ändra autentiseringstypen för en [!DNL Blob] basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL Blob] konto.

![Den nya kontoskärmen för Azure Blob Storage-källan.](../../../../images/tutorials/create/blob/new.png)

The [!DNL Blob] Källan stöder både autentisering av kontonycklar och autentisering med delad åtkomstsignatur (SAS). En kontonyckelbaserad autentisering kräver en anslutningssträng för verifiering, medan en SAS-autentisering använder en URI som tillåter säker delegerad autentisering av ditt konto.

Under det här steget kan du även ange vilka undermappar ditt konto ska ha åtkomst till genom att definiera namnet på behållaren och sökvägen till undermappen.

>[!BEGINTABS]

>[!TAB Anslutningssträng]

Om du vill autentisera med en kontonyckel väljer du **[!UICONTROL Account key authentication]** och ange anslutningssträngen. Under det här steget kan du även ange behållarnamnet och sökvägen till den undermapp som du vill ha åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![anslutningssträng](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS-URI]

Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Om du vill autentisera med en signatur för delad åtkomst väljer du **[!UICONTROL Shared access signature authentication]** och ange sedan din SAS-URI. Under det här steget kan du även ange behållarnamnet och sökvägen till den undermapp som du vill ha åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Blob] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
