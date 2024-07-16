---
title: API-guide för sandlådeverktyg
description: Med Sandbox Tooling i Adobe Experience Platform kan du exportera och importera en ögonblicksbild av sandlådekonfigurationer mellan sandlådor.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# API-guide för [!DNL Sandbox]

Verktygs-API:t [!DNL Sandbox] innehåller flera slutpunkter som gör att du kan exportera och importera ögonblicksbilder mellan sandlådor som är tillgängliga för dig i din organisation. Alla interaktioner sker via HTTP-slutpunkter. Källsandlådan kontrolleras för artefakter, som är objekten i ett paket, innan en ögonblicksbild exporteras. När en importbegäran görs hämtas en [!DNL Azure Blob]-ögonblicksbild och används som mall för att skapa nästan liknande artefakter för målsandlådan. I dokumentationen för [sandlådeverktyget](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) finns en lista över objekt och begränsningar som stöds.

Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

## Paket {#packages}

Slutpunkten för verktygspaket i sandlådan gör att du kan hantera paket. Verktygspaketet för sandlådan är en samling artefaktdefinitioner, inklusive paket-ID, namn, beskrivning, org-ID och skapar-ID. Mer information om hur du arbetar med paket i API finns i [paketslutpunktshandboken](./packages.md).

## Verktyg {#tools}

Med sandlådeverktygets slutpunkt kan du hämta JSON-data för jobbet oberoende av varandra. Mer information om hur du hämtar JSON-jobbdata i API:t finns i [verktygets slutpunktshandbok](./tools.md) .

## Nästa steg {#next-steps}

Om du vill börja ringa anrop med sandlådans verktyg-API läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
