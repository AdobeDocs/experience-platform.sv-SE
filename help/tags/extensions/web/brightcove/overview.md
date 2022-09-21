---
title: Översikt över tillägget för videospårning i BrightStor
description: Lär dig mer om taggtillägget för videospårning i BrightStor i Adobe Experience Platform.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---

# Översikt över tillägget för videospårning i BrightStor

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

## Krav

För varje taggegenskap i Adobe Experience Platform krävs följande tillägg som är installerade och konfigurerade på tilläggsskärmen:

* Adobe Analytics
* Experience Cloud Visitor ID-tjänst
* Kärntillägg har installerats

Använd kodfragmentet&quot;In-Page embed code (Advanced)&quot; HTML på varje webbsida där en videospelare ska återges. HTML-utdraget &quot;In-Page Embed code (Advanced)&quot; finns i [Brightcove-dokumentation](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Följande länk innehåller mer information om [hur du genererar inbäddad kod för både förhandsgransknings- och publicerade videospelare](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

Tilläggsversion 1.1.0 stöder inbäddning av flera BrightStor-videor på en enda webbsida. Om det finns flera `id` -egenskaper i de avancerade inbäddningstaggarna, se till att de har unika värden. Till exempel: `player1`, `player2`och så vidare.

>[!NOTE]
>
>På sidor med flera videoklipp använder varje video samma konfigurationsuppsättning som i den taggregel som körs på den sidan. Om du till exempel skapar en regel med en händelse som utlöser en video som är 50 % färdig, utlöser varje video på sidan regeln vid referenspunkten 50 %.

Om webbsidan som använder det här tillägget interagerar med videon innan det aktuella skriptet har lästs in fullständigt, finns det två åtgärder du kan vidta för att åtgärda problemet. För det första kan taggbiblioteket läsas in synkront och för det andra måste du placera `<script type="text/javascript">\_satellite.pageBottom();\</script\>` -element före videoinbäddningen på sidan.

Se [Dokumentation för BrightStor API](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) för mer information om komponentmetoder och -händelser som används i det här tillägget.

## Dataelement

Det finns sju dataelement tillgängliga i tillägget, varav inget kräver konfiguration.

* **Spelhuvudsposition:** När det här dataelementet anropas inom en taggregel spelas det in i sekunder som spelhuvudets placering på videons tidslinje.
* **ID för videokonto:** Detta dataelement registrerar ID:t för det Brightcove-konto som publicerade videon.
* **Videotid:** Det här dataelementet registrerar den totala längden (i sekunder) för videoinnehållet. Dessutom kan ett beräknat mätvärde skapas i Analytics för att konvertera antalet i sekunder till minuter eller timmar.
* **Stöd för videoreklam:** Det här dataelementet anger om annonser stöds i videon eller inte.
* **Video-ID:** Detta dataelement anger det BrightCove-ID som är associerat med videon.
* **Videonamn:** Detta dataelement anger videofilens beskrivande, eller egna namn.
* **Videotaggar:** Detta dataelement anger de specifika skript som är associerade med videon.

## Händelser

Det finns sju tillgängliga händelser i tillägget. Endast anpassad punktspårning kräver konfiguration.

* **Spårning av anpassad referenspunkt:** Den här händelsen utlöses när videon når det angivna tröskelvärdet för video i procent. Om en video till exempel är 60 sekunder lång och den angivna referenspunkten är 50 %, utlöses händelsen vid 30-sekundersmarkeringen.

>[!NOTE]
>
>Observera att den här händelsen utlöses varje gång referenspunkten nås. Om användaren till exempel når upp till 50 %-märket, söker efter videon före 50 %-markeringen och sedan når 50 %-markeringen igen, aktiveras utlösaren igen.

* **Video klar:** Den här händelsen utlöses när en video är klar.
* **Inlästa metadata för video:** Den här händelsen utlöses när spelaren har fått inledande information om varaktighet och dimension.
* **Pausa video:** Den här händelsen utlöses när videon pausas.
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

      * Händelsen för **Videostart** (exempel: event17)
      * Ett proffs/en eVar för **Videonamn** dataelement (exempel: eVar10)
      * Ett proffs/en eVar för **Videotid** dataelement (exempel: eVar11)
      * Ett proffs/en eVar för **Aktuell videoplats** dataelement (exempel: eVar12)
   1. Analysåtgärden&quot;Skicka Beacon&quot; (`s.tl`)
   1. Analysåtgärden&quot;Rensa variabler&quot;


>[!TIP]
>
>För dem som kanske inte vill tillhandahålla flera eVars eller props för varje videoelement sammanfogas datavärdesvärden som en alternativ metod. Därefter parsas de i klassificeringsrapporter med verktyget Klassificeringsregelbyggaren. Se [Verktyget Skapa klassificeringsregel](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) mer information. Slutligen används de som ett segment i Analysis Workspace.
>
>Det gör du genom att skapa ett nytt dataelement som kallas &quot;Video MetaData&quot; och programmera det för att hämta in alla videodataelement (som listas ovan) och sammanfoga dem.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
