---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en FTP- eller SFTP-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Skapa en FTP- eller SFTP-källanslutning i användargränssnittet

>[!NOTE]
>FTP- och SFTP-anslutningarna är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en FTP- eller SFTP-källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig FTP- eller SFTP-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

Experience Platform har stöd för följande filformat som kan importeras från externa källor:

* Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaseparerade värden (CSV). Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmän DSV ska ges i framtiden.
* JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till FTP- eller SFTP-servern på plattformen måste du ange serverns **värdnamn**, ett **användarnamn** och ett **lösenord**.

## Anslut till servern

När serverns autentiseringsuppgifter är klara kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar FTP- eller SFTP-servern till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Välj antingen *FTP* eller **SFTP** under kategorin **Cloud-lagring** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att visa dess dokumentation eller ansluta till källan. Om du vill skapa en ny inkommande basanslutning klickar du på **Anslut källa**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

I indataformuläret anger du basanslutningen med ett namn, en valfri beskrivning och autentiseringsuppgifter för FTP eller SFTP. Klicka slutligen på **Anslut** och tillåt lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

När en basanslutning till FTP- eller SFTP-servern har upprättats kan du fortsätta till nästa avsnitt och konfigurera ett dataflöde för att hämta data till plattformen.

## Nästa steg

I den här självstudiekursen har du upprättat en anslutning till FTP- eller SFTP-servern. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/batch/cloud-storage.md).
