---
title: Kopiera resurser
description: Lär dig hur du skapar en ny taggresurs med inställningarna för en befintlig taggresurs i Adobe Experience Platform.
exl-id: 7e52ceae-97df-4c64-aba3-4f5ba6018a47
source-git-commit: 319496975bcdbfd0a670cf8d36fb7e562b2ef2de
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 5%

---

# Kopiera resurser

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Ibland kan det vara praktiskt att skapa en ny resurs med inställningarna för en befintlig resurs. I så fall kan du göra en kopia.

Egenskaper, tillägg, regler och dataelement kan kopieras.

Om du kopierar en resurs skapas en dubblett av den resursen i det angivna målet. Detta är en diskret engångsåtgärd och det finns ingen pågående relation mellan den ursprungliga resursen och eventuella kopior som gjorts.

## Initiera en kopia

Du kan initiera en kopia av ett tillägg genom att visa dina installerade tillägg, markera listrutepilen på knappen **[!UICONTROL Configure]** och välja **[!UICONTROL Copy]**.

![Kopierar analystillägget](../../images/copy-initiate-extension.png)

För egenskaper, regler och dataelement markerar du bara den resurs som du vill kopiera och väljer sedan **[!UICONTROL Copy]** på Åtgärder-menyn.

![Kopierar min analysregel](../../images/copy-initiate-rule.png)

Om du kopierar en regel eller ett dataelement kan du använda listrutan i kopieringsdialogrutan för att välja en målegenskap som du vill kopiera till (standardinställningen är den aktuella egenskapen). Det går inte att kopiera tillägg till samma egenskap, vilket innebär att de inte innehåller det alternativet.

>[!NOTE]
>
>Det går inte att kopiera resurser till en annan egenskap om en egenskap är konfigurerad för tilläggsutveckling och den andra inte är det.

När du har konfigurerat det beteende du vill använda väljer du **[!UICONTROL Copy]**.

## Kopiera egenskaper

När du gör en kopia av en fullständig egenskap finns det några saker du bör känna till om processen.

>[!IMPORTANT]
>
>Resurser som använder variabeltypen för uppdatering av dataelement kräver ytterligare steg efter kopiering. Redigera varje åtgärd för att uppdatera variabeln, ändra ett värde i data- eller XDM-objektet och spara ändringarna. Det publicerade biblioteket ska sedan fungera som förväntat. Kontakta teknisk support om du har frågor om den här processen.

* Egenskapsinställningarna kopieras exakt som de är (domäner, avancerade inställningar osv.)
* Regler, dataelement och tillägg från egenskapen origin kopieras till den nya egenskapen target.  Adaptrar, miljöer och bibliotek kopieras inte.
* Nödvändiga tillägg (tillägg som krävs av befintliga dataelement eller regelkomponenter) kopieras till egenskapen target även om de har avinstallerats från egenskapen origin.
* Det kan ta en stund att kopiera en egenskap.  Detta händer i bakgrunden.  Du kan övervaka kopians förlopp eller fortsätta med andra åtgärder medan den utförs.
* Om du ändrar en enskild resurs efter att den redan har kopierats till målegenskapen (men innan kopian har slutförts) kopieras inte de nya ändringarna.

## Kopierar tillägg

När du kopierar ett tillägg till en annan egenskap finns det några saker som du bör förstå.

* Om målegenskapen inte har tillägget installerat installeras det med samma inställningar som egenskapen origin.
* Om målegenskapen redan har tillägget installerat kopieras bara inställningarna.
* Om målegenskapen har en lägre version av tillägget installerad får du ett meddelande om att du måste uppgradera tillägget för målegenskapen innan du kan utföra kopieringen.  Tilläggsutvecklare kan lägga till inställningar i sina tillägg över tiden, så inställningar från ett nyare tillägg kan inte tillämpas på ett tillförlitligt sätt på äldre versioner.
* Om målegenskapen har en senare version av tillägget installerad kopieras inställningarna över, men ingen nedgradering utförs.  Destinationsegenskapen behåller fortfarande sitt aktuella versionsnummer.

## Kopiera regler och dataelement

Alla regler och dataelement tillhandahålls av ett tillägg, så när du kopierar mellan egenskaper måste Experience Platform ta hänsyn till dessa underliggande tillägg.

![Kopierar en regel till min demoegenskap](../../images/copy-rules-dialog1.png)

I dialogrutan Kopiera ges en förklaring av exakt vad som kommer att hända innan du börjar kopiera. Ovanstående dialogruta är för en regel, men samma gäller för dataelement.

1. **Tillägg som krävs av dessa regler kopieras.** Detta visar att nödvändiga tillägg följer regeln.  Dessa kopior följer samma regler som en vanlig tilläggskopia som beskrivs ovan.
1. **Tilläggsinställningar kopieras INTE om tillägget redan är installerat.** Det innebär att om de nödvändiga tilläggen redan finns i målegenskapen ändras inte tillägget.  Om du även vill kopiera tilläggsinställningarna kan du använda växlingsknappen **Ersätt tilläggsinställningar för målegenskap** och förklaringen uppdateras därefter.
1. **Dataelement som krävs av dessa regler kopieras INTE.** Den här förklaringen gäller endast regler.  Regler förlitar sig ofta på dataelement för att fungera korrekt.  Om du kopierar en regel till en ny egenskap måste du också kopiera alla nödvändiga dataelement som en separat åtgärd.
