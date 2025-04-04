---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;enhetlig profil;enhetlig;profil;rtcp;XDM-diagram
title: Custom Accessibility Solutions for Experience Platform
type: Documentation
description: Läs mer om tillgänglighetslösningarna i Adobe Experience Platform användargränssnitt.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# Anpassade tillgänglighetslösningar för Experience Platform

Adobe Experience Platform har ständigt förbättrats för att tillgodose behoven hos alla typer av användare och följer världsstandarden som omfattar personer med nedsatt syn, hörsel, mobilitet eller andra funktionshinder. I det här dokumentet beskrivs anpassade tillgänglighetslösningar i Experience Platform användargränssnitt.

## Översikt över startsidan och användargränssnittet

Experience Platform gränssnitt uppfyller de kontrastförhållanden som krävs för normal text, grafik och gränssnittskomponenter. Färgerna i användargränssnittet har också valts för att ge stöd åt tillgänglighet för alla användare, även för dem med visuella funktionshinder.

I kan även gränssnittselement som är klickbara eller kan användas med en pekare aktiveras med ett tangentbord. Detta inkluderar vänster navigering, videospelare, tabeller med mera.

Experience Platform strävar efter att följa internationella tillgänglighetsstandarder, inklusive Web Content Accessibility Guidelines 2.1 Level A och Level AA samt Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA).

![Adobe Experience Platform-gränssnittets hemsida.](images/homepage.png)

## Vänster navigering

Den vänstra navigeringen i Experience Platform-användargränssnittet går att komma åt via tangentbordet och ger färgkontrast vid normal, hovring och markering som uppfyller tillgänglighetsstandarder.

På hemskärmen kan användarna tabba in i den vänstra navigeringen. Om du väljer **Skift+Tabb** återgår användaren till hemskärmen.

![Experience Platform har lämnat navigeringen.](images/left-navigation-select.png)

Med den vänstra navigeringen i fokus tar **Tabb** användare till interaktionen för att expandera och komprimera. Möjligheten att utöka eller komprimera den vänstra navigeringen aktiveras med **Enter (Retur)**.

![Navigeringen för vänster Experience Platform har komprimerats.](images/left-navigation-collapse.png)

Med den vänstra navigeringen i fokus navigerar upp- och nedpilarna till varje objekt i navigeringen och bläddrar kontinuerligt (med andra ord flyttas inte fokus förrän användaren tabbar bort från den vänstra navigeringen). Fokus visas för navigeringsobjekt när de är markerade. Den aktuella markeringen visas med en högdager och fet text. När du väljer ett vänstra navigeringsobjekt öppnar **Enter (Retur)** det valda gränssnittsobjektet i den högra panelen, men fokus ligger kvar i den vänstra navigeringen tills användaren tabbar bort.

![Experience Platform lämnade navigeringen med Källor markerat.](images/left-navigation-sources.png)

Vissa funktioner i Experience Platform är inte aktiverade för alla användare. Dessa objekt visas i navigeringen men kan inte markeras. När du navigerar med ett tangentbord hoppas dessa objekt över vid pilnavigering och kan inte markeras med **Enter (Retur)**.

![Delar av den vänstra navigeringen i Experience Platform som inte är aktiverade för användaren kan inte markeras.](images/left-navigation-sections-disabled.png)

## Dialogrutan Inbäddad video

Videor kan visas i Experience Platform med tangentbordsnavigering för att markera och välja en tillgänglig videolänk. Då öppnas en inbäddad videodialogruta i Experience Platform-gränssnittet.

![En blå kantlinje visas runt ett markerat element som anger att fokus har använts.](images/profile-overview-tab.png)

## Tangentbordstillgänglighet i dialogrutan Video

Du kan även navigera i den inbäddade videodialogrutan med hjälp av tangentbordet. I följande tabell visas den fullständiga tangentbordsnavigeringen som är tillgänglig för den inbäddade videodialogrutan.

