---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anslut med Looker
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Anslut med [!DNL Looker]

Följ stegen nedan för att ansluta [!DNL Looker] till [!DNL Query Service] Adobe Experience Platform:

När du har loggat in [!DNL Looker]klickar du på **[!UICONTROL Admin]**, följt av **[!UICONTROL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

På den här sidan klickar du på **Ny anslutning**.

![](../images/clients/looker/click-new-connection.png)

Härifrån kan du fylla i informationen för anslutningsinställningarna.

![](../images/clients/looker/new-connection.png)

- **Namn:** Namnet på anslutningen.
- **Dialekt:** Den dialekt som används för SQL-databasen. [!DNL Query Service] använder **[!DNL PostgreSQL]**.
- **Värd och port:** Värdslutpunkten och dess port för [!DNL Query Service].
- **Databas:** Databasen som ska användas.
- **Användarnamn och lösenord:** De inloggningsuppgifter som ska användas. Användarnamnet kommer att ha formatet `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Mer information om hur du hittar värd och port, databasnamn och inloggningsuppgifter finns på [inloggningssidan på Platform](https://platform.adobe.com/query/configuration). Logga in på, [!DNL Platform]klicka **[!UICONTROL Queries]** och klicka sedan på **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

När du har angett anslutningsinformationen klickar du på **[!UICONTROL Test These Settings]** för att kontrollera att inloggningsuppgifterna fungerar som de ska. Om de gör det visas ett meddelande om att du kan ansluta nedan. Om anslutningen lyckas klickar du på **[!UICONTROL Add Connection]** för att skapa anslutningen.

![](../images/clients/looker/click-test-connection.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Looker] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../creating-queries/creating-queries.md).