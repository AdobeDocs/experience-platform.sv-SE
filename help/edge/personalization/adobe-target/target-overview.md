---
title: Använda Adobe Target med Platform Web SDK
description: Lär dig hur du återger anpassat innehåll med Experience Platform Web SDK med Adobe Target
keywords: mål;adobe target;activity.id;experience.id;renderDecision;DecisionScopes;prehide snippet;vec;Form Based Experience Composer;xdm;audiences;Decision;scope;schema;system chart;chart
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 5a048505be139b58dbb3bf85120df5e3cc46881e
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 3%

---

# Använda [!DNL Adobe Target] med [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan leverera och återge personaliserade upplevelser som hanteras i [!DNL Adobe Target] till webbkanalen. Du kan använda en WYSIWYG-redigerare som kallas [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), eller ett icke-visuellt gränssnitt, [Formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), för att skapa, aktivera och leverera era aktiviteter och personaliseringsupplevelser.

>[!IMPORTANT]
>
>Lär dig hur du migrerar målinsimplementeringen till Platform Web SDK med [Migrera mål från at.js 2.x till Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) självstudiekurs.
>
>Lär dig implementera Target för första gången med [Implementera Adobe Experience Cloud med Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) självstudiekurs. Mer information om Target finns i självstudieavsnittet med namnet [Konfigurera Target med Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Följande funktioner har testats och stöds för närvarande i [!DNL Target]:

* [A/B-tester](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Impression och konverteringsrapportering](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-verksamhet](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Experience Targeting-aktiviteter](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivariata tester (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-verksamhet](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Inställnings- och konverteringsrapportering för Native Target](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-stöd](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] systemdiagram

Följande diagram hjälper dig att förstå arbetsflödet i [!DNL Target] och [!DNL Platform Web SDK] kantbeslut.

![Diagram över Adobe Target edge-beslut med Platform Web SDK](./assets/target-platform-web-sdk.png)

| Utlysning | Information |
| --- | --- |
| 1 | Enheten läser in [!DNL Platform Web SDK]. The [!DNL Platform Web SDK] skickar en begäran till edge-nätverket med XDM-data, DataStreams Environment ID, inskickade parametrar och Customer ID (valfritt). Sidan (eller behållarna) är fördold. |
| 2 | edge-nätverket skickar begäran till edge-tjänsterna för att berika den med besökar-ID, samtycke och annan kontextinformation för besökare, som geopositionering och enhetsvänliga namn. |
| 3 | edge-nätverket skickar den berikade personaliseringsbegäran till [!DNL Target] kant med besökar-ID och inskickade parametrar. |
| 4 | Profilskript körs och matas sedan in i [!DNL Target] profillagring. Profillagring hämtar segment från [!UICONTROL Audience Library] (till exempel segment som delas från [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | Baserat på parametrar för URL-begäran och profildata, [!DNL Target] avgör vilka aktiviteter och upplevelser som ska visas för besökaren för den aktuella sidvyn och för framtida förhämtade vyer. [!DNL Target] skickar sedan tillbaka detta till gränsnätverket. |
| 6 | a. Kantnätverket skickar personaliseringssvaret tillbaka till sidan, eventuellt inklusive profilvärden för ytterligare personalisering. Personaliserat innehåll på den aktuella sidan visas så snabbt som möjligt utan att man behöver flimra standardinnehållet.<br>b. Personanpassat innehåll för vyer som visas som ett resultat av användaråtgärder i ett Single Page-program (SPA) cachelagras så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. <br>c. Edge-nätverket skickar besökar-ID och andra värden i cookies, som samtycke, sessions-ID, identitet, cookie-kontroll, personalisering och så vidare. |
| 7 | Edge-nätverket framåt [!UICONTROL Analytics for Target] (A4T) information (aktivitets-, upplevelse- och konverteringsmetadata) till [!DNL Analytics] kant. |

## Aktivering [!DNL Adobe Target]

Aktivera [!DNL Target]gör du följande:

1. Aktivera [!DNL Target] i [datastream](../../datastreams/overview.md) med rätt klientkod.
1. Lägg till `renderDecisions` till dina händelser.

Du kan sedan även lägga till följande alternativ:

* **`decisionScopes`**: Hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen) genom att lägga till det här alternativet till dina händelser.
* **[Dölja fragment](../manage-flicker.md)**: Dölj endast vissa delar av sidan.

## Använda Adobe Target VEC

Så här använder du VEC med en [!DNL Platform Web SDK] implementera, installera och aktivera antingen [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) eller [Krom](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Mer information finns i [Hjälptillägg för Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) i *Adobe Target Guide*.

## Återge personaliserat innehåll

Se [Återger innehåll för personalisering](../rendering-personalization-content.md) för mer information.

## Målgrupper i XDM

När du definierar målgrupper för [!DNL Target] aktiviteter som levereras via [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) måste definieras och användas. När du har definierat XDM-scheman, klasser och schemafältgrupper kan du skapa en [!DNL Target] målgruppsregel som definieras av XDM-data för målinriktning. Inom [!DNL Target], visas XDM-data i [!UICONTROL Audience Builder] som en anpassad parameter. XDM-filen serialiseras med punktnotation (till exempel `web.webPageDetails.name`).

Om du har [!DNL Target] aktiviteter med fördefinierade målgrupper som använder anpassade parametrar eller en användarprofil levereras de inte korrekt via SDK. I stället för att använda egna parametrar eller användarprofilen måste du använda XDM i stället. Det finns dock färdiga målgruppsfält som stöds via [!DNL Platform Web SDK] som inte kräver XDM. Dessa fält är tillgängliga i [!DNL Target] Gränssnitt som inte kräver XDM:

* Målbibliotek
* Geo
* Nätverk
* Operativsystem
* Webbplatssidor
* Webbläsare
* Trafikkällor
* Tidsram

Mer information finns i [Kategorier för målgrupper](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) i *Adobe Target Guide*.

### Svarstoken

Svarstoken används främst för att skicka metadata till tredje part som Google, Facebook, osv. Svarstoken returneras i `meta` fält inom `propositions` -> `items`. Här följer ett exempel:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Om du vill samla in svarstoken måste du prenumerera på `alloy.sendEvent` löfte, iterera genom `propositions`
och extrahera detaljerna från `items` -> `meta`. Varje `proposition` har en `renderAttempted` booleskt fält som anger om `proposition` återgavs eller inte. Se exemplet nedan:

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

När automatisk återgivning är aktiverat innehåller propositionsarrayen:

#### Vid sidinläsning:

* Formulärbaserad dispositionsbaserad `propositions` med `renderAttempted` flaggan är inställd på `false`
* Visual Experience Composer-baserade förslag med `renderAttempted` flaggan är inställd på `true`
* Visual Experience Composer-baserade förslag för en enkelsidig programvy med `renderAttempted` flaggan är inställd på `true`

#### I vyn - ändra (för cachelagrade vyer):

* Visual Experience Composer-baserade förslag för en enkelsidig programvy med `renderAttempted` flaggan är inställd på `true`

När automatisk återgivning är inaktiverat innehåller propositionsarrayen:

#### Vid sidinläsning:

* Formulärbaserad dispositionsbaserad `propositions` med `renderAttempted` flaggan är inställd på `false`
* Visual Experience Composer-baserade förslag med `renderAttempted` flaggan är inställd på `false`
* Visual Experience Composer-baserade förslag för en enkelsidig programvy med `renderAttempted` flaggan är inställd på `false`

#### I vyn - ändra (för cachelagrade vyer):

* Visual Experience Composer-baserade förslag för en enkelsidig programvy med `renderAttempted` flaggan är inställd på `false`

### Uppdatering av en profil

The [!DNL Platform Web SDK] gör att du kan uppdatera profilen till [!DNL Target] och [!DNL Platform Web SDK] som en upplevelsehändelse.

Så här uppdaterar du en [!DNL Target] kontrollerar du att profildata skickas med följande:

* Under `"data {"`
* Under `"__adobe.target"`
* Prefix `"profile."` t.ex. enligt nedan

| Nyckel | Typ | Beskrivning |
| --- | --- | --- |
| `renderDecisions` | Boolean | Anger om personaliseringskomponenten ska tolka DOM-åtgärder |
| `decisionScopes` | Array `<String>` | En lista över omfattningar som kan hämta beslut för |
| `xdm` | Objekt | Data formaterade i XDM som landar i Platform Web SDK som en upplevelsehändelse |
| `data` | Objekt | Godtyckliga nyckel-/värdepar skickade till [!DNL Target] lösningar under målklassen. |

Normal [!DNL Platform Web SDK] koden som använder det här kommandot ser ut så här:

**`sendEvent`med profildata**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Så här skickar du profilattribut till Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Begär rekommendationer

Följande tabell innehåller [!DNL Recommendations] och om vart och ett stöds via [!DNL Platform Web SDK]:

| Kategori | Attribut | Supportstatus |
| --- | --- | --- |
| Recommendations - Standardenhetsattribut | entity.id | Stöds |
|  | entity.name | Stöds |
|  | entity.categoryId | Stöds |
|  | entity.pageUrl | Stöds |
|  | entity.thumbnailUrl | Stöds |
|  | entity.message | Stöds |
|  | entity.value | Stöds |
|  | entity.inventory | Stöds |
|  | entity.brand | Stöds |
|  | entity.margin | Stöds |
|  | entity.event.detailsOnly | Stöds |
| Recommendations - Anpassade entitetsattribut | entity.yourCustomAttributeName | Stöds |
| Recommendations - Reserverade mbox-/page-parametrar | excludeIds | Stöds |
|  | cartIds | Stöds |
|  | productPurchasedId | Stöds |
| Sida eller artikelkategori för kategoritillhörighet | user.categoryId | Stöds |

**Så här skickar du Recommendations-attribut till Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Felsökning

mboxTrace och mboxDebug har tagits bort. Använd [[!DNL Platform Web SDK] felsökning](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologi

__Förslag:__ I [!DNL Target], korrelerar förslag till upplevelsen som väljs från en aktivitet.

__Schema:__ Schemat för ett beslut är den typ av erbjudande som [!DNL Target].

__Omfång:__ Beslutets omfattning. I [!DNL Target]är omfattningen mBox. Den globala mBox är `__view__` omfång.

__XDM:__ XDM serialiseras till punktnotation och sätts sedan i [!DNL Target] som mBox-parametrar.
