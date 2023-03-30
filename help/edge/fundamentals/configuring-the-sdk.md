---
title: Konfigurera Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar Adobe Experience Platform Web SDK.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: konfigurera;konfiguration;SDK;edge;Web SDK;konfigurera;edgeConfigId;context;web;device;environment;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;urlDestal inationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 3%

---

# Konfigurera Platform Web SDK

Konfigurationen för SDK görs med `configure` -kommando.

>[!IMPORTANT]
>
>`configure` är *alltid* det första kommandot anropades.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Det finns många alternativ som kan anges under konfigurationen. Alla alternativ finns nedan, grupperade efter kategori.

## Allmänna alternativ

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations har omprofilerats till Datastreams. Ett datastream-ID är samma som ett konfigurations-ID.**

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Sträng | Ja | Ingen |

{style="table-layout:auto"}

Ditt tilldelade konfigurations-ID, som länkar SDK till rätt konton och konfiguration. När du konfigurerar flera instanser på en sida måste du konfigurera ett `edgeConfigId` för varje instans.

### `context` {#context}

| **Typ** | Obligatoriskt | **Standardvärde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array med strängar | Nej | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Anger vilka sammanhangskategorier som ska samlas in automatiskt enligt beskrivningen i [Automatisk information](../data-collection/automatic-information.md). Om den här konfigurationen inte anges används alla kategorier som standard.

>[!IMPORTANT]
>
>Alla kontextegenskaper, med undantag för `highEntropyUserAgentHints`, är aktiverade som standard. Om du har angett kontextegenskaper manuellt i Web SDK-konfigurationen måste du aktivera alla kontextegenskaper för att kunna fortsätta samla in den information som behövs.

