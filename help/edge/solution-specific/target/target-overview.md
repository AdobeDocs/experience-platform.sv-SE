---
title: 'Adobe Target och Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK och Adobe Target
description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK med Adobe Target
seo-description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK med Adobe Target
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Målöversikt

Adobe Experience Platform Web SDK är integrerat med Adobe Target via den [personaliseringsfunktionen](../../fundamentals/rendering-personalization-content.md) och gör att ni enkelt kan leverera personaliserat innehåll och beslut.

## Aktivera Adobe Target

Om du vill aktivera Target måste du göra följande:

- Aktivera målet i [kantkonfigurationen](../../fundamentals/edge-configuration.md) med rätt klientkod.
- Lägg till alternativet `renderDecisions` till dina händelser.

Då kan du också:

- Lägg `scopes` till dina händelser för att hämta specifika aktiviteter (användbart för aktiviteter som skapats med den formulärbaserade dispositionen).
- Lägg till det [fördolda fragmentet](../../fundamentals/managing-flicker.md) så att endast vissa delar av sidan döljs.

## Använda VEC

Med SDK kan du använda VEC normalt med ett undantag. Du måste ha [måltillägget](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) för VEC-hjälpen installerat och aktiverat.

## Använda den formulärbaserade dispositionen

Den formulärbaserade dispositionen kan också användas för att returnera innehåll. Omfången visas som platser (mBoxes) i målgränssnittet. Du bör också se till att utvecklaren letar efter svaren om de bestämmer sig för att använda omfattningar.

## Målgrupper i XDM

I Target XDM visas data i Audience Builder som en anpassad parameter. XDM-filen serialiseras med punktnotation (t.ex. `web.webPageDetails.name`)

## Terminologi

__Besluten__ - I Target korrelerar de till den erfarenhet som väljs från en aktivitet.

__Tillämpningsområde__ - Beslutets tillämpningsområde. I Target är det här mBox. Den globala mBox är `__view__` omfånget.

__Schema__ - Schemat för ett beslut är typen av erbjudande i Target.

__XDM__ - XDM serialiseras till punktnotation och sätts sedan i Target som mBox-parametrar.