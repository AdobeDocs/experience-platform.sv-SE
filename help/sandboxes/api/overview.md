---
keywords: Experience Platform;home;populära topics;sandbox developguide
solution: Experience Platform
title: API-guide för sandlådor
description: Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# API-guide för [!DNL Sandbox]

API:t [!DNL Sandbox] innehåller flera slutpunkter som gör att du kan hantera alla sandlådor som är tillgängliga för dig i din organisation programmatiskt. Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Sandbox] API-referensen](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Tillgängliga sandlådor

Med den tillgängliga sandlådeslutpunkten kan du visa en lista över alla tillgängliga sandlådor som är tillgängliga för den aktuella användaren, inklusive information om varje sandlådans namn, titel, läge, typ och region. De tillgängliga sandlådeslutpunkterna i API:t [!DNL Sandbox] kan nås av alla användare, inklusive de som saknar åtkomstbehörigheter för sandlådeadministration. Läs [slutpunktshandboken för tillgängliga sandlådor](./available.md) om du vill veta mer om hur du visar tillgängliga sandlådor i API:t.

## Sandlådehantering

En sandlåda är en virtuell partition i en enda instans av Adobe Experience Platform, som möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Du kan skapa, visa, redigera, återställa och ta bort produktions- och utvecklingssandlådor med slutpunkten `/sandboxes`. Mer information om hur du använder den här slutpunkten finns i [stödlinjen för sandlådor](./sandboxes.md).

## Sandlådetyper

För närvarande är de sandlådetyper som stöds i Experience Platform produktions- och utvecklingssandlådor. En Experience Platform-standardlicens ger dig totalt fem sandlådor, som du kan klassificera som produktion eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor. Läs [slutpunktshandboken för sandlådetyper](./types.md) om du vill veta mer om hur du visar vilka sandlådetyper som stöds för din organisation i API:t.

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Sandbox] läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
