---
keywords: Experience Platform;hem;populära ämnen;tableau;query service;Query service;connect to query service;
solution: Experience Platform
title: Anslut tabell till frågetjänst
topic-legacy: connect
description: Det här dokumentet går igenom de olika stegen för att ansluta Tableau till Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Anslut [!DNL Tableau] till frågetjänst

Det här dokumentet beskriver hur du ansluter Tableau till Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Tableau] och känner till hur man navigerar i gränssnittet. Mer information om [!DNL Tableau] finns i [officiell [!DNL Tableau] dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Ansluta [!DNL Tableau] till [!DNL Query Service], öppna [!DNL Tableau]och i **[!DNL To a Server]** avsnittsmarkera **[!DNL More]** följt av **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Nu kan du ange värden som ska kopplas till Adobe Experience Platform. Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md). Logga in på [!DNL Platform]väljer **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

Kontrollera att du har markerat **[!UICONTROL SSL Required]** innan du försöker ansluta.

>[!IMPORTANT]
>
>Se [[!DNL Query Service] SSL-dokumentation](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter med `verify-full` SSL-läge.

![](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>Kapslade datastrukturer i BI-verktyg från tredje part kan förenklas för att förbättra användbarheten och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data. Läs dokumentationen på[`FLATTEN` funktion](../best-practices/flatten-nested-data.md) för instruktioner om hur du aktiverar den här inställningen vid anslutning till en databas.

När du har fyllt i alla dina uppgifter väljer du **[!DNL Sign In]** för att fortsätta.

Du har nu anslutit till Adobe Experience Platform, med en lista över tabellerna på sidan.

![](../images/clients/tableau/connected.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Tableau] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden [köra frågor](../best-practices/writing-queries.md).
