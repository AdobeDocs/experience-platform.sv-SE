---
keywords: Experience Platform;hem;populära ämnen;tableau;query service;Query service;connect to query service;
solution: Experience Platform
title: Koppla tabell till frågetjänst
description: Det här dokumentet går igenom de olika stegen för att ansluta Tableau till Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Anslut [!DNL Tableau] till frågetjänst

Det här dokumentet innehåller information om anslutning [!DNL Tableau] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Tableau] och känner till hur man navigerar i gränssnittet. Mer information om [!DNL Tableau] finns i [officiell [!DNL Tableau] dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instruktioner om hur du [ansluta till en PostgreSQL-server med Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) finns på den officiella Tableu-webbplatsen. När dialogrutan för anslutningsinställningar visas anger du plattformsautentiseringsuppgifterna i parameterfälten för att ansluta till Adobe Experience Platform. En lista över de anslutningsparametrar som krävs visas nedan.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!DNL Server]** | Adress till din SFTP-lagringsplats. Använd värdet på Experience Platform **[!UICONTROL Host]** autentiseringsuppgifter. |
| **[!DNL Port]:** | Porten för [!DNL Query Service]. Du måste använda port **80** eller **5432** att ansluta till [!DNL Query Service]. |
| **[!DNL Database]** | De databaser som du vill komma åt. Använd värdet på Experience Platform **[!UICONTROL Database]** autentiseringsuppgifter: `prod:all`. |
| **[!DNL Authentication]:** | Den metod du valt för att bevisa användaridentiteten. Vi rekommenderar att du väljer [!DNL Username and Password] från de tillgängliga alternativen i listrutan. |
| **[!DNL Username]** | Detta är ditt ID för plattformsorganisation. Använd värdet på Experience Platform **[!UICONTROL Username]** autentiseringsuppgifter. ID:t kommer att ha formatet `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Den här alfanumeriska strängen är Experience Platform **[!UICONTROL Password]** autentiseringsuppgifter. Om du vill använda icke-förfallande autentiseringsuppgifter är det här värdet det sammanfogade argumentet från `technicalAccountID` och `credential` hämtas i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. Konfigurations-JSON-filen för icke-förfallande autentiseringsuppgifter är en engångshämtning under initieringen som Adobe inte har någon kopia av. |

Mer information om hur du hittar ditt användarnamn, lösenord och inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md). Logga in på [!DNL Platform]väljer **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

Kontrollera att du har markerat **[!UICONTROL Require SSL]** innan du försöker ansluta. Se [Dokumentation för SSL-lägen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Kapslade datastrukturer i BI-verktyg från tredje part kan förenklas för att förbättra användbarheten och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data. Läs dokumentationen på[`FLATTEN` funktion](../key-concepts/flatten-nested-data.md) för instruktioner om hur du aktiverar den här inställningen vid anslutning till en databas.

När du har fyllt i alla dina inloggningsuppgifter bekräftar du dina inställningar för att fortsätta. Du har nu en koppling till Adobe Experience Platform.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Tableau] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden [köra frågor](../best-practices/writing-queries.md).
