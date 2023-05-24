---
title: Jämför resursändringar
description: Lär dig hur du visar ändringshistoriken för en taggresurs i Adobe Experience Platform.
exl-id: 95b22641-9f6f-4aac-a727-d99098f040a4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Jämför resursrevisioner

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Jämför resursrevisioner för att se historiken för en enskild resurs.  Du kan jämföra resursens aktuella tillstånd med äldre versioner eller jämföra den publicerade versionen av en resurs med den senaste uppsättning ändringar som har sparats.

## Starta en jämförelse

Att starta en jämförelse är detsamma för alla resurstyper.  Öppna redigeringsvyn för en enskild resurs och leta sedan upp ikonen med tre punkter bredvid ikonen **[!UICONTROL Save]** om du vill visa tillgängliga åtgärder för resursen.  Välj **[!UICONTROL Compare Revisions]** från listan.

![Starta en jämförelse för ett tillägg](../../images/compare-initiate-extension.png)

För tillägg öppnar du detaljvyn genom att välja **[!UICONTROL Configure]** när du visar en lista över installerade tillägg.  För dataelement och regler väljer du ett i listan.

## Använda Jämförelsevisning

När du startar en jämförelse visar standardvyn den senaste versionen till höger.  Den här versionen innehåller alla osparade ändringar som du har gjort i resursen i redigeringsvyn. (Lägg märke till etiketten&quot;Osparade ändringar&quot; till höger i bilden nedan.)

Till vänster kan du välja mellan alla befintliga versioner att jämföra med&quot;Senaste&quot;.

![Jämföra versioner av Analytics-tillägget](../../images/compare-interpret-extension.png)

Välj **[!UICONTROL Use These Changes]** om du vill kopiera inställningarna från den valda revisionen (vänster) till den senaste versionen (höger).  Detta kopierar inställningarna från den gamla versionen till de senaste osparade ändringarna.  Om du vill att de här ändringarna ska fastna, se till att **[!UICONTROL Save]** när du har avslutat jämförelsevyn.

>[!TIP]
>Enskilda resurser kan ha både attribut och inställningar.  Dessa inställningar lagras som ett JSON-block, som är ett strukturerat sätt att lagra data, men tillräckligt flexibelt så att tilläggsutvecklare kan placera det de behöver för att få sina tillägg att göra vad de vill.
>I den första versionen av jämförelsevyn visas inställningarna i Raw-format som JSON. Framtida förbättringar gör att du kan visa versioner på olika sätt, inklusive detaljerade kodjämförelser och använda tilläggsvyn från tilläggsutvecklarna.

## Jämföra tillägg

Tillägg har en enda skärm som visar skillnaderna mellan versionerna.

I Jämförelsevisning markeras skillnader mellan inställningsversioner.  Tillägg och borttagningar till enskilda inställningar indikeras av en expansion av en linje i båda riktningarna.

![Jämföra olika versioner av Analytics-tillägget](../../images/compare-extension.png)

Ovanför ser du följande ändringar:

* The [!DNL Adobe Analytics] tillägget uppdateras till en ny version, vilket anges av det orange versionsnumret högst upp.
* The `orgID` och `currencyCode` ändras till de inställningar som anges av utökningen av den orangefärgade delen i inställningarna.

## Jämföra dataelement

Dataelementen har en enda skärm för att visa skillnader, men eftersom dataelementen har ytterligare attribut utöver sina inställningar visas ytterligare information.  Attribut som har ändrats markeras med orange.

![Jämföra olika versioner av ett dataelement](../../images/compare-data-element.png)

Ovanför ser du följande ändringar:

* Namnet har ändrats från &quot;Sidnamn 2&quot; till &quot;Mitt specialsidnamn&quot;, vilket anges av den orange listen.
* Typen har ändrats från JavaScript-variabel till Sidinformation.
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
* The &quot;[!DNL Adobe Analytics] - Åtgärden Rensa variabler har tagits bort, vilket anges av den orangefärgade &quot;-&quot; ikonen och frånvaron av komponenten på den högra sidan.
* The &quot;[!DNL Adobe Analytics] - Åtgärden Ange variabler har ändrats, vilket anges av den orange linjen mellan komponentversionerna på vänster och höger sida. Den här linjen är rak om komponentordningen inte har ändrats.
* The &quot;[!DNL Adobe Analytics] - Ange variabler och[!DNL Adobe Analytics] - Åtgärdsordningen Skicka signal har ändrats, vilket indikeras av de böjda linjerna som förbinder de olika komponentversionerna på vänster och höger sida

Om du vill visa specifika ändringar i en av regelkomponenterna markerar du den specifika komponent som du vill visa.  Linjen ändras till blå när du för musen över den.

![Markera komponenten som du vill se mer i detalj](../../images/compare-rule-component-click.png)

Jämförelsen för en enskild regelkomponent fungerar på samma sätt som jämförelsen för ett dataelement.

![Jämföra olika versioner av en enskild regelkomponent](../../images/compare-rule-component.png)

Ovanför ser du följande ändring:

* Regelkomponenten har ändrats till add eVar2 med värdet &quot;1&quot;.

Om inställningsblocket är stort kan du expandera inställningsavsnittet så att det syns bättre.
