---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningsetikett api;principtjänst api;dataanvändningsetiketter översikt
solution: Experience Platform
title: Översikt över dataanvändningsetiketter
topic: labels
description: Med Adobe Experience Platform Data Governance kan ni använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera varje dataanvändning enligt relaterade policyer för dataanvändning. Det här dokumentet innehåller en översikt över dataanvändningsetiketter i Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

Med Adobe Experience Platform [!DNL Data Governance] kan du använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera dem enligt relaterade dataanvändningsprinciper.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter i [!DNL Experience Platform]. Innan du läser den här guiden bör du läsa [översikten över datastyrning](../home.md) för att få en mer robust introduktion till ramverket för datastyrning.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform], eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera färdiga etiketter för&quot;viktig&quot; dataanvändning som täcker ett stort antal vanliga begränsningar för datastyrning. Mer information om de här etiketterna och de användarprofiler de representerar finns i guiden [etiketter för viktig dataanvändning](reference.md).

Förutom etiketterna från Adobe kan du även definiera egna etiketter för din organisation. Mer information finns i avsnittet [Hantera etiketter](#manage-labels).

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapats av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för motsvarande datauppsättningar. På så sätt kan Experience Platform tillhandahålla automatisk tillämpning av dataanvändningsprinciper när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Därför kan du enklare identifiera vilka attribut som ska uteslutas från dina segment och förhindra att de ärver etiketter från uteslutna fält.

Mer information om hur automatisk tillämpning fungerar i Platform finns i översikten om [automatisk policytillämpning](../enforcement/auto-enforcement.md).

### Arv från Adobe Audience Manager dataexportkontroller

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som är kända av [!DNL Experience Platform] [!DNL Data Governance].

En referens om hur specifika dataexportkontroller mappar till dataanvändningsetiketter i [!DNL Platform] finns i [Audience Manager-dokumentationen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Hantera dataanvändningsetiketter i [!DNL Experience Platform] {#manage-labels}

Du kan hantera dataanvändningsetiketter med hjälp av [!DNL Experience Platform] API:er eller användargränssnittet. Mer information om respektive avsnitt finns i underavsnitten nedan.

### Använda gränssnittet

Med arbetsytan **[!UICONTROL Policies]** i gränssnittet för [!DNL Experience Platform] kan du visa och hantera egna etiketter och etiketter för din organisation. Med arbetsytan **[!DNL Datasets]** kan du använda etiketter på datauppsättningar och fält. Mer information finns i användarhandboken för [etiketter](user-guide.md).

### Använda API:er

Med `/labels`-slutpunkten i [API:t för principtjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) kan du programmässigt hantera dataanvändningsetiketter, inklusive att skapa anpassade etiketter. Mer information finns i [etikettens slutpunktshandbok](../api/labels.md).

[API:t för datauppsättningstjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) används för att hantera etiketter för datauppsättningar och fält. Mer information finns i guiden [Hantera datauppsättningsrubriker](./dataset-api.md).

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsetiketter och deras roll inom ramverket för datastyrning. Mer information om hur du hanterar etiketter i [!DNL Experience Platform] finns i dokumentationen som är länkad till i den här handboken.