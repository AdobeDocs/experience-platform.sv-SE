---
title: Jämför resursändringar
description: Lär dig hur du visar ändringshistoriken för en taggresurs i Adobe Experience Platform.
exl-id: 95b22641-9f6f-4aac-a727-d99098f040a4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Jämför resursrevisioner

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Jämför resursrevisioner för att se historiken för en enskild resurs.  Du kan jämföra resursens aktuella tillstånd med äldre versioner eller jämföra den publicerade versionen av en resurs med den senaste uppsättning ändringar som har sparats.

## Starta en jämförelse

Att starta en jämförelse är detsamma för alla resurstyper.  Öppna redigeringsvyn för en enskild resurs och leta sedan upp ikonen med tre punkter bredvid knappen **[!UICONTROL Save]** för att visa tillgängliga åtgärder för den resursen.  Välj **[!UICONTROL Compare Revisions]** i listan.

![Starta en jämförelse för ett tillägg](../../images/compare-initiate-extension.png)

För tillägg öppnar du detaljvyn genom att klicka på knappen **[!UICONTROL Configure]** när du visar listan över installerade tillägg.  För dataelement och regler väljer du ett i listan.

## Använda Jämförelsevisning

När du startar en jämförelse visas den senaste versionen till höger i standardvyn.  Den här versionen innehåller alla ändringar som du har gjort för resursen i redigeringsvyn. (Lägg märke till etiketten&quot;Osparade ändringar&quot; till höger i bilden nedan.)

Till vänster kan du välja mellan alla befintliga versioner att jämföra med&quot;Senaste&quot;.

![Jämför versioner av Analytics-tillägget](../../images/compare-interpret-extension.png)

Välj **[!UICONTROL Use These Changes]** om du vill kopiera inställningarna från den valda revisionen (vänster) till den senaste versionen (höger).  Detta kopierar inställningarna från den gamla versionen till de senaste osparade ändringarna.  Om du vill att de här ändringarna ska fastna måste du se till att **[!UICONTROL Save]** är kvar när du har avslutat jämförelsevyn.

>[!TIP]
>Enskilda resurser kan ha både attribut och inställningar.  Dessa inställningar lagras som ett JSON-block, som är ett strukturerat sätt att lagra data, men tillräckligt flexibelt så att tilläggsutvecklare kan placera det de behöver för att få sina tillägg att göra vad de vill.
>I den första versionen av jämförelsevyn visas inställningarna i Raw-format som JSON. Framtida förbättringar gör att du kan visa versioner på olika sätt, inklusive detaljerade kodjämförelser och använda tilläggsvyn från tilläggsutvecklarna.

## Jämföra tillägg

Tillägg har en enda skärm som visar skillnaderna mellan versionerna.

I Jämförelsevisning markeras skillnader mellan inställningsversioner.  Tillägg och borttagningar till enskilda inställningar indikeras av en expansion av en linje i båda riktningarna.

![Jämför olika versioner av Analytics-tillägget](../../images/compare-extension.png)

Ovanför ser du följande ändringar:

* Tillägget [!DNL Adobe Analytics] uppdateras till en ny version, vilket anges av de orange versionsnumren högst upp.
* `orgID` och `currencyCode` har ändrats till de inställningar som anges av utökningen av den orange sektionen i inställningarna.

## Jämföra dataelement

Dataelementen har en enda skärm för att visa skillnader, men eftersom dataelementen har ytterligare attribut utöver sina inställningar visas ytterligare information.  Attribut som har ändrats markeras med orange.

![Jämföra olika versioner av ett dataelement](../../images/compare-data-element.png)

Ovanför ser du följande ändringar:

* Namnet har ändrats från &quot;Sidnamn 2&quot; till &quot;Mitt specialsidnamn&quot;, vilket anges av den orange listen.
* Typen har ändrats från JavaScript Variable till Sidinformation.
* Standardvärdet för b har lagts till.
* &quot;Tvinga gemener&quot; har valts.
* &quot;Ren text&quot; har valts.
* Inställningarna har ändrats. (Inställningarna för JavaScript-variabeltypen skiljer sig från sidinformationstypen.)

Om inställningsblocket är stort kan du expandera inställningsavsnittet så att det syns bättre.

## Jämföra regler

Regler består av många regelkomponenter.  Om du vill förstå ändringarna av en regel måste du veta mer om hur du lägger till och tar bort komponenter samt om hur du ändrar en enskild komponent.  När du jämför olika versioner av en regel finns det alltså två skärmar.

På den första skärmen visas en högnivåvy, som markerar ändringar i ordningen för regelkomponenter.  Ändringarna markeras. Flera olika typer av ändringar visas.

![Jämföra olika versioner av en regel](../../images/compare-rule.png)

Ovanför ser du följande ändringar:

* Regelnamnet har ändrats från Analytics (Analys) till Baseline Analytics (Baslinjeanalys), vilket anges av den orange raden med Name (Namn).
* Villkoret &quot;Core - Domain&quot; lades till, vilket anges av den orange &quot;+&quot;-ikonen och komponentens tillägg på den högra sidan.
* Åtgärden [!DNL Adobe Analytics] - Rensa variabler har tagits bort, vilket anges av den orangefärgade ikonen - och att komponenten inte finns på den högra sidan.
* Åtgärden [!DNL Adobe Analytics] - Ange variabler har ändrats, vilket anges av den orange linjen mellan komponentversionerna på vänster och höger sida. Den här linjen är rak om komponentordningen inte har ändrats.
* Åtgärden [!DNL Adobe Analytics] - Ange variabler och åtgärdsordningen [!DNL Adobe Analytics] - Skicka fyr har ändrats, vilket anges av de kurvor som förbinder de olika versionerna av komponenterna på vänster och höger sida

Om du vill visa specifika ändringar i en av regelkomponenterna markerar du den specifika komponent som du vill visa.  Linjen ändras till blå när du för musen över den.

![Markera den komponent som du vill se mer i detalj](../../images/compare-rule-component-click.png)

Jämförelsen för en enskild regelkomponent fungerar på samma sätt som jämförelsen för ett dataelement.

![Jämföra olika versioner av en enskild regelkomponent](../../images/compare-rule-component.png)

Ovanför ser du följande ändring:

* Regelkomponenten har ändrats till att lägga till eVar2 med värdet &quot;1&quot;.

Om inställningsblocket är stort kan du expandera inställningsavsnittet så att det syns bättre.
