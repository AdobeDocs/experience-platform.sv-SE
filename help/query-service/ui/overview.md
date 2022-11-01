---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;Query editor;
solution: Experience Platform
title: Användargränssnittshandbok för frågetjänst
topic-legacy: guide
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a085bac6b4ee825d534710ae91d6690fa076e873
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# [!DNL Query Service] Användargränssnittsguide

Adobe Experience Platform [!DNL Query Service] innehåller ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och komma åt frågor som har sparats av användare i IMS-organisationen. Åtkomst till användargränssnittet i [Adobe Experience Platform](https://platform.adobe.com), markera **[!UICONTROL Queries]** i den vänstra navigeringen.

## [!DNL Query Editor]

The [!DNL Query Editor] gör att du kan skriva och köra frågor utan att använda en extern klient. Välj **[!UICONTROL Create Query]** för att öppna [!DNL Query Editor] och skapa en ny fråga. Du kan även komma åt [!DNL Query Editor] genom att välja en fråga från **[!UICONTROL Log]** eller **[!UICONTROL Templates]** -tabbar. Om du väljer en fråga som har körts eller sparats tidigare öppnas [!DNL Query Editor] och visa SQL för den valda frågan.

![Kontrollpanelen Frågor med Skapa fråga markerad.](../images/ui/overview/overview.png)

[!DNL Query Editor] innehåller redigeringsutrymme där du kan börja skriva en fråga. När du skriver slutför redigeraren automatiskt reserverade ord, tabeller och fältnamn från SQL i tabeller. När du är klar med din fråga väljer du **Spela upp** för att köra frågan. The **[!UICONTROL Console]** under redigeraren visas [!DNL Query Service] gör för närvarande, vilket anger när en fråga har returnerats. The **[!UICONTROL Result]** bredvid konsolen visar frågeresultat. Se [Frågeredigeringsguide](./user-guide.md) för mer information om hur du använder [!DNL Query Editor].

![En zoomad vy med [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Mallar {#browse}

The **[!UICONTROL Templates]** -fliken visar frågor som sparats av användare i din organisation. Det är praktiskt att tänka på dessa som frågeprojekt, eftersom frågor som sparas här fortfarande kan vara under uppbyggnad. Frågor som visas på **[!UICONTROL Templates]** -fliken visas även som körningsfrågor i **[!UICONTROL Log]** om de har körts av [!DNL Query Service].

![En zoomad vy med fliken Mallar på kontrollpanelen Frågor som visar flera sparade frågor.](../images/ui/overview/templates.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Namnfältet är antingen frågenamnet som skapats av användaren eller de första tecknen i SQL-frågan. Alla frågor som skapas via gränssnittet med Frågeredigeraren får i början ett namn. Om frågan skapades via API är namnet på frågan ett fragment av det SQL-uttryck som användes för att skapa frågan. Du kan välja frågenamnet för att öppna frågan i [!DNL Query Editor]. Du kan också använda sökfältet för att söka efter [!UICONTROL Name] för en fråga. Sökningar är skiftlägeskänsliga. |
| **[!UICONTROL SQL]** | De första tecknen i SQL-frågan. Om du placerar pekaren över koden visas hela frågan. |
| **[!UICONTROL Modified by]** | Den sista användaren som ändrade frågan. Alla användare i organisationen som har tillgång till [!DNL Query Service] kan ändra frågor. |
| **[!UICONTROL Last modified]** | Datum och tid för den senaste ändringen av frågan, i webbläsarens tidszon. |

## Logg

The **[!UICONTROL Log]** -fliken innehåller en lista med frågor som tidigare har körts. Som standard listas frågorna i loggen i omvänd kronologi.

![En zoomad vy av loggfliken i kontrollpanelen för frågor som visar en lista med frågor i omvänd kronologisk ordning.](../images/ui/overview/log.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Frågenamnet som består av de första tecknen i SQL-frågan. Om du väljer ett namn öppnas [!DNL Query Editor]så att du kan redigera frågan. Du kan använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| **[!UICONTROL Created by]** | Namnet på den person som skapade frågan. |
| **[!UICONTROL Client]** | Klienten som används för frågan. |
| **[!UICONTROL Dataset]** | Den indatamängd som används av frågan. Välj den datauppsättning som du vill gå till informationsskärmen för indatauppsättningar. |
| **[!UICONTROL Status]** | Frågans aktuella status. |
| **[!UICONTROL Last run]** | När frågan kördes senast. Du kan sortera listan i stigande eller fallande ordning genom att markera pilen över den här kolumnen. |
| **[!UICONTROL Run time]** | Hur lång tid det tog att köra frågan. |

## Autentiseringsuppgifter

The **[!UICONTROL Credentials]** visas både dina förfallodatum och ej förfallodatum. Mer information om hur du använder dessa autentiseringsuppgifter för att ansluta till externa klienter finns i [inloggningsguide](../clients/overview.md).

![Kontrollpanelen Frågor med fliken Autentiseringsuppgifter markerad.](../images/ui/overview/credentials.png)

## Nästa steg

Nu när du är bekant med [!DNL Query Service] användargränssnitt på [!DNL Platform]kan du komma åt [!DNL Query Editor] för att börja skapa egna frågeprojekt som ska delas med andra användare i organisationen. Mer information om hur du skapar och kör frågor i [!DNL Query Editor], se [[!DNL Query Editor] användarhandbok](./user-guide.md).