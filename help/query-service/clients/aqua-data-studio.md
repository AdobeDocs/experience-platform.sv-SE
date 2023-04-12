---
keywords: Experience Platform;home;populära topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anslut Aqua Data Studio till Query Service
description: Det här dokumentet går igenom stegen för att ansluta Aqua Data Studio med Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Anslut [!DNL Aqua Data Studio] till frågetjänst

Det här dokumentet innehåller stegen för anslutning [!DNL Aqua Data Studio] med Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har åtkomst till [!DNL Aqua Data Studio] och känna till hur man navigerar i gränssnittet. Mer information om [!DNL Aqua Data Studio] finns i [officiell [!DNL Aqua Data Studio] dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Det finns [!DNL Windows] och [!DNL macOS] versioner av [!DNL Aqua Data Studio]. Skärmbilder i den här guiden har tagits med [!DNL macOS] datorprogram. Det kan finnas små skillnader i användargränssnittet mellan versionerna.

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL Aqua Data Studio] till Experience Platform måste du ha tillgång till [!UICONTROL Queries] i plattformsgränssnittet. Kontakta din organisations administratör om du inte har tillgång till [!UICONTROL Queries] arbetsyta.

## Registrera servern {#register-server}

Efter installation [!DNL Aqua Data Studio]måste du först registrera servern. I den officiella dokumentationen för Aqua Data Studio finns instruktioner om hur man gör [starta [!DNL Register Server] dialog](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) och [registrera servern](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

När **[!DNL Register Server]** visas för en PostgresSQL-server. Ange följande information för serverinställningarna.

- **[!DNL Name]**: Namnet på anslutningen. Du bör ange ett eget namn för att känna igen anslutningen.
- **[!DNL Login Name]**: Inloggningsnamnet är ditt organisations-ID. Det tar formen av `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Det här är en alfanumerisk sträng som finns på [!DNL Query Service] Instrumentpanel för autentiseringsuppgifter.
- **[!DNL Host and Port]**: Värdslutpunkten och dess port för [!DNL Query Service]. Du måste använda port 80 för att ansluta till [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas. Använd värdet för plattformsgränssnittets autentiseringsuppgifter `dbname`: `prod:all`.

### [!DNL Query Service] autentiseringsuppgifter

Logga in på [!DNL Platform] Användargränssnitt och markera **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Fullständiga anvisningar om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns i [inloggningsguide](../ui/credentials.md).

[!DNL Query Service] erbjuder även icke-utgångsdatum för att möjliggöra en engångskonfiguration med tredjepartsklienter. Läs dokumentationen för [fullständiga anvisningar om hur du genererar och använder ej utgångsdatum](../ui/credentials.md#non-expiring-credentials).

### Ställa in SSL-läge

Därefter måste du ange SSL-lägesvärdet som `?sslmode=require`. Detta görs från [!DNL Driver] -fliken i [!DNL Edit Server Properties] -dialogrutan. I den officiella dokumentationen för Aqua Data Studio finns instruktioner om hur man gör [redigera drivrutinsegenskaper](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) och [konfigurera SSL för [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Använd sökfältet för att hitta `sslmode` -egenskap.

>[!IMPORTANT]
>
>Se [[!DNL Query Service] SSL-dokumentation](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med `verify-full` SSL-läge.

När du har angett anslutningsinformationen väljer du **[!DNL Test Connection]** för att säkerställa att dina uppgifter fungerar som de ska. Om ditt anslutningstest lyckas väljer du **[!DNL Save]** för att registrera servern. En bekräftelsedialogruta visas som bekräftar anslutningen och anslutningsikonen visas på kontrollpanelen. Nu kan du ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till [!DNL Query Service]kan du använda **[!DNL Query Analyzer]** inom [!DNL Aqua Data Studio] för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
