---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;enhetlig profil;enhetlig;profil;rtcp;XDM-diagram
title: Custom Accessibility Solutions for Experience Platform
topic: guide
type: Documentation
description: Läs mer om de anpassade tillgänglighetslösningarna i Adobe Experience Platform användargränssnitt.
source-git-commit: 81db01c3e8d332e1fc8127d779c3a584bb498858
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---


# Anpassade tillgänglighetslösningar för Experience Platform

Adobe Experience Platform har ständigt förbättrats för att tillgodose behoven hos alla typer av användare och följer världsstandarden som omfattar personer med nedsatt syn, hörsel, mobilitet eller andra funktionshinder. I det här dokumentet finns skräddarsydda tillgänglighetslösningar för Experience Platform i användargränssnittet.

## Översikt över startsidan och användargränssnittet

Användargränssnittet i Experience Platform uppfyller de kontrastförhållanden som krävs för normal text, bilder och gränssnittskomponenter. Färgerna i användargränssnittet har också valts för att ge stöd åt tillgänglighet för alla användare, även för dem med visuella funktionshinder.

I Platform kan även gränssnittselement som är klickbara eller kan användas med en pekare aktiveras med ett tangentbord. Detta inkluderar vänster navigering, videospelare, tabeller med mera.

Experience Platform strävar efter att följa internationella tillgänglighetsstandarder, inklusive Web Content Accessibility Guidelines 2.1 Level A och Level AA samt Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA).

![Adobe Experience Platform hemsida.](images/homepage.png)

## Vänster navigering

Den vänstra navigeringen i användargränssnittet för Experience Platform är tangentbordsanpassad och ger färgkontrast i normalt läge, hovring- och markeringsläge som uppfyller tillgänglighetsstandarder.

På hemskärmen kan användarna tabba in i den vänstra navigeringen. Om du väljer **Skift+Tabb** återgår användaren till hemskärmen.

![Experience Platform vänster navigering.](images/left-navigation-select.png)

Med den vänstra navigeringen i fokus tar **Tabb** användarna till interaktionen för att expandera och komprimera. Möjligheten att utöka eller komprimera den vänstra navigeringen aktiveras med **Enter (Return)**.

![Navigeringen Experience Platform till vänster komprimerades.](images/left-navigation-collapse.png)

Med den vänstra navigeringen i fokus navigerar upp- och nedpilarna till varje objekt i navigeringen och bläddrar kontinuerligt (med andra ord flyttas inte fokus förrän användaren tabbar bort från den vänstra navigeringen). Fokus visas för navigeringsobjekt när de är markerade. Den aktuella markeringen visas med en högdager och fet text. När du väljer ett vänstra navigeringsobjekt öppnar **Enter (Retur)** det valda gränssnittsobjektet i den högra panelen, men fokus ligger kvar i vänsternavigeringen tills användaren tabbar bort.

![Navigering Experience Platform till vänster med Källor markerat.](images/left-navigation-sources.png)

Vissa funktioner på plattformen är inte aktiverade för alla användare. Dessa objekt visas i navigeringen men kan inte markeras. När du navigerar med ett tangentbord hoppas dessa objekt över vid pilnavigering och kan inte markeras med **Enter (Return)**.

![De avsnitt av navigeringen till vänster i Experience Platform som inte är aktiverade för användaren kan inte markeras.](images/left-navigation-sections-disabled.png)

## Dialogrutan Inbäddad video

Videor kan visas i Experience Platform med tangentbordsnavigering för att markera och välja en tillgänglig videolänk. Då öppnas en inbäddad videodialogruta i användargränssnittet för plattformen.

![En blå kant visas runt ett markerat element för att ange att fokus har använts.](images/profile-overview-tab.png)

## Tangentbordstillgänglighet i dialogrutan Video

Du kan även navigera i den inbäddade videodialogrutan med hjälp av tangentbordet. I följande tabell visas den fullständiga tangentbordsnavigeringen som är tillgänglig för den inbäddade videodialogrutan.

