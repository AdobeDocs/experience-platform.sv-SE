---
keywords: Experience Platform;hem;populära ämnen;tableau;query service;Query service;connect to query service;
solution: Experience Platform
title: Koppla tabell till frågetjänst
description: Det här dokumentet går igenom de olika stegen för att ansluta Tableau till Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Anslut [!DNL Tableau] till frågetjänsten

Det här dokumentet innehåller information om hur du ansluter [!DNL Tableau] till Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Tableau] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Tableau] finns i [officiell [!DNL Tableau] dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instruktioner om hur du [ansluter till en PostgreSQL-server med Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) finns på den officiella Tableau-webbplatsen. När dialogrutan för anslutningsinställningar visas anger du dina Experience Platform-inloggningsuppgifter i parameterfälten för att ansluta till Adobe Experience Platform. En lista över de anslutningsparametrar som krävs visas nedan.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!DNL Server]** | Adress till din SFTP-lagringsplats. Använd värdet för dina Experience Platform **[!UICONTROL Host]**-autentiseringsuppgifter. |
| **[!DNL Port]:** | Porten för [!DNL Query Service]. Du måste använda porten **80** eller **5432** för att ansluta till [!DNL Query Service]. |
| **[!DNL Database]** | De databaser som du vill komma åt. Använd värdet för dina Experience Platform **[!UICONTROL Database]**-autentiseringsuppgifter: `prod:all`. |
| **[!DNL Authentication]:** | Den metod du valt för att bevisa användaridentiteten. Du rekommenderas att välja [!DNL Username and Password] bland de tillgängliga alternativen på den nedrullningsbara menyn. |
| **[!DNL Username]** | Det här är ditt företags-ID för Experience Platform. Använd värdet för dina Experience Platform **[!UICONTROL Username]**-autentiseringsuppgifter. ID:t har formatet `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Den här alfanumeriska strängen är din Experience Platform **[!UICONTROL Password]**-autentiseringsuppgift. Om du vill använda autentiseringsuppgifter som inte förfaller är det här värdet de sammanfogade argumenten från `technicalAccountID` och `credential` som hämtats i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. JSON-konfigurationsfilen för icke-förfallodatum är en engångshämtning under initieringen som Adobe inte behåller någon kopia av. |

Mer information om hur du hittar ditt användarnamn, lösenord och inloggningsuppgifter finns i handboken för [inloggningsuppgifter](../ui/credentials.md). Logga in på [!DNL Experience Platform] och välj sedan **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina autentiseringsuppgifter.

>[!IMPORTANT]
>
>Som användare av Tableau eller Power BI kan du ansluta Customer Journey Analytics till dina BI-verktyg från fliken med autentiseringsuppgifter för frågetjänsten. Instruktioner om hur du [ansluter dina BI-verktyg till Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics) finns i dokumentationen för autentiseringsuppgifter.

Kontrollera att du har markerat rutan **[!UICONTROL Require SSL]** innan du försöker ansluta. Läs [dokumentationen för SSL-lägen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Kapslade datastrukturer i BI-verktyg från tredje part kan förenklas för att förbättra användbarheten och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data. Mer information om hur du aktiverar den här inställningen vid anslutning till en databas finns i dokumentationen för [`FLATTEN`-funktionen](../key-concepts/flatten-nested-data.md).

När du har fyllt i alla dina inloggningsuppgifter bekräftar du dina inställningar för att fortsätta. Du har nu en koppling till Adobe Experience Platform.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Tableau] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden för [frågor som körs](../best-practices/writing-queries.md).
