---
title: Utveckla ett tillägg
description: Det här dokumentet innehåller en allmän översikt över tagghanteringsprocessen med länkar till ytterligare dokumentation för mer detaljerade processer.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Utveckla ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Ett taggtillägg ska betraktas som en (liten) produkt med egna krav. Om du fastställer hur en Adobe Experience Platform-användare ska använda tillägget kan det hjälpa dig att sortera funktionaliteten efter vilka händelsetyper, villkorstyper, åtgärdstyper och dataelementtyper som tillägget ska innehålla.

Med den kunskapen kan du planera vilka komponenter som ska ingå i tillägget.

## Användarhandböcker

Med en plan på plats kan dessa guider hjälpa dig att förstå utvecklingsprocessen för tillägg:

* Guiden [Komma igång](../getting-started.md) och andra dokument under **Tilläggsutveckling** i den vänstra navigeringen är bra referensmaterial för att förstå tillägg. De innehåller information om vad tillägg kan göra, hur användarinformation lagras och skickas mellan tillägget och Adobe Experience Platform, hur koden paketeras i bibliotek och hur tilläggskoden tolkas och används vid körning i webbläsaren.
* Självstudievideon [för tillägg ](https://youtu.be/rxjtC9o4rl0) är en bra startplats.
* YouTube-spellistan [Introduktion till tillägg](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) går igenom processen med att skapa tilläggspaket.
* [Förstå JSON-schemaartikel](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](https://jsonlint.com/).
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome-tillägg för att markera och skriva ut JSON &amp; JSONP.
* [jsonschema.net](https://jsonschema.net/#/editor)-redigerare som hjälper dig att skapa JSON-schema från ditt objekt.
* [JSON-schemaverifierare](https://www.jsonschemavalidator.net) En interaktiv JSON-schemavaliderare online.

## Verktyg

Det finns också ett antal nPM-verktyg som du kan använda för att utveckla tilläggspaket:

* [Med verktyget för taggtillägg ](https://www.npmjs.com/package/@adobe/reactor-scaffold) kan du enkelt skapa ett startprojekt på den lokala datorn.
* [Tag Extension Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) hjälper dig att validera dina tilläggsvyer och moduler på din lokala dator.
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) är ett kommandoradsverktyg som används för att paketera ett taggtillägg i en zip-fil.
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader) är ett interaktivt kommandoradsverktyg som du kan använda för att ange autentiseringsuppgifter för ditt tekniska konto och överföra tilläggspaketet till taggar.
* [Tagg Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) är ett interaktivt kommandoradsverktyg som hjälper dig att frigöra tillägget till privat tillgänglighet.

## Exempel på tillägg

Det finns exempeltillägg för GitHub som du kan granska eller använda som startprojekt:

* [Hello World-exempeltillägg](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook exempeltillägg](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Exempeltillägg för Typekit](https://github.com/jeffchasin/extension-typekit)
* [Pinterest exempeltillägg](https://github.com/jeffchasin/extension-pinterest)

## Slack arbetsyta

Du kan begära åtkomst till Slack-communityarbetsytan där tilläggsförfattare kan stödja varandra med hjälp av det här [begärandeformuläret](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Obs!** Även om det finns medlemmar i Adobe på den här arbetsytan i Slack är det en community-resurs som inte sponsras eller modereras av Adobe.
