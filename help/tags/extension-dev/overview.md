---
title: Översikt över tilläggsutveckling
description: Lär dig mer om de primära komponenterna för olika taggtilläggstyper och tilläggsutvecklingsprocessen i Adobe Experience Platform.
source-git-commit: 421d1d0660c4c9c7280974f8a812a8f0e4f7cbea
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Översikt över tilläggsutveckling

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Ett av de främsta målen med Adobe Experience Platform är att skapa ett öppet ekosystem där ingenjörer utanför kärnteamet kan visa upp ytterligare funktionalitet med hjälp av taggar. Detta görs via taggtillägg. När ett tillägg har installerats på en taggegenskap av en användare, blir det tilläggets funktioner tillgängliga för alla användare av egenskapen.

I det här dokumentet beskrivs de primära komponenterna för olika tilläggstyper och det finns länkar till ytterligare dokumentation som kan hjälpa dig med tilläggsutvecklingsprocessen.

## Biblioteksmoduler

Biblioteksmoduler är delar av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i taggens körningsbibliotek. Beroende på om du utvecklar ett webbtillägg eller ett kanttillägg, skiljer sig de tillgängliga modultyperna och deras användningsfall åt. I följande underavsnitt finns en översikt över modulerna för varje tilläggstyp:

* [Moduler för webbtillägg](#web-modules)
* [Moduler för kanttillägg](#edge-modules)

### Moduler för webbtillägg {#web-modules}

I webbtillägg aktiveras regler via händelser, som sedan kan köra specifika åtgärder om en viss uppsättning villkor uppfylls. Mer information finns i översikten om [modulflöde i webbtillägg](./web/flow.md).

Förutom [kärnmodulerna](./web/core.md) från Adobe kan du definiera följande biblioteksmodultyper i dina webbtillägg:

* [Händelsetyper](#web-event)
* [Villkorstyper](#web-condition)
* [Åtgärdstyper](#web-action)
* [Dataelementtyper](#web-data-element)
* [Delade moduler](#shared)

>[!NOTE]
>
>Mer information om vilket format som krävs för att implementera biblioteksmoduler i webbtillägg finns i [modulformatöversikt](./web/format.md).

#### Händelsetyper {#web-event}

En regelhändelse är en aktivitet som måste inträffa innan en regel aktiveras.

Ett tillägg kan till exempel innehålla en händelsetyp av typen &quot;gest&quot; som letar efter en viss mus- eller pekgest. När gesten är klar utlöses regeln av händelselogiken.

Händelsetyper består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, där användarna kan ändra inställningarna för händelsen och (2) en biblioteksmodul som skickas i biblioteket för tagghantering för att tolka inställningarna och för att se efter att en viss aktivitet inträffar.

[Läs mer](./web/event-types.md)

#### Villkorstyper {#web-condition}

Ett regelvillkor utvärderas efter att en regelhändelse har inträffat. Alla villkor måste returnera true för att regeln ska kunna fortsätta bearbetningen. Undantaget är när användare uttryckligen placerar villkor i en &quot;undantagsbucket&quot;, i vilket fall alla villkor i bucket måste returnera false för att regeln ska fortsätta bearbetningen.

Ett tillägg kan till exempel innehålla villkorstypen &quot;viewport contains&quot;, där användaren kan ange en CSS-väljare. När villkoret utvärderas på klientens webbplats kan tillägget hitta element som matchar CSS-väljaren och returnera om något av dem finns i användarens visningsruta.

Villkorstyperna består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, där användarna kan ändra inställningarna för villkoret, och (2) en biblioteksmodul som skickas från biblioteket för tagghantering för att tolka inställningarna och utvärdera ett villkor.

[Läs mer](./web/condition-types.md)

#### Åtgärdstyper {#web-action}

En regelåtgärd är en åtgärd som utförs efter att regelhändelsen har inträffat och villkoren har godkänts i utvärderingen.

Ett tillägg kan till exempel innehålla en&quot;show support chat&quot;-åtgärdstyp som kan visa en supportchattdialogruta för att hjälpa användare som kan ha problem med utcheckningen.

Åtgärdstyperna består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, som gör att användare kan ändra inställningar för åtgärden och (2) en biblioteksmodul som skickas i biblioteket för tagghantering för att tolka inställningarna och utföra en åtgärd.

[Läs mer](./web/action-types.md)

#### Dataelementtyper {#web-data-element}

Dataelement är i princip alias för datadelar på en sida, oavsett om dessa data hittas i frågesträngsparametrar, cookies, DOM-element eller någon annan plats. Ett dataelement kan refereras av regler och fungerar som en abstraktion för att komma åt dessa datadelar. När platsen för data ändras i framtiden (till exempel från ett DOM-elements `innerHTML` till en JavaScript-variabels värde), kan ett enskilt dataelement konfigureras om medan alla regler som refererar till det dataelementet kan förbli oförändrade.

Med en dataelementtyp kan användarna konfigurera dataelement så att de får tillgång till en datadel på ett visst sätt. Ett tillägg kan t.ex. innehålla ett dataelement av typen&quot;lokal lagringspost&quot;, där användaren kan ange ett lokalt lagringsobjektnamn. När en regel refererar till dataelementet kan tillägget söka efter det lokala lagringsobjektets värde med hjälp av det lokala lagringsobjektets namn som användaren angav när dataelementet konfigurerades.

Dataelementtyper består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, där användarna kan ändra inställningarna för dataelementet, och (2) en biblioteksmodul som skickas i biblioteket för tagghantering för att tolka inställningarna och hämta datadelar.

[Läs mer](./web/data-element-types.md)

#### Delade moduler {#shared}

En delad modul är en modul som visas av ett tillägg och som ska användas av ett annat. Detta kan vara en mycket användbar mekanism för kommunikation mellan tillägg. Tillägg A kan till exempel läsa in en datadel asynkront och göra den tillgänglig för tillägg B via ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Delade moduler inkluderas i biblioteket även när de aldrig anropas inifrån andra tillägg. Om du inte vill öka biblioteksstorleken i onödan bör du vara försiktig med vad du visar som en delad modul.

Delade moduler har ingen vykomponent.

[Läs mer](./web/shared.md)

### Moduler för kanttillägg {#edge-modules}

I edge-tillägg aktiveras regler via villkorskontroller, som sedan utför specifika åtgärder om dessa kontroller godkänns. Mer information finns i översikten om [modulflöde i kanttillägg](./edge/flow.md).

Du kan definiera egna biblioteksmoduler i dina edge-tillägg. Dessa kan kategoriseras i följande typer:

* [Villkorstyper](#condition)
* [Åtgärdstyper](#action)
* [Dataelementtyper](#data-element)

>[!NOTE]
>
>Mer information om vilket format som krävs för implementering av biblioteksmoduler i edge-tillägg finns i [modulformatöversikt](./edge/format.md).

#### Villkorstyper {#condition}

Ett regelvillkor utvärderas efter att en regelhändelse har inträffat. Alla villkor måste returnera true för att regeln ska kunna fortsätta bearbetningen. Undantaget är när användare uttryckligen placerar villkor i en &quot;undantagsbucket&quot;, i vilket fall alla villkor i bucket måste returnera false för att regeln ska fortsätta bearbetningen.

Ett tillägg kan till exempel innehålla villkorstypen &quot;viewport contains&quot;, där användaren kan ange en CSS-väljare. När villkoret utvärderas på klientens webbplats kan tillägget hitta element som matchar CSS-väljaren och returnera om något av dem finns i användarens visningsruta.

Villkorstyperna består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, där användarna kan ändra inställningarna för villkoret, och (2) en biblioteksmodul som skickas från biblioteket för tagghantering för att tolka inställningarna och utvärdera ett villkor.

[Läs mer](./web/condition-types.md)

#### Åtgärdstyper {#action}

En regelåtgärd är något som utförs efter att regelvillkoren har godkänts i utvärderingen.

Ett tillägg kan till exempel innehålla en&quot;show support chat&quot;-åtgärdstyp som kan visa en supportchattdialogruta för att hjälpa användare som kan ha problem med utcheckningen.

Åtgärdstyperna består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, som gör att användare kan ändra inställningar för åtgärden och (2) en biblioteksmodul som skickas i biblioteket för tagghantering för att tolka inställningarna och utföra en åtgärd.

[Läs mer](./web/action-types.md)

#### Dataelementtyper {#data-element}

Dataelement är i stort sett alias för datadelar på en sida, oavsett var dessa data finns i händelsen som servern tar emot. Ett dataelement kan refereras av regler och fungerar som en abstraktion för att komma åt dessa datadelar. När platsen för data ändras i framtiden (till exempel den händelsenyckel som innehåller värdet ändras) kan ett enskilt dataelement konfigureras om medan alla regler som refererar till det dataelementet kan förbli oförändrade.

Dataelementtyper består vanligtvis av (1) en vy som visas i användargränssnittet för datainsamling, där användarna kan ändra inställningarna för dataelementet, och (2) en biblioteksmodul som skickas i biblioteket för tagghantering för att tolka inställningarna och hämta datadelar.

[Läs mer](./web/data-element-types.md)

## Tilläggskonfiguration

Ett tilläggs konfiguration syftar på det sätt som de samlar in globala inställningar från en användare. Ta till exempel ett tillägg som gör att användaren kan skicka en fyr med en Skicka fyr-åtgärd och fyren alltid måste innehålla ett konto-ID. Vi vill inte besvära användare genom att fråga dem om konto-ID varje gång de konfigurerar en Skicka Beacon-åtgärd. Tillägget ska i stället be om konto-ID en gång från tilläggskonfigurationsvyn. Varje gång en beacon ska skickas kan åtgärdsbiblioteksmodulen Skicka beacon hämta konto-ID:t från tilläggskonfigurationen och lägga till det i beacon.

När användare installerar ett tillägg till en taggegenskap visas tilläggskonfigurationsvyn. De kan inte slutföra installationen av tillägget utan att slutföra tilläggskonfigurationen.

Tilläggskonfigurationen består av en visningskomponent som exporterar inställningar som sedan skickas i taggens körningsbibliotek som ett enkelt objekt.

[Läs mer](./configuration.md)

## Tilläggsstruktur

Ett tillägg består av en katalog med filer. Här följer en översikt över hur dessa filer ska struktureras. Information om filinnehåll finns i andra avsnitt.

En [`extension.json`](./manifest.md)-fil måste finnas i katalogens rot. Den här filen beskriver bland annat hur tillägget ser ut och var vissa filer finns i katalogen. Detta liknar en [`package.json`](https://docs.npmjs.com/files/package.json)-fil i [npm](https://www.npmjs.com/).

Varje biblioteksmodul (den logik som ska skickas i taggens körningsbibliotek) måste vara en egen fil vars innehåll följer [CommonJS-modulstandarden](http://wiki.commonjs.org/wiki/Modules/1.1.1). Om vi till exempel skapar en&quot;skicka fyr&quot;-åtgärdstyp måste vi ha en fil som innehåller den logik som skickar fyren. Innehållet i den här filen kommer att skickas från taggens körningsbibliotek. Du kan kalla det `sendBeacon.js`. Platsen för filen i katalogen är inte viktig eftersom `extension.json` beskriver var den finns.

Varje vy måste vara en HTML-fil som kan läsas in i en iframe i taggprogrammet. Vyn måste innehålla ett skript från taggar och följa ett litet API för att kunna kommunicera med programmet. Det finns inga begränsningar för vilka bibliotek som används i vyerna. Du kan med andra ord använda jQuery, Understreck, React, Angular, Bootstrap eller andra bibliotek. Vi hoppas dock att du kommer att få tillägget att se likadant ut som programmet.

Vi rekommenderar att du placerar alla vyrelaterade filer (HTML, CSS, JavaScript) i en enda underkatalog som är isolerad från biblioteksmodulfilerna. I `extension.json` beskriver du var den här underkatalogen för vyn finns. Plattformen hanterar sedan den här underkatalogen (och endast den här underkatalogen) från sina webbservrar.
