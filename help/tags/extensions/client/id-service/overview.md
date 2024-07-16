---
title: Adobe Experience Cloud Identity Service Extension - översikt
description: Läs mer om taggtillägget Adobe Experience Cloud Identity Service i Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Översikt över tillägget Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Använd den här referensen för information om hur du konfigurerar Adobe Experience Cloud ID-tillägget och de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

Använd det här tillägget om du vill integrera Experience Cloud Identity Service med din egendom. Med Experience Cloud Identity Service kan ni skapa och lagra unika och beständiga identifierare för era webbplatsbesökare.

## Konfigurera Experience Cloud ID-tillägget

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar tillägget Experience Cloud-ID.

Om Experience Cloud ID-tillägget inte har installerats än öppnar du egenskapen, väljer **[!UICONTROL Extensions > Catalog]**, hovrar över Experience Cloud ID-tillägget och väljer **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken Tillägg, håller pekaren över tillägget och väljer **[!UICONTROL Configure]**.

![](../../../images/optin.jpg)

Följande konfigurationsalternativ är tillgängliga:

### Experience Cloud organisation-ID

ID för din Experience Cloud-organisation.

Ditt ID är en alfanumerisk sträng med 24 tecken följt av `@AdobeOrg`. Kontakta kundtjänst om du inte känner till detta ID.

### Uteslut specifika sökvägar

Experience Cloud-ID:t läses inte in om URL:en matchar någon av de angivna sökvägarna.

(Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

Välj **[!UICONTROL Add]** om du vill exkludera en annan sökväg.

### Anmäl dig

Använd alternativen för att välja om du vill att besökarna ska välja Adobe-tjänster på din webbplats, inklusive om de ska skapa cookies som spårar besökarens aktivitet.

Opt In är den centraliserade referenspunkten för alla plattformslösningens klientbibliotek för att avgöra om cookies kan skapas på en användares enhet eller webbläsare när du besöker din webbplats. Anmäl dig till har inte stöd för att samla in eller lagra inställningar för användargodkännande.

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

Ange namn/värde-par som Experience Cloud ID-instansegenskaper. Använd listrutan för att markera en variabel och skriv eller välj sedan ett värde. Mer information om de olika variabelerna finns i [Experience Cloud-identitetstjänstens dokumentation](https://experiencecloud.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html).

## Åtgärdstyper för tillägg till Experience Cloud ID

I det här avsnittet beskrivs de åtgärdstyper som finns i tillägget Experience Cloud ID.

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
