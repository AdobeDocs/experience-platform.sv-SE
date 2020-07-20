---
title: Konfigurera SDK
seo-title: Konfigurera Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar Experience Platform Web SDK
seo-description: Lär dig hur du konfigurerar Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '733'
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

Anger vilka sammanhangskategorier som ska samlas in automatiskt enligt beskrivningen i [Automatisk information](../reference/automatic-information.md).  Om den här konfigurationen inte anges används alla kategorier som standard.

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

Den domän som används för att interagera med Adobes tjänster. Detta används endast om du har en förstahandsdomän (CNAME) som proxies-begäranden till Adobe Edge-infrastrukturen.

### `orgId`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Ditt tilldelade [!DNL Experience Cloud] organisations-ID.  När du konfigurerar flera instanser på en sida måste du konfigurera olika inställningar `orgId` för varje instans.

## Datainsamling

### `clickCollectionEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Anger om data som är associerade med länkklick ska samlas in automatiskt. För klickningar som kvalificerar som länkklick samlas följande [webbinteraktionsdata](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) in:

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

### `defaultConsent`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Objekt | Nej | `{"general": "in"}` |

Anger användarens standardsamtycke. Detta används när det inte finns någon inställning för samtycke som redan har sparats för användaren. Det andra giltiga värdet är `{"general": "pending"}`. När detta är inställt kommer arbetet att ställas i kö tills användaren ger sitt medgivande. När användarens inställningar har angetts fortsätter arbetet eller avbryts baserat på användarens inställningar. Mer information finns i [Supporting Consent](supporting-consent.md) .

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

Aktiverar [!DNL Audience Manager] , [!UICONTROL cookie destinations]vilket möjliggör inställning av cookies baserat på segmentkvalificering.

### `urlDestinationsEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Aktiverar [!DNL Audience Manager] , [!UICONTROL URL destinations]vilket gör det möjligt att bränna URL:er baserat på segmentkvalificering.

## Identitetsalternativ

### `idSyncContainerId`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Siffra | Nej | ingen |

Behållar-ID som anger vilket ID-synk som utlöses. Det här är ett icke-negativt heltal som du kan få från din konsult.

### `idSyncEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | `true` |

Aktiverar synkroniseringsfunktionen för ID, som gör det möjligt att aktivera URL:er för att synkronisera det unika användar-ID:t från Adobe med det unika användar-ID:t för en datakälla från tredje part.

### `thirdPartyCookiesEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | Nej | sant |

Aktiverar inställning av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Detta är användbart om du har flera webbplatser eller vill dela data med partners. Men ibland är detta inte önskvärt av sekretesskäl.