| Dialogruteelement | Tangentbordstillgänglighet | Beskrivning |
|---|---|---|
| Spela upp och pausa | Tabb<br/>Blanksteg | Använd **Tabb** för att ställa in fokus på uppspelningsknappen. **Med** mellanslagstangenten startas videouppspelningen och videouppspelningen pausas. |
| Skrubber | Tabb<br/>Vänsterpil<br/>Högerpil | När videon spelas upp använder du **Tabb** för att fokusera navigeringen. När navigeringslisten är i fokus hoppar **vänster- och högerpilstangenterna** över videouppspelningen framåt respektive bakåt 5 sekunder. |
| Ljud av | Tabb<br/>Blanksteg | Använd **Tabb** för att fokusera volymelementet för ljud av. Använd **blanksteg** för att stänga av eller slå på videouppspelningen. |
| Volym | Tabb<br/>Vänsterpil<br/>Högerpil | Använd **Tabb** för att fokusera på volymelementet. **Vänster- och högerpilstangenterna** flyttar volymen uppåt respektive nedåt. |
| [!UICONTROL Closed Captions] (&quot;cc&quot;) | Tabb<br/>Ange<br/>Uppåtpil<br/>Nedåtpil | **** Tabto  [!UICONTROL Closed Captions] (&quot;cc&quot;)-element. Använd **Enter** för att öppna menyn och **upp- och nedpilarna** för att välja språk för bildtexter. **Enterprise** bekräftar ditt val. |
| [!UICONTROL Quality] | Tabb<br/>Ange<br/>Uppåtpil<br/>Nedåtpil | Använd **Tabb** för att fokusera [!UICONTROL Quality]-elementet. Använd **Enter** för att öppna menyn och **upp- och nedpilarna** för att välja videokvalitet. **Enterprise** bekräftar ditt val. |
| Helskärmsläge | Tabb<br/>Blanksteg eller Retur<br/>Esc | Använd **Tabb** för att fokusera helskärmselementet. Använd **blanksteg eller Enter** för att aktivera helskärmsläge. **Esc** (&quot;esc&quot;) avslutar helskärmsläget. |
| Stäng | Tabb<br/>Blanksteg eller Retur | Använd **Tabb** för att fokusera stängningsknappen. Använd **blankstegstangenten eller Enter**-tangenten för att stänga videodialogrutan. |

>[!NOTE]
>
>När som helst under uppspelningen kan Esc-tangenten (&quot;esc&quot;) användas för att stänga den inbäddade videodialogrutan.

![Den inbäddade videodialogen med nummer som identifierar navigeringselement på tangentbordet.](images/video-dialog.png)

## Dra och släpp filer

I Experience Platform går det att komma åt alla dra och släpp-zoner för filmarkering via tangentbordet. Om du använder **tabbtangenten** för att markera **[!UICONTROL Choose files]** och **Enter eller blankstegstangenten** för att markera den anropas operativsystemets filvalsgränssnitt.

När en fil har överförts kan du ta bort den markerade filen med en borttagningsikon och överföra en ny. Användare kan använda **Tabb** för att fokusera på borttagningsikonen och **Ange eller blanksteg** för att markera den. När filen har tagits bort är **[!UICONTROL Choose files]** automatiskt i fokus och kan markeras.

Om filen som överförs inte har rätt format visas en felikon tillsammans med ett felmeddelande och knappen **[!UICONTROL Choose files]** är i fokus och kan markeras.

![En dra och släpp-zon med ett felmeddelande och knappen Välj filer i fokus.](images/drag-and-drop.png)

Om du använder en mus för att markera dra och släpp-zonen anropas även gränssnittet för filval, eller så kan en musanvändare markera en fil och dra till zonen för att börja överföra den.

![En dra och släpp-zon som är i fokus när en musanvändare drar en fil till zonen.](images/drag-and-drop-mouse-over.png)

## Bläddra i tabeller

Alla tabeller i användargränssnittet i Experience Platform går att komma åt via tangentbordet. Det går att bläddra och interagera med tabellrader och kolumner via en serie kortkommandon:

