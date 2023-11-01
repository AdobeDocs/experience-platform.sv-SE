---
title: Tips för användaragentklient
description: Lär dig hur klienttips för användaragenter fungerar i Web SDK. Klienttips gör att webbplatsägare kan komma åt mycket av den information som finns i användaragentsträngen, men på ett mer sekretessbeständigt sätt.
keywords: användaragent;klienttips; sträng; användaragentsträng; låg entropi; hög entropi
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 2%

---

# Tips för användaragentklient

## Översikt {#overview}

Varje gång en webbläsare skickar en begäran till en webbserver innehåller begärans huvud information om webbläsaren och miljön som webbläsaren körs i. Alla dessa data sammanställs i en sträng, som kallas användaragentsträng.

Här är ett exempel på hur en användaragentsträng ser ut på en begäran som kommer från en Chrome-webbläsare som körs på en [!DNL Mac OS] enhet.

>[!NOTE]
>
>Under årens lopp har mängden webbläsarinformation och enhetsinformation som ingår i användaragentsträngen ökat och ändrats flera gånger. I exemplet nedan visas ett urval av den vanligaste användaragentinformationen.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Fält | Värde |
|---|---|
| Programvarunamn | Krom |
| Programversion | 105 |
| Fullversion | 105.0.0.0 |
| Namn på layoutmotor | AppleWebKit |
| Layoutmotorversion | 537.36 |
| Operativsystem | MAC OS X |
| Operativsystemversion | 10.15.7 |
| Enhet | Intel Mac OS X 10_15_7 |

## Användningsfall {#use-cases}

Användaragentsträngar har länge använts för att ge marknadsförings- och utvecklingsteam viktiga insikter i hur webbläsare, operativsystem och enheter visar webbplatsinnehåll samt hur användarna interagerar med webbplatser.

Användaragentsträngar används också för att blockera skräppost och filterbottar som crawlar webbplatser för en mängd andra syften.

## Användaragentsträngar i Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud lösningar använder användaragentsträngarna på olika sätt.

* Adobe Analytics använder användaragentsträngen för att utöka och hämta ytterligare information om operativsystem, webbläsare och enheter som används för att besöka en webbplats.
* Adobe Audience Manager och Adobe Target kvalificerar slutanvändare för segmenterings- och personaliseringskampanjer baserat på informationen i användaragentsträngen.

## Introduktion till klienttips för användaragent {#ua-ch}

Under de senaste åren har webbplatsägare och marknadsföringsleverantörer använt användaragentsträngar tillsammans med annan information i begäranderubriker för att skapa digitala fingeravtryck. Dessa fingeravtryck kan användas som ett sätt att identifiera användare utan deras kännedom.

Trots det viktiga syftet med användaragentsträngar för webbplatsägare har webbläsarutvecklare beslutat att ändra hur användaragentsträngar fungerar, för att begränsa eventuella sekretessproblem för slutanvändare.

