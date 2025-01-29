---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;application;datatype;data type;data type;
solution: Experience Platform
title: Programdatatyp
description: Läs mer om datatypen XDM (Application Experience Data Model).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Datatypen [!UICONTROL Application]

[!UICONTROL Application] är en XDM-datatyp (Standard Experience Data Model) som beskriver detaljer som rör interaktioner som genereras av ett program. Ett program avser en programvaruupplevelse, till exempel ett mobil- eller datorprogram som kan installeras, köras, stängas eller avinstalleras av en slutanvändare. Egenskaperna för den här datatypen är inte avsedda att beskriva agenter som chattbottar, webbläsarbaserade plugin-program eller andra upplevelser som inte gäller för program.

![programbild](../images/data-types/application.PNG){width=500}

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
| `userPerspective` | Sträng | Perspektivet eller det fysiska förhållandet mellan användaren och appen eller varumärket när en händelse inträffade. Om du förstår användarens perspektiv i förhållande till appen blir det lättare att generera sessioner korrekt, eftersom större delen av tiden du inte vill inkludera `background`- och `detached`-händelser som en del av en&quot;aktiv&quot; session. Värdet för den här egenskapen måste vara lika med ett av de uppräkningsvärden som anges nedan. <li> `foreground`: Användaren och appen interagerar direkt med varandra. </li> <li> `background`: Programmet och användaren interagerar indirekt med varandra. Programmet kan till exempel mäta ett värde och uppdatera medan skärmen är låst eller när ett annat program används i förgrunden.  </li> <li> `detached`: Frånkopplad innebär att händelsen var relaterad till appen men inte kom direkt från appen, till exempel att ett e-postmeddelande eller ett push-meddelande skickades från ett externt system. |
| `version` | Sträng | Versionen av programmet. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
