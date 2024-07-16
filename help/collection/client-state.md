---
title: Klienttillståndshantering
description: Läs om hur Adobe Experience Platform Edge Network hanterar klienttillstånd
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: klient;tillstånd;hantering;edge;network;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Klienttillståndshantering

Själva Edge Network är statslös (den behåller inte sin egen session). Det finns dock vissa användningsfall som kräver att klientsidans tillstånd är beständigt, till exempel:

* Enhetsidentifiering (se [identifiering av besökare](visitor-identification.md))
* Samla in och framtvinga användargodkännande
* Sessions-ID för personalisering behålls

Edge Network använder ett protokoll för statushantering, som delegerar lagringsaspekten till klienten/SDK, och inkluderar tillståndsposter i sina svar. För webbläsare lagras posterna som cookies.

Klientansvaret är att lagra och inkludera dem i alla efterföljande begäranden. Klienten måste också se till att tävlingsbidragen förfaller enligt gatewayens anvisningar. När posterna har sparats som cookies utförs allt detta automatiskt i webbläsaren.

Även om lägesposterna alltid har ett oformaterat `String`-värde (som är synligt för anroparen/SDK), bör du inte använda eller manipulera värdena på något sätt. Värdets struktur/format eller till och med namnet kan ändras när som helst, vilket kan leda till oväntat beteende för klienter som använder läget internt. Tillståndet är alltid avsett att användas av själva gatewayen eller andra edge-tjänster.

## Bevarar klientstatus som metadata

Läget som returneras av [!DNL Edge Network] i svarstexten är ett `Handle`-objekt med typen `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Attribut | Typ | Beskrivning |
| --- | --- | --- |
| `key` | Sträng | **Krävs**. Postens namn. |
| `value` | Sträng | *Valfritt*. Postvärdet. |
| `maxAge` | Heltal | *Valfritt* Tiden (i sekunder) till inmatningen förfaller. Om det saknas bör poster endast lagras för den aktuella sessionen. |
| `attrs` | `Map<String, String>` | *Valfritt*. En valfri lista med postattribut. För alla säkra anslutningar med en säker referens-HTTP-rubrik anges attributet `SameSite` till `None`. |


Om du vill ha stöd för flera taggar (d.v.s. flera SDK-instanser i samma egenskap, som eventuellt refererar till olika organisationer), kommer alla tillståndsposter automatiskt att prefixeras med `kndctr_` och URL-säkra organisations-ID:n.

När klientens SDK tar emot en `state:store`-referens i svaret måste den göra följande:

* Lagra poster på klientsidan, med hänsyn till den förfallotid som anges av gatewayen.
* Läs in dem från klientarkivet och inkludera alla poster som inte har förfallit i efterföljande begäranden.

Här är ett exempel på en begäran som skickas i det sparade tillståndet på klientsidan:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Bevarar klientstatus i webbläsarcookies

När du arbetar med webbläsarklienter kan Edge Network automatiskt behålla posterna som webbläsarcookies. Detta ger stöd för genomskinlig lagring eftersom webbläsare som standard respekterar protokollet för tillståndshantering.

Nästan alla poster materialiseras som cookies från första part när de aktiveras och stöds (se anteckningen nedan), men gatewayen kan även lagra vissa cookies från tredje part när domänen `adobedc.demdex.net` från tredje part används.

Eftersom posterna alltid är bundna till ett specifikt omfång (enhet/program) enligt definition, kommer endast den delmängd som är kompatibel med det aktuella begärandesammanhanget att skrivas av Edge Network. Oskrivna poster
returnerades inom en `state:store`-referens.

Som en allmän regel skrivs poster med programomfång alltid som cookies från första part, medan poster med enhetsomfång skrivs som cookies från tredje part. Anroparen kan bestämma vilken post som ska skrivas, beroende på samtalskontexten.

Anroparen måste uttryckligen aktivera stöd för lagring av klienttillstånd som cookies via flaggan `meta.state.cookiesEnabled`:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Attribut | Typ | Beskrivning |
| --- | --- | --- |
| `cookiesEnabled` | Boolean | Aktivera stöd för cookies när inställningen är vald. Standardvärdet är `false`. |
| `domain` | Sträng | Krävs när `cookiesEnabled: true`. Den toppnivådomän som cookies ska skrivas på. Edge Network använder det här värdet för att avgöra om läget kan sparas som cookies. |

Även om stöd för cookies är aktiverat via flaggan `cookiesEnabled` skriver Adobe Experience Platform Edge Network bara tillståndsposterna om den begärande toppnivådomänen matchar den `domain` som har angetts av anroparen. Om det finns ett matchningsfel returneras poster i en `state:store`-referens.

Det går inte att skriva cookies från första part (även om stöd är aktiverat) i följande fall:

* Begäran kommer på domänen `adobedc.demdex.net` från tredje part.
* Begäran kommer på en förstahandsdomän, `CNAME`, som skiljer sig från den som har angetts av anroparen i `meta.state.domain`.

## Cookie-säkerhet

Alla cookies har [den säkra flaggan](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) aktiverad när det är möjligt.

Alla säkra cookies har attributet [SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) inställt på `None`, vilket innebär att cookies skickas i alla sammanhang, både från den första parten och från korsursprung.

* För cookies (`kndcrt_*`) från första part anges flaggan `Secure` endast när frågekontexten är säker (HTTPS) och när referenten ([Refererande HTTP-huvud](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) också är HTTPS. Om referenten inte är säker (HTTP) utelämnas flaggan `Secure` så att Web SDK kan läsa dem. En säker cookie kan inte läsas från en osäker kontext.
* För cookie-filen (demdex) från tredje part anges alltid flaggan `Secure` eftersom alla begäranden är HTTPS, vilket innebär att begärandekontexten är säker och att denna cookie aldrig läses från JavaScript.

Flaggan `Secure` finns inte i [metadatarepresentationen av cookies](#state-as-metadata). Endast attributet `SameSite` inkluderas. I det här fallet är det klientens ansvar att ange flaggan `Secure` korrekt när attributet `SameSite` finns. Cookies med `SameSite=None` måste även ange attributet `Secure` eftersom de kräver en säker kontext (HTTPS).
