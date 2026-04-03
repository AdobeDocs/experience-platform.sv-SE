---
title: Dela identitet från mobilappar till mobil webb/WebViews
description: Överför identitet från en mobilapp till mobilwebbinnehåll eller en WebView så att rapportering och personalisering kan fortsätta i webbsammanhang.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Dela identitet från mobilappar till mobil webb/WebViews

När en besökare flyttar från en mobilapp till en WebView- eller mobilwebbsida behåller appar och webbkontexter sin egen identitet. Utan en explicit överlämning behandlar webbupplevelsen besökaren som en ny, okänd person, som fragmenterar rapportering och startar om personaliseringen.

Identitetsdelning från mobilen till webben löser detta genom att skicka besökarens [Experience Cloud ID (ECID)](./overview.md) från mobilappen till webbdestinationen via en `adobe_mc` frågesträngsparameter. Parametern innehåller ECID, ditt företags-ID och en tidsstämpel. När webbdestinationen läses in med en giltig `adobe_mc`-parameter, läser Web SDK automatiskt upp den och använder den överförda identiteten på sin första Edge Network-begäran, så båda kontexterna delar samma besökare.

Använd det här mönstret när mobilappen öppnar en WebView- eller mobilwebbsida som din organisation kontrollerar och du vill att appaktiviteten och webbaktiviteten ska vara knutna till samma besökare. Om ditt mål är identitetskontinuitet mellan webbplatser på olika domäner ska du använda [korsdomänsdelning](cross-domain-sharing.md) i stället.

## Förutsättningar

Innan du börjar kontrollerar du att implementeringen uppfyller följande krav:

* **Mobilapp**: Adobe Experience Platform Mobile SDK med [Identity for Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) extension version **1.1.0 eller senare** (iOS och Android).
* **Webbmål**: [Web SDK](/help/collection/js/js-overview.md) version **2.11.0 eller senare** eller Web SDK-taggtillägget.
* **URL-kontroll**: Din kod kontrollerar den URL som appen skickar till WebView eller webbläsaren så att du kan lägga till frågesträngsparametrar till den.
* **Matchande konfiguration**: Samma Experience Cloud-organisations-ID har konfigurerats i både mobil- och webbimplementeringar.

## Hämta identitet från mobilappen {#retrieve-identity}

Använd API:t [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) från tillägget Identitet för Edge Network för att hämta besökarens identitet som en frågesträng. Du kan sedan lägga till strängen i URL:en innan du öppnar WebView eller webbläsaren.

Den returnerade strängen innehåller följande URL-kodade parametrar:

| Parameter | Beskrivning |
| --- | --- |
| `MCID` | Experience Cloud-id (ECID). |
| `MCORGID` | Ditt Experience Cloud-organisations-ID. Den här parametern måste matcha den organisation som är konfigurerad i Web SDK på målsidan. |
| `TS` | En tidsstämpel. Målet måste ta emot det här värdet inom **fem minuter**, annars avvisas överföringen. |

I följande kodexempel visas hur en beställning kan se ut i din mobilapp:

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Ta emot identitet på webbsidan {#receive-identity}

Ingen ytterligare kod krävs på webbmålet. När Web SDK finns på sidan och URL:en innehåller en giltig `adobe_mc`-parameter extraherar SDK automatiskt ECID:t och tillämpar det på besökarens identitetskarta på den första Edge Network-begäran.

Om webbdestinationen använder taggtillägget Web SDK och du behöver dirigera om besökaren till en annan sida samtidigt som du bevarar identiteten, använder du åtgärden [Omdirigera med identitet](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) för att vidarebefordra parametern `adobe_mc` till nästa sida.

>[!NOTE]
>
>Parametern `adobe_mc` upphör att gälla efter **fem minuter**. Se till att webbmålet läses in och skickar sin första Edge Network-begäran omedelbart efter att URL-adressen har öppnats.
