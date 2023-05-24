---
title: Bakåtkompatibilitetsstandard
description: Läs om den bakåtkompatibla standarden i Adobe Experience Platform som säkerställer att uppdaterade versioner av taggtillägg är kompatibla med tidigare versioner.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Bakåtkompatibilitetsstandard

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Uppdateringar av ett taggtillägg i Adobe Experience Platform måste vara bakåtkompatibla med tidigare versioner av tillägget. Detta innebär att

* Alla ändringar av tilläggens primära komponenter måste vara kompatibla med tidigare versioner.  Detta inkluderar tilläggskonfiguration, händelsetyper, villkorstyper, åtgärdstyper, dataelementtyper och delade moduler.
* Komponenter som en användare har skapat med den äldre tilläggsversionen måste kunna validera mot scheman som tillhandahålls av den nyare versionen.
* En Adobe Experience Platform-användare bör kunna installera en uppdaterad version av tillägget och ha allt de gjort tills de avsiktligt ändrar något.

## Tillåtna ändringar

Följande typer av ändringar av tillägget tillåts:

1. Du kan lägga till nya komponenter (händelsetyper, villkorstyper osv.).
1. Du kan lägga till nya valfria fält i tilläggskonfigurationsinställningarna.
1. Du kan ändra obligatoriska fält till valfria fält.

## Otillåtna ändringar

Följande typer av ändringar av tillägget tillåts inte:

1. Du får inte byta namn på en komponent.
1. Du får inte ta bort en komponent.
1. Du får inte ta bort ett fält från en komponent.
1. Du kan inte ändra valfria fält till obligatoriska fält.
1. Du får inte lägga till nya obligatoriska fält.
1. Du får inte ändra API:t för befintliga delade moduler.

Om du gör någon av dessa ändringar kommer alla som har installerat tillägget i sin egenskap omedelbart att få problem som:

* Regler återges inte längre korrekt eftersom en av regelkomponenterna söker efter en komponent som inte finns
* Alla byggen misslyckas eftersom biblioteket innehåller en överordnad resurs som inte längre finns i tillägget
* Alla byggen misslyckas eftersom biblioteket innehåller en resurs med inställningar som inte kan valideras mot det nya schemat

Särskilt i det här andra fallet kan användare lämnas utan en åtgärd och det finns inget sätt att åtgärda sina egenskaper så att de kan publicera igen.

## Ta bort funktioner

Det kan finnas scenarier när du har en giltig affärshändelse och du tror att du verkligen behöver göra en förbjuden ändring (som listas ovan).  Du kan fortfarande inte göra det, men här kan du göra istället:

1. Jag vill ta bort en komponent => Skapa en ny komponent och ersätta den gamla
1. Jag vill ta bort ett fält från en komponent => Skapa en ny komponent med det fältet borttaget och ta bort det gamla
1. Jag vill ändra ett valfritt fält till obligatoriskt => Gör en ny komponent som kräver det önskade fältet och ersätt det gamla
1. Jag vill ändra API:t för en delad modul => Skapa en ny delad modul och ta bort den gamla

Du kanske plockar upp en vanlig tråd.  Det är bra.  När du tar bort en gammal komponent måste du meddela användarna att tillägget har tagits bort och att de måste byta till en ny.  Några förslag om hur du kommunicerar med användare:

* Uppdatera den gamla komponentens visningsnamn så att det innehåller&quot;(inaktuellt)&quot;.
* Uppdatera vyn för den gamla komponenten så att den innehåller stor röd varningstext om att den här komponenten har tagits bort och att användaren ska växla till den nya komponenten.
* Uppdatera modulkoden för att logga meddelanden om borttagning i konsolen.  Tänk på att dessa kommer att visa för slutanvändarna, så håll dem rena och lite generiska.
* Skicka vänliga e-postmeddelanden från CRM-systemet.

Om den gamla funktionen inte bara är oönskad, utan faktiskt inte längre finns i din lösning, finns det ytterligare ett steg du kan ta - men det bör du bara göra efter att du har meddelat användarna och gett dem tid att uppdatera.

* Uppdatera innehållet i modulen så att den inte gör något.  Detta tar bort funktionaliteten från användarens distribuerade bibliotek i nästa version, men bryter inte mot några regler eller byggen.

### Återställa borttagna funktioner

Om du redan har tagit bort funktioner och får höra från användarna att saker och ting har gått sönder måste du släppa en ny version av tillägget som återställer de komponenter du har tagit bort.

Det går bra att återställa dem i ett föråldrat läge enligt beskrivningen ovan, men de måste finnas.

Anta att du har en v1.0 som har komponent-XYZ som andra använder.  Därefter släpper du en v1.1 som inte längre har Component XYZ.  Användarna har fått höra att tillägget hade sönder sina egenskaper och att du måste åtgärda det.  Du måste släppa en v1.2 som återställer komponent-XYZ (kanske i ett föråldrat läge - det är upp till dig) och låta användarna uppgradera till v1.2 för att få saker och ting att fungera igen.