Aktivera [hög entropi-klienttips](user-agent-client-hints.md#enabling-high-entropy-client-hints) i Web SDK-distributionen måste du lägga till `highEntropyUserAgentHints` kontextalternativ, tillsammans med befintlig konfiguration.

Om du till exempel vill hämta klienttips för hög entropi från webbegenskaper ser konfigurationen ut så här:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `false` |

{style="table-layout:auto"}

Anger om felsökning är aktiverat. Konfigurationen anges till `true` har följande funktioner:

| **Funktion** | ** -funktion** |
| ---------------------- | ------------------ |
| Konsolloggning | Gör att felsökningsmeddelanden kan visas i webbläsarens JavaScript-konsol |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Fyll i det här fältet med din förstahandsdomän. Mer information finns i [dokumentation](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

Domänen liknar `data.{customerdomain.com}` på www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Sökväg efter den edgeDomain som används för att kommunicera och interagera med Adobes tjänster.  Detta ändras ofta bara om du inte använder standardproduktionsmiljön.

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Sträng | Nej | ee |

{style="table-layout:auto"}

### `orgId`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Sträng | Ja | Ingen |

{style="table-layout:auto"}

Ditt uppdrag [!DNL Experience Cloud] organisations-ID. När du konfigurerar flera instanser på en sida måste du konfigurera en annan `orgId` för varje instans.

## Datainsamling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style="table-layout:auto"}

Anger om data som är associerade med länkklick samlas in automatiskt. Se [Automatisk länkspårning](../data-collection/track-links.md#automaticLinkTracking) för mer information. Länkarna kallas också för nedladdningslänkar om de innehåller ett nedladdningsattribut eller om länken avslutas med ett filtillägg. Hämtningslänkkvalificerare kan konfigureras med ett reguljärt uttryck. Standardvärdet är `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
|  -funktion | Nej | () => odefinierad |

{style="table-layout:auto"}

Konfigurera ett återanrop som anropas för varje händelse precis innan den skickas. Ett objekt med fältet `xdm` skickas in till återanropet. Om du vill ändra vad som skickas ändrar du `xdm` -objekt. Inuti återanropet finns `xdm` -objektet har redan data som skickas i händelsekommandot och den automatiskt insamlade informationen. Mer information om tidpunkten för det här återanropet och ett exempel finns i [Ändra händelser globalt](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
|  -funktion | Nej | () => odefinierad |

{style="table-layout:auto"}

Konfigurera ett återanrop som anropas för varje länkklickningshändelse precis innan det skickas. Callback-funktionen skickar ett objekt med `xdm`, `clickedElement`och `data` fält.

När du filtrerar länkspårningen med hjälp av DOM-elementstrukturen kan du använda `clickElement` -kommando. `clickedElement` är DOM-elementnoden som du klickade på och som har kapslat in det överordnade nodträdet.

Om du vill ändra vilka data som skickas ändrar du `xdm` och/eller `data` objekt. Inuti återanropet finns `xdm` -objektet har redan data som skickas i händelsekommandot och den automatiskt insamlade informationen.

* Alla andra värden än `false` gör att händelsen kan bearbetas och att återanropet kan skickas.
* Om återanropet returnerar `false` värde, händelsebearbetning stoppas, utan fel och händelsen skickas inte. Den här funktionen gör att vissa händelser kan filtreras bort genom att händelsedata undersöks och returneras `false` om händelsen inte ska skickas.
* Om återanropet genererar ett undantag stoppas bearbetningen för händelsen och händelsen skickas inte.


## Sekretessalternativ

### `defaultConsent` {#default-consent}

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Objekt | Nej | `"in"` |

{style="table-layout:auto"}

Anger användarens standardsamtycke. Använd den här inställningen när ingen inställning för samtycke redan har sparats för användaren. De andra giltiga värdena är `"pending"` och `"out"`. Det här standardvärdet sparas inte i användarens profil. Användarprofilen uppdateras bara när `setConsent` anropas.
* `"in"`: När den här inställningen är inställd eller inget värde anges fortsätter arbetet utan användarens samtycke.
* `"pending"`: När den här inställningen är angiven står arbetet i kö tills användaren ger sitt medgivande.
* `"out"`: När den här inställningen är angiven ignoreras arbetet tills användaren ger sitt medgivande.
När användarens inställningar har angetts fortsätter arbetet eller avbryts baserat på användarens inställningar. Se [Stöd för samtycke](../consent/supporting-consent.md) för mer information.

## Anpassningsalternativ {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Sträng | Nej | Ingen |

{style="table-layout:auto"}

Används för att skapa en CSS-formatdefinition som döljer innehållsområden på webbsidan när anpassat innehåll läses in från servern. Om det här alternativet inte anges försöker SDK inte dölja några innehållsområden när anpassat innehåll läses in, vilket kan leda till&quot;flimmer&quot;.

Om ett element på webbsidan till exempel har ID:t `container`, vars standardinnehåll du vill dölja när anpassat innehåll läses in från servern, använder följande fördolda format:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Det här alternativet bör användas när du migrerar enskilda sidor från [!DNL at.js] till Web SDK.

Använd det här alternativet om du vill att Web SDK ska kunna läsa och skriva det äldre `mbox` och `mboxEdgeCluster` cookies som används av [!DNL at.js]. Detta hjälper dig att behålla besökarprofilen när du flyttar från en sida där Web SDK används till en sida där [!DNL at.js] bibliotek och vice versa.

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `false` |

## Målgruppsalternativ

### `cookieDestinationsEnabled`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style="table-layout:auto"}

Aktiverar [!DNL Audience Manager] cookie-destinationer, som gör det möjligt att ställa in cookies baserat på segmentkvalificering.

### `urlDestinationsEnabled`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style="table-layout:auto"}

Aktiverar [!DNL Audience Manager] URL-destinationer, som gör det möjligt att bränna URL:er baserat på segmentkvalificering.

## Identitetsalternativ

### `idMigrationEnabled` {#id-migration-enabled}

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style="table-layout:auto"}

Om true läser SDK in gamla AMCV-cookies. Med det här alternativet kan du gå över till Adobe Experience Platform Web SDK medan Visitor.js fortfarande används i vissa delar av webbplatsen.

Om Visitor API är definierat på sidan frågar SDK om Visitor API för ECID. Med det här alternativet kan du dubbeltagga sidor med Adobe Experience Platform Web SDK och fortfarande ha samma ECID.

### `thirdPartyCookiesEnabled`

| Typ | Obligatoriskt | Standardvärde |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

{style="table-layout:auto"}

Aktiverar inställningen av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Använd det här alternativet om du har flera webbplatser eller om du vill dela data med partners. Men ibland är det här alternativet inte önskvärt av sekretesskäl.