Den lösning de utvecklade kallas [klienttips för användaragent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Klienttips gör det fortfarande möjligt för webbplatser att samla in nödvändig information om webbläsare, operativsystem och enheter, samtidigt som det ger ett bättre skydd mot dolda spårningsmetoder, som fingeravtryck.

Klienttips gör att webbplatsägare kan komma åt mycket av den information som finns i användaragentsträngen, men på ett mer sekretessbeständigt sätt.

När moderna webbläsare skickar en användare till en webbserver, skickas hela användaragentsträngen vid varje begäran, oavsett om den krävs eller inte. Klienttips tvingar å andra sidan en modell där servern måste fråga webbläsaren om ytterligare information om klienten. När webbläsaren tar emot den här begäran kan den tillämpa egna profiler eller användarkonfiguration för att avgöra vilka data som returneras. I stället för att visa hela användaragentsträngen som standard för alla begäranden, hanteras nu åtkomsten på ett explicit och spårbart sätt.

## Stöd för webbläsare {#browser-support}

[Tips för användaragentklient](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) introducerades med [!DNL Google Chrome]version 89.

Ytterligare Chromium-baserade webbläsare stöder API:t för klienttips, som:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Kategorier {#categories}

Det finns två typer av klienttips för användaragenten:

* [Tips för låg entropi-klient](#low-entropy)
* [Tips för hög entropi-klient](#high-entropy)

### Tips för låg entropi-klient {#low-entropy}

Klienttips för låg entropi innehåller grundläggande information som inte kan användas för fingeravtrycksanvändare. Information som webbläsarens varumärke, plattform och om begäran kommer från en mobil enhet.

Klienttips med låg entropi är aktiverade som standard i Web SDK och skickas för varje begäran.

| HTTP-huvud | JavaScript | Ingår i användaragent som standard | Ingår i klienttips som standard |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Ja | Ja |
| `Sec-CH-UA-Platform` | `platform` | Ja | Ja |
| `Sec-CH-UA-Mobile` | `mobile` | Ja | Ja |

### Tips för hög entropi-klient {#high-entropy}

High-entropy-klienttips är mer detaljerad information om klientenheten, som plattformsversion, arkitektur, modell, bitness (64- eller 32-bitars plattformar) eller fullständig operativsystemsversion. Den här informationen kan eventuellt användas vid fingeravtryck.

| HTTP-huvud | JavaScript | Ingår i användaragent som standard | Ingår i klienttips som standard |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Ja | Nej |
| `Sec-CH-UA-Arc` | `architecture` | Ja | Nej |
| `Sec-CH-UA-Model` | `model` | Ja | Nej |
| `Sec-CH-UA-Bitness` | `Bitness` | Ja | Nej |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Ja | Nej |

Klienttips för hög entropi är inaktiverade som standard i Web SDK. Om du vill aktivera dem måste du konfigurera Web SDK manuellt för att begära tips för hög entropi-klient.

## Högupplösta klienttips påverkar Experience Cloud-lösningar {#impact-in-experience-cloud-solutions}

Vissa Adobe Experience Cloud-lösningar förlitar sig på information som ingår i kundtips med hög entropi när rapporter genereras.

Om du inte aktiverar klienttips för hög entropi i din miljö fungerar inte rapporterna och egenskaperna som beskrivs nedan i Adobe Analytics och Audience Manager.

### Adobe Analytics rapporterar beroende av klienttips för hög entropi {#analytics}

The [Operativsystem](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) -dimensionen inkluderar operativsystemsversion som lagras som ett högt entropi-klienttips. Om tips för klienter med hög entropi inte är aktiverat kan det bero på att operativsystemets version inte stämmer för träffar som samlats in från Chromium-webbläsare.

### Audience Manager förlitar sig på klienttips med hög entropi {#aam}

[!DNL Google] har uppdaterat [!DNL Chrome] webbläsarfunktioner för att minimera den information som samlas in via `User-Agent` header. Därför använder Audience Manager kunder som använder [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html) inte längre får tillförlitlig information om egenskaper baserat på [tangenter på plattformsnivå](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

Audience Manager-kunder som använder plattformsnivånycklar för målinriktning måste gå över till [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) i stället för [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)och aktivera [High Entropy Client-tips](#enabling-high-entropy-client-hints) att fortsätta att ta emot tillförlitliga uppgifter om egenskaper.

## Aktivera tips för hög entropi-klient {#enabling-high-entropy-client-hints}

Om du vill aktivera klienttips för hög entropi vid Web SDK-distributionen måste du inkludera ytterligare `highEntropyUserAgentHints` kontextalternativ, enligt beskrivningen i [konfigurationsdokumentation](configuring-the-sdk.md#context), tillsammans med din befintliga konfiguration.

Om du till exempel vill hämta klienttips för hög entropi från webbegenskaper ser konfigurationen ut så här:

`context: ["highEntropyUserAgentHints", "web"]`

## Exempel {#example}

Klienttips som finns i rubrikerna för den första begäran som webbläsaren gör till en webbserver innehåller webbläsarvarumärket, huvudversionen av webbläsaren och en indikator på om klienten är en mobil enhet. Varje datadel har ett eget rubrikvärde i stället för att grupperas i en enda användaragentsträng, vilket visas nedan:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Motsvarande [!DNL User-Agent] sidhuvud för samma webbläsare skulle se ut så här:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Även om informationen är liknande innehåller den första begäran till servern klienttips. Dessa innehåller bara en delmängd av det som är tillgängligt i användaragentsträngen. Saknas i begäran är operativsystemets arkitektur, operativsystemets fullständiga version, namnet på layoutmotorn, versionen av layoutmotorn och webbläsarversionen.

Vid efterföljande förfrågningar [!DNL Client Hints API] gör att webbservrar kan fråga efter ytterligare information om enheten. När dessa värden begärs, beroende på webbläsarprincipen eller användarinställningarna, kan webbläsarsvaret inkludera den informationen.

Nedan visas ett exempel på JSON-objektet som returneras av [!DNL Client Hints API] när höga entropinavärden begärs:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
