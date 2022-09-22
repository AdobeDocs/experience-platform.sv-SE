---
title: Ta bort resurser
description: Lär dig hur du tar bort taggresurser i Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Ta bort resurser

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Att ta bort en resurs är en permanent borttagning av den från Adobe Experience Platform. Om du fortfarande vill att resursen ska visas i användargränssnittet för datainsamling, men inte i taggbiblioteket, kan du läsa [Ta bort resurser från ett bibliotek](remove-resources-from-library.md).

Du kan ta bort dataelement, regler, tillägg, värdar, miljöer och egenskaper. När resurserna har tagits bort går de inte att återställa.

Resurser som läggs till i bibliotek (dataelement, regler och tillägg) har särskild betydelse när du tar bort dem.

## Förbered en resurs för borttagning

Resurser finns i olika lägen och de är beroende av varandra. Innan du tar bort en resurs måste du se till att den är i ett läge där den kan tas bort.

Förbereda en resurs för borttagning består av två grundläggande steg:

1. Lös beroenden.
1. Ta bort från bibliotek.

### Lös beroenden

Regler, dataelement och tillägg är beroende av varandra, så oftast när du tar bort en effekt uppstår en överlappande effekt och du har andra saker du behöver ta bort.

#### Regler

Regler är beroende av andra resurser (tillägg och dataelement), men de har inga resurser som är beroende av dem. Om du tar bort en regel kan du inte längre använda den i ett bibliotek eller ens visa den, men du kommer inte att ha några beroenden att rensa upp efteråt.

#### Dataelement

Dataelement är beroende av tillägg, men till skillnad från regler kan dataelement ha regler och tillägg som är beroende av dem. Om du tar bort ett dataelement påverkas alla regler och tillägg som är beroende av det här dataelementet.

När dataelementet tagits bort returneras inte längre korrekt värde vid körning. Antingen returneras en tom sträng eller så returneras namnet på det borttagna dataelementet i %% (exempel: `%data-element-name%`). Det här beteendet kan konfigureras i egenskapsinställningarna.

Du kan lösa dessa beroenden före eller efter att du har tagit bort dataelementet.

#### Tillägg

Alla andra resurser (regler, regelkomponenter och dataelement) tillhandahålls av tillägg.

Regelkomponenter och dataelement är beroende av tillägg för deras beteende, men visas även i användargränssnittet för datainsamling. Om du tar bort tillägget innan du löser beroenden kan du inte längre visa dessa överblivna resurser. De överblivna resurserna visas i listvyer, men du får ett felmeddelande när du försöker öppna detaljvyn.

Därför bör du vara mycket försiktig när du tar bort tillägg och du bör lösa beroenden innan du tar bort dem.

### Ta bort från bibliotek

Innan du kan ta bort en resurs måste du ta bort den från alla bibliotek där den finns. Den här processen skiljer sig åt beroende på bibliotekets tillstånd.

#### Utveckling

1. Öppna biblioteket.
1. Ta bort resursen.
1. Spara biblioteket.
1. Ta bort resursen.

#### Skickat eller godkänt

1. Avvisa biblioteket (flyttar det tillbaka till Development).
1. Följ stegen ovan för att ta bort en resurs från ett utvecklingsbibliotek.

#### Produktion

1. Inaktivera resursen.
1. Publicera den inaktiverade resursen till Production.
1. Ta bort resursen.

## Ta bort en resurs

I lämplig listvy väljer du den resurs du vill ta bort och väljer sedan **[!UICONTROL Delete]**.
