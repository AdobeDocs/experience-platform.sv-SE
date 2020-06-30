---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över etiketter för dataanvändning
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

Varumärkning och verkställighet av dataanvändning (DULE) är kärnmekanismen i Adobe Experience Platform datastyrning. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter (kallas även DULE-etiketter) i [!DNL Experience Platform]. Innan du läser den här guiden bör du läsa översikten över [datastyrning](../home.md) för att få en mer robust introduktion till DULE-ramverket.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

Mer information om tillgängliga dataanvändningsetiketter i [!DNL Experience Platform] och de användningsprinciper de representerar finns i guiden om [dataanvändningsetiketter](reference.md)som stöds.

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapas av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för sina motsvarande datauppsättningar. Detta gör att program som är byggda ovanpå [!DNL Experience Platform] (till exempel [!DNL Real-time Customer Data Platform]) automatiskt kan tillämpa dataanvändningsprinciper när segment aktiveras till mål.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Beroende på hur ditt [!DNL Platform]baserade program använder segment kan du eventuellt ange vilka fält som ska användas, vilket förhindrar segmentet från att ärva etiketter från exkluderade fält.

Mer information om hur automatisk exekvering fungerar i CDP i realtid finns i [Adobes realtidsöversikt](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)över CDP Data Governance.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Nästa steg

Nu när du har fått nya etiketter för dataanvändning kan du fortsätta läsa [användarhandboken](user-guide.md) och lära dig hur du hanterar etiketter i [!DNL Experience Platform] användargränssnittet. Anvisningar om hur du hanterar etiketter med API:er finns i lämpliga avsnitt i utvecklarhandboken [för](../../catalog/api/labels.md)katalogtjänsten.