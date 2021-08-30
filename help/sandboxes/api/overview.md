---
keywords: Experience Platform;hem;populära ämnen;handbok för sandlådeutvecklare
solution: Experience Platform
title: API-guide för sandlådor
topic-legacy: developer guide
description: Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Sandbox] API-guide

API:t [!DNL Sandbox] innehåller flera slutpunkter som gör att du kan hantera alla sandlådor som är tillgängliga för dig i din IMS-organisation programmatiskt. Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guiden](./getting-started.md) finns viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Sandbox] API-referensen](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Tillgängliga sandlådor

Med den tillgängliga sandlådeslutpunkten kan du visa en lista över alla tillgängliga sandlådor som är tillgängliga för den aktuella användaren, inklusive information om varje sandlådans namn, titel, läge, typ och region. De tillgängliga sandlådeslutpunkterna i [!DNL Sandbox]-API:t kan nås av alla användare, inklusive de som saknar åtkomstbehörigheter för sandlådeadministration. Se [slutpunktshandboken för tillgängliga sandlådor](./available.md) för att lära dig hur du visar tillgängliga sandlådor i API:t.

## Sandlådehantering

En sandlåda är en virtuell partition i en enda instans av Adobe Experience Platform, som möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Du kan skapa, visa, redigera, återställa och ta bort produktions- och utvecklingssandlådor med `/sandboxes`-slutpunkten. Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för sandlådor](./sandboxes.md).

## Sandlådetyper

För närvarande är de sandlådetyper som stöds på Experience Platform produktions- och utvecklingssandlådor. En standardplattformslicens ger dig totalt fem sandlådor, som du kan klassificera som produktion eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor. Se [slutpunktshandboken för sandlådetyper](./types.md) för att lära dig hur du visar vilka sandlådetyper som stöds för din organisation i API.

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Sandbox] läser du [Komma igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.