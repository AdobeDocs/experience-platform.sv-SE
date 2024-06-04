---
title: Frågeguide för AI Assistant
description: Läs det här dokumentet om du vill veta mer om exempelfrågor som du kan använda när du frågar i AI Assistant.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Frågeguide för AI Assistant

I det här dokumentet finns en uppsättning exempelfrågor som du kan använda när du frågar AI Assistant.

Du kan även använda det här dokumentet för att få tips om [formulera dina frågor](#phrasing-your-questions) för att få optimala svar från AI Assistant.

## Målsättningsbaserade frågor {#objectives-questions}

Följande exempelfrågor grupperas efter mål som du kan uppnå med AI Assistant:

| Syfte | Beskrivning | Exempel |
| --- | --- | --- |
| Utbildningsbegrepp och fortsatta arbetsflöden | <ul><li>Som nybörjare kan du använda AI Assistant för att lära dig Real-Time CDP- och Adobe Journey Optimizer-koncept och själv ta till vara produkter och funktioner som du inte känner till.</li><li>Som erfaren användare kan du använda AI Assistant för att lösa ett edge-fall som kan blockera ditt arbetsflöde. | <ul><li>Hur skapar jag en kontrollpanel i Journey Analytics?</li><li>Berätta några användningsfall för Real-Time CDP.</li></ul> |
| Felsökning | Använd AI Assistant för att lära dig hur du felsöker grundläggande fel som kan uppstå i arbetsflödet. | <ul><li>Vad är felet? {ERROR_MESSAGE} menar du?</li><li>Varför kan jag inte ta bort målgruppen Luma: Email Audience?</li></ul> |
| Sandlådehygien | Använd AI Assistant för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan underhålla sandlådan. | <ul><li>Kan ni visa mig målgrupper som är lika?</li><li>Finns det några scheman som inte har någon associerad datauppsättning?</li></ul> |
| Värdeanalys | Använd AI Assistant för att identifiera dina mest använda dataobjekt och utvärdera eventuella prestandaindikatorer eller hitta de värdefullaste dataobjekten. | <ul><li>Hur många profiler finns i segmentdefinitionen&quot;Luma: Email Audience&quot;?</li><li>När aktiverades målgrupper för målgrupper i Experience Cloud?</li></ul> |
| Sök | Använd AI Assistant för att hitta Experience Platform-objekt som stöds, som målgrupper, datauppsättningar, destinationer, scheman och källor. | <ul><li>Visa en lista över målgrupper som innehåller&quot;Luma&quot; i namnet som skapades under det senaste kvartalet.</li><li>Vilka attribut finns i XDM-schemat&quot;Luma: Custom Actions&quot;?</li></ul> |
| Effektanalys | Använd AI Assistant för att identifiera dataobjekt som har använts i vissa arbetsflöden, så att du kan bedöma effekten av eventuella ändringar. | <ul><li>Vilka målgrupper använder `homeAddress.city` i schemat &quot;Luma: PersonProfiles&quot;?</li><li>Vilka datamängder är `consents.marketing.push.val` vilket profilattribut som lagras i?</li></ul> |

{style="table-layout:auto"}

## Driftsinsikter per enhet och frågor om produktkunskap{#objects-questions}

Följande frågor grupperas efter dataobjekt och klassificeras som antingen [operativa insikter](./home.md#operational-insights) eller [produktkunskap](./home.md#product-knowledge).

| Objekt | Beskrivning |
| --- | --- |
| Målgrupper - operativa insikter | <ul><li>Vilka målgrupper använder andra målgrupper?</li><li>Vilken är fördelningen av antalet profiler mellan olika målgrupper?</li><li>Visa vilka målgrupper som senast ändrades innan {RELATIVE_DATE}.</li><li>Vilka målgrupper har 0 profiler?</li><li>Är {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} används i andra målgrupper?</li></ul> |
| Attribut - driftsinsikter | <ul><li>Vilka målgrupper som har XDM-attribut {ATTRIBUTE_PATH} i segmentdefinitionen?</li><li>Hur många XDM-schemaattribut används inte i någon målgrupp?</li><li>Vilka scheman har XDM-attribut {ATTRIBUTE_PATH} i dem?</li><li>Vilka XDM-attribut aktiveras?</li><li>Vilka XDM-attribut som används i målgrupper med fler än 10 profiler</li></ul> |
| Dataflöden - driftsinsikter | <ul><li>Vilka dataflöden bidrar till {DATASET_NAME} datauppsättning?</li><li>Vilka källdataflöden används inte eller har inga data längre?</li><li> |
| Datauppsättningar - driftsinsikter | <ul><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilken källkoppling är associerad med {DATASET_NAME} datauppsättning></li><li>Vilka datauppsättningar används för varje målgrupp?</li><li>Vilka scheman används inte i några datauppsättningar?</li><li>Hur många datauppsättningar har jag?</li></ul> |
| Destinationer - driftsinsikter | <ul><li>Vilka destinationer befinner sig i ett aktivt läge?</li><li>Vilka målkonton har 0 målgrupper aktiverade?</li><li> |
| Resor - operativa insikter | <ul><li>Hur många resor har jag?</li><li>Vilka resor som har skapats i {RELATIVE_DATE} (t.ex. förra veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?</li><li>Visa listan över resor som har ändrats i {RELATIVE_DATE} (t.ex. förra veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?</li><li>Lista de resor jag har.</li><li>Ange de målgrupper som används i direktresor.</li></ul> |
| Scheman - operativa insikter | <ul><li>Vilka schemafält har bidragit till de flesta målgrupper?</li><li>Hur många scheman är profiler aktiverade?</li><li>Visa alla scheman som har ändrats under den senaste veckan.</li><li>Vilka scheman används inte i några datauppsättningar?</li><li>Visa alla scheman som skapats den senaste veckan.</li></ul> |
| Källor - driftsinsikter | <ul><li>Vilka källor är i ett aktivt läge?</li><li>Vilken källanslutning som är associerad med datauppsättningen {DATASET_NAME}?</li><li>Vilken källanslutning har det högsta antalet associerade konton?</li><li>Visa dataflödena och tillhörande källanslutningar.</li></ul> |
| Lär dig mer - Produktkunskap (Real-Time CDP och Journey Optimizer) | <ul><li>Vad kan AI Assistant hjälpa till med?</li><li>Vad är lookalike-målgrupper?</li><li>Hur är användargrupper relaterade till roller?</li><li>När ska jag använda en datatyp jämfört med en fältgrupp?</li><li>Vad är skillnaden mellan en identitet och en primär eller extern nyckel?</li><li>Hur beräknas profilrikedomen?</li></ul> |
| Felsökning - produktkunskap (Real-Time CDP och Journey Optimizer) | <ul><li>Vad kan AI Assistant hjälpa till med?</li><li>Kan jag ta bort ett profilaktiverat schema efter att data har importerats?</li><li>Varför kan jag inte ta bort en publik?</li><li>Hur lång tid tar det för målgrupperna att utvärderas och för att resultaten ska vara tillgängliga för målinriktning?</li></ul> |

{style="table-layout:auto"}

## Tar hand om dina frågor {#phrasing-your-questions}

Du måste ge AI Assistant tydliga och kontextuella uppgifter för att få ett så korrekt svar som möjligt. Se följande lista med tips om hur du ställer en tydlig fråga i sitt sammanhang:

* Ange din uppgift och/eller fråga kortfattat.
* Undvik tvetydigt språk och alltför komplex syntax för att underlätta förståelsen.
* Ange relevant sammanhang för dina uppgifter och/eller frågor eftersom kontexten kan hjälpa AI Assistant att generera mer relevanta svar.

Läs tabellerna nedan för mer information om de effektivaste strategierna när du ställer frågor till AI Assistant.

I följande tabeller beskrivs de effektivaste strategierna du kan följa när du använder AI Assistant:

| Gör | Exempel |
| --- | --- |
| <ul><li>Var tydlig med objektet eller informationen som du vill hämta eller analysera.</li><li>Försök att ange dataobjektens namn inom citattecken. Om du bara känner till en del av objektnamnet kan du även ange det i frågan.</li><li>Använd [objekt som slutförs automatiskt](./ui-guide.md#use-auto-complete) för att hjälpa AI Assistant att bättre förstå sammanhanget i din fråga.</li></ul> | <ul><li>Vilka datauppsättningar använder schemat&quot;Luma - Loyalty&quot;?</li><li>Visa de aktiverade segmenten som har &quot;Luma&quot; i sina namn. Rangordna dem efter antal profiler.</li></ul> |
| <ul><li>Undvik tvetydighet och använd tydligt språk</li><li>Använd exakt terminologi för att få bättre tydlighet i frågan.</li><li>När du ställer frågor om Adobe Experience Platform kan du försöka använda terminologi som är specifik för Experience Platform för att förbättra relevansen i svaren.</li></ul> | <ul><li>Hur många profiler har jag i&quot;ACME Audience&quot;.</li><li>Visa de fem främsta XDM-attributen som används i aktiverade målgrupper.</li></ul> |
| <ul><li>Ange sammanhang eller ange ett villkor för att filtrera resultaten.</li><li>Använd ett filtervillkor i frågorna för att begränsa mängden data i svaret.</li></ul> | <ul><li>Visa målgrupper som inte har aktiverats och skapats för mer än sex månader sedan och som aldrig har ändrats.</li><li>Visa att målgrupper är aktiverade för&quot;ACME Destination&quot; och har fler än 10 000 profiler.</li></ul> |

{style="table-layout:auto"}

| Gör det inte | Exempel |
| --- | --- |
| Använd oklart eller tvetydigt språk. | <ul><li>Ge mig information om datauppsättningar.</li><li>Hur många användare har jag i&quot;ACME Audience&quot;?</li><li>Visa segment.</li><li>Listattribut.</li></ul> |
| Gör ofullständiga förfrågningar. | &quot;Luma - lojalitetsdatauppsättning&quot; |
| Anta kunskap utan kontext. | <ul><li>Målgrupper de senaste sex månaderna.</li><li>Bygg en fråga åt mig.</li></ul> |
| Formge alltför komplexa frågor. | Gör en omfattande analys av datalinjer för alla objekt och deras beroenden. |
| Utelämna villkor eller parametrar. | Visa datauppsättningar. |

{style="table-layout:auto"}

## Nästa steg

Genom att läsa det här dokumentet får du nu en förståelse för hur du optimerar dina frågor för AI Assistant. Mer information om hur du använder funktionen under arbetsflöden finns i [Användargränssnittshandbok för AI Assistant](ui-guide.md).