| Dialogruteelement | Tangentbordstillgänglighet | Beskrivning |
|---|---|---|
| Spela upp och pausa | Tabb<br/>Blanksteg | Använd **Tabb** för att ange fokus på uppspelningsknappen. **Mellanslag** startar videouppspelningen och pausar videouppspelningen. |
| Skrubber | Tabb<br/>Vänsterpil<br/>Högerpil | När videon spelas upp använder du **Tabb** för att fokusera navigeringen. När navigeringslisten är i fokus hoppar **vänster- och högerpilstangenterna** över videouppspelning framåt respektive bakåt 5 sekunder. |
| Ljud | Tabb<br/>Blanksteg | Använd **Tabb** om du vill fokusera på volymelementet för ljud av. Använd **mellanslagstangenten** för att stänga av eller slå på videouppspelningen. |
| Volym | Tabb<br/>Vänsterpil<br/>Högerpil | Använd **Tabb** för att fokusera på volymelementet. **Vänster- och högerpilstangenter** flyttar volymen uppåt respektive nedåt. |
| [!UICONTROL Closed Captions] (cc) | Tabb<br/>Retur<br/>Uppåtpil<br/>Nedåtpil | **Tabba** till elementet [!UICONTROL Closed Captions] (&quot;cc&quot;). Använd **Retur** för att öppna menyn och **upp- och nedpilarna** för att välja språk för bildtexter. **Ange** bekräftar ditt val. |
| [!UICONTROL Quality] | Tabb<br/>Retur<br/>Uppåtpil<br/>Nedåtpil | Använd **Tabb** för att fokusera elementet [!UICONTROL Quality]. Använd **Retur** för att öppna menyn och **upp- och nedpilarna** för att välja videokvalitet. **Ange** bekräftar ditt val. |
| Helskärmsläge | Tabb<br/>Blanksteg eller Retur<br/>Esc | Använd **Tabb** för att fokusera helskärmselementet. Använd **blankstegstangenten eller Retur** för att aktivera helskärmsläge. **Esc** (&quot;esc&quot;) avslutar helskärmsläget. |
| Stäng | Tabb<br/>Blanksteg eller Retur | Använd **Tabb** för att fokusera på stängningsknappen. Använd **blankstegstangenten eller Retur** för att stänga videodialogrutan. |

>[!NOTE]
>
>När som helst under uppspelningen kan Esc-tangenten (&quot;esc&quot;) användas för att stänga den inbäddade videodialogrutan.

![Den inbäddade videodialogen med siffror som identifierar navigeringselement för tangentbordet.](images/video-dialog.png)

## Dra och släpp filer

I Experience Platform går det att komma åt alla dra och släpp-zoner för filval via tangentbordet. Om du använder **Tabb** för att markera **[!UICONTROL Choose files]** och **Enter eller blanksteg** för att markera den anropas operativsystemets filvalsgränssnitt.

När en fil har överförts kan du ta bort den markerade filen med en borttagningsikon och överföra en ny. Användare kan använda **Tabb** för att fokusera på borttagningsikonen och **Enter eller blanksteg** för att markera den. När filen har tagits bort är **[!UICONTROL Choose files]** automatiskt i fokus och kan markeras.

Om filen som överförs inte har rätt format visas en felikon med ett felmeddelande och knappen **[!UICONTROL Choose files]** är i fokus och kan markeras.

![En dra och släpp-zon med ett felmeddelande och knappen Välj filer i fokus.](images/drag-and-drop.png)

Om du använder en mus för att markera dra och släpp-zonen anropas även gränssnittet för filval, eller så kan en musanvändare markera en fil och dra till zonen för att börja överföra den.

![En dra och släpp-zon i fokus när en musanvändare drar en fil till zonen.](images/drag-and-drop-mouse-over.png)

## Bläddra i tabeller

Alla tabeller i Experience Platform användargränssnitt kan öppnas via tangentbordet. Det går att bläddra och interagera med tabellrader och kolumner via en serie kortkommandon:

* Använd **nedpilen** i tabellhuvudet för att bläddra i tabellen. Tabellrubriker kan markeras vid navigering via **Tabb**, och du kan ändra sorteringsordningen med **blanksteg**.
* **Upp- och nedpilarna** flyttas uppåt och nedåt genom raderna i tabellen.
* När en rad är markerad eller i fokus kan du använda **Retur** på raden för att få information i den högra listen.
* När en rad är markerad eller i fokus använder du **piltangenterna** för att flytta genom varje objekt på raden.
* Använd **Retur** för att markera ett objekt i raden. Användare med skärmläsare får ett varningsmeddelande om ett nytt fönster måste öppnas.
* När du zoomar till 200 % eller mer visas ikonen **rälsinspektören** när den högra rälen komprimeras för att ge mer visningsutrymme för tabellen.

