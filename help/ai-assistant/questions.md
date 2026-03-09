---
title: Frågeguide för AI Assistant (äldre)
description: Läs det här dokumentet om du vill veta mer om exempelfrågor som du kan använda när du frågar i AI Assistant (äldre).
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '2086'
ht-degree: 1%

---

# Frågeguide för AI Assistant (äldre)

I det här dokumentet kan du läsa en uppsättning exempelfrågor som du kan använda när du frågar i AI Assistant (äldre).

Du kan också använda det här dokumentet för att lära dig tips om [hur du formulerar dina frågor](#phrasing-your-questions) för att få optimala svar från AI Assistant (äldre).

## Målsättningsbaserade frågor {#objectives-questions}

Följande exempelfrågor grupperas efter mål som du kan uppnå med AI Assistant (äldre):

| Syfte | Beskrivning | Exempel |
| --- | --- | --- |
| Utbildningsbegrepp och fortsatta arbetsflöden | <ul><li>Som nybörjare kan du använda AI Assistant (äldre) för att lära dig Real-Time CDP- och Adobe Journey Optimizer-koncept och själv ta till vara produkter och funktioner som du inte känner till.</li><li>Som erfaren användare kan du använda AI Assistant (äldre) för att lösa ett edge-fall som kan blockera arbetsflödet. | <ul><li>Hur skapar jag en kontrollpanel i Journey Analytics?</li><li>Berätta några användningsfall för Real-Time CDP.</li></ul> |
| Felsökning | Använd AI Assistant (äldre) för att lära dig hur du felsöker grundläggande fel som kan uppstå i arbetsflödet. | <ul><li>Vad betyder det här felet {ERROR_MESSAGE}?</li><li>Varför kan jag inte ta bort målgruppen Luma: Email Audience?</li></ul> |
| Sandlådehygien | Använd AI Assistant (äldre) för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan underhålla sandlådan. | <ul><li>Kan ni visa mig målgrupper som är lika?</li><li>Finns det några scheman som inte har någon associerad datauppsättning?</li></ul> |
| Värdeanalys | Använd AI Assistant (äldre) för att identifiera dina mest använda dataobjekt och utvärdera eventuella prestandaindikatorer eller hitta de värdefullaste dataobjekten. | <ul><li>Hur många profiler finns i segmentdefinitionen&quot;Luma: Email Audience&quot;?</li><li>När aktiverades målgrupper på Experience Cloud målgrupper?</li></ul> |
| Sök | Använd AI Assistant (äldre) för att hitta Experience Platform-objekt som stöds, som målgrupper, datauppsättningar, mål, scheman och källor. | <ul><li>Visa en lista över målgrupper som innehåller&quot;Luma&quot; i namnet som skapades under det senaste kvartalet.</li><li>Vilka attribut finns i XDM-schemat&quot;Luma: Custom Actions&quot;?</li></ul> |
| Effektanalys | Använd AI Assistant (äldre) för att identifiera dataobjekt som har använts i vissa arbetsflöden, så att du kan bedöma effekten av eventuella ändringar. | <ul><li>Vilka målgrupper använder `homeAddress.city` i Luma: PersonProfiles-schemat?</li><li>Vilka datauppsättningar lagras profilattributet `consents.marketing.push.val` i?</li></ul> |

{style="table-layout:auto"}

## Driftsinsikter per enhet och frågor om produktkunskap{#objects-questions}

Följande frågor grupperas efter dataobjekt och klassificeras antingen som [operativa insikter](./home.md#operational-insights) eller [produktkunskaper](./home.md#product-knowledge).

![](./images/prompt.png)

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
   * Vilka mål befinner sig i ett aktivt läge?
   * Vilka målkonton har 0 målgrupper aktiverade?
   * Hur många målgrupper aktiveras för varje mål?
   * Vilka destinationer har det högsta antalet aktiva målgrupper?
* **Resor - driftsinsikter**
   * Hur många resor har jag?
   * Vilka resor har skapats i {RELATIVE_DATE} (t.ex. den sista veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?
   * Visa mig listan över resor som har ändrats i {RELATIVE_DATE} (t.ex. den senaste veckan) eller {RELATIVE_DATE} (t.ex. före/efter/på ett visst datum)?
   * Ange de resor jag har.
   * Lista de målgrupper som används i live-resor.
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
* **Felsökning - produktkunskap (Real-Time CDP och Journey Optimizer)**
   * Vad kan AI Assistant (äldre) hjälpa till med?
   * Kan jag ta bort ett profilaktiverat schema efter att data har matats in?
   * Varför kan jag inte ta bort en publik?
   * Hur lång tid tar det för målgrupperna att utvärderas och resultaten blir tillgängliga för målinriktning?

## Tar hand om dina frågor {#phrasing-your-questions}

Du måste ge AI Assistant (äldre) en tydlig och sammanhangsberoende formulering för att få ett så korrekt svar som möjligt. Se följande lista med tips om hur du ställer en tydlig fråga i sitt sammanhang:

* Ange din uppgift och/eller fråga kortfattat.
* Undvik tvetydigt språk och alltför komplex syntax för att underlätta förståelsen.
* Ange relevant sammanhang för din uppgift och/eller fråga eftersom kontext kan hjälpa AI Assistant (äldre) att generera mer relevanta svar.

Läs tabellerna nedan för mer information om de effektivaste strategierna när du ställer frågor till AI Assistant (äldre).

I följande tabeller beskrivs de effektivaste strategierna du kan följa när du använder AI Assistant (äldre):

| Gör | Exempel |
| --- | --- |
| <ul><li>Var tydlig med objektet eller informationen som du vill hämta eller analysera.</li><li>Försök att ange dataobjektens namn inom citattecken. Om du bara känner till en del av objektnamnet kan du även ange det i frågan.</li><li>Använd [objekt som fylls i automatiskt](./ui-guide.md#use-auto-complete) för att hjälpa AI Assistant (äldre) att förstå frågans sammanhang bättre.</li></ul> | <ul><li>Vilka datauppsättningar använder schemat&quot;Luma - Loyalty&quot;?</li><li>Visa de aktiverade segmenten som har &quot;Luma&quot; i sina namn. Rangordna dem efter antal profiler.</li></ul> |
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

## Datauppsättningssynlighet {#dataset-observability}

AI Assistant (äldre) kan nu besvara frågor om specifika datamängdsmått som lagringsstorlek och radantal.

* Vilka är mina största datauppsättningar efter storlek?
* Vilken är min största datauppsättning av rader?
* Hur många datauppsättningar är tomma?
* Vilka datauppsättningar är tomma?

Dessutom kan ni förmedla liknande avsikter via ett antal olika varianter till de fyra ovannämnda frågorna.

+++Välj det här alternativet om du vill visa godkända variationer av frågor om datauppsättningens observerbarhet

* Vilka är de fem viktigaste datauppsättningarna efter storlek?
* Vilken datauppsättning har det största antalet rader?
* Hur många datauppsättningar saknar data?
* Vill du visa datauppsättningar med en storlek på >10 MB?
* Visa datauppsättningar med rader under 10.
* Kan du visa de datauppsättningar som är helt tomma?
* Vilken datamängd är störst av lagringsstorleken?
* Vilken är den minsta datauppsättningen när det gäller radantal?
* Hur många av mina datauppsättningar har data och hur många är tomma?
* Vad är antalet rader för datauppsättningen med namnet {DATASET_NAME}?
* Hur är storleken på {DATASET_NAME} jämfört med mina andra datauppsättningar?
* Vilken är storleken på {DATASET_NAME}?
* Hur många rader har {DATASET_NAME}?
* Vad är storleken och antalet rader för {DATASET_NAME}?
* Kan du lista de största och minsta datauppsättningarna efter lagringsstorlek?

+++

Du kan också förfina dina frågor om datasynlighet med en kvalificerare för att filtrera frågan efter en viss tidsperiod:

* Datauppsättningar som tar emot batchar under de senaste (x) dagarna
* Datauppsättningar som inte tar emot batchar under de senaste (x) dagarna
* Datauppsättningar med de mest insamlade data de senaste (x) dagarna
* Antal poster för en viss datauppsättning under de senaste (x) dagarna

+++Välj det här alternativet om du vill visa godkända variationer av frågor om datauppsättningens observerbarhet

* Hur många datauppsättningar har tagit emot batchar under de senaste (x) dagarna?
* Vilka datauppsättningar har tagit emot batchar under de senaste (x) dagarna?
* Kan du lista de datauppsättningar som hade inhämtats under de senaste (x) dagarna?
* Hur många datauppsättningar fick nya batchar under de föregående (x) dagarna?
* Vilka datauppsättningar har uppdaterats med nya data under de senaste (x) dagarna?
* Visa datauppsättningar som haft batchaktivitet under de senaste (x) dagarna.
* Hur många datauppsättningar har inte tagit emot batchar under de senaste (x) dagarna?
* Vilka datauppsättningar har inte tagit emot några batchar under de senaste (x) dagarna?
* Kan du identifiera datauppsättningar utan dataintag under de senaste (x) dagarna?
* Hur många datauppsättningar fick inte uppdateringar under de senaste (x) dagarna?
* Vilka datauppsättningar har varit inaktiva de senaste (x) dagarna?
* Visa datauppsättningar som inte har fått nya grupper under de senaste (x) dagarna.
* När var senaste gången data hämtades på datauppsättningen (x)?
* Vilka är de tio populäraste datauppsättningarna där de flesta data har importerats under de senaste (x) dagarna?
* Vilka är de 10 viktigaste datauppsättningarna per datavolym som har importerats under de senaste (x) dagarna?
* Vilka 10 datauppsättningar hade det största dataintaget de senaste (x) dagarna?
* Visa de 10 främsta datauppsättningarna med det högsta dataintaget under de föregående (x) dagarna.
* Vilka är de viktigaste datauppsättningarna för data som tagits emot under de senaste (x) dagarna?
* Visa en lista över de 10 mest använda datauppsättningarna som har inhämtat de senaste (x) dagarna.
* Hur många poster har tagits emot i datauppsättningen (x) under de senaste (y) dagarna?
* Hur många poster har datauppsättningen (x) fått under de senaste (y) dagarna?
* Hur många poster har importerats för datauppsättningen (x) under de senaste (y) dagarna?
* Kan du ange antalet poster som lagts till i datauppsättningen (x) under de senaste (y) dagarna?
* Hur mycket data har tagits emot av datauppsättningen (x) under de senaste (y) dagarna?
* Hur många poster som har importerats för datauppsättningen (x) under de föregående (y) dagarna?

+++


## Exempel på frågor som inte stöds {#unsupported-questions}

Nedan följer ett antal exempel på frågor som för närvarande inte stöds av AI Assistant (äldre).

+++Markera för att visa exempel på frågor som inte stöds

### Driftsinsikter

* Hur många profiler finns det i den här sandlådan i Kalifornien? (**Obs!**: för liknande frågor måste du ange ett specifikt villkor för att ge tillräckligt med innehåll för din begäran. I det här fallet är det specifika villkoret&quot;live in California&quot;).
* Vilka segment finns den här profilen i {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Hur många profiler i datauppsättningen har ett e-postmeddelande?
* Vilken datauppsättning utgör det maximala antalet profiler i den här sandlådan?
* Hur många segment har tagits bort i {RELATIVE_DATE}?
* Ge mig en profil i {AUDIENCE_NAME}.
* Vad är det totala antalet profiler i min sandlåda?
* Hur många identitetsnamnutrymmen är associerade med målgruppen {AUDIENCE_NAME}?
* Visa mig en rapport över alla målgruppssegment som utvärderats idag
* Hur många segment har överlappande profiler?
* Hur många batchar som läses in {DATASET_NAME}
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

Genom att läsa det här dokumentet får du nu en förståelse för hur du kan optimera dina frågor för AI Assistant (äldre). Mer information om hur du använder funktionen under arbetsflöden finns i [AI Assistant (äldre) gränssnittshandboken &#x200B;](ui-guide.md).
