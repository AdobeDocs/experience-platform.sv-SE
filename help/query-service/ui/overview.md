---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Användargränssnittshandbok för Adobe Experience Platform Query Service
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Handbok för frågetjänst

Adobe Experience Platform Query Service tillhandahåller ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation. Om du vill få åtkomst till gränssnittet i [Adobe Experience Platform][platform-ui]väljer du **Frågor** i den vänstra navigeringen.

## Frågeredigeraren

Med frågeredigeraren kan du skriva och köra frågor utan att använda en extern klient. Klicka på **Skapa fråga** för att öppna Frågeredigeraren och skapa en ny fråga. Du kan även öppna frågeredigeraren genom att välja en fråga på flikarna *Logg* eller *Bläddra* . Om du väljer en fråga som har körts eller sparats tidigare öppnas Frågeredigeraren och SQL:en för den valda frågan visas.

![Bild](../images/queries/ui-overview/overview.png)

Frågeredigeraren innehåller redigeringsutrymme där du kan börja skriva en fråga. När du skriver fyller redigeraren automatiskt i reserverade ord, tabeller och fältnamn från SQL i tabeller. När du är klar med frågan klickar du på **Spela** upp för att köra frågan. Fliken *Konsol* under redigeraren visar vad frågetjänsten gör just nu, vilket anger när en fråga har returnerats. Fliken *Resultat* , bredvid konsolen, visar frågeresultat. Mer information om hur du använder frågeredigeraren finns i [Frågeredigeringsguiden][query-editor] .

![Bild](../images/queries/ui-overview/query-editor.png)

## Bläddra

På fliken *Bläddra* visas frågor som sparats av användare i din organisation. Det är praktiskt att tänka på dessa som frågeprojekt, eftersom frågor som sparas här fortfarande kan vara under uppbyggnad. Frågor som visas på fliken *Bläddra* visas även som körningsfrågor på fliken *Logg* om de tidigare har körts av frågetjänsten.

![Bild](../images/queries/ui-overview/browse.png)

| Kolumn | Beskrivning |
| --- | --- |
| Namn | Frågenamnet som har skapats av användaren. Du kan klicka på namnet för att öppna frågan i Frågeredigeraren. Du kan också använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| SQL | De första tecknen i SQL-frågan. Om du placerar pekaren över koden visas hela frågan. |
| Ändrad av | Den sista användaren som ändrade frågan. Alla användare i organisationen som har tillgång till frågetjänsten kan ändra frågor. |
| Senast ändrad | Datum och tid för den senaste ändringen av frågan, i webbläsarens tidszon. |

## Logg

Fliken *Logg* innehåller en lista med frågor som tidigare har körts. Som standard visas frågorna i loggen i omvänd kronologi.

![Bild](../images/queries/ui-overview/log.png)

| Kolumn | Beskrivning |
| --- | --- |
| Namn | Frågenamnet som består av de första tecknen i SQL-frågan. Om du klickar på namnet öppnas frågeredigeraren så att du kan redigera frågan. Du kan använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| Skapad av | Namnet på den person som skapade frågan. |
| Klient | Klienten som används för frågan. |
| Datauppsättning | Den indatamängd som används av frågan. Klicka på datauppsättningen för att gå till skärmen med information om indatauppsättningar. |
| Status | Frågans aktuella status. |
| Senaste körning | När frågan kördes senast. Du kan sortera listan i stigande eller fallande ordning genom att klicka på pilen över den här kolumnen. |
| Körningstid | Hur lång tid det tog att köra frågan. |

## Autentiseringsuppgifter

På fliken *Autentiseringsuppgifter* visas dina autentiseringsuppgifter för Postgres. Klicka på ikonen **Kopiera** bredvid ett fält för att lagra innehållet i tangentbordsbufferten. Mer information om hur du använder dessa autentiseringsuppgifter för att ansluta till externa klienter finns i [handboken][connect-clients]för att ansluta till klienter.

![Bild](../images/queries/ui-overview/credentials.png)

## Nästa steg

Nu när du är bekant med användargränssnittet i Query Service på Platform kan du öppna Query Editor och börja skapa egna frågeprojekt som du kan dela med andra användare i organisationen. Mer information om hur du redigerar och kör frågor i Frågeredigeraren finns i användarhandboken [för][query-editor]Frågeredigeraren.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
