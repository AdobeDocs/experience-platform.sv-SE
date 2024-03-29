---
title: Skicka snabbare frågor
description: En introduktion till API:t för accelererade frågor.
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
source-git-commit: fbb627787580c6a4ffd1deb0009105f1ba821b6f
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Skicka accelererade frågor

Som en del av Data Distiller SKU [API för frågetjänst](https://developer.adobe.com/experience-platform-apis/references/query-service/) gör att du kan ställa tillståndslösa frågor till det accelererade arkivet. The [slutpunkt för accelererade frågor](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) returnerar resultat baserat på aggregerade data för att minska väntetiden för resultat och ge ett mer interaktivt informationsutbyte.

Se [Slutpunkt för accelererade frågor](../../api/accelerated-queries.md) dokumentation som innehåller anvisningar om hur du frågar efter det accelererade arkivet.

Med det förbättrade arkivet kan du skapa en anpassad datamodell och/eller utöka en befintlig Adobe Real-time Customer Data Platform datamodell. Om du vill interagera med eller bädda in dina rapportinsikter i ett ramverk för rapportering/visualisering kan du läsa [guide för frågeaccelererade butiksrapportinsikter](./reporting-insights-data-model.md). Du kan även läsa dokumentationen till Real-time Customer Data Platform Insights-datamodellen för att lära dig hur du [anpassa dina SQL-frågemallar för att skapa Real-Time CDP-rapporter för dina KPI-fall (Marketing and Key Performance Indicator)](../../../dashboards/cdp-insights-data-model.md). Du kan använda [attribueringsbaserad åtkomstkontroll](../../../access-control/abac/overview.md), för att styra begränsningsnivån för datauppsättningar i det accelererade arkivet. Se [datastyrning i frågetjänsten](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
för mer information.