* I tabellhuvudet använder du **nedpilen** för att bläddra i tabellen. Tabellrubriker kan markeras när du navigerar via **Tabb**, och du kan ändra sorteringsordningen med **blanksteg**.
* **Uppåt- och nedåtpilarna** rör sig uppåt och nedåt genom raderna i tabellen.
* När en rad är markerad eller i fokus kan du använda **Enter** på raden för att få information i den högra listen.
* När en rad är markerad eller i fokus använder du **piltangenterna** för att flytta mellan varje objekt på raden.
* Använd **Ange** för att markera ett objekt i raden. Användare med skärmläsare får ett varningsmeddelande om ett nytt fönster måste öppnas.

### Bläddra bland tabellens tangentbordstillgänglighet

| Tangentbordstillgänglighet | Beskrivning |
|---|---|
| HOME (Function + vänsterpil) | När raden är i fokus flyttar användare till det första objektet på raden |
| END (Funktion + högerpil) | När raden är i fokus flyttar användare till det sista objektet på raden |
| Page up | Går 10 rader uppåt i tabellen (per sida) |
| Sida ned | Går igenom 10 rader nedåt i tabellen (per sida) |
| Ctrl + HOME | Går till första raden i tabellen |
| Ctrl + END | Går till första ordet i tabellen per sida |

## Gränssnittet för schemaredigeraren

Gränssnittet för schemaredigeraren är tillgängligt med följande funktioner:

* Schemaredigeraren stöder tangentbordsnavigering, inklusive användning av **Tabb** för navigering via gränssnittselement.
* **I** Tabbar anges sökfältet och sedan i schematrädet.
* Schematrädet stöder användning av piltangenter för att navigera i schematrädets gränssnitt
   * **Upp- och nedpilarna** kan användas för att gå igenom trädet.
   * **Vänster och höger** pilspets kan användas för att expandera och komprimera noder eller flytta mellan infogade åtgärder i schematrädet.
* **Med Retur** aktiveras enskilda noddetaljer på detaljpanelen till höger.
* Tangenten **Hem** går tillbaka till trädets övre del.
* **End**-tangenten navigerar till trädns nederkant.
* Schematrädet innehåller även ARIA-etiketter för skärmläsare.

## Segmentbyggargränssnitt

När du använder användargränssnittet i Segment Builder för att skapa, redigera och interagera med segment i Experience Platform förbättras tillgängligheten med följande funktioner:

* Gränssnittet för segmentbyggaren är tillgängligt via tangentbordsnavigering.
* Skärmläsare bör känna igen märkord för rubriker och kan meddela rubriken tillsammans med nivån.
* Andra hjälpmedelstekniker kan ändra den visuella visningen av en sida genom att använda korrekt kodade rubriker för att visa en disposition eller alternativ vy.

## Frågetjänstredigerare

Följande tillgänglighetsfunktioner är tillgängliga i frågetjänstens redigerare:

* Färgkontrast i redigeringsgränssnittet för frågetjänsten uppfyller kraven för tillgänglighet.
* Tangentbordsnavigering stöds utanför redigerarens användargränssnitt. Redigerarens användargränssnitt är en inbäddad kodspegling.

## Fliken Systemvy i Källor och Destinationer

När du bläddrar i **[!UICONTROL System View]** i Källor och Destinationer förbättras tillgängligheten med följande funktioner:

* **Fästpunkterna** fokuserar på det första källanslutningskortet
   * **Fokusera** på knappen i kortet igen
   * Välj **Ange** om du vill aktivera knappen för att ringa till åtgärd i kortet
* Om du väljer **Enter** på anslutningskortet aktiveras även mer information i den högra listen
   * När den högra listen är aktiverad ställs fokus in på det området. **Tabbar** fokuserar på  **** stängning för den högra rutan. Om du väljer **Tabb** igen flyttas fokus genom panelen för den högra listen
   * Om det finns mer än ett källanslutningskort förflyttar sig **Tabb** mellan anslutningarna
   * Använd **piltangenterna (upp, ned, vänster och höger)** för att gå igenom källlistan
   * Välj **Tabb** för att ange fokus på panelen för den högra listen