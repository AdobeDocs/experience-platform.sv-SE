---
title: Anteckningar
description: Lär dig hur du lägger till textanteckningar i vissa taggresurser i Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Anteckningar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

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
* Registrera historik
* Påminn dig själv om vad en resurs gör, varför den har byggts som den är eller var den används

## Skapa en anteckning

Anteckningsbara resurser har en smal skena till höger på skärmen.  Rälen innehåller en ikon för anteckningar.  Den här ikonen visar det aktuella antalet anteckningar som är kopplade till resursen.

Välj **[!UICONTROL Notes]** om du vill expandera den högra listen och visa anteckningarna, med de senaste anteckningarna överst.  Om du vill lägga till en ny anteckning anger du anteckningstexten i rutan längst upp och väljer **[!UICONTROL Add Note]**.

## Övriga

* Anteckningar om taggresurser matchar anteckningarna i DTM, eftersom de inte kan ändras och inte kan redigeras eller tas bort.
* När äldre versioner av en resurs visas endast de anteckningar som skapades före den revisionens `created_at`-datum.
* När du tar bort en resurs tas även alla anteckningar som är kopplade till resursen bort.
