---
title: personalisering
description: Återge olika innehåll till olika användare och skapa en personlig upplevelse för dem.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

Objektet `personalization` konfigurerar vilka personaliseringsbeslut (erbjudanden eller förslag) som begärs och hur de hanteras i begäran och svaret. Det är särskilt värdefullt i Adobe Target- och Adobe Journey Optimizer-implementeringar, eftersom det är den pådrivande kraften som gör att du kan anpassa visuellt innehåll per användare.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

Objektet `personalization` innehåller följande egenskaper:

## `personalization.decisionScopes`

Egenskapen `decisionScopes` är en matris med strängar som instruerar Web SDK att hämta och returnera personaliseringsbeslut. Varje objekt i arrayen identifierar en plats, kontext eller logisk placering där personaliserat innehåll önskas.

Den här egenskapen är användbar när du uttryckligen vill hämta anpassat innehåll för specifika områden eller komponenter på en sida. Det är särskilt värdefullt i enkelsidiga program som kan kräva olika uppsättningar erbjudanden när användarens navigering eller vy ändras. Du kan också använda den här egenskapen för att optimera prestanda genom att bara hämta erbjudanden för de gränssnittselement som är relevanta för användaren.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

I Adobe Target mappas varje beslutsomfattning till en mbox eller aktivitet. I Adobe Journey Optimizer mappas varje beslutsomfång till beslutsbaserade webbplatser eller kampanjer. I Offer Decisioning mappas beslutsomfattningar till vilka erbjudanden eller erbjudanden som besökaren ska ta emot.

>[!TIP]
>
>Om du vill begära (eller blockera) det globala omfånget använder du [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) i stället för att ange det här i `decisionScopes`.

## `personalization.surfaces`

