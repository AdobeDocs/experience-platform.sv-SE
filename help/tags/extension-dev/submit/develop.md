---
title: Utveckla ett tillägg
description: Det här dokumentet innehåller en allmän översikt över tagghanteringsprocessen med länkar till ytterligare dokumentation för mer detaljerade processer.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Utveckla ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Ett taggtillägg ska betraktas som en (liten) produkt med egna krav. Om du fastställer hur en Adobe Experience Platform-användare ska använda tillägget kan det hjälpa dig att sortera funktionaliteten efter vilka händelsetyper, villkorstyper, åtgärdstyper och dataelementtyper som tillägget ska innehålla.

Med den kunskapen kan du planera vilka komponenter som ska ingå i tillägget.

## Stödlinjer

Med en plan på plats kan dessa guider hjälpa dig att förstå utvecklingsprocessen för tillägg:

* Guiden [Komma igång](../getting-started.md) och andra dokument under **Tilläggsutveckling** i den vänstra navigeringen är bra referensmaterial för att förstå tillägg. De innehåller information om vad tillägg kan göra, hur användarinformation lagras och skickas mellan tillägget och Adobe Experience Platform, hur koden paketeras i bibliotek och hur tilläggskoden tolkas och används vid körning i webbläsaren.
* Självstudievideon [för tillägg](https://youtu.be/rxjtC9o4rl0) är en bra startpunkt.
* [Introduktion till tillägg](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube spellista går igenom processen att skapa tilläggspaket.
* [Förstå JSON-](https://spacetelescope.github.io/understanding-json-schema/index.html#) schemartikeln.
* [JSON Lint/Validator](http://jsonlint.com/).
* [JSON ](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) ViewerChrome-tillägg för att markera och skriva ut JSON &amp; JSONP.
* [jsonschema.](https://jsonschema.net/#/editor) neteditor för att skapa JSON-schema från ditt objekt.
* [JSON Schema ](http://www.jsonschemavalidator.net/) ValidatorEn interaktiv JSON Schema-validerare online.

## Verktyg

Det finns också ett antal nPM-verktyg som du kan använda för att utveckla tilläggspaket:

* [Med ](https://www.npmjs.com/package/@adobe/reactor-scaffold) verktyget för taggtillägg kan du enkelt skapa ett startprojekt på den lokala datorn.
* [Med ](https://www.npmjs.com/package/@adobe/reactor-sandbox) sandlådan Tag Extension kan du validera dina tilläggsvyer och moduler på din lokala dator.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packagerär ett kommandoradsverktyg som paketerar ett taggtillägg i en zip-fil.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploader är ett interaktivt kommandoradsverktyg som du kan använda för att ange inloggningsuppgifter för ditt tekniska konto och överföra tilläggspaketet till taggar.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-releaser) Releaserär ett interaktivt kommandoradsverktyg som hjälper dig att göra tillägget tillgängligt privat.

## Exempel på tillägg

Det finns exempeltillägg för GitHub som du kan granska eller använda som startprojekt:

* [Exempeltillägg för Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook exempeltillägg](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Exempeltillägg för Typekit](https://github.com/jeffchasin/extension-typekit)
* [Pinterest exempeltillägg](https://github.com/jeffchasin/extension-pinterest)

## Slack arbetsyta

Du kan begära åtkomst till Slack-communityarbetsytan där tilläggsförfattare kan stödja varandra med hjälp av det här [begärandeformuläret](http://join.launchdevelopers.chat).

**Obs**! även om det finns medlemmar i Adobe på den här arbetsytan i Slack är det en community-resurs som inte sponsras eller modereras av Adobe.
