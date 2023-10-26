---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningsetikett api;principtjänst api;dataanvändningsetiketter översikt
solution: Experience Platform
title: Översikt över dataanvändningsetiketter
description: Läs om hur dataanvändningsetiketter används för att säkerställa regelefterlevnad för datastyrning i Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Översikt över etiketter för dataanvändning {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Styr åtkomsten till känsliga och skyddade data"
>abstract="<h2>Beskrivning</h2><p>Styr åtkomsten till specifika dataattribut och/eller segment, så att ni kan utforma flexibla arbetsflöden för de olika personer och team som arbetar med Experience Platform.</p>"

Med Adobe Experience Platform kan du använda dataanvändningsetiketter på datauppsättningar och fält och kategorisera dem efter relaterade [datastyrningsprinciper](../policies/overview.md) och [åtkomstkontrollprinciper](../../access-control/abac/ui/policies.md).

Det här dokumentet innehåller en översikt över dataanvändningsetiketter i [!DNL Experience Platform].

## Förstå etiketter för dataanvändning

Med dataanvändningsetiketter kan du kategorisera datauppsättningar och fält enligt styrningsprinciper som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de hämtas in till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform].

Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning.

[!DNL Platform] innehåller flera färdiga etiketter för&quot;viktig&quot; dataanvändning som täcker ett stort antal vanliga begränsningar för datastyrning. Mer information om de här etiketterna och de styrningspolicyer de representerar finns i handboken [etiketter för användning av kärndata](reference.md).

Förutom etiketterna från Adobe kan du även definiera egna etiketter för din organisation. Se avsnittet om [hantera etiketter](#manage-labels) för mer information.

## Etikettarv för målgruppssegment

Alla målgruppssegment skapade av [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md) ärver användningsetiketterna för deras motsvarande datamängder. På så sätt kan Experience Platform tillhandahålla automatisk policystyrning när segment aktiveras för destinationer.

Förutom att ärva etiketter på datauppsättningsnivå ärver segment som standard alla etiketter på fältnivå från de associerade datauppsättningarna. Därför kan du enklare identifiera vilka attribut som ska uteslutas från dina segment och förhindra att de ärver etiketter från uteslutna fält.

Mer information om hur automatisk verkställighet fungerar i Platform finns i översikten på [automatisk policytillämpning](../enforcement/auto-enforcement.md).

### Arv från Adobe Audience Manager dataexportkontroller

[!DNL Experience Platform] kan dela segment med Adobe Audience Manager. Alla dataexportkontroller som har tillämpats på Audience Manager-segment översätts till motsvarande etiketter och marknadsföringsåtgärder som erkänns av [!DNL Experience Platform] Datastyrning.

En referens om hur specifika dataexportkontroller mappas till dataanvändningsetiketter i [!DNL Platform], se [Audience Manager dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Hantera dataanvändningsetiketter i [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instruktioner"
>abstract="<ul><li>Ge XDM-fält och -segment etiketter för att klassificera de fält och/eller segment som du vill begränsa åtkomsten till.</li><li>Etikettroller: om du lägger till etiketter i en roll kan du definiera etiketterna som medlemmar i den här rollen ska ha begränsningar för.</li><li>Skapa profiler, en profil skapar en relation mellan etiketterna för etiketterade objekt som XDM-fält och segment och etiketterna för roller. Om etiketterna matchar varandra kan antingen ett tillstånd eller en begränsad åtkomst definieras.</li></ul>"

Du kan hantera dataanvändningsetiketter med [!DNL Experience Platform] API:er eller användargränssnittet. Mer information om respektive avsnitt finns i underavsnitten nedan.

### Använda gränssnittet

The **[!UICONTROL Policies]** arbetsytan i [!DNL Experience Platform] Med användargränssnittet kan du visa och hantera etiketter och anpassade etiketter för din organisation. Du kan använda **[!UICONTROL Schemas]** arbetsyta till [använda etiketter i XDM-scheman (Experience Data Model)](../../xdm/tutorials/labels.md)eller lära dig hur [skapa och hantera egna etiketter i[!UICONTROL Policies] UI](./user-guide.md) genom att läsa användarhandboken för dataanvändningsetiketter i stället.

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Etiketter som tidigare använts på datauppsättningens objektnivå stöds fortfarande i plattformsgränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. Se avsnittet om [migrera tidigare använda etiketter](../e2e.md#migrate-labels) för instruktioner om hur man gör detta.

### Använda API:er

The `/labels` slutpunkt i [API för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/) Med kan du programmässigt hantera dataanvändningsetiketter, inklusive skapa anpassade etiketter. Se [slutpunktshandbok för etiketter](../api/labels.md) för mer information.

The [API för datauppsättningstjänst](https://www.adobe.io/experience-platform-apis/references/dataset-service/) används för att hantera etiketter för datauppsättningar och fält. Se guiden på [hantera datauppsättningsrubriker](./dataset-api.md) för mer information.

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsetiketter och deras roll inom ramverket för datastyrning. Mer information om hur du hanterar etiketter i finns i dokumentationen som är länkad till i den här handboken. [!DNL Experience Platform].
