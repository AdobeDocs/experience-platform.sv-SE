---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-guide för principtjänst
description: Med API:t för principtjänsten kan utvecklare hantera dataanvändningsetiketter och principer i Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# API-guide för [!DNL Policy Service]

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Den spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, bland annat i fråga om kataloger, datalinje, etikettering av dataanvändning, dataanvändningsprinciper och kontroll av användningen av data för marknadsföringsåtgärder.

API:t [!DNL Policy Service] innehåller flera slutpunkter som gör att du kan hantera etiketter och principer för dataanvändning programmatiskt, samt utvärdera marknadsföringsåtgärder för policyöverträdelser. Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Policy Service] API-växlaren](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etiketter

Använd dataanvändningsetiketter på scheman för att kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform], eller så snart data blir tillgängliga för användning i [!DNL Experience Platform]. Du kan skapa, visa, redigera och ta bort etiketter med slutpunkten `/labels`. Om du vill lära dig hur du använder den här slutpunkten kan du gå till [etikettguiden](./labels.md).

## Marknadsföringsåtgärder

Marknadsföringsåtgärder (kallas även användningsfall för marknadsföring), inom ramverket för datastyrning, är åtgärder som en [!DNL Experience Platform]-datakonsument kan vidta och som din organisation vill begränsa dataanvändningen för. Mer information om hur du arbetar med marknadsföringsåtgärder finns i [slutpunktshandboken för marknadsföringsåtgärder](./marketing-actions.md).

## Policyer

Datastyrningsprinciper är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data i [!DNL Experience Platform].

>[!NOTE]
>
>Datastyrningsprinciper ska inte blandas ihop med åtkomstkontrollprinciper, som avgör vilka specifika dataattribut som vissa Experience Platform-användare i organisationen kan komma åt. Mer information finns i guiden om [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md).

En datastyrningspolicy definieras enligt följande:

1. En specifik marknadsföringsåtgärd
1. Etiketter för dataanvändning som åtgärden är begränsad från att utföras mot

Mer information om hur du hanterar principer i API:t finns i [policyslutpunktshandboken](./policies.md)

## Utvärdering

När dataanvändningsetiketter har tillämpats på Experience Platform-scheman och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

API:t [!DNL Policy Service] innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några principöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning. Mer information finns i [handboken för utvärderingsslutpunkter](./evaluation.md).

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Policy Service] läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter. Om du vill arbeta med etiketter och profiler med hjälp av användargränssnittet för [!DNL Experience Platform] kan du läsa användarhandboken för [etiketter](../labels/user-guide.md) respektive [profiler](../policies/user-guide.md).
