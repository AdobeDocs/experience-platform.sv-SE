---
keywords: Experience Platform;home;populära topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anslut Aqua Data Studio till Query Service
description: Det här dokumentet går igenom stegen för att ansluta Aqua Data Studio med Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Anslut [!DNL Aqua Data Studio] till frågetjänsten

Det här dokumentet innehåller stegen för att ansluta [!DNL Aqua Data Studio] till Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har tillgång till [!DNL Aqua Data Studio] och känner till hur du navigerar i gränssnittet. Mer information om [!DNL Aqua Data Studio] finns i [officiell [!DNL Aqua Data Studio] dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Det finns [!DNL Windows] och [!DNL macOS] versioner av [!DNL Aqua Data Studio]. Skärmbilder i den här guiden har tagits med skrivbordsappen [!DNL macOS]. Det kan finnas små skillnader i användargränssnittet mellan versionerna.

Om du vill få de nödvändiga autentiseringsuppgifterna för att ansluta [!DNL Aqua Data Studio] till Experience Platform måste du ha tillgång till arbetsytan [!UICONTROL Queries] i Experience Platform-gränssnittet. Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan [!UICONTROL Queries].

## Registrera servern {#register-server}

När du har installerat [!DNL Aqua Data Studio] måste du först registrera servern. I den officiella dokumentationen för Aqua Data Studio finns anvisningar om hur du [startar  [!DNL Register Server] dialogrutan](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) och [registrerar servern](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

När dialogrutan **[!DNL Register Server]** visas för en PostgresSQL-server anger du följande information för serverinställningarna.

- **[!DNL Name]**: Namnet på anslutningen. Du bör ange ett eget namn för att känna igen anslutningen.
- **[!DNL Login Name]**: Inloggningsnamnet är ditt företags-ID för Experience Platform. Det har formen `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Det här är en alfanumerisk sträng som finns på instrumentpanelen för autentiseringsuppgifter i [!DNL Query Service].
- **[!DNL Host and Port]**: Värdslutpunkten och dess port för [!DNL Query Service]. Du måste använda port 80 för att ansluta till [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas. Använd värdet för Experience Platform-användargränssnittets autentiseringsuppgifter `dbname`: `prod:all`.

### [!DNL Query Service] autentiseringsuppgifter

Om du vill hitta dina autentiseringsuppgifter loggar du in på [!DNL Experience Platform]-gränssnittet och väljer **[!UICONTROL Queries]** i den vänstra navigeringen, följt av **[!UICONTROL Credentials]**. Fullständiga anvisningar om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns i handboken [för inloggningsuppgifter](../ui/credentials.md).

[!DNL Query Service] erbjuder även autentiseringsuppgifter som inte upphör att gälla så att det går att konfigurera en gång med tredjepartsklienter. I dokumentationen finns [fullständiga instruktioner om hur du genererar och använder inloggningsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials).

### Ange SSL-läge

Sedan måste du ange SSL-lägesvärdet som `?sslmode=require`. Detta görs på fliken [!DNL Driver] i dialogrutan [!DNL Edit Server Properties]. I den officiella dokumentationen för Aqua Data Studio finns instruktioner om hur du [redigerar drivrutinsegenskaper](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) och [konfigurerar SSL för  [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Använd sökfältet för att hitta egenskapen `sslmode`.

>[!IMPORTANT]
>
>Läs [[!DNL Query Service] SSL-dokumentationen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter i SSL-läge `verify-full`.

När du har angett anslutningsinformationen väljer du **[!DNL Test Connection]** på samma flik för att se till att autentiseringsuppgifterna fungerar som de ska. Om ditt anslutningstest lyckas väljer du **[!DNL Save]** för att registrera servern. En bekräftelsedialogruta visas som bekräftar anslutningen och anslutningsikonen visas på kontrollpanelen. Nu kan du ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till [!DNL Query Service] kan du använda **[!DNL Query Analyzer]** i [!DNL Aqua Data Studio] för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [guiden ](../best-practices/writing-queries.md) som kör frågor.
