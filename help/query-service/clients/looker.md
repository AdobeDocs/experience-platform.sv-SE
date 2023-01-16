---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;Sökare;sökare;ansluta till frågetjänst;
solution: Experience Platform
title: Anslut sökare till frågetjänst
description: Det här dokumentet går igenom stegen för att ansluta Looker till Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Anslut [!DNL Looker] till frågetjänst

Det här dokumentet innehåller stegen för anslutning [!DNL Looker] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Looker] och känner till hur man navigerar i gränssnittet. Mer information om [!DNL Looker] finns i [officiell [!DNL Looker] dokumentation](https://docs.looker.com/).

## Skapa en ny databasanslutning {#create-connection}

Efter inloggning [!DNL Looker], markera **[!DNL Admin]**, följt av **[!DNL Connections]**. The [!DNL Connections] sidan öppnas. På [!DNL Connections] sida, markera **[!DNL Add Connection]**.

Här anger du information om de anslutningsinställningar som anges nedan. Läs den officiella Looker-dokumentationen för [instruktioner för att skapa en ny databasanslutning och beskrivningar av tillgängliga egenskaper](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Namnet på anslutningen.
- **[!DNL Dialect]:** Den dialekt som används för SQL-databasen. [!DNL Query Service] använder **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Värdslutpunkten och dess port för [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas.
- **[!DNL Username and Password]:** De inloggningsuppgifter som ska användas. Användarnamnet kommer att ha formatet `ORG_ID@AdobeOrg`.
- **SSL**: Aktivera SSL för att säkerställa en säker anslutning över nätverket.

Om du vill hitta de autentiseringsuppgifter som krävs för att ansluta Looker med Query Service loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar **värd**, **port**, **databas**, **användarnamn** och **lösenord** autentiseringsuppgifter, läs [inloggningsguide](../ui/credentials.md).

![Sidan Autentiseringsuppgifter på arbetsytan Experience Platform Frågor med Autentiseringsuppgifter och Utgångsuppgifter markerade.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] erbjuder även icke-utgångsdatum för att möjliggöra en engångskonfiguration med tredjepartsklienter. Läs dokumentationen för [fullständiga anvisningar om hur du genererar och använder ej utgångsdatum](../ui/credentials.md#non-expiring-credentials). Du måste slutföra den här processen om du vill ansluta Looker som en engångsinstallation. The `credential` och `technicalAccountId` förvärvade värden utgör värdet för Looker `password` parameter.

Mer information om SSL-stöd för tredjepartsanslutningar i Adobe Experience Platform finns i [[!DNL Query Service] SSL-dokumentation](./ssl-modes.md). Det här dokumentet innehåller instruktioner om hur du ansluter med `verify-full` SSL-läge.

När du har angett anslutningsinformationen väljer du **[!DNL Test These Settings]** för att säkerställa att dina uppgifter fungerar som de ska. Mer information om [testa dina anslutningsinställningar](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) finns i den officiella Looker-dokumentationen. När anslutningen lyckades visas ett meddelande på skärmen som anger att du kan ansluta. När anslutningen är klar väljer du **[!DNL Add Connection]** för att skapa din anslutning.

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Looker] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
