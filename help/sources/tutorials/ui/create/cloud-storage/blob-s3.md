---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Blob- eller Amazon S3-källanslutning i gränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# Skapa en [!DNL Azure Blob] - eller [!DNL Amazon] S3-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Blob] (nedan kallad &quot;Blob&quot;) eller en S3- [!DNL Amazon] (nedan kallad S3) källkoppling med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en blob- eller S3-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

[!DNL Experience Platform] har stöd för följande filformat som ska importeras från externa lagringsplatser:

- Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
- JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
- Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt blobblagringsutrymme [!DNL Platform]måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som krävs för att komma åt data i blobblagringen. Blobanslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Mer information om hur du kommer igång finns i [det här Azure Blob-dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

Du måste på samma sätt ange giltiga värden för följande autentiseringsuppgifter för att få åtkomst till din S3-bucket på [!DNL Platform] :

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `s3AccessKey` | Åtkomstnyckel-ID för din S3-lagring. |
| `s3SecretKey` | Det hemliga nyckel-ID:t för din S3-lagring. |

Mer information om hur du kommer igång finns i [det här AWS-dokumentet](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/).

## Anslut ditt Blob- eller S3-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt Blob- eller S3-konto att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för, och varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Azure Blob Storage]** eller **[!UICONTROL Amazon S3]** klickar **på +-ikonen (+)** för att skapa en ny [!DNL Blob] - eller S3-koppling.

![katalog](../../../../images/tutorials/create/blob/catalog.png)

Sidan visas *[!UICONTROL Connect to Azure Blob Storage]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina autentiseringsuppgifter för [!DNL Blob] eller S3. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/blob/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Blob] eller S3-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/blob/existing.png)

## Nästa steg och ytterligare resurser

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Blob] eller ditt S3-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till Platform](../../dataflow/batch/cloud-storage.md).