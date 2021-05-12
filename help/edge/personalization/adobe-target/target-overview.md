---
title: Använda Adobe Target med Platform Web SDK
description: Lär dig hur du återger anpassat innehåll med Experience Platform Web SDK med Adobe Target
keywords: mål;adobe target;activity.id;experience.id;renderDecision;DecisionScopes;prehide snippet;vec;Form Based Experience Composer;xdm;audiences;Decision;scope;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 20adb26fbd55302ac8005978968a0d69bdda8755
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 2%

---

# Använda Adobe Target med Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kan leverera och återge personaliserade upplevelser som hanteras i Adobe Target i webbkanalen. Du kan använda en WYSIWYG-redigerare som kallas [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC) eller ett icke-visuellt gränssnitt, [formulärbaserad Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), för att skapa, aktivera och leverera dina aktiviteter och personaliseringsupplevelser.

Följande funktioner har testats och stöds för närvarande i Target:

* A/B-tester
* A4T Impression och konverteringsrapportering
* Automated Personalization
* Experience Targeting
* Multivariata tester
* Impression- och konverteringsrapportering för inbyggda mål
* VEC-stöd

## Aktivera Adobe Target

Så här aktiverar du [!DNL Target]:

1. Aktivera Target i din [datastream](../../fundamentals/datastreams.md) med rätt klientkod.
1. Lägg till alternativet `renderDecisions` i dina händelser.

Du kan sedan även lägga till följande alternativ:

* `decisionScopes`: Hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen) genom att lägga till det här alternativet till dina händelser.
* [Dölja fragment](../manage-flicker.md): Dölj endast vissa delar av sidan.

## Använda Adobe Target VEC

Om du vill använda VEC med en Platform Web SDK-implementering installerar och aktiverar du antingen [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) eller [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

## Återge VEC-aktiviteter automatiskt

Adobe Experience Platform Web SDK kan automatiskt återge de upplevelser som definieras via Adobe Target VEC på webben för dina användare. Om du vill ange för Adobe Experience Platform Web SDK att automatiskt återge VEC-aktiviteter skickar du en händelse med `renderDecisions = true`:

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

Den formulärbaserade Experience Composer är ett icke-visuellt gränssnitt som är användbart för att konfigurera A/B-tester, [!DNL Experience Targeting]-, Automated Personalization- och Recommendations-aktiviteter med olika svarstyper, t.ex. JSON, HTML, Image. Beroende på vilken svarstyp eller vilket beslut som returneras av Adobe Target kan din affärslogik användas. Om du vill hämta beslut för dina formulärbaserade dispositionsaktiviteter skickar du en händelse med alla&quot;beslutScopes&quot; som du vill ta emot ett beslut för.

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

`decisionScopes` definierar avsnitt, platser eller delar av sidorna där du vill återge en personlig upplevelse. Dessa `decisionScopes` är anpassningsbara och användardefinierade. För nuvarande [!DNL Target]-kunder kallas `decisionScopes` även&quot;mboxes&quot;. I gränssnittet [!DNL Target] visas `decisionScopes` som &quot;locations&quot;.

## Omfånget `__view__`

Adobe Experience Platform Web SDK innehåller funktioner där du kan hämta VEC-åtgärder utan att förlita dig på SDK för att återge VEC-åtgärder åt dig. Skicka en händelse med `__view__` definierad som `decisionScopes`.

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

När du definierar målgrupper för målaktiviteter som levereras via Adobe Experience Platform Web SDK måste [XDM](https://docs.adobe.com/content/help/sv-SE/experience-platform/xdm/home.html) definieras och användas. När du har definierat XDM-scheman, klasser och schemafältgrupper kan du skapa en målgruppsregel som definieras av XDM-data för målgruppsanpassning. I Target visas XDM-data i Audience Builder som en anpassad parameter. XDM-filen serialiseras med punktnotation (till exempel `web.webPageDetails.name`).

Om du har Target-aktiviteter med fördefinierade målgrupper som använder anpassade parametrar eller en användarprofil levereras de inte korrekt via SDK. I stället för att använda egna parametrar eller användarprofilen måste du använda XDM i stället. Det finns dock färdiga målgruppsfält som stöds via Adobe Experience Platform Web SDK och som inte kräver XDM. Dessa fält är tillgängliga i målgränssnittet som inte kräver XDM:

* Målbibliotek
* Geo
* Nätverk
* Operativsystem
* Webbplatssidor
* Webbläsare
* Trafikkällor
* Tidsram

## Terminologi

__Beslut:__ I  [!DNL Target]det här fallet korrelerar beslut till den erfarenhet som valts i en aktivitet.

__Schema:__ Schemat för ett beslut är den typ av erbjudande som finns i  [!DNL Target].

__Tillämpningsområde:__ Beslutets tillämpningsområde. I [!DNL Target] är omfattningen mBox. Den globala mBox är `__view__`-scopet.

__XDM:__ XDM serialiseras till punktnotation och sätts sedan in  [!DNL Target] som mBox-parametrar.
