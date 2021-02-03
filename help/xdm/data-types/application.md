---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;application;datatype;data type;data type;
solution: Experience Platform
title: Programdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM (Application Experience Data Model).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---


# [!UICONTROL Application] datatyp

[!UICONTROL Application] är en XDM-datatyp (Standard Experience Data Model) som beskriver detaljer som rör de programgenererade interaktionerna. Ett program avser en programvaruupplevelse, till exempel ett mobil- eller datorprogram som kan installeras, köras, stängas eller avinstalleras av en slutanvändare. Egenskaperna för den här datatypen är inte avsedda att beskriva agenter som chattbottar, webbläsarbaserade plugin-program eller andra upplevelser som inte gäller för program.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Measure]](./measure.md) | Beskriver information om när ett program avslutas. |
| `crashes` | [[!UICONTROL Measure]](./measure.md) | Den här egenskapen utlöses när programmet inte avslutas som det ska. |
| `featureUsages` | [[!UICONTROL Measure]](./measure.md) | Beskriver alla data från aktiveringen av en programfunktion som mäts. |
| `firstLaunches` | [[!UICONTROL Measure]](./measure.md) | Innehåller data vid första starten. Den här egenskapen aktiveras vid första starten efter en installation. |
| `installs` | [[!UICONTROL Measure]](./measure.md) | Registrerar installationen av ett program på en enhet när en specifik installationshändelse är tillgänglig. |
| `launches` | [[!UICONTROL Measure]](./measure.md) | Beskriver ett värde som är associerat med programstarten. Detta aktiveras för varje körning, inklusive krascher, installationer och återanvändning från bakgrunden när sessionens tidsgräns har överskridits. |
| `upgrades` | [[!UICONTROL Measure]](./measure.md) | Innehåller data om uppgraderingen av ett program som tidigare har installerats. Detta aktiveras första gången programmet startas efter en uppgradering. |
| `id` | Sträng | En unik identifierare för programmet. |
| `name` | Sträng | Programmets namn. |
| `userPerspective` | Sträng | Perspektivet eller det fysiska förhållandet mellan användaren och appen eller varumärket när en händelse inträffade. Om du förstår användarens perspektiv i förhållande till programmet blir det lättare att generera sessioner korrekt, eftersom större delen av tiden du inte vill ta med `background`- och `detached`-händelser som en del av en&quot;aktiv&quot; session. Värdet för den här egenskapen måste vara lika med ett av de uppräkningsvärden som anges nedan. <li> `foreground`: Användaren och appen interagerar direkt med varandra. </li> <li> `background`: Programmet och användaren interagerar indirekt med varandra. Programmet kan till exempel mäta ett värde och uppdatera medan skärmen är låst eller när ett annat program används i förgrunden.  </li> <li> `detached`: Frånkopplad innebär att händelsen var relaterad till appen men inte kom direkt från appen, till exempel genom att ett e-postmeddelande eller ett push-meddelande skickades från ett externt system. |
| `version` | Sträng | Versionen av programmet. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)