---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;Sökare;sökare;ansluta till frågetjänst;
solution: Experience Platform
title: Anslut sökare till frågetjänst
topic: connect
description: Det här dokumentet går igenom stegen för att ansluta Looker till Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Anslut [!DNL Looker] till frågetjänsten

Det här dokumentet innehåller stegen för att ansluta [!DNL Looker] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Looker] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Looker] finns i [officiell [!DNL Looker] dokumentation](https://docs.looker.com/).

När du har loggat in på [!DNL Looker] väljer du **[!DNL Admin]** följt av **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Välj **[!DNL New Connection]** på den här sidan.

![](../images/clients/looker/click-new-connection.png)

Här kan du fylla i information om anslutningsinställningarna.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Namnet på anslutningen.
- **[!DNL Dialect]:** Den dialekt som används för SQL-databasen. [!DNL Query Service] använder  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Värdslutpunkten och dess port för  [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas.
- **[!DNL Username and Password]:** De inloggningsuppgifter som ska användas. Användarnamnet kommer att ha formatet `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Mer information om hur du hittar värd och port, databasnamn och inloggningsuppgifter finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Logga in på [!DNL Platform] och välj **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

När du har angett anslutningsinformationen väljer du **[!DNL Test These Settings]** för att se till att dina autentiseringsuppgifter fungerar som de ska. Om de gör det visas ett meddelande om att du kan ansluta nedan. Om anslutningen lyckas väljer du **[!DNL Add Connection]** för att skapa anslutningen.

![](../images/clients/looker/click-test-connection.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Looker] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../best-practices/writing-queries.md) som körs.