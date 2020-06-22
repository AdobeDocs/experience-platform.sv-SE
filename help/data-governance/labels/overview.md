---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över etiketter för dataanvändning
topic: labels
translation-type: tm+mt
source-git-commit: e3c69589e0d4f8224b74a663b23f67e6731ddec4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

Varumärkning och verkställighet av dataanvändning (DULE) är kärnmekanismen i Adobe Experience Platform datastyrning. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter (kallas även DULE-etiketter) i Experience Platform. Innan du läser den här guiden bör du läsa översikten över [datastyrning](../home.md) för att få en mer robust introduktion till DULE-ramverket.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till märkning så snart data har importerats till Experience Platform, eller så snart data blir tillgängliga för användning i Platform.

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

Mer information om tillgängliga etiketter för dataanvändning i Experience Platform och vilka användarprofiler de representerar finns i guiden om [dataanvändningsetiketter](reference.md)som stöds.

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapas av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för sina motsvarande datauppsättningar. På så sätt kan applikationer som är byggda ovanpå Experience Platform (till exempel kunddata i realtid Platform) automatiskt tillämpa dataanvändningspolicyn när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Beroende på hur ditt Platform-baserade program använder segment kan du eventuellt ange vilka fält som ska användas, vilket förhindrar att segmentet ärver etiketter från exkluderade fält.

Mer information om hur automatisk exekvering fungerar i CDP i realtid finns i [realtidsöversikten](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)för CDP-datastyrning.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Nästa steg

Nu när du har fått nya etiketter för dataanvändning kan du fortsätta att läsa [användarhandboken](user-guide.md) och lära dig hur du hanterar etiketter i användargränssnittet i Experience Platform. Anvisningar om hur du hanterar etiketter med API:er finns i lämpliga avsnitt i utvecklarhandboken [för](../../catalog/api/labels.md)katalogtjänsten.