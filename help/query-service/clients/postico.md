---
keywords: Experience Platform;home;populära topics;Query service;query service;postico;Postico;connect to query service;
solution: Experience Platform
title: Anslut position till frågetjänst
description: Det här dokumentet innehåller länken för installation av klienten Postico för Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Anslut [!DNL Postico] till frågetjänsten (Mac)

Det här dokumentet innehåller stegen för att ansluta [!DNL Postico] till Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Postico] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Postico] finns i [officiell [!DNL Postico] dokumentation](https://eggerapps.at/postico/docs).
> 
> Dessutom är [!DNL Postico] **endast** tillgängligt på macOS-enheter.

Om du vill ansluta [!DNL Postico] till frågetjänsten öppnar du [!DNL Postico] och väljer **[!DNL New Favorite]**. Dialogrutan för anslutningsinställningar visas. Härifrån kan du ange parametervärden som ska kopplas till Adobe Experience Platform. Ange anslutningsinställningarna som anges nedan. Instruktioner om hur du [ansluter till en PostgreSQL-server med Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) finns också på den officiella Postico-webbplatsen.

| Anslutningsparameter | Beskrivning |
|---|---|
| **[!DNL Host]:** | Värdnamnet för PostgreSQL-servern. |
| **[!DNL Port]:** | Porten för [!DNL Query Service]. Du måste använda porten **80** eller **5432** för att ansluta till [!DNL Query Service]. |
| **[!DNL User]** | Skapa ett namn för den specifika anslutningen. Lämna fältet tomt om du vill använda ditt inloggningsnamn för Mac. |
| **[!DNL Password]** | Den här alfanumeriska strängen är din **[!UICONTROL Password]**-autentiseringsuppgift i Experience Platform. Om du vill använda autentiseringsuppgifter som inte förfaller är det här värdet de sammanfogade argumenten från `technicalAccountID` och `credential` som hämtats i JSON-konfigurationsfilen. Lösenordsvärdet har följande format: {technicalAccountId}:{credential}. Konfigurations-JSON-filen för icke-förfallande autentiseringsuppgifter är en engångshämtning under initieringen som Adobe inte har någon kopia av. |
| **[!DNL Database]** | Använd Experience Platform **[!UICONTROL Database]**-autentiseringsuppgifter: `prod:all`. |

Mer information om hur du söker efter databasnamn, värd, port och inloggningsuppgifter finns i [referenshandboken](../ui/credentials.md). Logga in på [!DNL Platform] och välj sedan **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina autentiseringsuppgifter.

När du har infogat dina autentiseringsuppgifter väljer du **[!DNL Connect]** för att ansluta till frågetjänsten.

När du har anslutit till plattformen kan du se en lista över alla relationer som tidigare gjorts med Query Service.

## Skapa SQL-satser

Om du vill skapa en ny SQL-fråga väljer du **[!DNL SQL Query]** i sidofältet. Du kan också använda kortkommandot ( ⇧ T) för att navigera till frågevyn och ange den fråga som du vill köra. När du är klar väljer du **[!DNL Execute Statement]** för att köra frågan. En tabell visas med resultatet av den slutförda frågekörningen.

Mer information om [att använda frågevyn](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html) finns i den officiella dokumentationen för Postico.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Postico] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guiden ](../best-practices/writing-queries.md) som kör frågor.
