---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Blob- eller Amazon S3-källanslutning i gränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---


# Skapa en Azure Blob- eller Amazon S3-källanslutning i gränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Azure Blob- (nedan kallad &quot;Blob&quot;) eller Amazon S3-källanslutning (nedan kallad &quot;S3&quot;) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en blob- eller S3-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

Experience Platform har stöd för följande filformat som kan importeras från externa lagringsplatser:

- Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
- JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
- Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt blobblagringsutrymme på plattformen måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som krävs för att komma åt data i blobblagringen. Blobanslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Mer information om hur du kommer igång finns i [det här Azure Blob-dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

Du måste på samma sätt ange giltiga värden för följande autentiseringsuppgifter för att få åtkomst till din S3-bucket på Platform:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `s3AccessKey` | Åtkomstnyckel-ID för din S3-lagring. |
| `s3SecretKey` | Det hemliga nyckel-ID:t för din S3-lagring. |

Mer information om hur du kommer igång finns i [det här AWS-dokumentet](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/).

## Anslut ditt Blob- eller S3-konto

När autentiseringsuppgifterna för molnlagringen är klara kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar ditt blob- eller S3-konto till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under kategorin *Cloud Storage* väljer du antingen **Azure Blob Storage** eller **Amazon S3** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att visa dess dokumentation eller ansluta till källan. Om du vill skapa en ny inkommande basanslutning klickar du på **Anslut källa**.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

I indataformuläret anger du basanslutningen med ett namn, en valfri beskrivning och autentiseringsuppgifterna för blob eller S3. Klicka slutligen på **Anslut** och tillåt lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt Azure Blob- eller Amazon S3-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/batch/cloud-storage.md).