Egenskapen `surfaces` är en matris med [&#x200B; yt-URI](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri)-strängar som manuellt definierar kanalen, enheten eller kontexten som personalisering begärs från. De gör det möjligt för er att skilja mellan olika digitala upplevelser, som domäner, appar eller enhetsplattform i ert flerkanalssystem. Som standard ligger biblioteket under standardytan från den aktuella sidan. Du kan använda den här egenskapen för att åsidosätta den automatiskt härledda ytan för den aktuella sidan.

Den här egenskapen är värdefull när ni vill använda personalisering över flera kanaler och måste skilja på hur personalisering fungerar mellan olika kanaler. Det gör att ni kan skapa distinkta erbjudanden för olika webbplatser inom samma Adobe Experience Platform-organisation.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Den här egenskapen används till grunden med Adobe Journey Optimizer, eftersom den matchar ytor som skapats i Journey Optimizer-kampanjer och ythantering.

## `personalization.schemas`

Egenskapen `schemas` är en matris med URI-strängar för schema som filtrerar de typer av personaliseringsinnehåll som begärs från Edge Network. Om du ställer in den här egenskapen begränsas det svar du får från Adobe så att endast erbjudanden som matchar de innehållstypdefinitioner du anger tas med. Om det utelämnas begär biblioteket erbjudanden av alla tillgängliga scheman för de matchade områdena eller ytorna.

Den här egenskapen hjälper till att optimera svarsstorleken och ser till att din webbplats eller ditt program bara får erbjudandetyper som den kan hantera. Det är också användbart när det används med enkelsidiga program som återger anpassat innehåll på ett specifikt sätt (till exempel genom att endast använda DOM-åtgärder eller endast JSON-objekt).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Följande schema-URI:er stöds:

* **`https://ns.adobe.com/personalization/dom-action`**: Erbjudanden som är direkta DOM-åtgärder, som vanligtvis genereras av Visual Experience Composer i Adobe Target. De innehåller instruktioner för att automatiskt hantera element på sidan utan extra kod. Det är standarden för automatisk återgivning av webbpersonalisering.
* **`https://ns.adobe.com/personalization/html-content-item`**: Erbjudanden som innehåller obearbetat HTML levereras som en sträng. Implementeringen infogar vanligtvis det här innehållet på önskad plats på sidan, vilket ger dig större kontroll än DOM-åtgärder. Används vanligen för banners, fragment eller modalt innehåll.
* **`https://ns.adobe.com/personalization/json-content-item`**: Erbjudanden som är formaterade som ett JSON-objekt. Det vanligaste är API-baserade implementeringar eller gränssnitt där strukturerade data förväntas i stället för HTML- eller DOM-ändringar.
* **`https://ns.adobe.com/personalization/redirect-item`**: Erbjudanden som omdirigerar till en annan URL. Används för att ta användaren till en ny sida baserad på målgrupps- eller beslutslogik, till exempel landningssidor eller introduktionsflöden.
* **`https://ns.adobe.com/personalization/ruleset-item`**: Levererar ett block med affärslogik för att driva en regelmotor på klientsidan. Innehåller en versionshanteringsregeluppsättning som definierar logiska villkor och konsekvenser (om/sedan personaliseringslogik).
* **`https://ns.adobe.com/personalization/message/in-app`**: Erbjudanden som är särskilt formaterade för Adobe Journey Optimizer-meddelanden i appen, återges vanligtvis som modaler, banners, popup-fönster eller övertäckningar.
* **`https://ns.adobe.com/personalization/message/content-card`**: Erbjudanden som är särskilt formaterade för Adobe Journey Optimizer-innehållskort, utformade för beständiga feeds eller inkorg-feeds i webb- eller mobilappar.
* **`https://ns.adobe.com/personalization/message/native-alert`**: Erbjudanden som är särskilt formaterade för Adobe Journey Optimizer-systemspecifika aviseringar, vilket utlöser plattformsspecifika meddelandedialogrutor.
* **`https://ns.adobe.com/personalization/measurement`**: Används för att spåra klickningar och interaktioner i personaliserade erbjudanden. Innehåller inte innehåll som kan återges.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: Schema för att ändra en besökares händelsehistorik i lokal lagring. Används internt av SDK:er för att spåra vilka upplevelser som har levererats eller blockerats. Innehåller inte innehåll som kan återges.
* **`https://ns.adobe.com/personalization/default-content-item`**: Reservinnehåll eller standardinnehåll, vanligtvis när inget anpassat erbjudande är giltigt. Det ser till att icke-kvalificerade användare fortfarande får innehåll, vilket ger en enhetlig upplevelse.

## `personalization.sendDisplayEvent`

Egenskapen `sendDisplayEvent` är en boolesk egenskap som avgör om en händelse för visningsmeddelanden automatiskt skickas till Edge Network omedelbart efter att anpassat innehåll har återgetts på sidan. Om det utelämnas är standardvärdet `true`. Ange den här variabeln till `false` om du inte vill ange att anpassat innehåll har återgetts för visningsspårning.

Det vanligaste användningsfallet när du anger den här variabeln till `false` är när du planerar att skicka ett annat kommando någon annanstans i implementeringen som flaggar en visningshändelse. Vissa implementeringar har både intrycks- och Analytics-händelser. Den här egenskapen ger dig full kontroll över vilka `sendEvent`-kommandon som ökar intrycket.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>I tidigare versioner av Web SDK (version 2.12.0 och tidigare) används `sendDisplayNotifications` i stället.

## `personalization.includePendingDisplayNotifications`

Egenskapen `includePendingDisplayNotifications` är en boolesk egenskap som kontrollerar om väntande visningsmeddelanden paketeras i det aktuella `sendEvent`-anropet. Väntande visningsmeddelanden är visningar för anpassat innehåll som har återgetts men ännu inte rapporterats till Edge Network som en displayhändelse. Den här egenskapen är användbar när du använder enkelsidiga program, eftersom återgivning av anpassat innehåll och `sendEvent` anrop kan vara asynkrona för varandra.

Standardvärdet för egenskapen är `false`. Ange den här egenskapen till `true` om du vill gruppera och tömma väntande visningsmeddelanden så att deras visningar spelas in korrekt. Synkron implementering, till exempel traditionella webbplatser, behöver vanligtvis inte ange den här egenskapen.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

Egenskapen `defaultPersonalizationEnabled` är en boolesk egenskap som ger dig explicit kontroll över hur Web SDK begär standardområdet för sidomfattande anpassning (`__view__`) och ytan för det här `sendEvent`-kommandot. Som standard gäller att SDK på det första `sendEvent`-kommandot efter en sidinläsning erbjuder standardomfånget för sidövergripande anpassning och tillhörande ytor. Efterföljande `sendEvent`-kommandon begär inte standardanpassning. Du kan använda den här egenskapen för att åsidosätta det beteendet. Det är värdefullt i applikationsimplementationer på en sida där du kanske vill begära standardanpassning igen när användaren navigerar på webbplatsen. Du kan också använda den här egenskapen när du vill _endast_ skicka en visningshändelse utan att duplicera hämtning av erbjudanden.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Den här egenskapen använder följande logik beroende på hur den ställs in:

* **Inte angivet**: Begär standardanpassning när den ännu inte har begärts. Standardanpassning begärs vanligtvis den första `sendEvent` efter sidinläsning och efterfrågas inte igen vid efterföljande `sendEvent` anrop på samma sida. Om du anger den här egenskapen åsidosätts det här beteendet.
* **`true`**: Begär sidomfånget och standardytan explicit, även om det här `sendEvent`-kommandot inte är det första efter att sidan har lästs in. Det är lämpligt att ange den här egenskapen till `true` när du behöver framtvinga en standardbegäran om anpassning, som i enkelsidiga programscenarier.
* **`false`**: Undertrycker uttryckligen begäran för sidomfånget och standardytan, även om det här `sendEvent`-kommandot är det första efter en sidinläsning. Det är en idealisk tidpunkt att ange den här egenskapen till `false` när du vill att ett givet `sendEvent`-kommando inte ska begära nya erbjudanden, utan bara skicka data till Analytics eller skicka en visningshändelse.

## Personalization-komponenter med taggtillägget Web SDK

SDK-taggtillägget för webben för den här egenskapen är avsnittet [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) när en [!UICONTROL Send event]-åtgärd konfigureras.
