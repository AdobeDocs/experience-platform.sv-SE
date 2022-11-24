---
title: Adobe Analytics Extension - översikt
description: Läs om Adobe Analytics-taggtillägget i Adobe Experience Platform.
exl-id: 33ebdcb6-9bf0-44e6-b016-e93fe78af578
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2253'
ht-degree: 2%

---

# Översikt över Adobe Analytics-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Använd den här referensen för information om hur du konfigurerar Adobe Analytics-tillägget och de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Konfigurera Adobe Analytics-tillägget

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar Adobe Analytics-tillägget.

Om Adobe Analytics-tillägget inte är installerat ännu öppnar du din egenskap och väljer **[!UICONTROL Extensions > Catalog]** hovra över Adobe Analytics-tillägget och välj **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken Tillägg, håller pekaren över tillägget och väljer sedan **[!UICONTROL Configure]**.

![](../../../images/ext-analytics-config.png)

## Bibliotekshantering

Välj ett alternativ i avsnittet Bibliotekshantering på konfigurationssidan. Följande konfigurationsalternativ är tillgängliga:

### Hantera biblioteket åt mig

#### Rapportsviter

Ange en eller flera rapportsviter för var och en av följande miljöer:

* Utveckling
* Mellanlagring
* Produktion

### Använda biblioteket som redan är installerat på sidan

#### Ange följande rapportsviter för spåraren

Om du väljer det här alternativet anger du en eller flera rapportsviter för var och en av följande miljöer:

* Utveckling
* Mellanlagring
* Produktion

#### Använda modulen för aktivitetskarta

Aktivitetskartan läses in som en separat modul (som AAM). Som standard är aktivitetskartan aktiverad, men om du vill stänga av den kan du göra det genom att avmarkera rutan i konfigurationen.

#### Spåraren är tillgänglig på den globala variabeln med namnet

Om du markerar den här rutan kan spårningsobjektet användas globalt. Du kan till exempel definiera variabeln `window.s.pageName` var som helst på din webbplats.

### Läsa in biblioteket från en anpassad URL

#### HTTP-URL

Ange den URL där biblioteket finns.

#### HTTPS-URL

Ange den URL där biblioteket finns.

#### Ange följande rapportsviter för spåraren

Om du väljer det här alternativet anger du en eller flera rapportsviter för var och en av följande miljöer:

* Utveckling
* Mellanlagring
* Produktion

#### Spåraren är tillgänglig på den globala variabeln med namnet

Ange spårningsobjektet som ska användas globalt.

### Ange egen bibliotekskod

#### Öppna redigeraren

Gör att du kan infoga kärnan [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) kod. Den här koden fylls i automatiskt när den automatiska konfigurationsmetoden används.

>[!NOTE]
>
>Valideraren som används i kodredigeraren är utformad för att identifiera problem med kod som skrivits av utvecklare. Kod som har genomgått en miniatyrprocess, t.ex. den AppMeasurement.js-kod som hämtats från kodhanteraren, kan felaktigt flaggas som att den har problem av taggvalideraren, som vanligtvis kan ignoreras.

#### Ange följande rapportsviter för spåraren

Om du väljer det här alternativet anger du en eller flera rapportsviter för var och en av följande miljöer:

* Utveckling
* Mellanlagring
* Produktion

#### Spåraren är tillgänglig på den globala variabeln med namnet

Ange spårningsobjektet som ska användas globalt.

## Allmänt

Välj ett alternativ i avsnittet Allmänt på konfigurationssidan. Följande konfigurationsalternativ är tillgängliga:

### Aktivera EU-kompatibilitet för Adobe Analytics

Aktiverar eller inaktiverar spårning baserat på EU:s sekretess-cookie.

När du markerar kryssrutan EU-efterlevnad visas [!UICONTROL Tracking Cookie Name] visas. Spårningskakikonen åsidosätter standardnamnet på spårningskakien. Du kan anpassa det namn som taggar använder för att spåra din avanmälningsstatus för att ta emot andra cookies.

