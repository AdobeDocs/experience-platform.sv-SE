---
title: miljö
description: Den byggmiljö som taggegenskapen använder för närvarande.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 4%

---

# `environment`

Objektet `_satellite.environment` anger vilken byggmiljö som taggegenskapen använder för närvarande.

```js
readonly _satellite.environment: Environment
```

## Tillgängliga fält

Följande fält är tillgängliga när det här objektet anropas.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Namn | Typ | Beskrivning |
|---|---|---|
| **`id`** | `string` | Unik identifierare för miljön. Du kan hitta miljö-ID:t genom att välja ikonen **[!UICONTROL Install]** under [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) i tagggränssnittet. |
| **`stage`** | `development \| staging \| production` | Miljötypen. |
