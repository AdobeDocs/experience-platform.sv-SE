---
title: Anteckningar
description: Lär dig hur du lägger till textanteckningar i vissa taggresurser i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Anteckningar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Anteckningar är textanteckningar som du kan lägga till i vissa taggresurser i Adobe Experience Platform. Anteckningar kan bifogas följande resurser:

* Tillägg
* Dataelement
* Regler
* Regelkomponenter
* Bibliotek
* Egenskaper

Anteckningar kan innehålla upp till 512 Unicode-tecken.

Anteckningar är kommentarer som inte har någon effekt på beteendet för de resurser de är kopplade till. De ingår inte i byggbiblioteken.  Du kan använda anteckningar för att:

* Ange bakgrundsinformation för en resurs
* Funktion som att göra-lista för framtida förbättringar
* Skicka resursanvändningsråd till andra användare
* Ge instruktioner till andra teammedlemmar
* Posthistorik
* Påminn dig själv om vad en resurs gör, varför den har byggts som den är eller var den används

## Skapa en anteckning

Anteckningsbara resurser har en smal skena till höger på skärmen.  Rälen innehåller en ikon för anteckningar.  Den här ikonen visar det aktuella antalet anteckningar som är kopplade till resursen.

Välj **[!UICONTROL Notes]** om du vill expandera den högra listen och visa anteckningarna, med de senaste anteckningarna överst.  Om du vill lägga till en ny anteckning anger du anteckningstexten i rutan längst upp och väljer **[!UICONTROL Add Note]**.

## Övriga

* Anteckningar om taggresurser matchar anteckningarna i DTM, eftersom de inte kan ändras och inte kan redigeras eller tas bort.
* När du visar äldre versioner av en resurs visas endast de anteckningar som skapades före den revisionens `created_at`-datum.
* När du tar bort en resurs tas även alla anteckningar som är kopplade till resursen bort.
