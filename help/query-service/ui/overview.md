---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Användargränssnittshandbok för frågetjänst
topic-legacy: guide
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 483bcea231ed5f25c76771d0acba7e0c62dfed16
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# [!DNL Query Service] guide

Adobe Experience Platform [!DNL Query Service] har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och komma åt frågor som sparats av användare i din IMS-organisation. Om du vill komma åt användargränssnittet i [Adobe Experience Platform](https://platform.adobe.com) väljer du **[!UICONTROL Queries]** i den vänstra navigeringen.

## [!DNL Query Editor]

Med [!DNL Query Editor] kan du skriva och köra frågor utan att använda en extern klient. Välj **[!UICONTROL Create Query]** för att öppna [!DNL Query Editor] och skapa en ny fråga. Du kan även komma åt [!DNL Query Editor] genom att välja en fråga på flikarna **[!UICONTROL Log]** eller **[!UICONTROL Browse]**. Om du väljer en fråga som redan har körts eller sparats öppnas [!DNL Query Editor] och SQL-uttrycket för den valda frågan visas.

![Bild](../images/ui/overview/overview.png)

[!DNL Query Editor] innehåller redigeringsutrymme där du kan börja skriva en fråga. När du skriver slutför redigeraren automatiskt reserverade ord, tabeller och fältnamn från SQL i tabeller. När du är klar med frågan väljer du knappen **Spela upp** för att köra frågan. På fliken **[!UICONTROL Console]** nedanför redigeraren visas vad [!DNL Query Service] gör just nu, vilket anger när en fråga har returnerats. Fliken **[!UICONTROL Result]**, bredvid konsolen, visar frågeresultat. Mer information om hur du använder [!DNL Query Editor] finns i [Frågeredigeringsguiden](./user-guide.md).

![Bild](../images/ui/overview/query-editor.png)

## Bläddra

På fliken **[!UICONTROL Browse]** visas frågor som sparats av användare i din organisation. Det är praktiskt att tänka på dessa som frågeprojekt, eftersom frågor som sparas här fortfarande kan vara under uppbyggnad. Frågor som visas på fliken **[!UICONTROL Browse]** visas också som körningsfrågor på fliken **[!UICONTROL Log]** om de tidigare har körts av [!DNL Query Service].

![Bild](../images/ui/overview/browse.png)

| Kolumn | Beskrivning |
| --- | --- |
| Namn | Frågenamnet som har skapats av användaren. Du kan välja ett namn för att öppna frågan i [!DNL Query Editor]. Du kan också använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| SQL | De första tecknen i SQL-frågan. Om du placerar pekaren över koden visas hela frågan. |
| Ändrad av | Den sista användaren som ändrade frågan. Alla användare i organisationen som har åtkomst till [!DNL Query Service] kan ändra frågor. |
| Senast ändrad | Datum och tid för den senaste ändringen av frågan, i webbläsarens tidszon. |

## Logg

Fliken **[!UICONTROL Log]** innehåller en lista med frågor som tidigare har körts. Som standard listas frågorna i loggen i omvänd kronologi.

![Bild](../images/ui/overview/log.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Frågenamnet som består av de första tecknen i SQL-frågan. Om du väljer namnet öppnas [!DNL Query Editor] så att du kan redigera frågan. Du kan använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| **[!UICONTROL Created By]** | Namnet på den person som skapade frågan. |
| **[!UICONTROL Client]** | Klienten som används för frågan. |
| **[!UICONTROL Dataset]** | Den indatamängd som används av frågan. Välj den datauppsättning som du vill gå till informationsskärmen för indatauppsättningar. |
| **[!UICONTROL Status]** | Frågans aktuella status. |
| **[!UICONTROL Last Run]** | När frågan kördes senast. Du kan sortera listan i stigande eller fallande ordning genom att markera pilen över den här kolumnen. |
| **[!UICONTROL Run Time]** | Hur lång tid det tog att köra frågan. |

## Autentiseringsuppgifter

På fliken **[!UICONTROL Credentials]** visas dina [!DNL Postgres]-autentiseringsuppgifter. Markera ikonen **[!UICONTROL Copy]** bredvid ett fält för att lagra dess innehåll i tangentbordsbufferten. Mer information om hur du använder dessa autentiseringsuppgifter för att ansluta till externa klienter finns i [handboken för att ansluta till klienter](../clients/overview.md).

![Bild](../images/ui/overview/credentials.png)

## Nästa steg

Nu när du är bekant med [!DNL Query Service]-användargränssnittet på [!DNL Platform] kan du komma åt [!DNL Query Editor] och börja skapa egna frågeprojekt att dela med andra användare i organisationen. Mer information om hur du redigerar och kör frågor i [!DNL Query Editor] finns i [användarhandboken för Frågeredigeraren](./user-guide.md).