---
title: Konfigurera SDK
seo-title: Konfigurera Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar Experience Platform Web SDK
seo-description: Lär dig hur du konfigurerar Experience Platform Web SDK
keywords: configuring;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;environment;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehidingStyle;opacity;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 4%

---


# Konfigurera SDK

Konfigurationen för SDK görs med `configure` kommandot.

>[!IMPORTANT]
>
>`configure` ska *alltid* vara det första anropade kommandot.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Det finns många alternativ som kan anges under konfigurationen. Alla alternativ finns nedan, grupperade efter kategori.

## Allmänna alternativ

### `edgeConfigId`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Ditt tilldelade konfigurations-ID, som länkar SDK till rätt konton och konfiguration.  När du konfigurerar flera instanser på en sida måste du konfigurera olika inställningar `edgeConfigId` för varje instans.

### `context`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array med strängar | Nej | `["web", "device", "environment", "placeContext"]` |

Anger vilka sammanhangskategorier som ska samlas in automatiskt enligt beskrivningen i [Automatisk information](../data-collection/automatic-information.md).  Om den här konfigurationen inte anges används alla kategorier som standard.

### `debugEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `false` |

Anger om felsökning ska vara aktiverat. Om du ställer in den här konfigurationen på `true` aktiveras följande funktioner:

| **Funktion** | ** -funktion** |
| ---------------------- | ------------------ |
| Synkron validering | Validerar data som samlas in mot schemat och returnerar ett fel i svaret under följande etikett: `collect:error OR success` |
| Konsolloggning | Gör att felsökningsmeddelanden kan visas i webbläsarens JavaScript-konsol |

### `edgeDomain`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ------------------ |
| Sträng | Nej | `beta.adobedc.net` |

Domänen som används för att interagera med Adobe-tjänster. Detta används endast om du har en förstahandsdomän (CNAME) som proxies begär till infrastrukturen i Adobe edge.

### `orgId`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Ditt tilldelade [!DNL Experience Cloud] organisations-ID.  När du konfigurerar flera instanser på en sida måste du konfigurera olika inställningar `orgId` för varje instans.

## Datainsamling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Anger om data som är associerade med länkklick ska samlas in automatiskt. För klickningar som kvalificerar som länkklick samlas följande [webbinteraktionsdata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/webinteraction.schema.md) in:

| **Egenskap** | **Beskrivning** |
| ------------ | ----------------------------------- |
| Länknamn | Namnet bestäms av länkkontexten |
| Länk-URL | Normaliserad URL |
| Länktyp | Ange om du vill hämta, avsluta eller någon annan |

### `onBeforeEventSend`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
|  -funktion | Nej | () => odefinierad |

Ange detta för att konfigurera ett återanrop som anropas för varje händelse precis innan den skickas.  Ett objekt med fältet `xdm` skickas till återanropet.  Ändra objektet `xdm` om du vill ändra vad som skickas.  I återanropet skickas data från händelsekommandot och den automatiskt insamlade informationen till objektet. `xdm`  Mer information om tidpunkten för det här återanropet och ett exempel finns i [Ändra händelser globalt](tracking-events.md#modifying-events-globally).

## Sekretessalternativ

### `defaultConsent` {#default-consent}

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Objekt | Nej | `"in"` |

Anger användarens standardsamtycke. Detta används när det inte finns någon inställning för samtycke som redan har sparats för användaren. Det andra giltiga värdet är `"pending"`. När detta är inställt kommer arbetet att ställas i kö tills användaren ger sitt medgivande. När användarens inställningar har angetts fortsätter arbetet eller avbryts baserat på användarens inställningar. Mer information finns i [Supporting Consent](../consent/supporting-consent.md) .

## Anpassningsalternativ

### `prehidingStyle`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Nej | ingen |

Används för att skapa en CSS-formatdefinition som döljer innehållsområden på webbsidan när anpassat innehåll läses in från servern. Om det här alternativet inte anges försöker SDK inte dölja några innehållsområden när anpassat innehåll läses in, vilket kan leda till&quot;flimmer&quot;.

Om du t.ex. har ett element på webbsidan med ett ID `container` vars standardinnehåll du vill dölja när anpassat innehåll läses in från servern, blir ett exempel på ett fördolt format följande:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Målgruppsalternativ

### `cookieDestinationsEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Aktiverar destinationer för [!DNL Audience Manager] cookies, vilket gör det möjligt att ställa in cookies baserat på segmentkvalificering.

### `urlDestinationsEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Aktiverar [!DNL Audience Manager] URL-mål, vilket gör det möjligt att bränna URL:er baserat på segmentkvalificering.

## Identitetsalternativ

### `idMigrationEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | sant |

Om true läser SDK in gamla AMCV-cookies. Detta underlättar vid övergång till AEP Web SDK medan vissa delar av webbplatsen fortfarande använder Visitor.js. Om dessutom Visitor-API är definierat på sidan kommer SDK att efterfråga besökar-API:t för ECID. På så sätt kan du dubbeltagga sidor med AEP Web SDK och fortfarande ha samma ECID.

### `thirdPartyCookiesEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | sant |

Aktiverar inställningen av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Detta är användbart om du har flera webbplatser eller vill dela data med partners. Men ibland är detta inte önskvärt av sekretesskäl.
