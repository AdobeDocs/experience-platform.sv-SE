---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Översikt över tvingande av policy
topic: guide
description: När dataanvändningsetiketter har tillämpats på Adobe Experience Platform datauppsättningar, och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser. Det finns två metoder för policytillämpning som tillhandahålls av datastyrningsfunktioner på plattformen, API-baserad tillämpning och automatisk tillämpning.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Översikt över policytillämpning

När dataanvändningsetiketter har tillämpats på datauppsättningar, och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan du med Adobe Experience Platform Data Governance tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

Det finns två metoder för policytillämpning som tillhandahålls av [!DNL Data Governance]-funktioner i [!DNL Platform]: API-baserad tillämpning och automatisk tillämpning.

## API-baserad tillämpning

API:t [!DNL Policy Service] innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några principöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning.

I självstudiekursen om [API-baserad tvingande](./api-enforcement.md) finns anvisningar om hur du utvärderar principer med API:t.

## Automatisk kontroll

Experience Platform utnyttjar funktioner för datalinje, dataklassificering och policyhantering för att automatiskt utvärdera och upptäcka överträdelser av policyer. Mer information finns i översikten om [automatisk policytillämpning](./auto-enforcement.md).