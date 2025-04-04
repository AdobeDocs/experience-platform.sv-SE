---
title: Adobe Experience Cloud Identity Service Extension - översikt
description: Läs mer om taggtillägget Adobe Experience Cloud Identity Service i Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 5%

---

# Översikt över tillägget Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Använd den här referensen för information om hur du konfigurerar Adobe Experience Cloud ID-tillägget och de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

Använd det här tillägget för att integrera Experience Cloud identitetstjänst med din egendom. Med Experience Cloud identitetstjänst kan du skapa och lagra unika och beständiga identifierare för webbplatsens besökare.

## Konfigurera Experience Cloud ID-tillägget

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar Experience Cloud ID-tillägget.

Om Experience Cloud ID-tillägget ännu inte är installerat öppnar du din egenskap, väljer **[!UICONTROL Extensions > Catalog]**, hovrar över Experience Cloud ID-tillägget och väljer **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken Tillägg, håller pekaren över tillägget och väljer **[!UICONTROL Configure]**.

![](../../../images/optin.jpg)

Följande konfigurationsalternativ är tillgängliga:

### Experience Cloud Organization ID

ID för din Experience Cloud-organisation.

Ditt ID är en alfanumerisk sträng med 24 tecken följt av `@AdobeOrg`. Kontakta kundtjänst om du inte känner till detta ID.

### Uteslut specifika sökvägar

Experience Cloud-id:t läses inte in om URL:en matchar någon av de angivna sökvägarna.

(Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

Välj **[!UICONTROL Add]** om du vill exkludera en annan sökväg.

### Anmäl dig

Använd alternativen för att välja om du vill att besökarna ska välja Adobe-tjänster på din webbplats, inklusive om de ska skapa cookies som spårar besökarens aktivitet.

Opt In är den centraliserade referenspunkten för alla Experience Platform-baserade klientbibliotek för att avgöra om cookies kan skapas på en användares enhet eller webbläsare när du besöker din webbplats. Anmäl dig till har inte stöd för att samla in eller lagra inställningar för användargodkännande.

**Aktivera anmälan?**

Det valda alternativet avgör om din webbplats väntar på samtycke för att spåra en besökares aktiviteter på din webbplats.

Det finns tre alternativ:

* **Nej:** väntar inte på godkännande för att spåra besökaren. Det här är standardbeteendet om du inte väljer något alternativ.
* **Ja:** Väntar på samtycke för att spåra besökaren.
* **Fastställd vid körning med funktionen:** Fastställer programmatiskt om värdet är true eller false vid körning. Om du väljer det här alternativet blir fältet Välj dataelement tillgängligt. Välj ett dataelement som kan avgöra om du ska vänta på samtycke. Detta dataelement tolkas som ett booleskt värde. Du kan till exempel välja ett dataelement som ger samtycke beroende på om besökarens land är beläget i EU.

**Är avanmälan i lagring aktiverat?**

Om det här alternativet är aktiverat lagras samtycke i en cookie för första part på din domän. Om detta inte är aktiverat sparas medgivandeinställningarna i din CMP eller i en cookie som du hanterar.

**Vill du vara med i cookie-domänen?**

Använd den här valfria inställningen för att ange den domän där cookie för anmälan lagras om lagring är aktiverat. Du kan ange en domän eller välja ett dataelement som innehåller domänen.

**Anmäl dig när lagringsutrymmet går ut?**

Ange när cookie-filen för anmälan upphör att gälla om lagring är aktiverat, i sekunder.

Ange ett tal och välj sedan en tidsenhet i listrutan. Ange till exempel 2 och välj **[!UICONTROL Weeks]**. Standard är 13 månader.

**Behörigheter?**

Skicka föregående samtycke till anmäl dig till biblioteket. Välj ett dataelement som innehåller medgivandet. Elementtypen måste vara ett objekt eller en JSON-sträng. Åsidosätter förval i godkännanden.

Exempel:

`"{"aa":true,"aam":true,"ecid":true}"`

**Anmäl dig till godkännanden?**

Definiera vilka kategorier som godkänns eller nekas när ingen inställning har angetts av besökaren. Samtycke antas för de valda lösningarna från den tidpunkt då sidan läses in. Elementtypen måste vara ett objekt eller en JSON-sträng (exempel: `{aam: true}`).

### Variabel

Ange namn/värde-par som Experience Cloud ID-instansegenskaper. Använd listrutan för att markera en variabel och skriv eller välj sedan ett värde. Mer information om de olika variablerna finns i [dokumentationen för Experience Cloud Identity Service](https://experiencecloud.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html).

## Åtgärdstyper för Experience Cloud ID-tillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Experience Cloud ID-tillägget.

### Åtgärdstyper

#### Ange kund-ID

Ange ett eller flera kund-ID.

1. Ange integreringskoden.

   Integrationskoden ska innehålla det värde som angetts som en datakälla i Audience Manager eller Kundattribut.

1. Välj ett värde.

   Värdet ska vara ett användar-ID. Dataelement lämpar sig bäst för dynamiska värden som ID:n från ett klientspecifikt internt system.

1. Välj ett autentiseringstillstånd.

   Tillgängliga alternativ är:

   * Okänd
   * Autentiserad
   * Utloggad

1. (Valfritt) Välj **[!UICONTROL Add]** om du vill ange fler kund-ID:n.
1. Välj **[!UICONTROL Keep Changes]**.
