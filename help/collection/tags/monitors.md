---
title: bildskärmar
description: Lägg till händelseavlyssnare för att felsöka taggimplementeringen.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# `_monitors`

Med objektet `_satellite._monitors` kan du skapa händelseavlyssnare och köra anpassad kod när biblioteket identifierar en utlöst regel. Dess huvudsakliga användning är att hjälpa till med felsökning av implementeringen för att säkerställa att reglerna utlöses korrekt.

>[!IMPORTANT]
>
>Det här objektet är endast till för felsökning. Koppla inte produktionslogik till det här objektet. Tillgängligheten för egenskaper eller namn i det här objektet kan ändras av Adobe när som helst.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

Du kan lyssna efter följande händelsetyper:

## `ruleTriggered`

Den här återanropsfunktionen aktiveras när en händelse utlöser en regel innan regelns villkor och åtgärder har bearbetats. Om den här funktionen utlöses, utlöses antingen `ruleCompleted` eller `ruleConditionFailed` kort efter (ömsesidigt uteslutande).

## `ruleCompleted`

Callback-funktionen `ruleCompleted` utlöses efter `ruleTriggered` när regelns villkorskriterier lyckas och alla regelåtgärder körs.

## `ruleConditionFailed`

Callback-funktionen `ruleConditionFailed` utlöses efter `ruleTriggered` när minst ett av regelns villkor misslyckas.

## `Rule` objekt

Varje återanropsfunktion visar ett `Rule`-objekt som ger information om själva regeln.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Namn | Typ | Beskrivning |
|---|---|---|
| **`id`** | `string` | Regelns unika identifierare. |
| **`name`** | `string` | Regelns egna namn. |
| **`events`** | `Event[]` | En array med händelser som du har konfigurerat för att utlösa regeln. |
| **`conditions`** | `Condition[]` | En array med villkor som du har konfigurerat för att utlösa regeln. |
| **`actions`** | `Action[]` | En array med åtgärder som du har konfigurerat att köra när regeln aktiveras. |

## Exempel

Lägg till följande kodfragment i din HTML i taggen `<head>` innan du anropar taggbiblioteksinläsaren:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Eftersom taggbiblioteket ännu inte har lästs in på sidan, skapas det ursprungliga `_satellite`-objektet och en matris på `_satellite._monitors` initieras. Skriptet lägger sedan till ett övervakarobjekt i den arrayen.

Tänk på följande när du använder bildskärmar:

* Observera att dessa felsökningsmeddelanden använder `console.log` i stället för [`_satellite.logger`](logger.md) eftersom krokarna skapas innan taggbiblioteket läses in.
* Även om kodexemplet innehåller alla tre callback-funktionerna är de inte obligatoriska fält. Du kan bara inkludera de önskade böckerna när du felsöker regler på webbplatsen.
* Flera bildskärmar tillåts, även för samma händelser. Om du använder flera bildskärmar för en enda händelse, garanteras inte samtalsordern.
* Se till att du skapar `_monitors` _innan_ läser in taggbiblioteket. Om du skapar de här krokarna när biblioteket har lästs in fångas bara de regler som utlöser från den punkten framåt.
