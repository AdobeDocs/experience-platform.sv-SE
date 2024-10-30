---
title: Komma igång med tilläggsutveckling
description: Kom igång med att utveckla egna taggtillägg i Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 077d3ac5a34f052ef6293927d67e3cc8afb27563
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 9%

---

# Komma igång med tilläggsutveckling

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens av terminologiändringarna.

För att du ska komma igång och bygga tillägg kommer vi att använda verktyget för öppen källkod, som tillhandahålls av Adobe-ingenjörer för att skapa de filer och den filstruktur som behövs för ditt tilläggspaket, så allt du har kvar att göra är den värdefulla delen: skriv koden i själva verket.

## Förhandskrav

* Installera [Node.js](https://nodejs.org/en/download/).

## Tilläggsinställningar

Skapa en katalog där tilläggsfilerna ska finnas.

```shell
mkdir example && cd example
```

Den här guiden använder tilläggsverktyget för att bygga ut den inledande tilläggsstrukturen så att utvecklare snabbt kan börja koda. Om du vill kan du utföra den här processen manuellt utan att använda verktyget för att skapa ställningar.

Kör verktyget ställningar.

```shell
npx @adobe/reactor-scaffold
```

Ställningsverktyget frågar efter några initiala konfigurationsalternativ enligt följande:

* Visningsnamn - det synliga namnet på tillägget
* Plattform - Anger om tillägget har utvecklats för webb, mobil eller kant
* Version - Tilläggets version
* Beskrivning - En kort beskrivning av syftet med tillägget
* Författare - Namnet på tilläggets författare

>[!NOTE]
> För mobiltillägg kommer flera frågor att ställas om strukturen för dina Android- och iOS-program.

Verktyget kommer sedan att innehålla alternativ för att skapa tilläggsstrukturen:

* [Vyn för tilläggskonfiguration](./configuration.md): Vyn, HTML-filen, genom vilken ett tillägg samlar in globala inställningar från en användare.
* [Händelsetyper](./web/event-types.md): Definierar en aktivitet för observation. Du kan till exempel veta när en användare rullar snabbt eller när en användare interagerat med ett sidelement. Händelser kan sedan användas i regler för att utföra åtgärder.
* [Villkorstyper](./web/condition-types.md): Villkorstyper utvärderar om något är sant eller falskt.
Detta kan till exempel returneras om användarens webbläsare är Chrome, om användaren använder en iPad eller om användaren finns på en viss domän.
* [Åtgärdstyper](./web/action-types.md): Den åtgärd som ska utföras när en händelse inträffar. Skicka till exempel en analysfyr, visa ett erbjudande, spara en cookie eller öppna en supportchatt.
* [Dataelementtyper](./web/data-element-types.md): Ett dataelement hämtar en datadel. Dessa data kan lagras lokalt, i en cookie, i ett DOM-element eller på en anpassad plats.
* [Delade moduler](./web/shared.md) (endast webben): En delad modul är en mekanism genom vilken tillägg kan kommunicera med andra tillägg.
* [Vyer](./web/views.md): Varje händelse, villkor, åtgärd eller dataelementtyp kan innehålla en vy som gör att användaren kan ange inställningar.
* URL för Exchange (endast webb och kant): När ett tillägg publiceras till den offentliga Adobe-katalogen anger du den URL som ska visas här.
* Ikonsökväg: En sökväg till en ikonfil för tillägget.

>[!NOTE]
>
>* Efterföljande körningar av byggnadsverktyget hoppar över den inledande konfigurationen.
>* Mer än en av varje händelse, villkor, åtgärd, kan läggas till.
>* Det får bara finnas en konfigurationsvy.

## Nästa steg

* Följ översikten över [överföringsprocessen](./submit/overview.md) och förbered dig för att [validera](./submit/upload-and-test.md#validate) och [överföra](./submit/upload-and-test.md#integration) tillägget för testning i taggens ekosystem.
