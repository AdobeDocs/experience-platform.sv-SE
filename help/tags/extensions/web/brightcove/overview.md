---
title: Översikt över tillägget för videospårning i BrightStor
description: Lär dig mer om taggtillägget för videospårning i BrightStor i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---

# Översikt över tillägget för videospårning i BrightStor

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

## Krav

För varje taggegenskap i Adobe Experience Platform krävs följande tillägg som är installerade och konfigurerade på tilläggsskärmen:

* Adobe Analytics
* Experience Cloud Visitor ID-tjänst
* Kärntillägg har installerats

Använd kodfragmentet&quot;In-Page embed code (Advanced)&quot; i HTML-koden för varje webbsida där en videospelare ska återges. HTML-kodfragmentet &quot;In-Page Embed code (Advanced)&quot; finns i [dokumentationen för Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Följande länk innehåller mer information om [hur du genererar inbäddad kod för både förhandsgransknings- och publicerade videospelare](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

Tilläggsversion 1.1.0 stöder inbäddning av flera BrightStor-videor på en enda webbsida. Om det finns flera `id`-egenskaper i de avancerade inbäddningstaggarna kontrollerar du att de har unika värden. Till exempel `player1`, `player2` och så vidare.

>[!NOTE]
>
>På sidor med flera videoklipp använder varje video samma konfigurationsuppsättning som i den taggregel som körs på den sidan. Om du till exempel skapar en regel med en händelse som utlöser en video som är 50 % färdig, utlöser varje video på sidan regeln vid referenspunkten 50 %.

Om webbsidan som använder det här tillägget interagerar med videon innan det aktuella skriptet har lästs in fullständigt, finns det två åtgärder du kan vidta för att åtgärda problemet. Först kan taggbiblioteket läsas in synkront och sedan placerar du `<script type="text/javascript">\_satellite.pageBottom();\</script\>`-elementet före videoinbäddningen på sidan.

Mer information om komponentmetoder och -händelser som används i det här tillägget finns i [API-dokumentationen för BrightStor](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer).

## Dataelement

Det finns sju dataelement tillgängliga i tillägget, varav inget kräver konfiguration.

* **Spelhuvudsposition:** När det här dataelementet anropas inom en taggregel spelas positionen för spelhuvudets position på tidslinjen in i sekunder.
* **ID för videokonto:** Detta dataelement registrerar ID för det Brightcove-konto som publicerade videon.
* **Videovaraktighet:** Det här dataelementet registrerar den totala längden, i sekunder, för videoinnehållet. Dessutom kan ett beräknat mätvärde skapas i Analytics för att konvertera antalet i sekunder till minuter eller timmar.
* **Stöd för videoannonsering:** Detta dataelement anger om annonser stöds i videon eller inte.
* **Video-ID:** Detta dataelement anger det BrightStor-ID som är kopplat till videon.
* **Videonamn:** Detta dataelement anger videofilens beskrivande eller egna namn.
* **Videotaggar:** Detta dataelement anger de specifika skript som är associerade med videon.

## Händelser

Det finns sju tillgängliga händelser i tillägget. Endast anpassad punktspårning kräver konfiguration.

* **Anpassad referenspunktsspårning:** Den här händelsen utlöses när videon når det angivna tröskelvärdet i procent. Om en video till exempel är 60 sekunder lång och den angivna referenspunkten är 50 %, utlöses händelsen vid 30-sekundersmarkeringen.

>[!NOTE]
>
>Observera att den här händelsen utlöses varje gång referenspunkten nås. Om användaren till exempel når upp till 50 %-märket, söker efter videon före 50 %-markeringen och sedan når 50 %-markeringen igen, aktiveras utlösaren igen.

* **Video slutförd:** Den här händelsen utlöses när en video har slutförts helt.
* **Inlästa metadata för video:** Den här händelsen utlöses när spelaren har fått inledande tids- och dimensionsinformation.
* **Videopaus:** Den här händelsen utlöses när videon pausas.
* **Återuppta video:** Den här händelsen utlöses när videoinnehållet återupptas efter en pause-händelse.
* **Ändring av videobildskärm:** Händelsen utlöses när videon växlar in eller ut från helskärmsläge.
* **Videostart:** Den här händelsen utlöses när videoinnehållet startar för första gången.

## Användning

En taggregel kan anges för varje videohändelse (de sju händelserna ovan). Skapa en specifik taggregel för varje händelse som du vill spåra. Om du inte vill spåra en händelse utelämnar du helt enkelt att skapa en regel för den.

Reglerna har tre åtgärder:

1. Ange Adobe Analytics-variabler. (Skapa dataelement för alla eller några av dataelementen som listas ovan.)
1. Skicka Adobe Analytics fyr.
1. Rensa Adobe Analytics-variablerna.

## Exempelmärkordsregel för &quot;Videostart&quot;

Följande videotilläggsobjekt ska inkluderas:

* **Händelser**

   1. &quot;Videostart&quot;: Den här händelsen gör att regeln utlöses när besökaren börjar spela upp en BrightStor-video.

* **Villkor**

   1. Ingen

* **Instruktioner**

   1. Ange följande i en Analytics-åtgärd,&quot;Set Variables&quot;:

      * Händelsen för **videostart** (exempel: event17)
      * Ett prop/eVar för **videoelementet** (exempel: eVar10)
      * Ett prop/eVar för **videovaraktigheten**-dataelementet (exempel: eVar11)
      * Ett prop/eVar för **det aktuella videoplatselementet** (exempel: eVar12)
   1. Analysåtgärden&quot;Skicka Beacon&quot; (`s.tl`)
   1. Analysåtgärden&quot;Rensa variabler&quot;


>[!TIP]
>
>För dem som kanske inte vill etablera flera eVars eller props för varje videoelement finns det en alternativ metod. Värden för dataelement kan sammanfogas i användargränssnittet för datainsamling. Därefter parsas de i klassificeringsrapporter med verktyget Klassificeringsregelbyggaren. Mer information finns i [dokumentationen för verktyget Skapa klassificeringsregel](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html). Slutligen används de som ett segment i Analysis Workspace.
>
>Det gör du genom att skapa ett nytt dataelement som kallas &quot;Video MetaData&quot; och programmera det för att hämta in alla videodataelement (som listas ovan) och sammanfoga dem.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
