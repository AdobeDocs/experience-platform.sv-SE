---
keywords: Experience Platform;startsida;populära ämnen;handbok för utvecklare av sandlådor
solution: Experience Platform
title: API-guide för sandlådor
description: Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# [!DNL Sandbox] API-guide

The [!DNL Sandbox] API innehåller flera slutpunkter som gör att du kan hantera alla sandlådor som är tillgängliga för dig i organisationen programmatiskt. Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

Om du vill se alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Sandbox] API-referens](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Tillgängliga sandlådor

Med den tillgängliga sandlådeslutpunkten kan du visa en lista över alla tillgängliga sandlådor som är tillgängliga för den aktuella användaren, inklusive information om varje sandlådans namn, titel, läge, typ och region. Den tillgängliga sandlådeslutpunkten i [!DNL Sandbox] API kan nås av alla användare, även användare utan administratörsbehörighet för sandlådan. Se [slutpunktsguide för tillgängliga sandlådor](./available.md) om du vill lära dig hur du visar tillgängliga sandlådor i API:t.

## Sandlådehantering

En sandlåda är en virtuell partition i en enda instans av Adobe Experience Platform, som möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Du kan skapa, visa, redigera, återställa och ta bort produktions- och utvecklingssandlådor med `/sandboxes` slutpunkt. Om du vill lära dig hur du använder den här slutpunkten kan du läsa [slutpunktsguide för sandlådor](./sandboxes.md).

## Sandlådetyper

För närvarande är de sandlådetyper som stöds på Experience Platform produktions- och utvecklingssandlådor. En standardplattformslicens ger dig totalt fem sandlådor, som du kan klassificera som produktion eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor. Se [slutpunktsguide för sandlådetyper](./types.md) om du vill lära dig hur du visar vilka sandlådetyper som stöds för din organisation i API:t.

## Nästa steg

Börja ringa samtal med [!DNL Sandbox] API, läs [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.
