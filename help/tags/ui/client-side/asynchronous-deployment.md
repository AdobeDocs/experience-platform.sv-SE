---
title: Asynkron distribution
description: Lär dig hur du distribuerar taggbibliotek från Adobe Experience Platform asynkront på din webbplats.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# Asynkron distribution {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Asynkron distribution"
>abstract="Om det här alternativet är aktiverat börjar webbläsaren att läsa in JavaScript-filen när den här skripttaggen tolkas, men i stället för att vänta på att biblioteket ska läsas in och köras fortsätter den att analysera och återge resten av dokumentet. Detta kan förbättra webbsidans prestanda men har viktiga konsekvenser när det gäller hur vissa regler körs. Mer information finns i dokumentationen."

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Prestanda och icke-blockerande driftsättning av JavaScript-bibliotek som krävs av våra produkter blir allt viktigare för Adobe Experience Cloud-användare. verktyg som [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) rekommenderar användare att ändra sitt sätt att distribuera Adobe-bibliotek på sin webbplats. I den här artikeln beskrivs hur du använder JavaScript-bibliotek i Adobe på ett asynkront sätt.

## Synkron jämfört med asynkron

### Synkron distribution

Biblioteken läses ofta in synkront i `<head>` -tagg för en sida. Exempel:

```markup
<script src="example.js"></script>
```

Som standard tolkar webbläsaren dokumentet och når den här raden. Sedan börjar webbläsaren hämta JavaScript-filen från servern. Webbläsaren väntar tills filen returneras, tolkar och kör sedan JavaScript-filen. Slutligen fortsätter den att analysera resten av HTML-dokumentet.

Om tolken visas över `<script>` -taggen innan synligt innehåll återges, kommer visningen av innehållet att fördröjas. Om JavaScript-filen som läses in inte är absolut nödvändig för att visa innehåll för dina användare, behöver du inte nödvändigtvis vänta på innehållet. Ju större bibliotek, desto längre fördröjning.  Därför är prestandatestverktyg som [!DNL Google PageSpeed] eller [!DNL Lighthouse] flagga ofta synkront inlästa skript.

Tagghanteringsbibliotek kan snabbt bli stora om du har många taggar att hantera.

### Asynkron distribution

Du kan läsa in alla bibliotek asynkront genom att lägga till en `async` attributet till `<script>` -tagg. Exempel:

```markup
<script src="example.js" async></script>
```

Detta anger för webbläsaren att när skripttaggen tolkas ska webbläsaren börja läsa in JavaScript-filen, men i stället för att vänta på att biblioteket ska läsas in och köras bör den fortsätta att tolka och återge resten av dokumentet.

## Att tänka på vid asynkron distribution

I synkrona distributioner pausar webbläsaren parsning och återgivning av sidan medan taggbiblioteket i Adobe Experience Platform läses in och körs, vilket beskrivs ovan. I asynkrona distributioner fortsätter webbläsaren däremot att analysera och återge sidan medan biblioteket läses in. Variabiliteten i när taggbiblioteket kan slutföra inläsningen i relation till sidtolkning och återgivning måste beaktas.

För det första, eftersom taggbiblioteket kan slutföra inläsningen före eller efter sidans nederkant har tolkats och körts, bör du inte längre anropa `_satellite.pageBottom()` från sidkoden (`_satellite` är inte tillgängligt förrän biblioteket har lästs in). Detta förklaras i [Inläsning av taggar bäddar in kod asynkront](#loading-the-tags-embed-code-asynchronously).

För det andra kan taggbiblioteket slutföra inläsningen före eller efter [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) webbläsarhändelse (DOM Ready) har inträffat.

På grund av dessa två punkter är det värt att visa hur [Bibliotek inläst](../../extensions/client/core/overview.md#library-loaded-page-top), [Sidan nederst](../../extensions/client/core/overview.md#page-bottom), [DOM-klart](../../extensions/client/core/overview.md#page-bottom)och [Fönster inläst](../../extensions/client/core/overview.md#window-loaded) händelsetyper från Core-tilläggsfunktionen när du läser in ett taggbibliotek asynkront.

Om taggegenskapen innehåller följande fyra regler:

* Regel A: använder händelsetypen Library Loaded
* Regel B: använder händelsetypen Sidundersida
* Regel C: använder händelsetypen DOM Ready
* Regel D: använder händelsetypen Window Loaded

Oavsett när taggbiblioteket har lästs in, kommer alla regler garanterat att köras och de kommer att köras i följande ordning:

Regel A → Regel B → Regel C → Regel D

Även om ordningen alltid används, kan vissa regler köras direkt när taggbiblioteket har lästs in, medan andra kan köras senare. Följande inträffar när taggbiblioteket har lästs in:

1. Regel A verkställs omedelbart.
1. Om `DOMContentLoaded` webbläsarhändelse (DOM Ready) har redan inträffat, regel B och regel C körs omedelbart. Annars körs regel B och regel C senare när [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) webbläsarhändelse inträffar.
1. Om [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) webbläsarhändelse (Window Loaded) har redan inträffat. Regel D körs omedelbart. Annars kommer regel D att köras senare när [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) webbläsarhändelse inträffar. Observera, att om du har installerat taggbiblioteket enligt instruktionerna, är taggbiblioteket *alltid* slutar läsa in före [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) webbläsarhändelse inträffar.

När du tillämpar dessa principer på din egen webbplats bör du tänka på följande:

* **En regel som använder händelsetypen Library Loaded kan köras innan datalagret har lästs in helt.**  Detta kan leda till att regelns åtgärder körs med data som saknas eftersom data ännu inte var tillgängliga på sidan. Den här typen av problem kan åtgärdas genom att du anpassar regelkonfigurationen. I stället för att ha en regel som aktiveras av händelsetypen Biblioteksinläsning kan du i stället använda händelsetypen Anpassad händelse eller Direktanrop som aktiveras av sidkoden så fort datalagret har lästs in.
* **Händelsetypen Sidundersida ger inte särskilt mycket värde när biblioteket läses in asynkront.**  Överväg i stället att använda händelsetyperna Library Loaded, DOM Ready, Window Loaded eller någon annan.

Om du ser saker som inte fungerar som de ska är det troligt att du har timingproblem att gå igenom. Distributioner som kräver exakt timing kan behöva använda händelseavlyssnare och händelsetypen Custom Event eller Direct Call för att göra implementeringarna mer robusta och konsekventa.

## Inläsning av taggar bäddar in kod asynkront

Med taggar kan du aktivera asynkron inläsning när du skapar en inbäddningskod när du konfigurerar en [miljö](../publishing/environments.md). Du kan också konfigurera asynkron inläsning själv:

1. Lägg till ett asynkront attribut i `<script>` -tagg för att läsa in skriptet asynkront.

   För taggarnas inbäddningskod innebär det att du ändrar detta:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   till detta:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Ta bort kod som du tidigare har lagt till längst ned i taggen:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Den här koden anger för plattformen att webbläsarparsern har nått sidans nederkant. Det är troligt att taggar inte har lästs in och körts tidigare och därför anropas `_satellite.pageBottom()` resulterar i ett fel och händelsetypen Sidslut kanske inte fungerar som förväntat.