När en sida har lästs in kontrollerar systemet om en cookie med namnet sat\_track har ställts in (eller det egna cookie-namnet som har angetts på sidan Redigera egenskap). Tänk på följande information:

* Om cookien inte finns eller om cookien finns och är inställd på något annat än true, hoppas verktygsinläsningen över när den här inställningen är aktiverad. Detta innebär att alla delar av en regel som använder verktyget inte kommer att gälla. Om en regel har analyser på EU-efterlevnad av kod och tredjepartskod och cookien är inställd på false, körs fortfarande tredjepartskoden. Analysvariablerna kommer dock inte att anges.
* Om cookien finns men är inställd på true läses verktyget in normalt.

Du ansvarar för att ställa in sat\_track-cookie (eller anpassad namngiven cookie) på false om en besökare väljer bort. Du kan göra detta med anpassad kod:

```javascript
_satellite.cookie.set("sat_track", "false");
```

Du måste också ha en funktion för att ange den cookien till true om du vill att en besökare ska kunna anmäla sig senare:

```javascript
_satellite.cookie.set("sat_track", "true");
```

### Teckenuppsättning

Anger hur bildbegäran kodas. Om implementeringen eller webbplatsen använder tecken som inte är ASCII-tecken är det viktigt att definiera teckenuppsättningen här. Du kan välja en förinställd teckenuppsättning eller ange en anpassad teckenuppsättning. Adobe rekommenderar att du använder samma teckenkodning som din webbplats. Vanligtvis är det här värdet UTF-8.

Teckenuppsättning kan anges i anpassad kod för Analytics med variabeln `s.charSet`.
Mer information om teckenuppsättningar finns i [charSet-dokumentation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html).

### Valutakod

Bestämmer konverteringsgraden som ska användas för intäkt- och valutakurshändelser. Om sajten tillåter besökare att handla i flera valutor, säkerställer inställningen av valutakoden att det monetära beloppet konverteras och lagras korrekt.

Mer information om vilka valutakoder som stöds finns i [currencyCode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html).

### Spårningsserver

Används för cookie-implementeringar från första part för att bestämma var cookie-filen ska lagras. Om du använder Experience Cloud ID-tjänsten rekommenderar Adobe att du inte fyller i det här fältet.

Spårningsservern kan anges i anpassad Analytics-kod med hjälp av variabeln `s.trackingServer`.

Se [trackingServer](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html) i Adobe Analytics Implementeringshandbok.

### SSL-spårningsserver

Används för SSL-cookie-implementeringar från första part för att bestämma var cookie-filen ska lagras. Om du använder Experience Cloud ID-tjänsten rekommenderar Adobe att du inte fyller i det här fältet. Om det inte definieras använder SSL-data en spårningsserver.

SSL Tracking Server kan anges i anpassad Analytics-kod med variabeln `s.trackingServerSecure`.

Se [trackingServerSecure](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html).

## Globala variabler

Använd det här avsnittet för att konfigurera [eVars and Props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html)och för att skapa hierarkier.

Globala variabler är variabler som ställs in på Analytics-spårningsobjektet när det objektet initieras på sidan. Alla variabler som du anger här ställs in när spårningsobjektet skapas på varje sida. När variablerna har angetts fungerar de precis som andra variabler har angetts på något annat sätt. Detta innebär i synnerhet att en regel kan ändra, ändra eller rensa dessa variabler.

Om webbprogrammet vanligtvis skickar en beacon per sida kan det här avsnittet göra det enklare att ställa in variablerna på ett ställe. Om programmet skickar mer än en fyr per sida (till exempel i ett enkelsidigt program) och du behöver rensa variablerna och återställa dem med samma spårningsobjekt, är det enklare att förlita sig på regler för att ställa in och rensa variablerna.

## Länkspårning

Välj ett alternativ under Länkspårning på konfigurationssidan. Följande konfigurationsalternativ är tillgängliga:

### Aktivera ClickMap

