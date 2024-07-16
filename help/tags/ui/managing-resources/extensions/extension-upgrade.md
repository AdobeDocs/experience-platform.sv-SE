---
title: Tillägg - uppgraderingar
description: Lär dig hur tilläggsuppgraderingar paketeras och representeras i tilläggskatalogen.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Tillägg - uppgraderingar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Tilläggsutvecklare lägger ständigt till nya funktioner i sina tillägg och åtgärdar ofta fel. Dessa uppdateringar paketeras i nya versioner av ett tillägg och görs tillgängliga i tilläggskatalogen som uppgraderingar.

## Tilläggskatalog

När en tilläggsutvecklare har tillhandahållit en ny version av tillägget blir den nya versionen tillgänglig i tilläggskatalogen. Katalogen visar bara den senaste versionen av ett tillägg. Du kan inte installera någon annan tilläggsversion än `latest`.

När du installerar ett tillägg i din egenskap installeras den version som är tillgänglig för tillfället, och din egenskap behålls med den specifika versionen från den tidpunkten och framåt, även om nyare versioner läggs till i katalogen.

## Uppgraderingsmeddelanden

När du har installerat ett tillägg för din egenskap och en nyare version är tillgänglig i katalogen visas knappen [!UICONTROL Upgrade] på tilläggskortet när du visar sidan Installerade tillägg.

Du kommer också att se ett meddelande när du redigerar resurser som ingår i det tillägget.

## Uppgraderingarna är permanenta

Om du vill uppgradera till en nyare version som är tillgänglig i katalogen måste du installera den uppgraderingen själv. En uppgradering är en&quot;ändring&quot; som måste läggas till i ett bibliotek, testas och publiceras innan den påverkar dina driftsatta taggar.

Uppgraderingen bör inte tas lätt. Du bör inte uppgradera om du inte är redo att testa det nya tillägget och är redo att distribuera det. När uppgraderingen har lagts till i din egenskap måste den ingå i alla bibliotek. Alla bibliotek som inte innehåller det uppgraderade tillägget misslyckas vid byggtillfället.

Det finns för närvarande ingen möjlighet att nedgradera tillägget till en tidigare version. När du har uppgraderat (oavsett om du publicerar eller inte) finns den nya tilläggsversionen kvar på din egendom.

## Uppgraderingsprocess

Att installera en uppgradering är ungefär detsamma som att installera tillägget för första gången.

1. Välj **[!UICONTROL Upgrade]** om du vill gå till skärmen [!UICONTROL Extension Configuration].
1. Gör de konfigurationsändringar du vill.
1. Välj **[!UICONTROL Save]**.

Uppgraderingen utförs inte förrän du trycker på **[!UICONTROL Save]**. Du kan när som helst före detta välja [!UICONTROL Cancel] och behålla den installerade versionen. Markering av **[!UICONTROL Save]** är punkten där inget returneras.

Tilläggsuppgraderingar tillåts inte om du har ett bibliotek i läget `Approved` eller `Submitted`.  Detta beror på att nästa version måste innehålla den nya tilläggsversionen.  För ett bibliotek som är `Approved` eller `Submitted` är nästa version produktionsbygget.  Det bygget misslyckas eftersom det inte innehåller den senaste versionen, så arbetsflödet är att publicera eller avvisa bibliotek i `Approved`- eller `Submitted`-läget _innan_ tillägget uppgraderas.

## Publicera en uppgradering

När det uppgraderade tillägget har installerats på din egenskap måste du inkludera det i alla bibliotek från och med den tidpunkten. Ett felmeddelande om byggfel visas för alla bibliotek som inte innehåller det.

Dessutom är det samma sak att lägga till det uppgraderade tillägget i ditt bibliotek som att [lägga till andra ändringar](../../publishing/libraries.md) i ett bibliotek.

På skärmen [!UICONTROL Edit Library] kan du använda knappen [!UICONTROL Add All Changed Resources] eller så kan du använda knappen [!UICONTROL Add a Resource] och välja det uppgraderade tillägget separat.

>[!TIP]
>
>Tilläggsutvecklare kan lägga till nya konfigurationsobjekt i sina tilläggsvyer för att aktivera nya funktioner.  Om du ser byggfel efter att ha uppgraderat till en ny tilläggsversion - och du har isolerat för att skapa fel i det tillägget - går du först till Tilläggets konfigurationssida och ser till att spara (även om du inte har ändrat något).  Lägg sedan till den nya ändringen i biblioteket och försök skapa igen.

När du har lagt till tilläggsuppgraderingen i biblioteket kan du följa stegen som beskrivs i [publiceringsflödet](../../publishing/publishing-flow.md) för att publicera biblioteket till Production.
