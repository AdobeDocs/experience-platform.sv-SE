---
title: API-guide för sandlådeverktyg
description: Med Sandbox Tooling i Adobe Experience Platform kan du exportera och importera en ögonblicksbild av sandlådekonfigurationer mellan sandlådor.
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!DNL Sandbox] guide för verktyg-API

The [!DNL Sandbox] I verktygs-API:t finns flera slutpunkter som gör att du kan exportera och importera ögonblicksbilder mellan sandlådor som är tillgängliga för dig i organisationen. Alla interaktioner sker via HTTP-slutpunkter. Källsandlådan kontrolleras för artefakter, som är objekten i ett paket, innan en ögonblicksbild exporteras. När en importbegäran görs, [!DNL Azure Blob] ögonblicksbild hämtas och används som mall för att skapa nästan liknande artefakter för målsandlådan. Se [sandlådeverktyg](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) dokumentation om en lista över objekt och begränsningar som stöds.

Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

## Paket {#packages}

Slutpunkten för verktygspaket i sandlådan gör att du kan hantera paket. Verktygspaketet för sandlådan är en samling artefaktdefinitioner, inklusive paket-ID, namn, beskrivning, org-ID och skapar-ID. Se [slutpunktsguide för paket](./packages.md) om du vill ha mer information om hur du arbetar med paket i API:t.

## Verktyg {#tools}

Med sandlådeverktygets slutpunkt kan du hämta JSON-data för jobbet oberoende av varandra. Se [slutpunktsguide för verktyg](./tools.md) om du vill ha mer information om hur du hämtar JSON-jobbdata i API:t.

## Nästa steg {#next-steps}

Läs mer om hur du börjar ringa anrop med verktygs-API:t för sandlådan i [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.
