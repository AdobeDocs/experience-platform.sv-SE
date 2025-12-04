---
title: container
description: Se hela taggbehållaren i ett enskilt objekt.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

Objektet `_satellite._container` innehåller den fullständiga konfigurationen och körningskontexten för taggegenskapen som lästs in på sidan. All information, som regler, dataelement, tillägg och miljöer, är tillgänglig i det här objektet. Dess huvudsakliga användning är att hjälpa till med felsökning av implementeringen så att du kan se exakt vilken logik som visas eller publiceras.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Det här objektet är endast till för felsökning. Koppla inte produktionslogik till det här objektet, referera det här objektet i implementeringen eller redigera värden i det här objektet. Tillgängligheten för egenskaper eller namn i det här objektet kan ändras av Adobe när som helst.

## Tillgängliga fält

Följande objekt är tillgängliga som referens:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

Objektet `_satellite._container.buildInfo` innehåller en kopia av [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

Objektet `_satellite._container.company` innehåller en kopia av [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

Objektet `_satellite._container.dataElements` tillhandahåller en referens för alla dataelement i taggegenskapen.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Varje dataelement innehåller följande egenskaper:

| Namn | Typ | Beskrivning |
|---|---|---|
| **`modulePath`** | `string` | Sökvägen till den JavaScript-fil som avgör logiken för den dataelementtypen. |
| **`settings`** | `Settings` | Dataelementets inställningar. Egenskaperna i det här objektet beror på dataelementtypen. |

## `environment`

Objektet `_satellite._container.environment` innehåller en kopia av [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

Objektet `_satellite._container.extensions` visar alla tillägg som publicerats till taggegenskapen.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Varje tillägg innehåller följande egenskaper:

| Namn | Typ | Beskrivning |
|---|---|---|
| **`displayName`** | `string` | Tilläggets egna namn. |
| **`hostedLibFilesUrl`** | `string` | Platsen på CDN där tillägget finns. |
| **`modules`** | `Modules` | JavaScript-logiken för alla händelser, åtgärder, villkor och dataelement som används i tillägget. Innehållet i det här objektet skiljer sig åt för varje tillägg. |

## `property`

Objektet `_satellite._container.property` innehåller information om taggegenskapen.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Namn | Typ | Beskrivning |
|---|---|---|
| **`id`** | `string` | Den unika identifieraren för taggegenskapen. |
| **`name`** | `string` | Eget namn för taggegenskapen. |
| **`settings`** | `PropertySettings` | Inställningar för egenskapen. Se tabellen nedan. |

| Inställningsnamn | Typ | Beskrivning |
|---|---|---|
| **`domains`** | `string[]` | De konfigurerade domänerna för egenskapen, enligt inställningen när [en taggegenskap](/help/tags/ui/administration/companies-and-properties.md) konfigureras. |
| **`ruleComponentSequencingEnabled`** | `boolean` | Avgör om kryssrutan **[!UICONTROL Run rule components in sequence]** är aktiverad när taggegenskapen konfigureras. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Avgör om kryssrutan **[!UICONTROL Return an empty string for undefined data elements]** är aktiverad när taggegenskapen konfigureras. |

## `_container.rules`

Objektarrayen `rules` innehåller en referens till alla regler i taggegenskapen.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Varje regel innehåller följande fält:

| Namn | Typ | Beskrivning |
|---|---|---|
| **`id`** | `string` | Regelns unika identifierare. |
| **`name`** | `string` | Regelns egna namn. |
| **`events`** | `Event[]` | En array med händelser som du har konfigurerat för att utlösa regeln. |
| **`conditions`** | `Condition[]` | En array med villkor som du har konfigurerat för att utlösa regeln. |
| **`actions`** | `Action[]` | En array med åtgärder som du har konfigurerat att köra när regeln aktiveras. |
