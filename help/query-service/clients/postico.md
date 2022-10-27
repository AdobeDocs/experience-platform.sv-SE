---
keywords: Experience Platform;home;populära topics;Query service;query service;postico;Postico;connect to query service;
solution: Experience Platform
title: Anslut position till frågetjänst
topic-legacy: connect
description: Det här dokumentet innehåller länken för installation av klienten Postico för Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Anslut [!DNL Postico] till Query Service (Mac)

Det här dokumentet innehåller stegen för anslutning [!DNL Postico] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Postico] och känner till hur man navigerar i gränssnittet. Mer information om [!DNL Postico] finns i [officiell [!DNL Postico] dokumentation](https://eggerapps.at/postico/docs).
> 
> Dessutom [!DNL Postico] är **endast** som finns på macOS-enheter.

Ansluta [!DNL Postico] till frågetjänst, öppna [!DNL Postico] och markera **[!DNL New Favorite]**.

![The [!DNL Postico] Gränssnitt med Ny favorit markerat.](../images/clients/postico/open-postico.png)

Nu kan du ange värden som ska kopplas till Adobe Experience Platform.

Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md). Logga in på [!DNL Platform]väljer **[!UICONTROL Queries]**, följt av **[!UICONTROL Credentials]**.

När du har infogat dina inloggningsuppgifter väljer du **[!DNL Connect]** för att ansluta till frågetjänsten.

![Dialogrutan Ny favorit med anslutning markerad.](../images/clients/postico/authentication-details.png)

När du har anslutit till plattformen kan du se en lista över alla relationer som tidigare gjorts med Query Service.

![En lista över anslutningar i [!DNL Postico] Gränssnitt.](../images/clients/postico/show-queries.png)

## Skapa SQL-satser

Om du vill skapa en ny SQL-fråga markerar du och öppnar SQL-frågan.

![The [!DNL Postico] Gränssnitt med kortkommandot SQL Query markerat.](../images/clients/postico/create-query.png)

En ruta visas och härifrån kan du skriva in frågan som du vill köra. När du är klar väljer du **[!DNL Execute Statement]** för att köra frågan.

![SQL-redigeraren med Execute Statement markerat.](../images/clients/postico/run-statement.png)

En tabell visas med resultatet av den slutförda frågekörningen.

![En resultattabell från exempelfrågan.](../images/clients/postico/query-results.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service]kan du använda [!DNL Postico] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i [köra frågeguide](../best-practices/writing-queries.md).
