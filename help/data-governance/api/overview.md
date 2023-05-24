---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-guide för principtjänst
description: Med API:t för principtjänsten kan utvecklare hantera dataanvändningsetiketter och principer i Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# [!DNL Policy Service] API-guide

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, inklusive katalogisering, datalinje, märkning av dataanvändning, dataanvändningspolicyer och kontroll av användningen av data för marknadsföringsåtgärder.

The [!DNL Policy Service] API innehåller flera slutpunkter som gör att du kan hantera etiketter och policyer för dataanvändning programmatiskt, samt utvärdera marknadsföringsåtgärder för policyöverträdelser. Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Policy Service] API-växling](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etiketter

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de hämtas in till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform]. Du kan skapa, visa, redigera och ta bort etiketter med `/labels` slutpunkt. Om du vill veta hur du använder den här slutpunkten går du till [slutpunktshandbok för etiketter](./labels.md).

## Marknadsföringsåtgärder

Marknadsföringsåtgärder (kallas även användningsfall för marknadsföring) inom ramen för datastyrning är åtgärder som [!DNL Experience Platform] dataanvändare kan använda, som din organisation vill begränsa dataanvändningen för. Detaljerad information om hur du arbetar med marknadsföringsåtgärder finns i [slutpunktsguide för marknadsföringsåtgärder](./marketing-actions.md).

## Policyer

Datastyrningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom [!DNL Experience Platform].

>[!NOTE]
>
>Datastyrningsprinciper ska inte blandas ihop med åtkomstkontrollprinciper, som avgör vilka specifika dataattribut som vissa plattformsanvändare i organisationen kan komma åt. Se guiden [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för mer information.

En datastyrningspolicy definieras enligt följande:

1. En specifik marknadsföringsåtgärd
1. Etiketter för dataanvändning som åtgärden är begränsad från att utföras mot

Om du vill veta mer om hur du hanterar principer i API:t kan du läsa [stödlinje för principslutpunkt](./policies.md)

## Utvärdering

När dataanvändningsetiketterna har tillämpats på [!DNL Platform] datauppsättningar och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, så att ni kan tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

The [!DNL Policy Service] API innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning. Se [guide för utvärderingsslutpunkter](./evaluation.md) för mer information.

## Nästa steg

Börja ringa samtal med [!DNL Policy Service] API, läs [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter. Arbeta med etiketter och profiler med [!DNL Experience Platform] Gränssnittet, se [användarhandbok för etiketter](../labels/user-guide.md) och [användarhandbok](../policies/user-guide.md), respektive.