[ClickMap](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) är ett plugin-program för Internet Explorer och Firefox samt en modul för rapporter och analyser.

### Spåra nedladdningslänkar

Spårar länkar till hämtningsbara filer på din plats.

Se [s.trackDownLoadLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html).

### Hämta tillägg

Om alternativet Spåra nedladdningslänkar är aktiverat kan du välja filtillägg för fillänkar som ingår i rapporten Nedladdningar Om din webbplats innehåller länkar till filer med något av de angivna tilläggen, visas URL:erna för dessa länkar i rapporten.

Se [s.linkDownloadFileTypes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html).

### Spåra utgående länkar

Avgör om en markerad länk är en slutlänk.

Se [s.trackExternalLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html).

**Överväganden om ensidiga appar:** På grund av hur vissa SPA webbplatser kodas kan en intern länk till en sida på den SPA webbplatsen se ut som om den är en utgående länk.

Du kan använda någon av följande metoder för att spåra utgående länkar från SPA platser:

* Om du inte vill spåra några utgående länkar från SPA infogar du en post i avsnittet Spåra aldrig.  Exempel, `http://testsite.com/spa/\#`. Alla \#-länkar till den här värden ignoreras. Alla utgående länkar till andra värdar spåras, till exempel [https://www.google.com](https://www.google.com).
* Om det finns länkar som du vill spåra på SPA använder du avsnittet Spåra alltid.

Om du t.ex. har en spa/\#/about-sida kan du skriva &quot;about&quot; i avsnittet Always Track.

