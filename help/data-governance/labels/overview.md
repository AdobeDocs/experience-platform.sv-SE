---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningsetikett api;principtjänst api;dataanvändningsetiketter översikt
solution: Experience Platform
title: Översikt över dataanvändningsetiketter
topic-legacy: labels
description: Med Adobe Experience Platform Data Governance kan ni använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera varje dataanvändning enligt relaterade policyer för dataanvändning. Det här dokumentet innehåller en översikt över dataanvändningsetiketter i Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Översikt över etiketter för dataanvändning

Med Adobe Experience Platform Data Governance kan du använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera varje dataanvändning enligt relaterade dataanvändningsprinciper.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter i [!DNL Experience Platform]. Innan du läser den här guiden ska du läsa [Datastyrning - översikt](../home.md) för en mer robust introduktion till ramverket för datastyrning.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de hämtas in till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera färdiga etiketter för&quot;viktig&quot; dataanvändning som täcker ett stort antal vanliga begränsningar för datastyrning. Mer information om dessa etiketter och de användarprofiler de representerar finns i handboken [etiketter för användning av kärndata](reference.md).

Förutom etiketterna från Adobe kan du även definiera egna etiketter för din organisation. Se avsnittet om [hantera etiketter](#manage-labels) för mer information.

## Etikettarv för målgruppssegment

Alla målgruppssegment skapade av [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md) ärver användningsetiketterna för deras motsvarande datamängder. På så sätt kan Experience Platform tillhandahålla automatisk tillämpning av dataanvändningsprinciper när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Därför kan du enklare identifiera vilka attribut som ska uteslutas från dina segment och förhindra att de ärver etiketter från uteslutna fält.

Mer information om hur automatisk verkställighet fungerar i Platform finns i översikten på [automatisk policytillämpning](../enforcement/auto-enforcement.md).

### Arv från Adobe Audience Manager dataexportkontroller

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som erkänns av [!DNL Experience Platform] Datastyrning.

Om du vill ha en referens om hur specifika dataexportkontroller mappas till dataanvändningsetiketter i [!DNL Platform], se [Audience Manager dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Hantera dataanvändningsetiketter i [!DNL Experience Platform] {#manage-labels}

Du kan hantera dataanvändningsetiketter med [!DNL Experience Platform] API:er eller användargränssnittet. Mer information om respektive avsnitt finns i underavsnitten nedan.

### Använda gränssnittet

The **[!UICONTROL Policies]** arbetsytan i [!DNL Experience Platform] Med användargränssnittet kan du visa och hantera etiketter och anpassade etiketter för din organisation. The **[!DNL Datasets]** kan du använda etiketter på datauppsättningar och fält. Mer information finns i [användarhandbok för etiketter](user-guide.md).

### Använda API:er

The `/labels` slutpunkt i [API för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/) Med kan du programmässigt hantera dataanvändningsetiketter, inklusive skapa anpassade etiketter. Se [slutpunktshandbok för etiketter](../api/labels.md) för mer information.

The [API för datauppsättningstjänst](https://www.adobe.io/experience-platform-apis/references/dataset-service/) används för att hantera etiketter för datauppsättningar och fält. Se guiden [hantera datauppsättningsrubriker](./dataset-api.md) för mer information.

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsetiketter och deras roll inom ramverket för datastyrning. Mer information om hur du hanterar etiketter i finns i dokumentationen som är länkad till i den här handboken. [!DNL Experience Platform].
