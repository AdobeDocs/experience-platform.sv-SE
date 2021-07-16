---
title: YouTube Video Tracking Extension - översikt
description: Läs mer om taggtillägget YouTube Video Tracking i Adobe Experience Platform.
source-git-commit: 5da1fd18e0032c5e3d6695639f98a7ee683819f1
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# Översikt över tillägget YouTube Video Tracking

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

**Förutsättningar**

För varje taggegenskap i Adobe Experience Platform krävs att följande tillägg installeras och konfigureras från skärmen Tillägg:

* Adobe Analytics
* Experience Cloud Visitor ID-tjänst
* Kärntillägg

Använd [&quot;Bädda in en spelare med taggen \&lt;iframe\>&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) från Googles utvecklardokument i HTML-koden för varje webbsida där en videospelare ska återges.

Det här tillägget, version 2.0.1, stöder inbäddning av en eller flera YouTube-videofilmer på en enda webbsida genom att infoga ett `id`-attribut med ett unikt värde i skripttaggen iframe och lägga till `enablejsapi=1` och `rel=0` i slutet av attributvärdet `src`, om det inte redan finns. Exempel:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Tillägget är även utformat för att dynamiskt kontrollera om det finns ett unikt ID-attributvärde, som `player1`, oavsett om frågesträngsparametrarna `enablejsapi` och `rel` finns och om deras förväntade värden är korrekta. Därför kan YouTube-skripttaggen läggas till på en webbsida med eller utan attributet `id` och om frågesträngsparametrarna `enablejsapi` och `rel` inkluderas eller inte.

>[!NOTE]
>
>På sidor med mer än en video använder varje video samma konfigurationsuppsättning som i taggregeln som körs på den sidan. Om du till exempel skapar en regel med en händelse som utlöser en 50 % slutförd video, utlöser varje video på sidan regeln vid referenspunkten 50 %.

Tillägget använder följande logik för att skriva om iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Det innebär att det blir ett lätt flimmer när sidan har lästs in. Detta beteende förväntas.

## Dataelement

Det finns sex tillgängliga dataelement i tillägget, varav inget kräver konfiguration.

* **Spelhuvudsposition:** Spelhuvudets placering i sekunder på tidslinjen när den anropas inom en tagg.
* **Video-ID:** Anger det YouTube-ID som är kopplat till videon.
* **Videonamn:** Anger videons beskrivande eller egna namn.
* **Video-URL:** Returnerar YouTube.com-URL:en för den inlästa/uppspelande videon.
* **Videotid:** Spelar in den totala längden (i sekunder) för videoinnehållet.
* **Tilläggsversion:** Det här dataelementet registrerar YouTube Tracking Extension-versionen, till exempel &quot;Video Tracking_YouTube_2.0.0&quot;.

## Händelser

Det finns åtta tillgängliga händelser i tillägget. Endast anpassad punktspårning kräver konfiguration.

* **Video Ready:** Utlöses när videon är klar att spelas upp.
* **Videostart:** utlöses när videon startas första gången och när  `player.getCurrentTime() === 0`
* **Videouppspelning:** Utlöses när videon spelas upp och spelas upp efter den första starten. Den här utlösaren aktiveras vid varje uppspelning.
* **Videopaus:** Utlöses när videon pausas.
* **Återuppta video:** utlöses när videon återupptas och när  `player.getCurrentTime() !== 0`
* **Custom Cue Tracking:** Utlösare när videon når det angivna tröskelvärdet i procent. Om en video till exempel är 60 sekunder och den angivna referenspunkten är 50 %, utlöses händelsen när spelhuvudets position är 30 sekunder. Referenspunktsspårning gäller både för inledande uppspelning och uppspelning. Observera att händelsen inte utlöses om användaren söker över en referenspunkt. Referenspunktshändelser utlöses bara när spelhuvudet korsar den beräknade referenspunktspositionen på tidslinjen och videospelaren spelas upp.
* **Videobuffert:** Utlöses när spelaren hämtar en viss mängd data innan videon börjar spelas upp.
* **Video avslutad:** Utlöses när en video är klar.

## Användning

En taggregel kan anges för varje videohändelse (de sju händelserna ovan). Skapa en specifik taggregel för varje händelse som du vill spåra. Om du inte vill spåra en händelse utelämnar du helt enkelt att skapa en regel för den.

Regler har tre åtgärder:

* **Ange variabler:** Ange Adobe Analytics-variabler (mappa till alla eller vissa inkluderade dataelement).
* **Skicka fyr:** Skicka Adobe Analytics-fyren som ett anpassat länkspårningsanrop och ange ett länknamn.
* **Rensa variabler:** Rensa Adobe Analytics-variabler.

## Exempeltaggregel för&quot;Videostart&quot;

Följande videotilläggsobjekt ska inkluderas.

* **Händelser**: &quot;Videostart&quot; (Den här händelsen aktiverar regeln när besökaren börjar spela upp en YouTube-video.)

* **Villkor**: Ingen

* **Åtgärder**: Använd  **Analytics-** tillägget för att ange variabler för att mappa:

   * Händelsen för videostart,
   * Ett prop/eVar för videovaraktighetsdataelementet
   * Ett prop/eVar för Video ID-dataelementet
   * Ett prop/eVar för videonamnets dataelement
   * Ett prop/eVar för Video URL-dataelementet

   Inkludera sedan åtgärden&quot;Skicka signal&quot; (`s.tl`) med länknamnet&quot;videostart&quot; följt av åtgärden&quot;Rensa variabler&quot;.

>[!TIP]
> 
>För implementeringar där flera eVars- eller props för varje videoelement inte kan användas, kan dataelementvärden sammanfogas inom Platform, parsas i klassificeringsrapporter med hjälp av verktyget Klassificeringsregelbyggaren, som förklaras i [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html), och sedan tillämpas som ett segment i Analysis Workspace.

Om du vill sammanfoga videoinformationsvärden skapar du ett nytt dataelement som kallas&quot;Videometadata&quot; och programmerar det så att det hämtas in alla videodataelement (som listas ovan) och sammanställer dem. Exempel:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
