---
title: Konfigurera Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar Adobe Experience Platform Web SDK.
seo-description: Lär dig hur du konfigurerar Experience Platform Web SDK
keywords: konfigurera;konfiguration;SDK;edge;Web SDK;konfigurera;edgeConfigId;context;web;device;environment;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;urlDestal inationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4b04f02a7a8843e667ea05b000bc93ebb065babd
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 3%

---

# Konfigurera Platform Web SDK

Konfigurationen för SDK görs med kommandot `configure`.

>[!IMPORTANT]
>
>`configure` är  ** alltid det första anropade kommandot.

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
| Sträng | Ja | Ingen |

{style=&quot;table-layout:auto&quot;}

Ditt tilldelade konfigurations-ID, som länkar SDK till rätt konton och konfiguration. När du konfigurerar flera instanser på en sida måste du konfigurera olika `edgeConfigId` för varje instans.

### `context`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array med strängar | Nej | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Anger vilka sammanhangskategorier som ska samlas in automatiskt enligt beskrivningen i [Automatisk information](../data-collection/automatic-information.md). Om den här konfigurationen inte anges används alla kategorier som standard.

### `debugEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `false` |

{style=&quot;table-layout:auto&quot;}

Anger om felsökning är aktiverat. Om du ställer in den här konfigurationen på `true` aktiveras följande funktioner:

| **Funktion** | ** -funktion** |
| ---------------------- | ------------------ |
| Synkron validering | Validerar data som samlas in mot schemat och returnerar ett fel i svaret under följande etikett: `collect:error OR success` |
| Konsolloggning | Gör att felsökningsmeddelanden kan visas i webbläsarens JavaScript-konsol |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Fyll i det här fältet med din förstahandsdomän. Mer information finns i [dokumentationen](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

Domänen liknar `data.{customerdomain.com}` för en webbplats på www.{customerdomain.com}.

### `orgId`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | Ingen |

{style=&quot;table-layout:auto&quot;}

Ditt [!DNL Experience Cloud]-organisations-ID. När du konfigurerar flera instanser på en sida måste du konfigurera olika `orgId` för varje instans.

## Datainsamling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style=&quot;table-layout:auto&quot;}

Anger om data som är associerade med länkklick samlas in automatiskt. Mer information finns i [Automatisk länkspårning](../data-collection/track-links.md#automaticLinkTracking). Länkarna kallas också för nedladdningslänkar om de innehåller ett nedladdningsattribut eller om länken avslutas med ett filtillägg. Hämtningslänkkvalificerare kan konfigureras med ett reguljärt uttryck. Standardvärdet är `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
|  -funktion | Nej | () => odefinierad |

{style=&quot;table-layout:auto&quot;}

Konfigurera ett återanrop som anropas för varje händelse precis innan den skickas. Ett objekt med fältet `xdm` skickas till återanropet. Ändra objektet `xdm` om du vill ändra vad som skickas. I återanropet har `xdm`-objektet redan de data som skickas i händelsekommandot och den automatiskt insamlade informationen. Mer information om tidpunkten för det här återanropet och ett exempel finns i [Ändra händelser globalt](tracking-events.md#modifying-events-globally).

## Sekretessalternativ

### `defaultConsent` {#default-consent}

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Objekt | Nej | `"in"` |

{style=&quot;table-layout:auto&quot;}

Anger användarens standardsamtycke. Använd den här inställningen när ingen inställning för samtycke redan har sparats för användaren. Övriga giltiga värden är `"pending"` och `"out"`. Det här standardvärdet sparas inte i användarens profil. Användarprofilen uppdateras bara när `setConsent` anropas.
* `"in"`: När den här inställningen är inställd eller inget värde anges fortsätter arbetet utan användarens samtycke.
* `"pending"`: När den här inställningen är angiven står arbetet i kö tills användaren ger sitt medgivande.
* `"out"`: När den här inställningen är angiven ignoreras arbetet tills användaren ger sitt medgivande.
När användarens inställningar har angetts fortsätter arbetet eller avbryts baserat på användarens inställningar. Mer information finns i [Supporting Consent](../consent/supporting-consent.md).

## Anpassningsalternativ

### `prehidingStyle`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Nej | Ingen |

{style=&quot;table-layout:auto&quot;}

Används för att skapa en CSS-formatdefinition som döljer innehållsområden på webbsidan när anpassat innehåll läses in från servern. Om det här alternativet inte anges försöker SDK inte dölja några innehållsområden när anpassat innehåll läses in, vilket kan leda till&quot;flimmer&quot;.

Om ett element på webbsidan till exempel har ID:t `container`, vars standardinnehåll du vill dölja när anpassat innehåll läses in från servern, använder du följande fördolda format:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Målgruppsalternativ

### `cookieDestinationsEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiverar [!DNL Audience Manager] cookie-mål, vilket gör det möjligt att ställa in cookies baserat på segmentkvalificering.

### `urlDestinationsEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiverar URL-mål för [!DNL Audience Manager], vilket gör det möjligt att bränna URL:er baserat på segmentkvalificering.

## Identitetsalternativ

### `idMigrationEnabled` {#id-migration-enabled}

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style=&quot;table-layout:auto&quot;}

Om true läser SDK in gamla AMCV-cookies. Med det här alternativet kan du gå över till Adobe Experience Platform Web SDK medan Visitor.js fortfarande används i vissa delar av webbplatsen. Om Visitor API är definierat på sidan frågar SDK om Visitor API för ECID. Med det här alternativet kan du dubbeltagga sidor med Adobe Experience Platform Web SDK och fortfarande ha samma ECID.

### `thirdPartyCookiesEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style=&quot;table-layout:auto&quot;}

Aktiverar inställningen av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Använd det här alternativet om du har flera webbplatser eller om du vill dela data med partners. Men ibland är det här alternativet inte önskvärt av sekretesskäl.