![Ikonen för spårkontrollen är i fokus när en användare zoomar till 200 %.](images/rail-inspector.png)

### Bläddra bland tabellens tangentbordstillgänglighet

| Tangentbordstillgänglighet | Beskrivning |
|---|---|
| HOME (Function + vänsterpil) | När raden är i fokus flyttar användare till det första objektet på raden |
| END (Funktion + högerpil) | När raden är i fokus flyttar användare till det sista objektet på raden |
| Page up | Går tio rader uppåt i tabellen (per sida) |
| Sida ned | Går igenom 10 rader nedåt i tabellen (per sida) |
| Ctrl + HOME | Går till första raden i tabellen |
| Ctrl + END | Går till första ordet i tabellen per sida |

## Gränssnittet för schemaredigeraren

Gränssnittet för schemaredigeraren är tillgängligt med följande funktioner:

* Schemaredigeraren stöder tangentbordsnavigering, inklusive användning av **Tabb** för navigering via gränssnittselement.
* **Fliken** anger sökfältet och sedan schematrädet.
* Schematrädet stöder användning av piltangenter för att navigera i schematrädets gränssnitt
   * **Upp- och nedpilarna** kan användas för att gå igenom trädet.
   * **Vänster- och högerpilarna** kan användas för att expandera och komprimera noder eller flytta mellan infogade åtgärder i schematrädet.
* **Enter (Retur)** aktiverar enskilda noddetaljer i detaljpanelen till höger.
* Tangenten **Hem** går tillbaka till trädets övre del.
* Tangenten **End** går till trädans nedre del.
* Schematrädet innehåller även ARIA-etiketter för skärmläsare.

## Segmentbyggargränssnitt

När du använder användargränssnittet i Segment Builder för att skapa, redigera och interagera med segment i Experience Platform förbättras tillgängligheten av följande funktioner:

* Gränssnittet för segmentbyggaren är tillgängligt via tangentbordsnavigering.
* Skärmläsare bör känna igen märkord för rubriker och kan meddela rubriken tillsammans med nivån.
* Andra hjälpmedelstekniker kan ändra den visuella visningen av en sida genom att använda korrekt kodade rubriker för att visa en disposition eller alternativ vy.

Du kan nu komprimera eller utöka vänster och höger radie för segmentbyggarbetsytan för att få mer utrymme på skärmen. Den här funktionen är särskilt användbar eftersom den har full funktionalitet vid 200 % zoomning.

![Segmentbyggararbetsytan med vänster och höger markeringswidget.](images/left-right-rail-expandables.png)

## Frågetjänstredigeraren

Följande tillgänglighetsfunktioner är tillgängliga i frågetjänstens redigerare:

* Färgkontrast i redigeringsgränssnittet för frågetjänsten uppfyller kraven för tillgänglighet.
* Tangentbordsnavigering stöds utanför redigeringsgränssnittet. Redigerarens användargränssnitt är en inbäddad kodspegling.

>[!NOTE]
>
>Frågeredigeraren hanterar inte tangenten **Tab** som standard. Om du vill aktivera **tabb**-funktionen när du är i redigeraren måste du trycka på **Esc** och sedan trycka på **Tabb** direkt efter den. Tryck på **Tabb** igen om du vill flytta fokus utanför redigeraren.

## Fliken Systemvy i Källor och mål

När du bläddrar i **[!UICONTROL System View]** i Källor och Destinationer förbättras tillgängligheten med följande funktioner:

* **Fliken** sätter fokus på det första källanslutningskortet
   * **Fliken** igen om du vill fokusera på knappen i kortet
   * Välj **Retur** om du vill aktivera knappen för att ringa till åtgärd i kortet
* Om du väljer **Retur** på anslutningskortet aktiveras även mer information i den högra listen
   * När den högra listen är aktiverad ställs fokus in på det området. **Tabb** fokuserar på **Close** för den högra rutan. Om du väljer **Tabb** igen flyttas fokus genom panelen för den högra listen
   * Om det finns mer än ett källanslutningskort förflyttar sig **Tabb** mellan anslutningarna
   * Använd **piltangenterna (upp, ned, vänster och höger)** för att gå igenom källlistan
   * Välj **Tabb** för att ange fokus på panelen för den högra listen
