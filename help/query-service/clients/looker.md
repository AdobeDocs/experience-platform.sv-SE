---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;Sökare;sökare;ansluta till frågetjänst;
solution: Experience Platform
title: Anslut sökare till frågetjänst
topic-legacy: connect
description: Det här dokumentet går igenom stegen för att ansluta Looker till Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Anslut [!DNL Looker] till frågetjänst

Det här dokumentet innehåller stegen för anslutning [!DNL Looker] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Looker] och känner till hur man navigerar i gränssnittet. Mer information om [!DNL Looker] finns i [officiell [!DNL Looker] dokumentation](https://docs.looker.com/).

Efter inloggning [!DNL Looker], markera **[!DNL Admin]**, följt av **[!DNL Connections]**.

![The [!DNL Looker] Kontrollpanel med anslutningar markerade på den nedrullningsbara menyn Admin.](../images/clients/looker/click-admin-connections.png)

På den här sidan väljer du **[!DNL New Connection]**.

![Arbetsytan Anslutningar med Ny anslutning markerad.](../images/clients/looker/click-new-connection.png)

Här kan du fylla i information om anslutningsinställningarna.

![Sidan Anslutningsinställningar för en ny anslutning.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Namnet på anslutningen.
- **[!DNL Dialect]:** Den dialekt som används för SQL-databasen. [!DNL Query Service] använder **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Värdslutpunkten och dess port för [!DNL Query Service].
- **[!DNL Database]:** Databasen som ska användas.
- **[!DNL Username and Password]:** De inloggningsuppgifter som ska användas. Användarnamnet kommer att ha formatet `ORG_ID@AdobeOrg`.
- **SSL**: Aktivera SSL för att säkerställa en säker anslutning över nätverket.

>[!IMPORTANT]
>
>Se [[!DNL Query Service] SSL-dokumentation](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med `verify-full` SSL-läge.

Mer information om hur du hittar värd och port, databasnamn och inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md). Logga in på [!DNL Platform]väljer **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

När du har angett anslutningsinformationen väljer du **[!DNL Test These Settings]** för att säkerställa att dina uppgifter fungerar som de ska. Om de gör det visas ett meddelande om att du kan ansluta nedan. Om anslutningen lyckas väljer du **[!DNL Add Connection]** för att skapa din anslutning.

![Sidan Anslutningsinställningar för en ny anslutning med Testa dessa inställningar är markerad.](../images/clients/looker/click-test-connection.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Looker] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
