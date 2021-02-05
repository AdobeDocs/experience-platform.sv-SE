---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-guide för principtjänst
topic: developer guide
description: Med API:t för principtjänsten kan utvecklare hantera dataanvändningsetiketter och principer i Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# [!DNL Policy Service] API-guide

Med Adobe Experience Platform [!DNL Data Governance] kan ni hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, bland annat för katalogisering, datalinje, etikettering av dataanvändning, dataanvändningsprinciper och kontroll av användningen av data för marknadsföringsåtgärder.

API:t [!DNL Policy Service] innehåller flera slutpunkter som gör att du kan hantera etiketter och policyer för dataanvändning programmatiskt samt utvärdera marknadsföringsåtgärder för policyöverträdelser. Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guiden](./getting-started.md) finns viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Policy Service] API-växlaren](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etiketter

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform], eller så snart data blir tillgängliga för användning i [!DNL Platform]. Du kan skapa, visa, redigera och ta bort etiketter med slutpunkten `/labels`. Mer information om hur du använder den här slutpunkten finns i [etikettens slutpunktshandbok](./labels.md).

## Marknadsföringsåtgärder

Marknadsföringsåtgärder (kallas även användningsfall för marknadsföring) i [!DNL Data Governance]-ramverket är åtgärder som en [!DNL Experience Platform]-datakonsument kan vidta och som din organisation vill begränsa dataanvändningen för. Detaljerad information om hur du arbetar med marknadsföringsåtgärder finns i [slutpunktshandboken för marknadsföringsåtgärder](./marketing-actions.md).

## Profiler

Dataanvändningsprinciper är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data i [!DNL Experience Platform]. En profil definieras av följande:

1. En specifik marknadsföringsåtgärd
1. Etiketter för dataanvändning som åtgärden är begränsad från att utföras mot

Mer information om hur du hanterar principer i API:t finns i [policyslutpunktshandboken](./policies.md)

## Utvärdering

När dataanvändningsetiketter har tillämpats på [!DNL Platform]-datauppsättningar, och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

API:t [!DNL Policy Service] innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några principöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning. Mer information finns i [handboken för utvärderingsslutpunkter](./evaluation.md).

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Policy Service] läser du [Komma igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter. Om du vill arbeta med etiketter och profiler med hjälp av användargränssnittet i [!DNL Experience Platform] läser du användarhandboken för [etiketter](../labels/user-guide.md) respektive [användarhandboken för ](../policies/user-guide.md).