Om-sidan är den enda utgående länken som spåras. Andra länkar på sidan (till exempel [https://www.google.com](https://www.google.com)) spåras inte.

>[!NOTE]
>
>Dessa två alternativ utesluter varandra.

### Behåll URL-parametrar

Bevarar frågesträngar.

Se [s.linkLeaveQueryString](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html).

## Cookies

Konfigurera fältbeskrivningar för de globala Cookies-inställningar som används för distribution av Adobe Analytics-tillägget. Följande konfigurationsalternativ är tillgängliga:

### Besökar-ID

Unikt värde som representerar en kund både online och offline.

Se [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html).

### Namnutrymme för besökare

Variabel som identifierar den domän som cookies är inställda på.

Se [visitorNamespace](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html).

### Domänperioder

Domänen som Analytics-cookien `s_cc` och `s_sq` anges genom att bestämma antalet punkter i domänen för sidans URL. Den här variabeln används även av vissa plugin-program för att fastställa rätt domän för att ange plugin-programmets cookie.

Se [s.cookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html).

### Domänperioder för första part

The `fpCookieDomainPeriods` är för cookies som anges av JavaScript (`s_sq`, `s_cc`, plugin-program) som i sig är cookies från första part, även om din implementering använder domänerna 2o7.net eller omtrdc.net från tredje part.

Se [s.fpCookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html).

### Cookie-livstid

Bestämmer en cookies livslängd.

Se [s.cookieLifetime](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html).

### Säkra cookies

Den här variabeln tillåter AppMeasurement att skriva säkra cookies.

Se [writeSecureCookies](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html)


## Anpassa sidkod

Anpassa sidkoden med redigeraren.

## Adobe Audience Manager

Använd det här avsnittet i tilläggskonfigurationen för att ange hur Audience Manager fungerar med Analytics.

Aktivera **Dela Analytics-data automatiskt med Audience Manager**.

Följande alternativ visas:

![](../../../images/an-ext-aam.png)

Underdomänen Audience Manager tilldelas av Adobe Audience Manager. Det kallas ibland för&quot;partnernamn&quot; eller&quot;partnerunderdomän&quot;. Kontakta din Adobe-konsult eller kundtjänst om du inte känner till ditt partnernamn.

Du kan konfigurera avancerade inställningar genom att välja **Visa avancerade inställningar** och ange dina inställningar.

![](../../../images/an-ext-aam-adv.png)

Om du vill ha information om varje inställning väljer du informationsikonen eller läser [Adobe Audience Manager-dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html).

## Åtgärdstyper för analystillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Analytics-tillägget.

Analystillägget innehåller följande åtgärder:

* [Ange variabler](#set-variables)
* [Skicka Beacon](#send-beacon)
* [Rensa variabler](#clear-variables)

### Ange variabler {#set-variables}

Viktigt: Beacon skickas inte när du använder åtgärden &quot;ange variabler&quot;. Du måste använda åtgärden&quot;skicka fyr&quot;.

#### eVars

Ange en eller flera [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html).

1. Välj en eVar i listrutan.
1. Ange om du vill ange eVar som ett värde (Ange som) eller kopiera (Duplicera från) en annan eVar.
1. Ange ett Ange som-värde eller markera den eVar som du vill duplicera.
1. (Valfritt) Välj Lägg till eVar för att ange fler eVars.
1. Välj **[!UICONTROL Keep Changes]**.

#### Props

Ange en eller flera [proppar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html).

1. Välj en profil i listrutan.
1. Ange om du vill ange att svällningen ska vara ett annat eVar (Ange som) eller kopiera (Duplicera från).
1. Ange ett Ange som-värde eller markera den eVar du vill duplicera utkastet från.
1. (Valfritt) Välj **[!UICONTROL Add prop]** för att få fler avtryck.
1. Välj **[!UICONTROL Keep Changes]**.

#### Händelser

Ange en eller flera [händelser](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html).

1. Välj en händelse i listrutan.
1. (Valfritt) Välj eller ange ett dataelement som används för [händelseserialisering](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html).
1. (Valfritt) Välj **[!UICONTROL Add event]** för att ställa in fler händelser.
1. Välj **[!UICONTROL Keep Changes]**.

#### Hierarki

Ange Analytics [Hierarki](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html) variabel.

Ange varje nivå i hierarkin.

Om du vill kan du konfigurera ytterligare hierarkier.

#### Sidnamn

Detta värde refererar till namnet på en viss sida och motsvarar [`pageName` variabel](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/pagename.html) i Analytics.

>[!IMPORTANT]
>
>I Adobe Experience Manager-implementeringar anger den här variabeln var den hämtade Analytics-rapporten ska lagras AEM. För att rapporterna ska bli korrekt beständiga måste sidnamnssträngen formateras som en kolonavgränsad sökväg till webbplatsen.
>
>En webbsida på `content/we-retail/language-masters/en/men.html` ska ha sidnamnsvärdet `content:we-retail:language-masters:en:men`.

#### Annan information

Ange annan information som används av sidorna.

Dessa inställningar inkluderar:

* Sidans URL
* Server
* Kanal
* Referent
* Campaign
* Inköps-ID

   Ange ett värde eller en frågeparameter

* Läge
* Postnummer
* Transaktions-ID

De här inställningarna finns på menyn Globala variabler genom att markera kryssrutan Ytterligare inställningar.

#### Egen sidkod

**Beskrivning**

Använd redigeraren för att ange din egen sidkod.

**Inställningar**

1. Välj **[!UICONTROL Open Editor]**.
1. Skriv den anpassade koden.
1. Välj **[!UICONTROL Save]**.

### Skicka Beacon {#send-beacon}

#### Öka en sidvy - s.t()

Välj det här alternativet om du vill stega upp en sidvy.

#### Öka inte en sidvy - s.tl()

Välj det här alternativet om du inte vill stega upp en sidvy.

**Inställningar**

1. Välj en länktyp.

   Du kan välja något av följande:

   * Anpassad länk
   * Hämta länk
   * Avsluta länk

1. Ange parametern för den markerade länken.
   * Egen länk: Ange länknamnet.
   * Ladda ned länk: Ange ett filnamn.
   * Avsluta länk: Ange mål-URL.
1. Välj **[!UICONTROL Keep Changes]**.

### Rensa variabler {#clear-variables}

Det finns inga konfigurationsalternativ om åtgärden Rensa variabler är markerad.
