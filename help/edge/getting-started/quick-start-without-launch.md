---
title: Snabbstart med oformaterad javascript
seo-title: 'Adobe Experience Platform Web SDK - snabbstart '
description: Snabbstartsguide för användning av Experience Platform Web SDK för att samla in data
seo-description: Snabbstartsguide för användning av Experience Platform Web SDK för att samla in data
translation-type: tm+mt
source-git-commit: 7c5d4306f9964553cf48a208166fce265dcdd94d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Välkommen

Den här guiden leder dig igenom de olika sätten att konfigurera Adobe Experience Platform Web SDK. Om du vill använda den här funktionen måste du vara vitlistad. Om du vill komma med på väntelistan kontaktar du din CSM.

- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME for Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men du behöver en innan du går till produktion
- Du har rätt till Adobe Experience Platform Data Platform.  Om du inte har köpt Platform tillhandahåller vi dig Experience Platform Data Services Foundation för användning i begränsad omfattning med SDK utan extra kostnad.
- Använd den senaste versionen av tjänsten för besökar-ID

## Skapa ett konfigurations-ID

Du kan skapa ett konfigurations-ID med [Edge-konfigurationsverktyget](../fundamentals/edge-configuration.md) i Adobe Launch, även om du inte använder tagghanteringsfunktionerna. På så sätt kan du aktivera Edge Network för att skicka data till de olika lösningarna. Information om hur du hittar de olika alternativen finns på sidan [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Din organisation måste vitlistas för funktionen. Kontakta din CSM för att komma med i listan för eventuell vitlistning.

## Förbered ett schema

Experience Platform Edge Network tar data som XDM. XDM är ett dataformat som gör att du kan definiera scheman. Schemat definierar hur Edge Network förväntar sig att data ska formateras. Om du vill skicka data måste du definiera ditt schema.

- [Skapa ett schema](../../xdm/tutorials/create-schema-ui.md)
- Lägg till Adobe Experience Platform Web SDK-mixin i det schema du skapade

## Installera SDK

Om du vill installera SDK kopierar och klistrar du in följande &quot;baskod&quot; så hög som möjligt i HTML-taggen: `<head>`

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Mer information om olika alternativ för att göra detta finns i [Installera SDK](../fundamentals/installing-the-sdk.md).

## Konfigurera SDK

Ange sedan din konfiguration för SDK. Detta görs med `configure` kommandot . Det här bör vara det första kommandot som anropas på varje sida.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Här anger du det konfigurations-ID som du skapade ovan samt ditt företags-ID. Detta är de enda två obligatoriska fälten. Det finns dock många andra [konfigurationsalternativ](../fundamentals/configuring-the-sdk.md).

## Skicka en händelse

När du har anropat kommandot configure kan du börja spåra händelser.

```javascript
alloy("sendEvent", {});
```

Vanligtvis skickar du händelser med vissa data. Du kan skicka XDM-data på det här sättet. Data som du skickar måste finnas i det schema som du skapade i XDM.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Mer information om hur du spårar händelser finns i [Spåra händelser](../fundamentals/tracking-events.md).

## Nästa steg

När du har data som flödar kan du göra följande:

- [Skapa ditt schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Läs mer om felsökning](../fundamentals/debugging.md)
- Lär dig [personalisera upplevelsen](../fundamentals/rendering-personalization-content.md)
- Lär dig hur du skickar data till flera lösningar
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
