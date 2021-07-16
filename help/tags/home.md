---
title: Översikt över taggar
description: Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Översikt över taggar

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](./term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.

Med taggar kan alla skapa och underhålla egna integreringar, som kallas *tillägg*. Dessa tillägg är tillgängliga för [!DNL Adobe Experience Cloud]-kunder i en appbutik så att de snabbt kan installera, konfigurera och distribuera sina taggar.

Taggar erbjuds [!DNL Adobe Experience Cloud]-kunder som en inkluderad funktion för att lägga till värde.

## Viktiga fördelar

* Snabbare time to value.
* Tillförlitliga data genom centraliserad insamling, organisering och leverans med dataelement.
* Engagerande upplevelser genom integrering av data- och marknadsföringsteknologi med regelbyggaren.

## Viktiga funktioner

### Tillägg

Ett tillägg är ett kodpaket (JavaScript, HTML och CSS) som utökar taggfunktionaliteten. Bygg, hantera och uppdatera integreringarna med hjälp av ett praktiskt taget självbetjäningsgränssnitt. Du kan tänka dig tillägg som appar som du använder för att utföra dina uppgifter.

### Tilläggskatalog

Sök, konfigurera och driftsätt marknadsförings-/annonsverktyg som byggts och underhålls av oberoende programvaruleverantörer.

### Regelverktyget

Skapa robusta regler som kombinerar flera händelser, sekventierade på det sätt som du bestämmer med if/then-logik med villkor och undantag. Regler innehåller alternativ för:

* Händelser
* Villkor
* Undantag
* Instruktioner

Regelbyggaren innehåller felkontroll i realtid och syntaxmarkering för din anpassade kod.

När villkoren i reglerna är uppfyllda utförs de definierade åtgärderna i ordning.

### Dataelement

Samla in, ordna och leverera data över webbaserad marknadsföring och annonsteknik.

### Enterprise publishing

Publiceringsprocessen gör att team kan publicera kod på sidor. Olika personer kan skapa en implementering, godkänna den och publicera den på dina sidor.

* Ändringar i koden kapslas in i de bibliotek du definierar.
* Du anger var och när du vill att koden ska distribueras.
* Flera bibliotek kan byggas parallellt av olika team.
* Obegränsade utvecklingsmiljöer.
* En avsiktlig behörighetsbaserad process för att sammanfoga bibliotek.

### Öppna API:er

Automatisera implementeringar av enskilda tekniker eller en grupp av tekniker.

* Taggar interagerar med Reaktors API.
* Distributioner kan automatiseras via API:er.
* Integrera API:erna med era egna interna system.
* Du kan skapa ett eget användargränssnitt om du vill.

### Ljus, modulär behållartagg

Innehållet i behållaren är minifierat, inklusive din egen kod. Allt är modulärt. Om du inte behöver något objekt inkluderas det inte i ditt bibliotek. Resultatet är en snabb och kompakt implementering. Se [Minification](./ui/publishing/builds.md).

## Andra högdagrar

Taggar har flera förbättringar jämfört med liknande system, bland annat:

* Ingen användning av `document.write ()` där Chrome inte tillåter det.
* Reglerna Sidbörjan och Sidslutet paketeras i huvudbiblioteket för att minimera onödiga HTTP-anrop.
* Anpassade åtgärdsskript i en regel kan läsas in parallellt, men körs sekventiellt.
* Om du undviker reglerna för sidans överkant och sidunderkant är koden i huvudsak asynkron, med en sökväg till fullständigt asynkron.
