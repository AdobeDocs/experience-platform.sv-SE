---
title: Använda Adobe Target med Platform Web SDK
description: Lär dig hur du återger anpassat innehåll med Experience Platform Web SDK med Adobe Target
keywords: mål;adobe target;activity.id;experience.id;renderDecision;DecisionScopes;prehide snippet;vec;Form Based Experience Composer;xdm;audiences;Decision;scope;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: e7f5074ef776fc6ccd4f9951722861d771a371de
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 3%

---

# Använda [!DNL Adobe Target] med [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan leverera och återge personaliserade upplevelser som hanteras  [!DNL Adobe Target] i webbkanalen. Du kan använda en WYSIWYG-redigerare som kallas [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) eller ett icke-visuellt gränssnitt, [formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), för att skapa, aktivera och leverera dina aktiviteter och personaliseringsupplevelser.

Följande funktioner har testats och stöds för närvarande i [!DNL Target]:

* [A/B-tester](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Impression och konverteringsrapportering](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-verksamhet](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Experience Targeting-aktiviteter](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivariata tester (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-verksamhet](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Inställnings- och konverteringsrapportering för Native Target](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-stöd](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## Aktivera [!DNL Adobe Target]

Så här aktiverar du [!DNL Target]:

1. Aktivera [!DNL Target] i din [datastream](../../fundamentals/datastreams.md) med rätt klientkod.
1. Lägg till alternativet `renderDecisions` i dina händelser.

Du kan sedan även lägga till följande alternativ:

* **`decisionScopes`**: Hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen) genom att lägga till det här alternativet till dina händelser.
* **[Dölja fragment](../manage-flicker.md)**: Dölj endast vissa delar av sidan.

## Använda Adobe Target VEC

Om du vill använda VEC med en [!DNL Platform Web SDK]-implementering installerar och aktiverar du antingen [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) eller [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Mer information finns i [hjälptillägget för Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) i *Adobe Target-handboken*.

## Återge VEC-aktiviteter automatiskt

[!DNL Adobe Experience Platform Web SDK] kan automatiskt återge dina upplevelser som definieras via [!DNL Adobe Target] VEC på webben för dina användare. Om du vill ange till [!DNL Experience Platform Web SDK] för att automatiskt återge VEC-aktiviteter skickar du en händelse med `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Använda den formulärbaserade dispositionen

[Formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) är ett icke-visuellt gränssnitt som är användbart för att konfigurera [!UICONTROL A/B Tests]-, [!UICONTROL Experience Targeting]-, [!UICONTROL Automated Personalization]- och [!UICONTROL Recommendations]-aktiviteter med olika svarstyper, som JSON, HTML, Image osv. Beroende på vilken svarstyp eller vilket beslut som har returnerats av [!DNL Target] kan din affärslogik köras. Om du vill hämta beslut för dina formulärbaserade dispositionsaktiviteter skickar du en händelse med alla&quot;beslutScopes&quot; som du vill ta emot ett beslut för.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Beslutsomfattningar

`decisionScopes` definiera avsnitt, platser eller delar av sidorna där du vill återge en personaliserad upplevelse. Dessa `decisionScopes` är anpassningsbara och användardefinierade. För nuvarande [!DNL Target]-kunder kallas `decisionScopes` även&quot;mboxes&quot;. I gränssnittet [!DNL Target] visas `decisionScopes` som &quot;locations&quot;.

## Omfånget `__view__`

[!DNL Experience Platform Web SDK] innehåller funktioner för att hämta VEC-åtgärder utan att förlita dig på SDK för att återge VEC-åtgärder åt dig. Skicka en händelse med `__view__` definierad som `decisionScopes`.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Målgrupper i XDM

När du definierar målgrupper för dina [!DNL Target]-aktiviteter som levereras via [!DNL Platform Web SDK] måste [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) definieras och användas. När du har definierat XDM-scheman, klasser och schemafältgrupper kan du skapa en [!DNL Target]-målgruppsregel som definieras av XDM-data för målinriktning. I [!DNL Target] visas XDM-data i [!UICONTROL Audience Builder] som en anpassad parameter. XDM-filen serialiseras med punktnotation (till exempel `web.webPageDetails.name`).

Om du har [!DNL Target]-aktiviteter med fördefinierade målgrupper som använder anpassade parametrar eller en användarprofil levereras de inte korrekt via SDK. I stället för att använda egna parametrar eller användarprofilen måste du använda XDM i stället. Det finns dock färdiga målgruppsfält som stöds via [!DNL Platform Web SDK] och som inte kräver XDM. Dessa fält är tillgängliga i [!DNL Target]-gränssnittet som inte kräver XDM:

* Målbibliotek
* Geo
* Nätverk
* Operativsystem
* Webbplatssidor
* Webbläsare
* Trafikkällor
* Tidsram

Mer information finns i [Kategorier för målgrupper](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) i *Adobe Target guide*.

### Uppdatering av en profil

Med [!DNL Platform Web SDK] kan du uppdatera profilen till [!DNL Target]-profilen och till [!DNL Platform Web SDK] som en upplevelsehändelse.

Om du vill uppdatera en [!DNL Target]-profil kontrollerar du att profildata skickas med följande:

* Under `“data {“`
* Under `“__adobe.target”`
* Prefix `“profile.”`, t.ex. enligt nedan

| Nyckel | Typ | Beskrivning |
| --- | --- | --- |
| `renderDecisions` | Boolean | Anger om personaliseringskomponenten ska tolka DOM-åtgärder |
| `decisionScopes` | Matris `<String>` | En lista över omfattningar som kan hämta beslut för |
| `xdm` | Objekt | Data formaterade i XDM som landar i Platform Web SDK som en upplevelsehändelse |
| `data` | Objekt | Godtyckliga nyckel/värde-par skickas till [!DNL Target]-lösningar under målklassen. |

Vanlig [!DNL Platform Web SDK]-kod som använder det här kommandot ser ut så här:

**`sendEvent`med profildata**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform stuff (event & profile) }
});
```

**Exempelkod**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
	"entity.id" : "123",
	"entity.genre" : "Drama"
      }
    }
  }
}) 
.then(console.log);
```

## Begär rekommendationer

I följande tabell visas [!DNL Recommendations]-attribut och om vart och ett stöds via [!DNL Platform Web SDK]:

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

## Felsökning

mboxTrace och mboxDebug har tagits bort. Använd [[!DNL Platform Web SDK] felsökning](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologi

__Beslut:__ I  [!DNL Target]det här fallet korrelerar beslut till den erfarenhet som valts i en aktivitet.

__Schema:__ Schemat för ett beslut är den typ av erbjudande som finns i  [!DNL Target].

__Tillämpningsområde:__ Beslutets tillämpningsområde. I [!DNL Target] är omfattningen mBox. Den globala mBox är `__view__`-scopet.

__XDM:__ XDM serialiseras till punktnotation och sätts sedan in  [!DNL Target] som mBox-parametrar.
