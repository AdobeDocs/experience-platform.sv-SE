---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# [!DNL Policy Service] Utvecklarhandbok för API

Med Adobe Experience Platform [!DNL Data Governance] kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, dataanvändningsetiketter, dataanvändningspolicyer och kontroll av användningen av data för marknadsföringsåtgärder.

API:t innehåller flera slutpunkter som gör det möjligt att programmässigt hantera etiketter och policyer för dataanvändning samt utvärdera marknadsföringsåtgärder för policyöverträdelser. [!DNL Policy Service] Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktshandböckerna för mer information och se [komma igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Policy Service] API-växlaren](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etiketter

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform]. Du kan skapa, visa, redigera och ta bort etiketter med hjälp av `/labels` slutpunkten. Mer information om hur du använder den här slutpunkten finns i [etikettens slutpunktshandbok](./labels.md).

## Marknadsföringsåtgärder

Marknadsföringsåtgärder (kallas även användningsfall för marknadsföring), inom ramen för [!DNL Data Governance] ramverket, är åtgärder som en [!DNL Experience Platform] datakonsument kan vidta och som din organisation vill begränsa dataanvändningen för. Detaljerad information om hur du arbetar med marknadsföringsåtgärder finns i slutpunktshandboken för [marknadsföringsåtgärder](./marketing-actions.md).

## Profiler

Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom [!DNL Experience Platform]. En profil definieras av följande:

1. En specifik marknadsföringsåtgärd
1. Etiketter för dataanvändning som åtgärden är begränsad från att utföras mot

Mer information om hur du hanterar principer i API:t finns i [policyslutpunktshandboken](./policies.md)

## Utvärdering

När dataanvändningsetiketter har tillämpats på datauppsättningar, och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser. [!DNL Platform]

API:t innehåller [!DNL Policy Service] slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning. Mer information finns i guiden [för](./evaluation.md) utvärderingsslutpunkter.

## Nästa steg

Om du vill börja ringa anrop med [!DNL Policy Service] API:t läser du guiden [](./getting-started.md) Komma igång och väljer sedan en av slutpunktsguiderna för att lära dig hur du använder specifika slutpunkter. Om du vill arbeta med etiketter och profiler med hjälp av [!DNL Experience Platform] användargränssnittet läser du användarhandboken [för](../labels/user-guide.md) etiketter och [profiler](../policies/user-guide.md).