---
title: Översikt över tilläggsutveckling
description: Lär dig mer om de primära komponenterna för olika taggtilläggstyper och tilläggsutvecklingsprocessen i Adobe Experience Platform.
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Översikt över tilläggsutveckling

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Ett av de främsta målen med taggar i Adobe Experience Platform är att skapa ett öppet ekosystem där ingenjörer utanför Adobe kan visa ytterligare funktioner på sina webbplatser och i mobilapplikationer. Detta uppnås genom taggtillägg. När ett tillägg har installerats på en taggegenskap blir det tilläggets funktioner tillgängliga för alla användare av egenskapen.

I det här dokumentet beskrivs de primära komponenterna i ett tillägg och det finns länkar till ytterligare dokumentation som kan hjälpa dig i utvecklingsprocessen för tillägget.

## Tilläggsstruktur

Ett tillägg består av en katalog med filer. Ett tillägg består av en manifestfil, biblioteksmoduler och vyer.

### Manifest-fil

En manifestfil ([`extension.json`](./manifest.md)) måste finnas i katalogens rot. Den här filen beskriver hur tillägget ser ut och var vissa filer finns i katalogen. Manifestfunktionerna liknar [`package.json`](https://docs.npmjs.com/files/package.json) i en [npm](https://www.npmjs.com/) projekt.

### Biblioteksmoduler

Biblioteksmodulerna är de filer som beskriver de olika [komponenter](#components) som ett tillägg innehåller (med andra ord den logik som ska skickas i taggens körningsbibliotek). Innehållet i varje biblioteksmodulfil måste följa [CommonJS-modulstandard](https://nodejs.org/api/modules.html#modules-commonjs-modules).

Om du till exempel skapar en åtgärdstyp med namnet&quot;skicka fyr&quot; måste du ha en fil som innehåller logiken som skickar fyndet. Om JavaScript används kan filen anropas `sendBeacon.js`. Innehållet i den här filen kommer att skickas från taggens körningsbibliotek.

Du kan placera biblioteksmodulfiler var du vill i tilläggskatalogen, förutsatt att du beskriver deras platser i `extension.json`.

### Vyer

En vy är en HTML-fil som kan läsas in i en [`iframe` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) i taggprogrammet, särskilt via användargränssnittet för plattformen och användargränssnittet för datainsamling. Vyn måste innehålla ett skript från tillägget och följa ett litet API för att kunna kommunicera med programmet.

Den viktigaste visningsfilen för alla tillägg är dess konfiguration. Se avsnittet om [tilläggskonfigurationer](#configuration) för mer information.

Det finns inga begränsningar för vilka bibliotek som används i vyerna. Du kan med andra ord använda jQuery, Understreck, React, Angular, Bootstrap eller andra. Vi rekommenderar dock att du gör så att tillägget ser likadant ut som gränssnittet.

Vi rekommenderar att du placerar alla visningsrelaterade filer (HTML, CSS, JavaScript) i en enda underkatalog som är isolerad från biblioteksmodulfilerna. I `extension.json`kan du beskriva var den här underkatalogen för vyn finns. Plattformen hanterar sedan den här underkatalogen (och endast den här underkatalogen) från sina webbservrar.

## Bibliotekskomponenter {#components}

Varje tillägg definierar en uppsättning funktioner. Dessa funktioner implementeras genom att inkluderas i en [bibliotek](../ui/publishing/libraries.md) som distribueras till din webbplats eller app. Bibliotek är en samling enskilda komponenter, inklusive villkor, åtgärder, dataelement med mera. Varje bibliotekskomponent är en del återanvändbar kod (som tillhandahålls av ett tillägg) som skickas inuti tagghjulet.

Beroende på om du utvecklar ett webbtillägg eller ett kanttillägg, skiljer sig de tillgängliga typerna av komponenter och deras användningsfall åt. I underavsnitten nedan finns en översikt över vilka komponenter som är tillgängliga för varje tilläggstyp.

### Komponenter för webbtillägg {#web}

I webbtillägg aktiveras regler via händelser, som sedan kan köra specifika åtgärder om en viss uppsättning villkor uppfylls. Se översikten på [modulflöde i webbtillägg](./web/flow.md) för mer information.

Förutom [kärnmoduler](./web/core.md) från Adobe kan du definiera följande bibliotekskomponenter i dina webbtillägg:

* [Händelser](./web/event-types.md)
* [Villkor](./web/condition-types.md)
* [Instruktioner](./web/action-types.md)
* [Dataelement](./web/data-element-types.md)
* [Delade moduler](./web/shared.md)

>[!NOTE]
>
>Mer information om vilket format som krävs för att implementera bibliotekskomponenter i webbtillägg finns i [översikt över modulformat](./web/format.md).

### Komponenter för kanttillägg {#edge}

I edge-tillägg aktiveras regler via villkorskontroller, som sedan utför specifika åtgärder om dessa kontroller godkänns. Se översikten på [tilläggsflöde](./edge/flow.md) för mer information.

Du kan definiera följande bibliotekskomponenter i dina edge-tillägg:

* [Villkor](./edge/condition-types.md)
* [Instruktioner](./edge/action-types.md)
* [Dataelement](./edge/data-element-types.md)

>[!NOTE]
>
>Mer information om det format som krävs för att implementera biblioteksmoduler i edge-tillägg finns i [översikt över modulformat](./edge/format.md).

## Tilläggskonfiguration {#configuration}

Ett tilläggs konfiguration syftar på det sätt som de samlar in globala inställningar från en användare. Konfigurationen består av en visningskomponent som exporterar och genererar inställningar i taggens körningsbibliotek som ett enkelt objekt.

Ta till exempel ett tillägg som gör att användaren kan skicka en fyr med en&quot;Skicka fyr&quot;-åtgärd, och fyren måste alltid innehålla ett konto-ID. I stället för att fråga användarna om ett konto-ID varje gång de konfigurerar en&quot;Skicka signal&quot;-åtgärd, bör tillägget be om konto-ID en gång från tilläggskonfigurationsvyn. Varje gång en beacon ska skickas kan åtgärden&quot;Skicka beacon&quot; hämta konto-ID:t från tilläggskonfigurationen och lägga till det i beacon.

När användare installerar ett tillägg för en egenskap i användargränssnittet visas tilläggskonfigurationsvyn, som de måste slutföra för att slutföra installationen.

Mer information finns i handboken [tilläggskonfigurationer](./configuration.md).

## Skicka tillägg

När du är klar med att skapa tillägget kan du skicka in det så att det visas i tilläggskatalogen i Platform. Se [överblick över överföringsprocessen för tillägg](./submit/overview.md) för mer information.
