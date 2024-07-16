---
title: Använd Adobe Target med Web SDK för personalisering
description: Lär dig hur du återger anpassat innehåll med Experience Platform Web SDK med Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 69406293dce5fdfc832adff801f1991626dafae0
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 1%

---

# Använd [!DNL Adobe Target] och [!DNL Web SDK] för personalisering

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan leverera och återge personaliserade upplevelser som hanteras i [!DNL Adobe Target] till webbkanalen. Du kan använda en WYSIWYG-redigerare, som kallas [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), eller ett icke-visuellt gränssnitt, [formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), för att skapa, aktivera och leverera dina aktiviteter och personaliseringsupplevelser.

>[!IMPORTANT]
>
>Lär dig hur du migrerar målinsimplementeringen till Platform Web SDK med självstudiekursen [Migrate Target från at.js 2.x till Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).
>
>Lär dig hur du implementerar Target för första gången med självstudiekursen [Implementera Adobe Experience Cloud med Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Mer information om Target finns i självstudieavsnittet [Konfigurera mål med plattformens webb-SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Följande funktioner har testats och stöds för närvarande i [!DNL Target]:

* [A/B-tester](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Impression and conversion reporting](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-aktiviteter](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Aktiviteter för målinriktning](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivariata tester (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-aktiviteter](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Inbyggt målinställnings- och konverteringsrapportering](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-support](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] systemdiagram

Följande diagram hjälper dig att förstå arbetsflödet för [!DNL Target]- och [!DNL Web SDK]-kantbeslut.

![Diagram över Adobe Target edge-beslut med Platform Web SDK](assets/target-platform-web-sdk-new.png)

| Utlysning | Information |
| --- | --- |
| 1 | Enheten läser in [!DNL Web SDK]. [!DNL Web SDK] skickar en begäran till Edge Network med XDM-data, datastreams Environment ID, inskickade parametrar och kundens ID (valfritt). Sidan (eller behållarna) är fördold. |
| 2 | Edge Network skickar begäran till edge services för att berika den med besökar-ID, samtycke och annan kontextinformation för besökare, som geopositionering och enhetsvänliga namn. |
| 3 | Edge Network skickar den berikade personaliseringsbegäran till kanten [!DNL Target] med besökar-ID:t och skickade parametrar. |
| 4 | Profilskript körs och matas sedan in i [!DNL Target]-profillagring. Profillagring hämtar segment från [!UICONTROL Audience Library] (till exempel segment som delas från [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | Baserat på parametrar för URL-begäran och profildata avgör [!DNL Target] vilka aktiviteter och upplevelser som ska visas för besökaren för den aktuella sidvyn och för framtida förhämtade vyer. [!DNL Target] skickar sedan tillbaka den här till Edge Network. |
| 6 | a. Edge Network skickar personaliseringssvaret tillbaka till sidan, eventuellt med profilvärden för ytterligare personalisering. Personaliserat innehåll på den aktuella sidan visas så snabbt som möjligt utan att man behöver flimra standardinnehållet.<br>b. Personanpassat innehåll för vyer som visas som ett resultat av användaråtgärder i ett Single Page-program (SPA) cachelagras så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. <br>c. Edge Network skickar besökar-ID och andra värden i cookies, som samtycke, sessions-ID, identitet, cookie-kontroll och personalisering. |
| 7 | Web SDK skickar meddelandet från enheten till Edge Network. |
| 8 | Edge Network vidarebefordrar information om [!UICONTROL Analytics for Target] (A4T) (aktivitet, upplevelse och konverteringsmetadata) till kanten [!DNL Analytics]. |

## Aktiverar [!DNL Adobe Target]

Så här aktiverar du [!DNL Target]:

1. Aktivera [!DNL Target] i [datastream](../../../datastreams/overview.md) med rätt klientkod.
1. Lägg till alternativet `renderDecisions` i dina händelser.

Du kan sedan även lägga till följande alternativ:

* **`decisionScopes`**: Hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen) genom att lägga till det här alternativet i dina händelser.
* **[Dölj fragment](../manage-flicker.md)**: Dölj endast vissa delar av sidan.

## Använda Adobe Target VEC

Om du vill använda VEC med en [!DNL Web SDK]-implementering installerar och aktiverar du [ Firefox ](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) eller [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Mer information finns i [Hjälptillägg för Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) i *Adobe Target-handboken*.

## Återge personaliserat innehåll

Mer information finns i [Återge anpassat innehåll](../rendering-personalization-content.md).

## Målgrupper i XDM

När du definierar målgrupper för dina [!DNL Target]-aktiviteter som levereras via [!DNL Web SDK] måste [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) definieras och användas. När du har definierat XDM-scheman, klasser och schemafältgrupper kan du skapa en [!DNL Target] målgruppsregel som definieras av XDM-data för målgruppsanpassning. I [!DNL Target] visas XDM-data i [!UICONTROL Audience Builder] som en anpassad parameter. XDM serialiseras med punktnotation (till exempel `web.webPageDetails.name`).

Om du har [!DNL Target] aktiviteter med fördefinierade målgrupper som använder anpassade parametrar eller en användarprofil levereras de inte korrekt via SDK. I stället för att använda egna parametrar eller användarprofilen måste du använda XDM i stället. Det finns dock färdiga målgruppsfält som stöds via [!DNL Web SDK] och som inte kräver XDM. De här fälten är tillgängliga i användargränssnittet [!DNL Target] som inte kräver XDM:

* Målbibliotek
* Geo
* Nätverk
* Operativsystem
* Webbplatssidor
* Webbläsare
* Trafikkällor
* Tidsram

Mer information finns i [Kategorier för målgrupper](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) i *Adobe Target-handboken*.

### Svarstoken

Svarstoken används för att skicka metadata till tredje part som Google eller Facebook. Svarstoken returneras
i fältet `meta` i `propositions` -> `items`. Här följer ett exempel:

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

Om du vill samla in svarstoken måste du prenumerera på `alloy.sendEvent`, iterera genom `propositions` och extrahera informationen från `items` -> `meta`.

Varje `proposition` har ett `renderAttempted` booleskt fält som anger om `proposition` återgavs eller inte. Se exemplet nedan:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
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

* Formulärbaserad dispositionsbaserad `propositions` med flaggan `renderAttempted` inställd på `false`
* Visual Experience Composer-baserade förslag med flaggan `renderAttempted` inställd på `true`
* Visual Experience Composer-baserade förslag för en programvy för en sida med flaggan `renderAttempted` inställd på `true`

#### I vyn - ändra (för cachelagrade vyer):

* Visual Experience Composer-baserade förslag för en programvy för en sida med flaggan `renderAttempted` inställd på `true`

När automatisk återgivning är inaktiverat innehåller propositionsarrayen:

#### Vid sidinläsning:

* [!DNL Form-based Composer]-baserad `propositions` med flaggan `renderAttempted` inställd på `false`
* [!DNL Visual Experience Composer]-baserade förslag med flaggan `renderAttempted` inställd på `false`
* [!DNL Visual Experience Composer]-baserade förslag för en enkelsidig programvy med flaggan `renderAttempted` inställd på `false`

#### I vyn - ändra (för cachelagrade vyer):

* Visual Experience Composer-baserade förslag för en programvy för en enstaka sida med flaggan `renderAttempted` inställd på `false`

### Uppdatering av en profil

Med [!DNL Web SDK] kan du uppdatera profilen till [!DNL Target]-profilen och till [!DNL Web SDK] som en upplevelsehändelse.

Om du vill uppdatera en [!DNL Target]-profil kontrollerar du att profildata skickas med följande:

* Under `"data {"`
* Under `"__adobe.target"`
* Prefix `"profile."`

| Nyckel | Typ | Beskrivning |
| --- | --- | --- |
| `renderDecisions` | Boolean | Anger om personaliseringskomponenten ska tolka DOM-åtgärder |
| `decisionScopes` | Matris `<String>` | En lista över omfattningar som kan hämta beslut för |
| `xdm` | Objekt | Data som är formaterade i XDM och som markeras i Web SDK som en upplevelsehändelse |
| `data` | Objekt | Godtyckliga nyckel-/värdepar skickade till [!DNL Target] lösningar under målklassen. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Fördröj sparandet av profil- eller enhetsparametrar tills innehållet har visats för slutanvändaren**

Om du vill fördröja inspelningsattribut i profilen tills innehållet visas anger du `data.adobe.target._save=false` i din begäran.

Till exempel innehåller din webbplats tre beslutsomfattningar som motsvarar tre kategorilänkar på webbplatsen (Män, Kvinnor och barn) och du vill spåra den kategori som användaren slutligen besökte. Skicka dessa förfrågningar med flaggan `__save` inställd på `false` för att undvika att kategorin bevaras när innehållet begärs. När innehållet har visualiserats skickar du rätt nyttolast (inklusive `eventToken` och `stateToken`) för motsvarande attribut som ska registreras.

<!--Save profile or entity attributes by default with:

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "__save" : true // Optional. __save=true is the default 
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt",
        "entity.id" : "1234",
      }
    }
  }
} ) ; 
```
-->

Exemplet nedan skickar ett trackEvent-liknande meddelande, kör profilskript, sparar attribut och registrerar omedelbart händelsen.

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt" ,
        "entity.id" : "1234" ,
        "track": {
          "scopes": [ "mbox1", "mbox2"],
          "type": "display|click|..."
        }
      }
    }
  }
} ) ;
```

>[!NOTE]
>
>Om direktivet `__save` utelämnas sparas profilen och entitetsattributen omedelbart, som om begäran har körts, även om resten av begäran är en förhämtning av personalisering. Direktivet `__save` är bara relevant för profil- och entitetsattribut. Om spårobjektet finns ignoreras direktivet `__save`. Data sparas omedelbart och meddelandet registreras.

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
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Begär rekommendationer

I följande tabell visas [!DNL Recommendations] attribut och om vart och ett stöds via [!DNL Web SDK]:

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
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Felsökning

mboxTrace och mboxDebug har tagits bort. Använd en metod för [Web SDK-felsökning](/help/web-sdk/use-cases/debugging.md) i stället.

## Terminologi

__Föreslag:__ I [!DNL Adobe Target] korrelerar förslag till upplevelsen som väljs från en aktivitet.

__Schema:__ Schemat för ett beslut är typen av erbjudande i [!DNL Adobe Target].

__Scope:__ Beslutets omfattning. I [!DNL Adobe Target] är omfattningen mBox. Den globala mBox är `__view__`-scopet.

__XDM:__ XDM serialiseras till punktnotation och placeras sedan i [!DNL Adobe Target] som mBox-parametrar.
