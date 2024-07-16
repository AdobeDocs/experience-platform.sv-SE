---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;Sökare;sökare;ansluta till frågetjänst;
solution: Experience Platform
title: Anslut sökare till frågetjänst
description: Det här dokumentet går igenom stegen för att ansluta Looker till Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Anslut [!DNL Looker] till frågetjänsten

Det här dokumentet innehåller stegen för att ansluta [!DNL Looker] till Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Looker] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Looker] finns i [officiell [!DNL Looker] dokumentation](https://docs.looker.com/).

## Skapa en ny databasanslutning {#create-connection}

När du har loggat in på [!DNL Looker] väljer du **[!DNL Admin]** följt av **[!DNL Connections]**. Sidan [!DNL Connections] öppnas. Välj **[!DNL Add Connection]** på sidan [!DNL Connections].

Här anger du information om de anslutningsinställningar som anges nedan. I den officiella Looker-dokumentationen finns [instruktioner om hur du skapar en ny databasanslutning och beskrivningar av de tillgängliga egenskaperna](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Namnet på anslutningen.
- **[!DNL Dialect]:** Den dialekt som används för SQL-databasen. [!DNL Query Service] använder **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Värdslutpunkten och dess port för [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas.
- **[!DNL Username and Password]:** De inloggningsuppgifter som ska användas. Användarnamnet kommer att ha formatet `ORG_ID@AdobeOrg`.
- **SSL**: Aktivera SSL för att säkerställa en säker anslutning över nätverket.

Om du vill hitta de autentiseringsuppgifter som krävs för att ansluta Looker med Query Service loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** i den vänstra navigeringen, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar autentiseringsuppgifterna **host**, **port**, **database**, **username** och **password** finns i handboken för [autentiseringsuppgifter](../ui/credentials.md).

![Sidan Autentiseringsuppgifter på arbetsytan för Experience Platform-frågor med autentiseringsuppgifter och Utgående autentiseringsuppgifter markerade.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] erbjuder även autentiseringsuppgifter som inte upphör att gälla så att det går att konfigurera en gång med tredjepartsklienter. I dokumentationen finns [fullständiga instruktioner om hur du genererar och använder inloggningsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials). Du måste slutföra den här processen om du vill ansluta Looker som en engångsinstallation. Värdena `credential` och `technicalAccountId` innehåller värdet för parametern Looker `password`.

Mer information om SSL-stöd för tredjepartsanslutningar i Adobe Experience Platform finns i [[!DNL Query Service] SSL-dokumentationen](./ssl-modes.md). Det här dokumentet innehåller instruktioner om hur du ansluter med SSL-läget `verify-full`.

När du har angett din anslutningsinformation väljer du **[!DNL Test These Settings]** för att se till att dina autentiseringsuppgifter fungerar som de ska. Mer information om att [testa dina anslutningsinställningar](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) finns i den officiella Looker-dokumentationen. När anslutningen lyckades visas ett meddelande på skärmen som anger att du kan ansluta. När anslutningen är klar väljer du **[!DNL Add Connection]** för att skapa anslutningen.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Looker] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [guiden ](../best-practices/writing-queries.md) som kör frågor.
