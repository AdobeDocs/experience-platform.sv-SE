---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över etiketter för dataanvändning
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Översikt över etiketter för dataanvändning

Varumärkning och verkställighet av dataanvändning (DULE) är huvudmekanismen för Adobe Experience Platform [!DNL Data Governance]. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning.

Det här dokumentet innehåller en översikt över dataanvändningsetiketter (kallas även DULE-etiketter) i [!DNL Experience Platform]. Innan du läser den här guiden bör du läsa översikten över [datastyrning](../home.md) för att få en mer robust introduktion till DULE-ramverket.

## Förstå etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera färdiga etiketter för&quot;viktig&quot; dataanvändning som täcker ett stort antal vanliga begränsningar för datastyrning. Mer information om dessa etiketter och de användarprofiler de representerar finns i guiden om etiketter för [viktig dataanvändning](reference.md).

Förutom etiketterna från Adobe kan du också definiera egna etiketter. Anvisningar om hur du gör detta i användargränssnittet finns i användarhandboken för [dataanvändningsetiketter](./user-guide.md). Anvisningar om hur du utför detta med API-anrop finns i API-handboken för [dataanvändningsetiketter](./api.md).

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapas av [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ärver användningsetiketterna för sina motsvarande datauppsättningar. Detta gör att program som är byggda ovanpå [!DNL Experience Platform] (till exempel [!DNL Real-time Customer Data Platform]) automatiskt kan tillämpa dataanvändningsprinciper när segment aktiveras till mål.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Beroende på hur ditt [!DNL Platform]baserade program använder segment kan du eventuellt ange vilka fält som ska användas, vilket förhindrar segmentet från att ärva etiketter från exkluderade fält.

Mer information om hur automatisk exekvering fungerar i CDP i realtid finns i [Adobes realtidsöversikt](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)över CDP Data Governance.

### Arv från dataexportkontroller i Adobe Audience Manager

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som erkänns av [!DNL Experience Platform][!DNL Data Governance].

En referens om hur specifika dataexportkontroller mappas till dataanvändningsetiketter i [!DNL Platform]finns i dokumentationen [för](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Nästa steg

Nu när du har fått nya etiketter för dataanvändning kan du fortsätta läsa [användarhandboken](user-guide.md) och lära dig hur du hanterar etiketter i [!DNL Experience Platform] användargränssnittet. Anvisningar om hur du hanterar etiketter med API:er finns i API-handboken för [användningsetiketter](./api.md).