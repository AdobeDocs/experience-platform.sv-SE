---
title: Kontext i Edge Extension Modules
description: Lär dig mer om kontextobjektet och den roll det spelar när det gäller att interagera med biblioteksmoduler i taggtillägg för kantegenskaper.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 1%

---

# Kontext i kanttilläggsmoduler

>[!NOTE]
>
> Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Alla biblioteksmoduler i edge-tillägg har en `context` när de körs. Det här dokumentet innehåller de egenskaper som finns i `context` objekt och den roll de spelar i biblioteksmoduler.

## Adobe Request Context (arc)

The `arc` -egenskapen är ett objekt som innehåller information om den händelse som utlöser regeln. Avsnitten nedan beskriver de olika underegenskaperna i objektet.

### [!DNL event]

The `event` -objektet representerar händelsen som utlöste regeln och innehåller följande värden:

```js
logger.log(context.arc.event);
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm` | Händelsens XDM-objekt. |
| `data` | Det anpassade datalagret. |

### [!DNL request]

inte blandas ihop med en begäran från klientenheten, `request` är ett något modifierat objekt som kommer från Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

The `request` objektet har två egenskaper på den översta nivån: `body` och `head`. The `body` egenskapen innehåller XDM-information (Experience Data Model) och kan inspekteras i Adobe Experience Platform Debugger när du navigerar till **[!UICONTROL Launch]** och väljer **[!UICONTROL Edge Trace]** -fliken.

### [!DNL ruleStash] {#rulestash}

`ruleStash` är ett objekt som samlar in alla resultat från åtgärdsmoduler.

```js
logger.log(context.arc.ruleStash);
```

Varje tillägg har ett eget namnutrymme. Om tillägget till exempel har namnet `send-beacon`, alla resultat från `send-beacon` åtgärder kommer att lagras på `ruleStash['send-beacon']` namnutrymme.

Namnutrymmet är unikt för varje tillägg och har värdet `undefined` i början.

Namnutrymmet åsidosätts av det returnerade resultatet från varje åtgärd. Ta till exempel en `transform` tillägg som innehåller två åtgärder: `generate-fullname` och `generate-fulladdress`. Dessa två åtgärder läggs sedan till i en regel.

Om resultatet av `generate-fullname` åtgärden är `Firstname Lastname`visas regelstrecket på följande sätt när åtgärden har slutförts:

```js
{
  transform: 'Firstname Lastname'
}
```

Om resultatet av `generate-address` åtgärden är `3900 Adobe Way`visas regelstrecket på följande sätt när åtgärden har slutförts:

```js
{
  transform: '3900 Adobe Way'
}
```

Observera att&quot;FirstName LastName&quot; inte längre finns i regelstrecket, eftersom `generate-address` funktionsmakrot åsidosätter det med ett nytt värde.

Om du vill `ruleStash` för att lagra resultaten från båda åtgärderna i `transform` namnutrymme kan du skriva din åtgärdsmodul som i följande exempel:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

Första gången den här åtgärden utförs, `ruleStash` börjar som `undefined` och initieras därför som ett tomt objekt. Nästa gång som åtgärden körs får den `ruleStash` som returnerades när åtgärden anropades tidigare. Använda ett objekt som `ruleStash` gör att du kan lägga till nya data utan att förlora data som tidigare angetts av andra åtgärder från vårt tillägg.

>[!NOTE]
>
>Var noga med att alltid returnera det fullständiga tillägget för regelstreck när du använder den här strategin. Om du bara returnerar ett värde skrivs alla andra egenskaper som du har angett över.

## Verktyg

The `utils` egenskapen representerar ett objekt som innehåller funktioner som är specifika för tagghanteringen.

### [!DNL logger]

The `logger` kan du logga meddelanden som ska visas under felsökningssessioner när du använder [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

Loggaren har följande metoder, där `message` är meddelandet som du vill logga:

| Metod | Beskrivning |
| --- | --- |
| `log(message)` | Loggar ett meddelande till konsolen. |
| `info(message)` | Loggar ett informationsmeddelande till konsolen. |
| `warn(message)` | Loggar ett varningsmeddelande till konsolen. |
| `error(message)` | Loggar ett felmeddelande till konsolen. |
| `debug(message)` | Loggar ett felsökningsmeddelande till konsolen. Detta visas bara när `verbose` loggning är aktiverat i webbläsarkonsolen. |

### [!DNL fetch]

Det här verktyget implementerar [Hämta API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). Du kan använda funktionen för att göra förfrågningar till slutpunkter från tredje part.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Det här verktyget returnerar ett objekt som innehåller information om hur det aktuella taggredigeringsbiblioteket byggs.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

Objektet innehåller följande värden:

| Egenskap | Beskrivning |
| --- | --- |
| `turbineVersion` | The [Turbin](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) version som används i det aktuella biblioteket. |
| `turbineBuildDate` | ISO 8601-datumet när versionen av [Turbin](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) som användes inuti behållaren skapades. |
| `buildDate` | ISO 8601-datumet när det aktuella biblioteket skapades. |
| `environment` | Den miljö som det här biblioteket skapades för. Möjliga värden är `development`, `staging`och `production.` |

Följande är ett exempel `getBuildInfo` objekt för att visa de värden som returneras:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Verktyget returnerar `settings` objekt som senast sparades från [tilläggskonfiguration](../configuration.md) vy.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Verktyget returnerar `settings` objekt som senast sparades från motsvarande biblioteksmodulvy.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Det här verktyget returnerar ett objekt som innehåller information om regeln som utlöser modulen.

```js
logger.log(context.utils.getRule());
```

Objektet kommer att innehålla följande värden:

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Regel-ID. |
| `name` | Regelnamnet. |
