---
keywords: Experience Platform;home;populära topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Anslut Aqua Data Studio till Query Service
description: Det här dokumentet går igenom stegen för att ansluta Aqua Data Studio med Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Anslut [!DNL Aqua Data Studio] till frågetjänst

Det här dokumentet innehåller stegen för anslutning [!DNL Aqua Data Studio] med Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har åtkomst till [!DNL Aqua Data Studio] och känna till hur man navigerar i gränssnittet. Mer information om [!DNL Aqua Data Studio] finns i [officiell [!DNL Aqua Data Studio] dokumentation](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Det finns [!DNL Windows] och [!DNL macOS] versioner av [!DNL Aqua Data Studio]. Skärmbilder i den här guiden har tagits med [!DNL macOS] datorprogram. Det kan finnas små skillnader i användargränssnittet mellan versionerna.

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL Aqua Data Studio] till Experience Platform måste du ha tillgång till [!UICONTROL Queries] i plattformsgränssnittet. Kontakta IMS-organisationens administratör om du inte har tillgång till [!UICONTROL Queries] arbetsyta.

## Registrera servern {#register-server}

Efter installation [!DNL Aqua Data Studio]måste du först registrera servern. Välj **[!DNL Server]**, följt av **[!DNL Register Server]**.

![Listrutan Server med Register Server markerad.](../images/clients/aqua-data-studio/register-server.png)

The **[!DNL Register Server]** visas. Under **[!DNL General]** flik, välja **[!DNL PostgreSQL]** från listan till vänster. Ange följande information för serverinställningarna i dialogrutan som visas.

- **[!DNL Name]**: Namnet på anslutningen. Du bör ange ett eget namn för att känna igen anslutningen.
- **[!DNL Login Name]**: Inloggningsnamnet är ditt organisations-ID. Det tar formen av `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Det här är en alfanumerisk sträng som finns på [!DNL Query Service] Instrumentpanel för autentiseringsuppgifter.
- **[!DNL Host and Port]**: Värdslutpunkten och dess port för [!DNL Query Service]. Du måste använda port 80 för att ansluta till [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas. Använd värdet för plattformsgränssnittets autentiseringsuppgifter `dbname`: `prod:all`.

![The [!DNL Aqua Data Studio] Fliken Allmänt med obligatoriska inmatningsfält markerade.](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] autentiseringsuppgifter

Logga in på [!DNL Platform] Användargränssnitt och markera **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Fullständiga anvisningar om hur du hittar inloggningsuppgifter, värd, port och databasnamn finns i [inloggningsguide](../ui/credentials.md).

[!DNL Query Service] erbjuder även icke-utgångsdatum för att möjliggöra en engångskonfiguration med tredjepartsklienter. Läs dokumentationen för [fullständiga anvisningar om hur du genererar och använder ej utgångsdatum](../ui/credentials.md#non-expiring-credentials).

### Ställa in SSL-läge

Välj sedan **[!DNL Driver]** -fliken. Under **[!DNL Parameters]**, ange värdet som `?sslmode=require`

>[!IMPORTANT]
>
>Se [[!DNL Query Service] SSL-dokumentation](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med `verify-full` SSL-läge.

![The [!DNL Aqua Data Studio] Fliken Drivrutin med fältet Parametrar markerat.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

När du har angett anslutningsinformationen väljer du **[!DNL Test Connection]** för att säkerställa att dina uppgifter fungerar som de ska. Om ditt anslutningstest lyckas väljer du **[!DNL Save]** för att registrera servern. En bekräftelsedialogruta visas som bekräftar anslutningen och anslutningen visas på instrumentpanelen. Nu kan du ansluta till servern och visa dess schemaobjekt.

## Nästa steg

Nu när du har anslutit till [!DNL Query Service]kan du använda **[!DNL Query Analyzer]** inom [!DNL Aqua Data Studio] för att köra och redigera SQL-satser. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
