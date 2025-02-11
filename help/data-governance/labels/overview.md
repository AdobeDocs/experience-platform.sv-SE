---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningsetikett api;principtjänst api;dataanvändningsetiketter översikt
solution: Experience Platform
title: Översikt över dataanvändningsetiketter
description: Läs om hur dataanvändningsetiketter används för att säkerställa regelefterlevnad för datastyrning i Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Översikt över etiketter för dataanvändning {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Styr åtkomsten till känsliga och skyddade data"
>abstract="<h2>Beskrivning</h2><p>Styr åtkomsten till specifika dataattribut och/eller segment så att ni kan utforma flexibla arbetsflöden för de olika personer och team som arbetar med Experience Platform.</p>"

Med Adobe Experience Platform kan du tillämpa dataanvändningsetiketter på datauppsättningar och fält och kategorisera dem enligt relaterade [datastyrningsprinciper](../policies/overview.md) och [åtkomstkontrollprinciper](../../access-control/abac/ui/policies.md).

Det här dokumentet innehåller en översikt över dataanvändningsetiketter i [!DNL Experience Platform].

## Förstå etiketter för dataanvändning

Med dataanvändningsetiketter kan du kategorisera datauppsättningar och fält enligt styrningsprinciper som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform], eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera körklara etiketter för viktig dataanvändning, som omfattar ett stort antal vanliga begränsningar för datastyrning. Mer information om de här etiketterna och de styrningsprinciper de representerar finns i guiden om [etiketter för kärndataanvändning](reference.md).

Förutom etiketterna från Adobe kan du även definiera egna etiketter för din organisation. Mer information finns i avsnittet [Hantera etiketter](#manage-labels).

## Etikettarv för målgruppssegment

Alla målgruppssegment som skapats av [Adobe Experience Platform Segmenteringstjänst](../../segmentation/home.md) ärver användningsetiketterna för sina motsvarande datauppsättningar. På så sätt kan Experience Platform tillhandahålla automatisk policystyrning när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Därför kan du enklare identifiera vilka attribut som ska uteslutas från dina segment och förhindra att de ärver etiketter från uteslutna fält.

Mer information om hur automatisk tvingande av principer fungerar i plattformen finns i översikten om [automatisk tillämpning av principer](../enforcement/auto-enforcement.md).

### Arv från Adobe Audience Manager dataexportkontroller

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som identifieras av [!DNL Experience Platform] Data Governance.

En referens om hur specifika dataexportkontroller mappar till dataanvändningsetiketter i [!DNL Platform] finns i [Audience Manager-dokumentationen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Hantera dataanvändningsetiketter i [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instruktioner"
>abstract="<ul><li>Ge XDM-fält och -segment etiketter för att klassificera de fält och/eller segment som du vill begränsa åtkomsten till.</li><li>Etikettroller: om du lägger till etiketter i en roll kan du definiera etiketterna som medlemmar i den här rollen ska ha begränsningar för.</li><li>Skapa profiler, en profil skapar en relation mellan etiketterna för etiketterade objekt som XDM-fält och segment och etiketterna för roller. Om etiketterna matchar varandra kan antingen ett tillstånd eller en begränsad åtkomst definieras.</li></ul>"

Du kan hantera dataanvändningsetiketter med [!DNL Experience Platform] API:er eller användargränssnittet. Mer information om respektive avsnitt finns i underavsnitten nedan.

### Använda gränssnittet

På arbetsytan **[!UICONTROL Policies]** i användargränssnittet för [!DNL Experience Platform] kan du visa och hantera kärnetiketter och anpassade etiketter för din organisation. Du kan använda arbetsytan **[!UICONTROL Schemas]** för att [använda etiketter i XDM-scheman (Experience Data Model)](../../xdm/tutorials/labels.md), eller lära dig hur du [skapar och hanterar anpassade etiketter i användarhandboken för **[!UICONTROL Policies] UI](./user-guide.md) genom att läsa användarhandboken för dataanvändningsetiketter i stället.

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Etiketter som tidigare använts på datauppsättningens objektnivå stöds fortfarande i plattformsgränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. Mer information om hur du gör detta finns i avsnittet [migrera tidigare använda etiketter](../e2e.md#migrate-labels).

### Använda API:er

`/labels`-slutpunkten i [ API:t för principtjänsten ](https://www.adobe.io/experience-platform-apis/references/policy-service/) gör att du kan hantera dataanvändningsetiketter programmatiskt, inklusive skapa anpassade etiketter. Mer information finns i [etikettens slutpunktshandbok](../api/labels.md).

[API:t för datauppsättningstjänsten](https://www.adobe.io/experience-platform-apis/references/dataset-service/) används för att hantera etiketter för datauppsättningar och fält. Mer information finns i guiden [Hantera datauppsättningsetiketter](./dataset-api.md).

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsetiketter och deras roll inom ramverket för datastyrning. Mer information om hur du hanterar etiketter i [!DNL Experience Platform] finns i dokumentationen som är länkad till i den här handboken.
