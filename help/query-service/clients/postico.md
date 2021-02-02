---
keywords: Experience Platform;home;populära topics;Query service;query service;postico;Postico;connect to query service;
solution: Experience Platform
title: Anslut med Postico
topic: connect
description: Det här dokumentet innehåller länken för installation av klienten Postico för Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# [!DNL Postico]

Det här dokumentet innehåller stegen för att ansluta [!DNL Postico] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Postico] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Postico] finns i [officiell [!DNL Postico] dokumentation](https://eggerapps.at/postico/docs).
> 
> Dessutom är [!DNL Postico] **endast** tillgängligt på macOS-enheter.

## Anslut [!DNL Postico] till frågetjänsten

Om du vill ansluta [!DNL Postico] till frågetjänsten öppnar du [!DNL Postico] och väljer **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Nu kan du ange värden som ska kopplas till Adobe Experience Platform.

Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Logga in på [!DNL Platform] och välj **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

När du har infogat dina inloggningsuppgifter väljer du **[!DNL Connect]** för att ansluta till frågetjänsten.

![](../images/clients/postico/authentication-details.png)

När du har anslutit till plattformen kan du se en lista över alla relationer som tidigare gjorts med Query Service.

![](../images/clients/postico/show-queries.png)

## Skapa SQL-satser

Om du vill skapa en ny SQL-fråga markerar du och öppnar SQL-frågan.

![](../images/clients/postico/create-query.png)

En ruta visas och härifrån kan du skriva in frågan som du vill köra. När du är klar väljer du **[!DNL Execute Statement]** för att köra frågan.

![](../images/clients/postico/run-statement.png)

En tabell visas med resultatet av den slutförda frågekörningen.

![](../images/clients/postico/query-results.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Postico] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [frågeguiden](../best-practices/writing-queries.md) som körs.