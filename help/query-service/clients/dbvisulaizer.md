---
keywords: Experience Platform;home;populära topics;query service;Query service;Db Visualizer;DbVisualizer;db visulaizer;connect to query service;
solution: Experience Platform
title: Koppla DbVisualizer till frågetjänsten
description: Det här dokumentet går igenom stegen för att ansluta DbVisualizer till Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 106a2e4606e94f71d6359cf947e05f193c19c660
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Anslut [!DNL DbVisualizer] till [!DNL Query Service] {#connect-dbvisualizer}

Det här dokumentet innehåller stegen för att ansluta [!DNL DbVisualizer] databasverktyg med Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har tillgång till [!DNL DbVisualizer] och känner till hur man navigerar i gränssnittet. Ladda ned [!DNL DbVisualizer] eller för mer information, se [officiell [!DNL DbVisualizer] dokumentation](https://www.dbvis.com/download/).

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL  DbVisualizer] för Experience Platform måste du ha tillgång till arbetsytan Frågor i användargränssnittet för plattformen. Kontakta IMS-organisationens administratör om du inte har tillgång till arbetsytan Frågor.

## Skapa en databasanslutning {#connect-database}

När du har installerat datorprogrammet på din lokala dator följer du BDVisualizer-instruktionerna för att [skapa en ny databasanslutning](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

När du har valt **[!DNL PostgreSQL]** från [!DNL Connections] lista, en [!DNL Object View] för den nya [!DNL PostgreSQL] anslutningen visas.

### Ange drivrutinsegenskaper för anslutningen {#properties}

Från [!DNL PostgreSQL] objektvy väljer du **[!DNL Properties]** följt av **[!DNL Driver Properties]** från navigeringssidlisten. Mer information om [drivrutinsegenskaper](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) finns i den officiella dokumentationen.

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

>[!NOTE]
>
>Lägga till en sekund `user` profil, välja `user` i parameterkolumnen väljer du den blå + (plus)-ikonen för att lägga till inloggningsuppgifter för varje användare. Välj **[!DNL Apply]** för att lägga till drivrutinsegenskapen.

The [!DNL Edited] kolumnen visar en bockmarkering som anger att parametervärdet har uppdaterats.

### Autentiseringsuppgifter för Input Query Service {#query-service-credentials}

Om du vill hitta de autentiseringsuppgifter som krävs för att ansluta BBVisualizer till frågetjänsten loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar **värd**, **port**, **databas**, **användarnamn** och **lösenord** autentiseringsuppgifter, läs [inloggningsguide](../ui/credentials.md).

![Sidan Autentiseringsuppgifter på arbetsytan Experience Platform Frågor med Autentiseringsuppgifter och Utgångsuppgifter markerade.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] erbjuder även icke-utgångsdatum för att möjliggöra en engångskonfiguration med tredjepartsklienter. Läs dokumentationen för [fullständiga anvisningar om hur du genererar och använder ej utgångsdatum](../ui/credentials.md#non-expiring-credentials). Du måste slutföra den här processen om du vill ansluta BDVisualizer som en engångsinstallation. The `credential` och `technicalAccountId` förvärvade värden utgör värdet för DBVisualizer `password` parameter.

## Autentisering {#authentication}

Om du vill kräva ett användar-ID och lösenordsbaserad autentisering varje gång en anslutning upprättas går du till [!DNL Properties] och markera **[!DNL Authentication]** från navigeringssidlisten under [!DNL PostgreSQL].

På panelen Anslutningsautentisering kontrollerar du båda **[!DNL Require Userid]** och **[!DNL Require Password]** kryssrutor markera **[!DNL Apply]**. Mer information om [ange autentiseringsalternativ](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) finns i den officiella dokumentationen.

## Anslut till plattform

Du kan upprätta en anslutning med hjälp av autentiseringsuppgifter som förfaller eller inte förfaller. Om du vill skapa en anslutning väljer du **[!DNL Connection]** från [!DNL PostgreSQL] objektvy och ange dina inloggningsuppgifter för Experience Platform för följande inställningar. Kompletterande anvisningar till [konfigurera en manuell anslutning](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) finns på DBVisualizers officiella webbplats.

>[!NOTE]
>
>Alla inloggningsuppgifter som krävs av BDVisualizer i tabellen nedan är desamma för utgångsdatum och ej utgångsdatum om inte annat anges i parameterbeskrivningen.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!UICONTROL Name]** | Skapa ett namn för anslutningen. Du bör ange ett användarvänligt namn för att känna igen anslutningen. |
| **[!UICONTROL Database Server]** | Det här är din Experience Platform **[!UICONTROL Host]** autentiseringsuppgifter. |
| **[!UICONTROL Database Port]** | Porten för [!DNL Query Service]. Du måste använda port **80** eller **5432** att ansluta till [!DNL Query Service]. |
| **[!UICONTROL Database]** | Använd Experience Platform **[!UICONTROL Database]** autentiseringsvärde: `prod:all`. |
| **[!UICONTROL Database Userid]** | Detta är ditt organisations-ID för plattformen. Använd Experience Platform **[!UICONTROL Username]** autentiseringsvärde. ID:t kommer att ha formatet `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Database Password]** | Den här alfanumeriska strängen är din Experience Platform **[!UICONTROL Password]** autentiseringsuppgifter. Om du vill använda icke-förfallande autentiseringsuppgifter är det här värdet det sammanfogade argumentet från `technicalAccountID` och `credential` hämtas i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. Konfigurations-JSON-filen för icke-förfallande autentiseringsuppgifter är en engångshämtning under initieringen som Adobe inte har någon kopia av. |

När du har angett alla relevanta autentiseringsuppgifter väljer du **[!DNL Connect]**.

The [!DNL Connect] visas vid det första tillfället av sessionen. Ange ditt serienummer och lösenord och välj **[!DNL Connect]**. Ett meddelande visas i loggen som bekräftar att anslutningen lyckades.

## Nästa steg

Nu när du är ansluten [!DNL DbVisualizer] med [!DNL Query Service]kan du använda [!DNL DbVisualizer] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guide för frågekörning](../best-practices/writing-queries.md).
