---
title: 'Adobe Target och Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK och Adobe Target
description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK med Adobe Target
seo-description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK med Adobe Target
translation-type: tm+mt
source-git-commit: 9d66e926ff86f23b3dea34f37d3bb16ba97eb0ef
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---


# Målöversikt

Adobe Experience Platform Web SDK kan leverera och återge personaliserade upplevelser som hanteras i Adobe Target till webbkanalen. Du kan använda en WYSIWYG-redigerare, som kallas [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), eller ett icke-visuellt gränssnitt, den [formulärbaserade Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), för att skapa, aktivera och leverera dina aktiviteter och personaliseringsupplevelser.

## Aktivera Adobe Target

Om du vill aktivera Target måste du göra följande:

1. Aktivera tokens för activity.id och experience.id-svar i målgränssnittet.

![target_response_token](../../solution-specific/target/assets/target_response_token.png)

1. Aktivera målet i [kantkonfigurationen](../../fundamentals/edge-configuration.md) med rätt klientkod.
1. Lägg till alternativet `renderDecisions` till dina händelser.

Om du vill kan du även:

* Lägg `decisionScopes` till dina händelser för att hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen).
* Lägg till det [fördolda fragmentet](../../solution-specific/target/flicker-management.md) om du bara vill dölja vissa delar av sidan.

## Använda Adobe Target VEC

Med SDK kan du använda VEC normalt med ett undantag: du behöver [VEC-hjälptillägget](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) installerat och aktivt.

## Återge VEC-aktiviteter automatiskt

AEP Web SDK kan automatiskt återge dina upplevelser som definierats via Adobe Target VEC på webben för dina användare. Skicka en händelse med `renderDecisions = true`:

```javascript
alloy
("event", 
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

Den formulärbaserade Experience Composer är ett icke-visuellt gränssnitt som är användbart för att konfigurera A/B-tester, Experience Targeting, Automated Personalization och Recommendations med olika svarstyper som JSON, HTML, Image, etc. Beroende på vilken svarstyp eller vilket beslut som Adobe Target returnerar kan din affärslogik användas. Om du vill hämta beslut för dina formulärbaserade dispositionsaktiviteter skickar du en händelse med alla&quot;beslutScopes&quot; som du vill ta emot ett beslut för.

```javascript
alloy
  ("event", { 
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

`decisionScopes` definierar avsnitt, platser eller delar av sidorna där du vill återge en personlig upplevelse. Dessa `decisionScopes` är anpassningsbara och användardefinierade. För nuvarande Target-kunder `decisionScopes` kallas även&quot;mboxes&quot;. I målgränssnittet visas `decisionScopes` det som&quot;platser&quot;.

## __visa__ omfång

AEP Web SDK innehåller en funktion där du kan hämta VEC-åtgärder utan att förlita dig på AEP Web SDK för att återge VEC-åtgärder åt dig. Skicka en händelse med `__view__` definierad som en `decisionScopes`.

```javascript
alloy("event", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Målgrupper i XDM

När du definierar målgrupper för målaktiviteter som ska levereras via AEP Web SDK måste [XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html) definieras och användas. När du har definierat XDM-scheman, klasser och blandningar kan du skapa en målgruppsregel som definieras av XDM-data för målinriktning. I Target visas XDM-data i Audience Builder som en anpassad parameter. XDM-filen serialiseras med punktnotation (till exempel `web.webPageDetails.name`).

Om du har Target-aktiviteter med fördefinierade målgrupper som använder anpassade parametrar eller en användarprofil bör du vara medveten om att de inte levereras korrekt via AEP Web SDK. I stället för att använda egna parametrar eller användarprofilen måste du använda XDM i stället. Det finns dock färdiga målgruppsfält som stöds via AEP Web SDK och som inte kräver XDM. Det här är de fält i målgränssnittet som inte kräver XDM:

* Målbibliotek
* Geo
* Nätverk
* Operativsystem
* Webbplatssidor
* Webbläsare
* Trafikkällor
* Tidsram

## Terminologi

__Beslut__ - I Target korrelerar dessa till den erfarenhet som väljs från en aktivitet.

__Tillämpningsområde__ - Beslutets tillämpningsområde. I Target är det här mBox. Den globala mBox är `__view__` omfånget.

__Schema__ - Schemat för ett beslut är typen av erbjudande i Target.

__XDM__ - XDM serialiseras till punktnotation och sätts sedan i Target som mBox-parametrar.
