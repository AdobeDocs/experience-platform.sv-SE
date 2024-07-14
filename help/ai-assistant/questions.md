---
title: Frågeguide för AI Assistant
description: Läs det här dokumentet om du vill veta mer om exempelfrågor som du kan använda när du frågar i AI Assistant.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 6860e1dc03920feaf0dfa83d09c4fca8f85a2ac2
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 0%

---

# Frågeguide för AI Assistant

I det här dokumentet finns en uppsättning exempelfrågor som du kan använda när du frågar AI Assistant.

Du kan också använda det här dokumentet för att lära dig tips om [hur du formulerar dina frågor](#phrasing-your-questions) för att få optimala svar från AI Assistant.

## Målsättningsbaserade frågor {#objectives-questions}

Följande exempelfrågor grupperas efter mål som du kan uppnå med AI Assistant:

| Syfte | Beskrivning | Exempel |
| --- | --- | --- |
| Utbildningsbegrepp och fortsatta arbetsflöden | <ul><li>Som nybörjare kan du använda AI Assistant för att lära dig Real-Time CDP- och Adobe Journey Optimizer-koncept och själv ta till vara produkter och funktioner som du inte känner till.</li><li>Som erfaren användare kan du använda AI Assistant för att lösa ett edge-fall som kan blockera ditt arbetsflöde. | <ul><li>Hur skapar jag en kontrollpanel i Journey Analytics?</li><li>Berätta några användningsfall för Real-Time CDP.</li></ul> |
| Felsökning | Använd AI Assistant för att lära dig hur du felsöker grundläggande fel som kan uppstå i arbetsflödet. | <ul><li>Vad betyder det här felet {ERROR_MESSAGE}?</li><li>Varför kan jag inte ta bort målgruppen Luma: Email Audience?</li></ul> |
| Sandlådehygien | Använd AI Assistant för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan underhålla sandlådan. | <ul><li>Kan ni visa mig målgrupper som är lika?</li><li>Finns det några scheman som inte har någon associerad datauppsättning?</li></ul> |
| Värdeanalys | Använd AI Assistant för att identifiera dina mest använda dataobjekt och utvärdera eventuella prestandaindikatorer eller hitta de värdefullaste dataobjekten. | <ul><li>Hur många profiler finns i segmentdefinitionen&quot;Luma: Email Audience&quot;?</li><li>När aktiverades målgrupper för målgrupper i Experience Cloud?</li></ul> |
| Sök | Använd AI Assistant för att hitta Experience Platform-objekt som stöds, som målgrupper, datauppsättningar, destinationer, scheman och källor. | <ul><li>Visa en lista över målgrupper som innehåller&quot;Luma&quot; i namnet som skapades under det senaste kvartalet.</li><li>Vilka attribut finns i XDM-schemat&quot;Luma: Custom Actions&quot;?</li></ul> |
| Effektanalys | Använd AI Assistant för att identifiera dataobjekt som har använts i vissa arbetsflöden, så att du kan bedöma effekten av eventuella ändringar. | <ul><li>Vilka målgrupper använder `homeAddress.city` i Luma: PersonProfiles-schemat?</li><li>Vilka datauppsättningar lagras profilattributet `consents.marketing.push.val` i?</li></ul> |

{style="table-layout:auto"}

## Driftsinsikter per enhet och frågor om produktkunskap{#objects-questions}

Följande frågor grupperas efter dataobjekt och klassificeras antingen som [operativa insikter](./home.md#operational-insights) eller [produktkunskaper](./home.md#product-knowledge).

* **Målgrupper - driftsinsikter**
   * Vilka målgrupper använder andra målgrupper?
   * Vilken är fördelningen av antalet profiler mellan olika målgrupper?
   * Visa målgrupper som senast ändrades före {RELATIVE_DATE}.
   * Vilka målgrupper har 0 profiler?
   * Används {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} i andra målgrupper?
* **Attribut - driftsinsikter**
   * Vilka målgrupper har xdm-attributet {ATTRIBUTE_PATH} i sin segmentdefinition?
   * Hur många XDM-schemaattribut används inte i någon målgrupp?
   * Vilka scheman innehåller xdm-attributet {ATTRIBUTE_PATH}?
   * Vilka XDM-attribut aktiveras?
   * Vilka XDM-attribut används i målgrupper med fler än 10 profiler?
* **Dataflöden - driftsinsikter**
   * Vilka dataflöden bidrar till datauppsättningen {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Vilka källdataflöden används inte eller har inga data längre?
   * Ange de källdataflöden jag har.
   * Vilka dataflöden har konfigurerats för varje källanslutning?
* **Datauppsättningar - driftsinsikter**
   * Hur många datauppsättningar har importerats med samma schema?
   * Vilken källanslutning är associerad med datauppsättningen {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Vilka datauppsättningar används för varje målgrupp?
   * Vilka scheman används inte i några datauppsättningar?
   * Hur många datauppsättningar har jag?
* **Destinationer - driftsinsikter**
   * Vilka destinationer befinner sig i ett aktivt läge?
   * Vilka målkonton har 0 målgrupper aktiverade?
   * Hur många målgrupper aktiveras för varje mål?
   * Vilka destinationer har det högsta antalet aktiva målgrupper?
* **Resor - driftsinsikter**
   * Hur många resor har jag?
   * Vilka resor har skapats i {RELATIVE_DATE} (t.ex. den sista veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?
   * Visa mig listan över resor som har ändrats i {RELATIVE_DATE} (t.ex. den senaste veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?
   * Ange de resor jag har.
   * Ange de målgrupper som används i direktresor.
* **Källor - driftsinsikter**
   * Vilka källor är i ett aktivt läge?
   * Vilken källanslutning som är associerad med datauppsättningen {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Vilken källanslutning har det högsta antalet associerade konton?
   * Visa dataflödena och tillhörande källanslutningar.
* **Målad inlärning - produktkunskap (Real-Time CDP och Journey Optimizer)**
   * Vad är lookalike-målgrupper?
   * Hur är användargrupper relaterade till roller?
   * När ska jag använda en datatyp jämfört med en fältgrupp?
   * Vad är skillnaden mellan en identitet och en primär eller extern nyckel?
   * Hur beräknas profilrikedomen?
* **Felsökning - produktkunskap (Real-Time CDP och Journey Optimizer)**
   * Vad kan AI Assistant hjälpa till med?
   * Kan jag ta bort ett profilaktiverat schema efter att data har importerats?
   * Varför kan jag inte ta bort en publik?
   * Hur lång tid tar det för målgrupperna att utvärderas och resultaten blir tillgängliga för målinriktning?

+++Välj för att visa ytterligare en lista med förslag

* Kan jag ta bort ett profilaktiverat schema efter att data har importerats?
* Hur är användargrupper relaterade till roller?
* När ska jag använda en datatyp jämfört med en fältgrupp?&#39;
* Vad är skillnaden mellan en identitet och en primär eller främmande nyckel?&#39;
* Hur lång tid tar det för segment att utvärderas och resultaten blir tillgängliga för målinriktning?
* Hur beräknas profilrikedomen?&#39;
* Berätta några vanliga användningsexempel för Real-Time CDP.
* Varför kan jag inte ta bort ett segment?
* Vilken typ av ändringar kan jag göra efter att ett schema har aktiverats för profilen?
* Varför kan jag inte komma åt Dashboards i AEP?
* Hur många segment använder xdm-attributet {FIELD_PATH}
* Har jag några segment som används i andra segment?
* Vilka fält i {SCHEMA_NAME}-schemat innehåller {STRING}?
* Vilka målgrupper har xdm-attributet {FULL_ATTRIBUTE_PATH} i sin segmentdefinition?
* Vilka scheman innehåller xdm-attributet {FULL_ATTRIBUTE_PATH}?
* Vilka källdataflöden används inte eller har inga data längre?
* Ange de resor jag har.
* Ange de målgrupper som används i direktresor.
* Vilka källor är i ett aktivt läge?

+++

## Tar hand om dina frågor {#phrasing-your-questions}

Du måste ge AI Assistant tydliga och kontextuella uppgifter för att få ett så korrekt svar som möjligt. Se följande lista med tips om hur du ställer en tydlig fråga i sitt sammanhang:

* Ange din uppgift och/eller fråga kortfattat.
* Undvik tvetydigt språk och alltför komplex syntax för att underlätta förståelsen.
* Ange relevant sammanhang för dina uppgifter och/eller frågor eftersom kontexten kan hjälpa AI Assistant att generera mer relevanta svar.

Läs tabellerna nedan för mer information om de effektivaste strategierna när du ställer frågor till AI Assistant.

I följande tabeller beskrivs de effektivaste strategierna du kan följa när du använder AI Assistant:

| Gör | Exempel |
| --- | --- |
| <ul><li>Var tydlig med objektet eller informationen som du vill hämta eller analysera.</li><li>Försök att ange dataobjektens namn inom citattecken. Om du bara känner till en del av objektnamnet kan du även ange det i frågan.</li><li>Använd [objekt som fylls i automatiskt](./ui-guide.md#use-auto-complete) för att hjälpa AI Assistant att förstå innehållet i din fråga bättre.</li></ul> | <ul><li>Vilka datauppsättningar använder schemat&quot;Luma - Loyalty&quot;?</li><li>Visa de aktiverade segmenten som har &quot;Luma&quot; i sina namn. Rangordna dem efter antal profiler.</li></ul> |
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

## Exempel på frågor som inte stöds {#unsupported-questions}

Nedan följer ett antal exempel på frågor som för närvarande inte stöds av AI Assistant.

+++Välj för att visa exempel på frågor som inte stöds

### Driftsinsikter

* Hur många profiler i den här sandlådan [uppfyller ett specifikt villkor, till exempel&quot;live in California&quot;]?
* Vilka segment finns den här profilen i {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Hur många profiler i datauppsättningen har ett e-postmeddelande?
* Vilken datauppsättning utgör det maximala antalet profiler i den här sandlådan?
* Vilken datauppsättning har det högsta antalet poster?
* Hur många segment har tagits bort i {RELATIVE_DATE}?
* Vilken av mina datauppsättningar har den största storleken?
* Ge mig en profil i {AUDIENCE_NAME}.
* Vad är det totala antalet profiler i min sandlåda?
* Hur många identitetsnamnutrymmen är associerade med målgruppen {AUDIENCE_NAME}?
* Visa mig en rapport över alla målgruppssegment som utvärderats idag
* Hur många segment har överlappande profiler?
* Hur många batchar som läses in i {DATASET_NAME}
* Hur många aktiva erbjudanden har jag?
* Hur många aktiva kampanjer har jag?
* Varifrån kommer mina datakällor?
* Vilken är den största datauppsättningen eller datakällan?
* Kan jag få en lista över användare som har skapat dessa scheman?

### Felsökning

* Varför bearbetas den här batchen {BATCH_NAME/BATCH_ID} fortfarande?
* Varför är ingen kvalificerande för den här målgruppen {AUDIENCE_NAME}?
* Jag kan inte se kundens AI, varför och hur åtgärdar jag det?
* Jag kan inte se förhandsgranskning av datauppsättning, varför och hur åtgärdar jag den?
* Varför kan jag inte ta bort {SEGMENT/DATASET/SCHEMA_NAME}?
* Har jag åtkomst till frågetjänsten?

### Uppgift och automatisering

* Skriv en fråga som ger mig en post från {DATASET_NAME}.
* Skriv ett exempel-API-anrop till /schemas/{schemaId}/fields/{fieldPath}/values.
* Konfigurera en källa/mål för mig.
* Skapa en målgrupp för mig med villkoren {USER_SPECIFIC_CRITERIA}.

+++

## Nästa steg

Genom att läsa det här dokumentet får du nu en förståelse för hur du optimerar dina frågor för AI Assistant. Mer information om hur du använder funktionen under arbetsflöden finns i [gränssnittsguiden för AI-assistenten](ui-guide.md).
