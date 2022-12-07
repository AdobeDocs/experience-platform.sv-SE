---
keywords: Experience Platform;home;populära topics;query service;Query service;Db Visualizer;DbVisualizer;db visulaizer;connect to query service;
solution: Experience Platform
title: Koppla DbVisualizer till frågetjänsten
topic-legacy: connect
description: Det här dokumentet går igenom stegen för att ansluta DbVisualizer till Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 7d38488c204e28c9cfd8ea50c06f1ce781d76c59
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Anslut [!DNL DbVisualizer] till [!DNL Query Service] {#connect-dbvisualizer}

Det här dokumentet innehåller stegen för att ansluta [!DNL DbVisualizer] databasverktyg med Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har tillgång till [!DNL DbVisualizer] och känner till hur man navigerar i gränssnittet. Ladda ned [!DNL DbVisualizer] eller för mer information, se [officiell [!DNL DbVisualizer] dokumentation](https://www.dbvis.com/download/).

>[!NOTE]
>
>Det finns [!DNL Windows], [!DNL macOS]och [!DNL Linux] versioner av [!DNL DbVisualizer]. Skärmbilder i den här guiden har tagits med [!DNL macOS] datorprogram. Det kan finnas små skillnader i användargränssnittet mellan versionerna.

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL  DbVisualizer] för Experience Platform måste du ha tillgång till arbetsytan Frågor i användargränssnittet för plattformen. Kontakta IMS-organisationens administratör om du inte har tillgång till arbetsytan Frågor.

## Skapa en databasanslutning {#connect-database}

När du har installerat datorprogrammet på din lokala dator startar du programmet och väljer **[!DNL Create a Database Connection]** från början [!DNL DbVisualizer] -menyn. Välj sedan **[!DNL Create a Connection]** i panelen till höger.

![The [!DNL DbVisualizer] huvudmenyn med &quot;Skapa en databasanslutning&quot; markerad.](../images/clients/dbvisualizer/create-db-connection.png)

Använd sökfältet eller markera [!DNL PostgreSQL] i listrutan med drivrutinsnamn. Arbetsytan Databasanslutning visas.

![Drivrutinens namn-listruta med [!DNL PostgreSQL] markerad.](../images/clients/dbvisualizer/driver-name.png)

### Ange egenskaper för anslutningen {#properties}

På arbetsytan för databasanslutning väljer du **[!DNL Properties]** följt av **[!DNL Driver Properties]** från navigeringssidlisten.

![Arbetsytan Databasanslutning med Egenskaper och Drivrutinsegenskaper markerade.](../images/clients/dbvisualizer/driver-properties.png)

Ange sedan drivrutinsegenskaperna som beskrivs i tabellen nedan.

>[!IMPORTANT]
>
>Om du vill ansluta DBVisualizer till Adobe Experience Platform måste du aktivera SSL. Se [Dokumentation för SSL-lägen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med `verify-full` SSL-läge.

| Egenskap | Beskrivning |
| ------ | ------ |
| `PGHOST` | Värdnamnet för [!DNL PostgreSQL] server. Det här värdet är din Experience Platform **[!UICONTROL Host]autentiseringsuppgifter**. |
| `ssl` | Definiera SSL-värdet `1` för att möjliggöra användning av SSL. |
| `sslmode` | Detta styr nivån på SSL-skyddet. Du rekommenderas att använda `require` SSL-läge vid anslutning av tredjepartsklienter till Adobe Experience Platform. The `require` läge garanterar att kryptering krävs för all kommunikation och att nätverket är betrott för att ansluta till rätt server. Server SSL-certifikatvalidering krävs inte. |
| `user` | Användarnamnet som är kopplat till databasen är ditt företags-ID. Det är en alfanumerisk sträng som slutar i `@Adobe.Org`. Det här värdet är din Experience Platform **[!UICONTROL Username]autentiseringsuppgifter**. |

Använd sökfältet för att hitta varje egenskap och markera sedan motsvarande cell för parameterns värde. Cellen markeras med blått. Ange dina autentiseringsuppgifter för plattformen i värdefältet och välj **[!DNL Apply]** för att lägga till drivrutinsegenskapen.

![Fliken Drivrutinsegenskaper för DBVisulator med ett värde angivet och Använd markerat.](../images/clients/dbvisualizer/apply-parameter-value.png)

>[!NOTE]
>
>Lägga till en sekund `user` profil, välja `user` i parameterkolumnen väljer du den blå + (plus)-ikonen för att lägga till inloggningsuppgifter för varje användare. Välj **[!DNL Apply]** för att lägga till drivrutinsegenskapen.

The [!DNL Edited] kolumnen visar en bockmarkering som anger att parametervärdet har uppdaterats.

### Indata[!DNL Query Service] autentiseringsuppgifter

Om du vill hitta de autentiseringsuppgifter som krävs för att ansluta BBVisualizer till frågetjänsten loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar **värd**, **port**, **databas**, **användarnamn** och **lösenord** autentiseringsuppgifter, läs [inloggningsguide](../ui/credentials.md).

![Sidan Autentiseringsuppgifter på arbetsytan Experience Platform Frågor med Autentiseringsuppgifter och Utgångsuppgifter markerade.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] erbjuder även icke-utgångsdatum för att möjliggöra en engångskonfiguration med tredjepartsklienter. Läs dokumentationen för [fullständiga anvisningar om hur du genererar och använder ej utgångsdatum](../ui/credentials.md#non-expiring-credentials). Du måste slutföra den här processen om du vill ansluta BDVisualizer som en engångsinstallation. The `credential` och `technicalAccountId` förvärvade värden utgör värdet för DBVisualizer `password` parameter.

## Autentisering

Om du vill kräva ett användar-ID och lösenordsbaserad autentisering varje gång en anslutning upprättas väljer du **[!DNL Authentication]** från navigeringssidlisten under [!DNL PostgreSQL].

På panelen Anslutningsautentisering kontrollerar du båda **[!DNL Require Userid]** och **[!DNL Require Password]** kryssrutor markera **[!DNL Apply]**.

![Autentiseringspanelen för [!DNL PostgreSQL] Databasanslutning med kryssrutorna Kräv seriell och Lösenord markerade.](../images/clients/dbvisualizer/connection-authentication.png)

## Anslut till plattform

Du kan upprätta en anslutning med hjälp av autentiseringsuppgifter som förfaller eller inte förfaller. Om du vill skapa en anslutning väljer du **[!DNL Connection]** på arbetsytan Databasanslutning och ange dina inloggningsuppgifter för Experience Platform för följande inställningar.

>[!NOTE]
>
>Alla inloggningsuppgifter som krävs av BDVisualizer i tabellen nedan är desamma för utgångsdatum och ej utgångsdatum om inte annat anges i parameterbeskrivningen.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!UICONTROL Name]** | Skapa ett namn för anslutningen. Du bör ange ett användarvänligt namn för att känna igen anslutningen. |
| **[!UICONTROL Database Server]** | Det här är din Experience Platform **[!UICONTROL Host]** autentiseringsuppgifter. |
| **[!UICONTROL Database Port]** | Porten för [!DNL Query Service]. Du måste använda port **80** att ansluta till [!DNL Query Service]. |
| **[!UICONTROL Database]** | Använd Experience Platform **[!UICONTROL Database]** autentiseringsvärde: `prod:all`. |
| **[!UICONTROL Database Userid]** | Detta är ditt organisations-ID för plattformen. Använd Experience Platform **[!UICONTROL Username]** autentiseringsvärde. ID:t kommer att ha formatet `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Database Password]** | Den här alfanumeriska strängen är din Experience Platform **[!UICONTROL Password]** credential.Om du vill använda icke-förfallande autentiseringsuppgifter är det här värdet det sammanfogade argumentet från `technicalAccountID` och `credential` hämtas i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. Konfigurations-JSON-filen för icke-förfallande autentiseringsuppgifter är en engångshämtning under initieringen som Adobe inte har någon kopia av. |

När du har angett alla relevanta autentiseringsuppgifter väljer du **[!DNL Connect]**.

![The [!DNL PostgreSQL] Arbetsytan Databasanslutning med fliken Anslutning och anslutningsknappen markerad.](../images/clients/dbvisualizer/connect.png)

The [!DNL Connect] visas vid det första tillfället av sessionen.

![Connect: [!DNL PostgreSQL] med textfälten Databas-ID och Databaslösenord markerade.](../images/clients/dbvisualizer/connect-dialog.png)

Ange ditt serienummer och lösenord och välj **[!DNL Connect]**. Ett meddelande visas i loggen som bekräftar att anslutningen lyckades.

## Nästa steg

Nu när du är ansluten [!DNL DbVisualizer] med [!DNL Query Service]kan du använda [!DNL DbVisualizer] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guide för frågekörning](../best-practices/writing-queries.md).
