---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Översikt över etiketter för dataanvändning
topic: labels
description: Med Adobe Experience Platform Data Governance kan ni använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera varje dataanvändning enligt relaterade policyer för dataanvändning. Det här dokumentet innehåller en översikt över dataanvändningsetiketter i Experience Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

Med Adobe Experience Platform [!DNL Data Governance] kan du använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera dem efter relaterade dataanvändningsprinciper.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter i [!DNL Experience Platform]. Innan du läser den här guiden bör du läsa översikten över [](../home.md) datastyrning för att få en mer robust introduktion till ramverket för datastyrning.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera färdiga etiketter för&quot;viktig&quot; dataanvändning som täcker ett stort antal vanliga begränsningar för datastyrning. Mer information om dessa etiketter och de användarprofiler de representerar finns i guiden om etiketter för [viktig dataanvändning](reference.md).

Förutom etiketterna från Adobe kan du även definiera egna etiketter för din organisation. Mer information finns i avsnittet [Hantera etiketter](#manage-labels) .

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapas av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för sina motsvarande datauppsättningar. Detta gör att program som är byggda ovanpå Experience Platform (till exempel [!DNL Real-time Customer Data Platform]) automatiskt kan tillämpa dataanvändningspolicyn när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Beroende på hur ditt [!DNL Platform]baserade program använder segment kan du eventuellt ange vilka fält som ska användas, vilket förhindrar segmentet från att ärva etiketter från exkluderade fält.

Mer information om hur automatisk exekvering fungerar i CDP i realtid finns i översikten om [datastyrning i CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)i realtid.

### Arv från Adobe Audience Manager dataexportkontroller

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som erkänns av [!DNL Experience Platform][!DNL Data Governance].

En referens om hur specifika dataexportkontroller mappas till dataanvändningsetiketter i [!DNL Platform]finns i dokumentationen [för](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Hantera dataanvändningsetiketter i [!DNL Experience Platform] {#manage-labels}

Du kan hantera dataanvändningsetiketter med hjälp av [!DNL Experience Platform] API:er eller användargränssnittet. Mer information om respektive avsnitt finns i underavsnitten nedan.

### Använda gränssnittet

På arbetsytan i **[!UICONTROL Policies]** [!DNL Experience Platform] användargränssnittet kan du visa och hantera egna etiketter och etiketter för din organisation. På arbetsytan kan du **[!DNL Datasets]** använda etiketter på datauppsättningar och fält. Mer information finns i användarhandboken för [etiketter](user-guide.md).

### Använda API:er

Med `/labels` slutpunkten i API:t för [principtjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) kan du programmässigt hantera dataanvändningsetiketter, inklusive skapa anpassade etiketter. Mer information finns i [etikettens slutpunktshandbok](../api/labels.md) .

API:t för [datauppsättningstjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) används för att hantera etiketter för datauppsättningar och fält. Mer information finns i guiden om [hantering av datauppsättningsrubriker](./dataset-api.md) .

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsetiketter och deras roll inom ramverket för datastyrning. Mer information om hur du hanterar etiketter i finns i dokumentationen som är länkad till i den här handboken [!DNL Experience Platform].