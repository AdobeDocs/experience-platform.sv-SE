---
title: Klienttillståndshantering
description: Lär dig hur Adobe Experience Platform Edge Network hanterar klienttillstånd
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: klient;tillstånd;hantering;edge;network;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 1%

---

# Klienttillståndshantering

Själva Edge-nätverket är tillståndslöst (det behåller inte sin egen session). Det finns dock vissa användningsfall som kräver att klientsidans tillstånd är beständigt, till exempel:

* Enhetsidentifiering (se [besökaridentifiering](visitor-identification.md))
* Samla in och framtvinga användargodkännande
* Sessions-ID för personalisering behålls

Edge Network använder ett protokoll för statushantering, som delegerar lagringsaspekten till klienten/SDK, och inkluderar tillståndsposter i sina svar. För webbläsare lagras posterna som cookies.

Klientansvaret är att lagra och inkludera dem i alla efterföljande begäranden. Klienten måste också se till att tävlingsbidragen förfaller enligt gatewayens anvisningar. När posterna har sparats som cookies utförs allt detta automatiskt i webbläsaren.

Även om lägesposterna alltid har en oformaterad `String` värde (som är synligt för anroparen/SDK) får du inte förbruka eller manipulera värdena på något sätt. Värdets struktur/format eller till och med namnet kan ändras när som helst, vilket kan leda till oväntat beteende för klienter som använder läget internt. Tillståndet är alltid avsett att användas av själva gatewayen eller andra edge-tjänster.

## Bevarar klientstatus som metadata

Det tillstånd som returneras av [!DNL Edge Network] i svarsbrödtexten är en `Handle` objekt med typen `state:store`.

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
| `key` | Sträng | **Obligatoriskt**. Postens namn. |
| `value` | Sträng | *Valfritt*. Postvärdet. |
| `maxAge` | Heltal | *Valfritt* Tid (i sekunder) tills inmatningen förfaller. Om det saknas bör poster endast lagras för den aktuella sessionen. |
| `attrs` | `Map<String, String>` | *Valfritt*. En valfri lista med postattribut. För alla säkra anslutningar med en säker referens-HTTP-rubrik finns följande `SameSite` attribute is set to `None`. |


Om du vill ha stöd för flertaggning (d.v.s. flera SDK-instanser i samma egenskap, som kan referera till olika organisationer), kommer alla lägesposter automatiskt att prefixeras med `kndctr_` och URL-säkert organisations-ID.

När klient-SDK får en `state:store` -hantering i svaret måste den göra följande:

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

Nästan alla poster materialiseras som cookies från första part när de är aktiverade och stöds (se anteckningen nedan), men gatewayen kan även lagra vissa cookies från tredje part när den tredje parten `adobedc.demdex.net` domän används.

Eftersom poster alltid är bundna till ett specifikt omfång (enhet/program) enligt definition, kommer bara den delmängd som är kompatibel med den aktuella begärandekontexten att skrivas av Edge Network. Oskrivna poster returneras inom en `state:store` handtag.

Som en allmän regel skrivs poster med programomfång alltid som cookies från första part, medan poster med enhetsomfång skrivs som cookies från tredje part. Anroparen kan bestämma vilken post som ska skrivas, beroende på samtalskontexten.

Anroparen måste uttryckligen aktivera stöd för lagring av klienttillstånd som cookies via `meta.state.cookiesEnabled` flagga:

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
| `domain` | Sträng | Krävs när `cookiesEnabled: true`. Den toppnivådomän som cookies ska skrivas på. Edge Network använder det här värdet för att avgöra om tillstånd kan sparas som cookies. |

Även om stöd för cookies är aktiverat via `cookiesEnabled` flagga, Adobe Experience Platform Edge Network skriver bara tillståndsposterna om den begärande toppnivådomänen matchar `domain` anges av anroparen. Om det finns en avvikelse returneras poster i en `state:store` handtag.

Det går inte att skriva cookies från första part (även om stöd är aktiverat) i följande fall:

* Begäran kommer från tredje part `adobedc.demdex.net` domän.
* Förfrågan kommer från en första part `CNAME` domän, som skiljer sig från den som anges av anroparen i `meta.state.domain`.

## Cookie-säkerhet

Alla cookies har [Säker flagga](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) aktiveras när det är möjligt.

Alla säkra cookies har [Attributet SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) ange till `None`, vilket innebär att cookies skickas i alla sammanhang, både från den första parten och från korsursprung.

* För cookies från första part (`kndcrt_*`), `Secure` -flaggan anges bara när begärandekontexten är säker (HTTPS) och när den refereras ([HTTP-huvud](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) är även HTTPS. Om referenten inte är säker (HTTP) `Secure` -flaggan utelämnas så att Web SDK kan läsa dem. En säker cookie kan inte läsas från en osäker kontext.
* För cookie (demdex) från tredje part `Secure` Flaggan är alltid inställd eftersom alla begäranden är HTTPS, så begärandekontexten är säker och denna cookie läses aldrig från JavaScript.

The `Secure` flaggan finns inte i [metadatarepresentation av cookies](#state-as-metadata). Endast `SameSite` är inkluderat. I det här fallet är det kundens ansvar att ställa in `Secure` flagga när `SameSite` attribut finns. Cookies med `SameSite=None` måste även specificera `Secure` eftersom de kräver ett säkert sammanhang (HTTPS).
