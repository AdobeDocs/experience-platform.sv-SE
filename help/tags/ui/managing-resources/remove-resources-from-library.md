---
title: Ta bort resurser från ett bibliotek
description: Lär dig hur du tar bort resurser från ett taggbibliotek.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Ta bort resurser från ett bibliotek

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

När du inte längre vill att en resurs ska ha en effekt i ett bygge måste du ta bort den från biblioteket som innehåller resursen och skapa ett nytt bygge.

>[!IMPORTANT]
>
>Resurser i bibliotek är beroende av varandra. Om du tar bort en resurs från ett bygge kan beteendet för andra resurser i bygget ändras.

Borttagningsprocessen fungerar lite annorlunda beroende på vilket läge biblioteket är i.

## Utvecklingsbibliotek

Resurser i utvecklingsbibliotek kan ändras direkt.

1. Öppna biblioteket.
1. Ta bort resursen.
1. Spara biblioteket.
1. Bygg biblioteket.

## Skickade och godkända bibliotek

Resurser som finns i skickade eller godkända bibliotek kan inte ändras direkt. Du måste flytta tillbaka biblioteket till utvecklingstillståndet.

1. Avvisa biblioteket (flyttar tillbaka biblioteket till Development).
1. Följ stegen i Utvecklingsbibliotek ovan för att ta bort resurser från Utvecklingsbibliotek.

## Produktionsbibliotek

Att ta bort resurser från ett produktionsbibliotek är det mest komplexa fallet. Du kan inte ändra biblioteksresurserna i det här läget och du kan inte heller flytta tillbaka dessa bibliotek till utvecklingstillståndet.

Du måste i stället inaktivera resursen. Den här inaktiveringen är en ändring som du sedan lägger till i ett utvecklingsbibliotek precis som andra ändringar. När den här ändringen har placerats i produktion flyttas resursen från ditt produktionsbibliotek.

1. Inaktivera resursen.
   1. Välj resursen i listvyn.
   1. Välj **[!UICONTROL Disable]**.
1. Skapa ett nytt utvecklingsbibliotek.
1. Lägg till `latest`-versionen av den inaktiverade resursen.
1. Spara och bygg.
1. Följ den normala processen för att marknadsföra bibliotek till produktion.
1. Publicera i produktion för att ta bort resursen.
