---
title: Komma igång med tilläggsutveckling
description: Kom igång med att utveckla egna taggtillägg i Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Komma igång med tilläggsutveckling

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

För att du ska komma igång och bygga tillägg kommer vi att använda verktyget för öppen källkod, som tillhandahålls av Adobe ingenjörer för att skapa de filer och den filstruktur som behövs för ditt tilläggspaket, så allt du har kvar att göra är den värdefulla delen: skriva koden.

## Förutsättningar

* Installera [Node.js](https://nodejs.org/en/download/).

## Tilläggsinställningar

Skapa en katalog där tilläggsfilerna ska finnas.

```shell
mkdir example && cd example
```

Den här guiden använder tilläggsverktyget för att bygga ut den inledande tilläggsstrukturen så att utvecklare snabbt kan börja koda. Om du vill kan du utföra den här processen manuellt utan att använda verktyget Skaffe.

Kör verktyget ställningar.

```shell
npx @adobe/reactor-scaffold
```

Ställningsverktyget frågar efter några initiala konfigurationsalternativ enligt följande:

* Visningsnamn - det synliga namnet på tillägget
* Version - Tilläggets version
* Beskrivning - En kort beskrivning av syftet med tillägget
* Författare - Namnet på tilläggets författare

Verktyget kommer sedan att innehålla alternativ för att skapa tilläggsstrukturen:

* [Vy för tilläggskonfiguration](./configuration.md): Vyn, HTML-fil, genom vilken ett tillägg samlar in globala inställningar från en användare.
* [Händelsetyper](./web/event-types.md): Definierar en aktivitet för observation. Du kan till exempel veta när en användare rullar snabbt eller när en användare interagerat med ett sidelement. Händelser kan sedan användas i regler för att utföra åtgärder.
* [Villkorstyper](./web/condition-types.md): Villkorstyperna utvärderar om något är sant eller falskt.
Detta kan till exempel returneras om användarens webbläsare är Chrome, om användaren använder en iPad eller om användaren finns på en viss domän.
* [Åtgärdstyper](./web/action-types.md): Den åtgärd som ska utföras när en händelse inträffar. Skicka till exempel en analysfyr, visa ett erbjudande, spara en cookie eller öppna en supportchatt.
* [Dataelementtyper](./web/data-element-types.md): En dataelementtyp hämtar en datadel. Dessa data kan lagras lokalt, i en cookie, i ett DOM-element eller på en anpassad plats.
* [Delade moduler](./web/shared.md): En delad modul är en mekanism genom vilken tillägg kan kommunicera med andra tillägg.
* [Vyer](./web/views.md): Varje händelse, villkor, åtgärd eller dataelementtyp kan innehålla en vy som gör att användaren kan ange inställningar.

>[!NOTE]
>
>* Efterföljande körningar av byggnadsverktyget hoppar över den inledande konfigurationen.
>* Mer än en av varje händelse, villkor, åtgärd, kan läggas till.
>* Det får bara finnas en konfigurationsvy.


## Nästa steg

* Följ [Översikt över överföringsprocessen](./submit/overview.md) och förbereda [validera](./submit/upload-and-test.md#validate) och [ladda upp](./submit/upload-and-test.md#integration) tillägget för testning i taggens ekosystem.
