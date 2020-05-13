---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över etiketter för dataanvändning
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

DULE (Data Usage Labeling and Enforcement) är huvudmekanismen i Adobe Experience Platform Data Governance. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter (kallas även DULE-etiketter) i Experience Platform. Innan du läser den här guiden bör du läsa översikten över [datastyrning](../home.md) för att få en mer robust introduktion till DULE-ramverket.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till märkning av data så snart de hämtas till Experience Platform, eller så snart data blir tillgängliga för användning i Platform.

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

Mer information om tillgängliga etiketter för dataanvändning i Experience Platform och de användarprofiler de representerar finns i guiden om [dataanvändningsetiketter](reference.md)som stöds.

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapas av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för motsvarande datauppsättningar. Detta gör att applikationer som är byggda ovanpå Experience Platform (som Customer Data Platform i realtid) kan tillhandahålla automatisk policytillämpning för dataanvändning när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Beroende på hur ditt plattformsbaserade program använder segment kan du eventuellt ange vilka fält som ska användas, vilket förhindrar segmentet från att ärva etiketter från exkluderade fält.

Mer information om hur automatisk exekvering fungerar i CDP i realtid finns i [realtidsöversikten](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)för CDP-datastyrning.

## Nästa steg

Nu när du har fått nya etiketter för dataanvändning kan du fortsätta läsa [användarhandboken](user-guide.md) och lära dig hur du hanterar etiketter i Experience Platform-gränssnittet. Anvisningar om hur du hanterar etiketter med API:er finns i lämpliga avsnitt i utvecklarhandboken [för](../../catalog/api/labels.md)katalogtjänsten.