---
title: Dela identitet över domäner
description: Bibehåll identitetskontinuiteten över domäner som organisationen äger för att förbättra personalisering och rapportering.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Dela identitet över domäner

När besökare förflyttar sig mellan domäner som din organisation äger behåller varje domän sin egen besöksidentitet som standard. Utan en explicit överlämning behandlas en besökare som klickar från en av dina domäner till en annan som en ny, okänd person på målplatsen. Den här typen av implementeringsfragment rapporterar och startar om personalisering.

Delning av identitet mellan domäner löser det här problemet genom att lägga till en `adobe_mc`-frågesträngsparameter till mål-URL:en när en besökare klickar på en länk eller omdirigeras. Den här parametern innehåller besökarens [Experience Cloud ID (ECID)](./overview.md), ditt organisations-ID och en tidsstämpel. När målsidan läses in med en giltig `adobe_mc`-parameter, läser Web SDK automatiskt upp den och använder överlämningsidentiteten på sin första Edge Network-begäran, så att båda domänerna delar samma besökare. Parametern `adobe_mc` går ut om fem minuter, så målsidan måste läsas in omedelbart efter omdirigeringen.

Det här användningsexemplet omfattar identitetsdelning mellan webbplatser på olika domäner. Om du vill skicka identitet från en mobilapp till en WebView- eller mobilwebbsida använder du [delning av mobil-till-webbidentitet](./mobile-to-web.md) i stället.

## Förutsättningar

Innan du börjar kontrollerar du att implementeringen uppfyller följande krav:

* **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) version **2.11.0 eller senare**, eller Web SDK-taggtillägget, är installerat på både käll- och måldomänerna.
* **Matchande konfiguration**: Alla deltagande domäner använder samma [`orgId`](../js/commands/configure/orgid.md) när Web SDK konfigureras.
* **URL-kontroll**: Din kod kontrollerar länkarna eller omdirigeringarna mellan domäner så att du kan lägga till frågesträngsparametrar till mål-URL:en.

## Implementera domänövergripande delning

Du måste konfigurera identitetsdelning för alla domäner som fungerar som en källa i en domänövergripande överföring. Om besökare kan navigera i båda riktningarna mellan två domäner konfigurerar du båda domänerna som källor.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

Använd kommandot [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) för att lägga till parametern `adobe_mc` till utgående länkar. Följande exempel lyssnar efter klick på ankarelement och lägger till identitet till alla länkar som pekar till en önskad domän:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Webbtaggtillägg för SDK]

Använd åtgärden [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) för att lägga till parametern `adobe_mc` till utgående länkar. Du kan skapa en regel med följande villkor för att få önskat beteende:

1. **Händelse**: Ange tillägget till **[!UICONTROL Core]** och händelsetypen till **[!UICONTROL Click]**. Under **[!UICONTROL Elements matching the CSS selector]** anger du `a[href]`.
2. **Villkor**: Ange tillägget till **[!UICONTROL Core]** och villkorstypen till **[!UICONTROL Value Comparison]**. Ange **[!UICONTROL Left Operand]** till `%this.hostname%`, **[!UICONTROL Operator]** till **[!UICONTROL Matches Regex]** och **[!UICONTROL Right Operand]** till ett reguljärt uttryck som matchar måldomänerna (till exempel `example\.com$|example\.org$`).
3. **Åtgärd**: Ange tillägget till **[!UICONTROL Adobe Experience Platform Web SDK]** och åtgärdstypen till **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Ta emot identitet på måldomänen

Ingen ytterligare kod krävs för måldomänen. När Web SDK finns på sidan och URL:en innehåller en giltig `adobe_mc`-parameter extraherar SDK automatiskt ECID:t och tillämpar det på besökarens identitetskarta på sin första Edge Network-begäran.

Kontrollera att måldomänen uppfyller följande villkor:

* Taggtillägget Web SDK eller Web SDK installeras och konfigureras med samma [`orgId`](../js/commands/configure/orgid.md) som källdomänen. Du kan använda taggtilläggen JavaScript-bibliotek och Web SDK utbytbart mellan domäner, förutsatt att de delar samma `orgId`.
* Sidan läses in och skickar sin första Edge Network-begäran inom **fem minuter** efter omdirigeringen, innan parametern `adobe_mc` förfaller.
