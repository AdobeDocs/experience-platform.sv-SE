---
title: Delning av mobil-till-webb och domänövergripande ID
description: Lär dig hur du behåller besökar-ID:n från mobil- till webbegenskaper och mellan domäner
keywords: Identitet;mobil;id;sharing;domain;cross-domain;sdk;platform;
source-git-commit: 55e28f749741c653a230b42fabf5a047ba8c7d01
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Delning av mobil-till-webb och domänövergripande ID

## Översikt

Adobe Experience Platform Web SDK har stöd för delning av besökar-ID, vilket gör det möjligt för kunderna att leverera personaliserade upplevelser på ett mer korrekt sätt, mellan mobilappar och mobilwebbinnehåll samt mellan domäner.

## Användningsfall {#use-cases}

### Leverera enhetlig personalisering mellan mobilappar och mobilwebbplatser

Ett klädföretag vill personalisera sina kunders upplevelse utifrån deras intressen och hålla personaliseringen korrekt i en mobilapplikation som även läser in WebViews. Genom att använda funktionen för delning av mobil-till-webb-ID kan de se till att de mest korrekta erbjudandena presenteras för kunderna, med samma besökaridentifierare i appen och mobilens webbinnehåll, genom att skicka [!DNL ECID] till mobil webb-URL.

### Leverera enhetlig personalisering över domäner

En återförsäljare med flera onlinebutiker vill personalisera shoppingupplevelsen över sina domäner utifrån kundernas intressen. Med hjälp av funktionen för delning av domänövergripande ID i Web SDK kan återförsäljaren leverera korrekta erbjudanden baserat på kundernas intressen i alla sina domäner.

### Förbättra rapporter om besöksaktivitet

En teknikhandlare vill förbättra sin rapportering om besökaraktivitet med information om när besökarna flyttar från mobilappen till mobilwebbplatsen eller till andra domäner. Med hjälp av funktionen för delning av domänövergripande ID i Web SDK kan marknadsföringsteamet spåra besökare på deras webbsajter och generera aktivitetsrapporter.

## Förutsättningar {#prerequisites}

Om du vill använda delning av mobil-till-webb och domänövergripande ID måste du uppdatera till [!DNL Web SDK] version 2.11.0 eller senare.

För mobilimplementeringar med Edge Network stöds den här funktionen i [Identitet för Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) från och med version 1.1.0 (iOS och Android).

## Delning av mobil-till-webb-ID {#mobile-to-web}

Använd `getUrlVariables` API från [Identitet för Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) för att hämta identifierare som frågeparametrar och bifoga dem till din URL när du öppnar [!DNL webViews].

Ingen ytterligare konfiguration krävs för att Web SDK ska acceptera `ECID` värden i frågesträngen.

Frågesträngsparametern innehåller:

* `MCID`: Experience Cloud-ID (`ECID`)
* `MCORGID`: Experience Cloud `orgID` som måste matcha `orgID` som konfigurerats i [!DNL Web SDK].
* `TS`: En tidsstämpelparameter som inte kan vara äldre än fem minuter.


Delning av mobil-till-webb-ID använder `adobe_mc` parameter. När `adobe_mc` parametern finns och är giltig, `ECID` från frågesträngen läggs automatiskt till i identitetskartan i den första begäran som görs i Edge Network. Alla efterföljande Edge Network-interaktioner kommer att använda `ECID`.

Mer information om hur du skickar besökar-ID:n från en mobilapp till en WebView finns i dokumentationen om [hantera WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Delning av domänövergripande ID {#cross-domain-sharing}

För delning av domänöverskridande ID har Web SDK version 2.11.0 stöd för `appendIdentityToUrl` -kommando. När kommandot används genereras `adobe_mc` frågesträngsparameter.

Kommandot accepterar ett objekt med en egenskap, `url`och returnerar ett objekt med egenskapen `url`.

Det här kommandot väntar inte på någon uppdatering av medgivandet. Om samtycke inte har angetts returneras URL:en oförändrad.

Om en `ECID` inte tillhandahålls, `/acquire` slutpunkten anropas för att generera en `ECID`.

Nedan visas ett exempel på hur en kund kan implementera delning av domänöverskridande ID på sin webbplats.

Den här koden lägger till en händelseavlyssnare för alla klickningar på sidan och om klickningen var på en länk till en matchande domän (i det här fallet `adobe.com` eller `behance.com`) lägger till identiteten i URL:en och dirigerar om användaren där.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Använda tillägget Taggar {#tags-extension}

Liknar när du använder [!DNL Web SDK], krävs ingen ytterligare konfiguration i [!DNL Tags] för att använda identiteter som skickas via URL:en.

Om du vill använda delning av mobil-till-webb och domänövergripande ID via taggtillägget måste du använda version 2.12.0 eller senare av taggtillägget.

Om du vill dela identiteter från den aktuella sidan till andra domäner finns det en ny åtgärd i [!DNL Web SDK] [!DNL Tags] tillägg. Den här åtgärden är avsedd att användas med en **[!UICONTROL Core - Click]** händelsetyp och villkor för värdejämförelse.

Följ anvisningarna [här](../../tags/ui/managing-resources/rules.md) för att skapa en regel med följande konfiguration:

* [!UICONTROL Event Configuration]:
   * **[!UICONTROL Extension: Core]**
   * **[!UICONTROL Event Type: Click]**
   * Välj **[!UICONTROL When the user clicks on > specific elements]**
   * Skriv i **[!UICONTROL Selector]**: `a[href]`. Den här händelsen aktiveras när någon klickar på en ankartagg på sidan med en `href` -egenskap.

      ![Användargränssnittsbild som visar händelsekonfigurationen med de inställningar som beskrivs ovan](assets/id-sharing-event-configuration.png)

* [!UICONTROL Condition Configuration]
   * **[!UICONTROL Logic Type]**: [!UICONTROL Regular]
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Condition Type]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Left Operand]**: [!UICONTROL `%this.hostname%`]. Detta är ett särskilt dataelement som fungerar med [!UICONTROL Core - Click] -händelser och löses till värdnamnet för länken som du klickade på.
   * **[!UICONTROL Operator]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Right Operand]**: Skriv ett reguljärt uttryck som matchar domänerna som du vill dela identiteter med. Om du till exempel vill matcha länkar med värdnamn som slutar med `adobe.com` eller `behance.com`använder du det här reguljära uttrycket: `behance.com$|adobe.com$`. Den länkade sidan måste ha [!DNL Web SDK] eller [!DNL Visitor ID] som installerats för att acceptera identiteten.

      ![Användargränssnittsbild som visar villkorskonfigurationen med de inställningar som beskrivs ovan](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Action Configuration]
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action Type]**: [!UICONTROL Redirect with identity]
   * **[!UICONTROL Instance]**: Markera instansen. I de flesta fall har du bara en instans konfigurerad. Om du har flera instanser väljer du den med den identitet som du vill dela.

      ![Användargränssnittsbild som visar åtgärdskonfigurationen med de inställningar som beskrivs ovan](assets/id-sharing-action-configuration.png)

The **[!UICONTROL Redirect with identity]** kommer att hindra webbläsaren från att navigera till länken. Sedan ska det ringa `appendIdentityToUrl` på [!DNL Web SDK] -instans.

Slutligen dirigeras användaren om till [!DNL URL] med `adobe_mc` frågesträngsparameter har lagts till.
