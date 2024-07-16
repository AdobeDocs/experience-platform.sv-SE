---
keywords: Experience Platform;home;populära topics;query service;Query service;Db Visualizer;DbVisualizer;db visulaizer;connect to query service;
solution: Experience Platform
title: Koppla DbVisualizer till frågetjänsten
description: Det här dokumentet går igenom stegen för att ansluta DbVisualizer till Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Anslut [!DNL DbVisualizer] till [!DNL Query Service] {#connect-dbvisualizer}

I det här dokumentet beskrivs stegen för att ansluta databasverktyget [!DNL DbVisualizer] med Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver att du redan har tillgång till skrivbordsappen [!DNL DbVisualizer] och känner till hur du navigerar i gränssnittet. Om du vill hämta datorprogrammet [!DNL DbVisualizer] eller om du vill ha mer information läser du [officiell [!DNL DbVisualizer] dokumentation](https://www.dbvis.com/download/).

Om du vill få de nödvändiga autentiseringsuppgifterna för att ansluta [!DNL  DbVisualizer] till Experience Platform måste du ha tillgång till arbetsytan Frågor i plattformsgränssnittet. Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan Frågor.

## Skapa en databasanslutning {#connect-database}

När du har installerat skrivbordsappen på den lokala datorn följer du de officiella BDVisualizer-instruktionerna för att [skapa en ny databasanslutning](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

När du har valt **[!DNL PostgreSQL]** i listan [!DNL Connections] visas en [!DNL Object View]-flik för den nya [!DNL PostgreSQL]-anslutningen.

### Ange drivrutinsegenskaper för anslutningen {#properties}

Välj fliken **[!DNL Properties]** på fliken för objektvyn i [!DNL PostgreSQL] följt av **[!DNL Driver Properties]** från navigeringssidlisten. Mer information om [drivrutinsegenskaper](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) finns i den officiella dokumentationen.

Ange sedan drivrutinsegenskaperna som beskrivs i tabellen nedan.

>[!IMPORTANT]
>
>Om du vill ansluta DBVisualizer till Adobe Experience Platform måste du aktivera SSL. Läs [dokumentationen för SSL-lägen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med SSL-läget `verify-full`.

| Egenskap | Beskrivning |
| ------ | ------ |
| `PGHOST` | Värdnamnet för servern [!DNL PostgreSQL]. Det här värdet är dina **[!UICONTROL Host]-autentiseringsuppgifter** i Experience Platform. |
| `ssl` | Definiera SSL-värdet `1` för att aktivera användning av SSL. |
| `sslmode` | Detta styr nivån på SSL-skyddet. Du rekommenderas att använda SSL-läget `require` när du ansluter tredjepartsklienter till Adobe Experience Platform. Läget `require` ser till att kryptering krävs för all kommunikation och att nätverket är betrott för att ansluta till rätt server. Server SSL-certifikatvalidering krävs inte. |
| `user` | Användarnamnet som är kopplat till databasen är ditt företags-ID. Det är en alfanumerisk sträng som slutar på `@Adobe.Org`. Det här värdet är dina **[!UICONTROL Username]-autentiseringsuppgifter** i Experience Platform. |

Använd sökfältet för att hitta varje egenskap och markera sedan motsvarande cell för parameterns värde. Cellen markeras med blått. Ange autentiseringsuppgifterna för plattformen i värdefältet och välj **[!DNL Apply]** för att lägga till drivrutinsegenskapen.

>[!NOTE]
>
>Om du vill lägga till en andra `user`-profil väljer du `user` i parameterkolumnen och sedan den blå + (plus)-ikonen för att lägga till autentiseringsuppgifter för varje användare. Välj **[!DNL Apply]** om du vill lägga till drivrutinsegenskapen.

Kolumnen [!DNL Edited] visar en bockmarkering som anger att parametervärdet har uppdaterats.

### Autentiseringsuppgifter för Input Query Service {#query-service-credentials}

Om du vill hitta de autentiseringsuppgifter som krävs för att ansluta BBVisualizer med frågetjänsten loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** i den vänstra navigeringen, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar autentiseringsuppgifterna **host**, **port**, **database**, **username** och **password** finns i handboken för [autentiseringsuppgifter](../ui/credentials.md).

![Sidan Autentiseringsuppgifter på arbetsytan för Experience Platform-frågor med autentiseringsuppgifter och Utgående autentiseringsuppgifter markerade.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] erbjuder även autentiseringsuppgifter som inte upphör att gälla så att det går att konfigurera en gång med tredjepartsklienter. I dokumentationen finns [fullständiga instruktioner om hur du genererar och använder inloggningsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials). Du måste slutföra den här processen om du vill ansluta BDVisualizer som en engångsinstallation. Värdena `credential` och `technicalAccountId` innehåller värdet för parametern DBVisualizer `password`.

## Autentisering {#authentication}

Om du vill kräva ett användar-ID och lösenordsbaserad autentisering varje gång en anslutning upprättas går du till fliken [!DNL Properties] och väljer **[!DNL Authentication]** i navigeringssidlisten under [!DNL PostgreSQL].

Markera kryssrutorna **[!DNL Require Userid]** och **[!DNL Require Password]** på panelen Anslutningsautentisering och välj sedan **[!DNL Apply]**. Mer information om att [ange autentiseringsalternativ](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) finns i den officiella dokumentationen.

## Anslut till plattform

Du kan upprätta en anslutning med hjälp av autentiseringsuppgifter som förfaller eller inte förfaller. Om du vill skapa en anslutning väljer du fliken **[!DNL Connection]** på fliken för objektvyn i [!DNL PostgreSQL] och anger dina inloggningsuppgifter för Experience Platform för följande inställningar. Kompletterande instruktioner för att [konfigurera en manuell anslutning](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) finns tillgängliga på den officiella DBVisualizer-webbplatsen.

>[!NOTE]
>
>Alla inloggningsuppgifter som krävs av BDVisualizer i tabellen nedan är desamma för utgångsdatum och ej utgångsdatum om inte annat anges i parameterbeskrivningen.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!UICONTROL Name]** | Skapa ett namn för anslutningen. Du bör ange ett användarvänligt namn för att känna igen anslutningen. |
| **[!UICONTROL Database Server]** | Det här är dina **[!UICONTROL Host]**-autentiseringsuppgifter för Experience Platform. |
| **[!UICONTROL Database Port]** | Porten för [!DNL Query Service]. Du måste använda porten **80** eller **5432** för att ansluta till [!DNL Query Service]. |
| **[!UICONTROL Database]** | Använd Experience Platform **[!UICONTROL Database]**-autentiseringsuppgifter: `prod:all`. |
| **[!UICONTROL Database Userid]** | Detta är ditt organisations-ID för plattformen. Använd autentiseringsuppgifter för Experience Platform **[!UICONTROL Username]**. ID:t har formatet `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Database Password]** | Den här alfanumeriska strängen är din **[!UICONTROL Password]**-autentiseringsuppgift i Experience Platform. Om du vill använda autentiseringsuppgifter som inte förfaller är det här värdet de sammanfogade argumenten från `technicalAccountID` och `credential` som hämtats i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. Konfigurations-JSON-filen för icke-förfallande autentiseringsuppgifter är en engångshämtning under initieringen som Adobe inte har någon kopia av. |

När du har angett alla relevanta autentiseringsuppgifter väljer du **[!DNL Connect]**.

Dialogrutan [!DNL Connect] visas vid första tillfället i sessionen. Ange ditt serienummer och lösenord och välj **[!DNL Connect]**. Ett meddelande visas i loggen som bekräftar att anslutningen lyckades.

## Nästa steg

Nu när du har anslutit [!DNL DbVisualizer] med [!DNL Query Service] kan du använda [!DNL DbVisualizer] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guiden om frågekörning](../best-practices/writing-queries.md).
