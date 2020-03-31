---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 8 april 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 8 april 2020

## Åtkomstkontroll

Experience Platform utnyttjar [produktprofiler i Adobe Admin Console](https://adminconsole.adobe.com) för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

### Viktiga funktioner

| Funktion | Beskrivning |
|--- | ---|
| Behörigheter | På Admin Console kan du på fliken _Behörigheter_ i en plattformsproduktprofil anpassa vilka plattformsfunktioner som är tillgängliga för användare som är kopplade till den profilen. Tillgängliga behörighetskategorier är: Datamodellering, datahantering, profilhantering, identiteter, dataövervakning, sandlådeadministration, mål, källor. |
| Åtkomst till sandlådor | Fliken _Behörigheter_ i en plattformsproduktprofil kan ge användare åtkomst till specifika sandlådor. Mer information finns i avsnittet om [sandlådor](#sandboxes) nedan. |

Mer information finns i översikten över [åtkomstkontrollen](../../access-control/home.md).

## Sandlådor

Experience Platform har byggts för att berika applikationer för digitala upplevelser på en global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Viktiga funktioner

| Funktion | Beskrivning |
|--- | ---|
| Produktionssandlåda | Experience Platform har en enda produktionssandlåda som inte kan tas bort eller återställas. |
| Sandlådor utan produktion | Du kan skapa flera icke-produktionssandlådor för en enda plattformsinstans, så att du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. |
| Sandlådeväxlare | I Experience Platforms användargränssnitt kan du med sandlådeväxlaren i skärmens övre vänstra hörn växla mellan tillgängliga sandlådor via en nedrullningsbar meny. |
| `x-sandbox-name` header | Alla anrop till Experience Platform API:er måste nu inkludera den nya `x-sandbox-name` `name` rubriken, vars värde refererar till attributet för den sandlåda som åtgärden ska äga rum i. |

Mer information finns i Översikt över [sandlådor](../../sandboxes/home.md).