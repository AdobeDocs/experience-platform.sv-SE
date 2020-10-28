---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Översikt över policytillämpning
topic: enforcement
description: När dataanvändningsetiketter har tillämpats på Adobe Experience Platform datauppsättningar, och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser. Det finns två metoder för policytillämpning som tillhandahålls av datastyrningsfunktioner på plattformen, API-baserad tillämpning och automatisk tillämpning.
translation-type: tm+mt
source-git-commit: 83f1392ffab3571ebd91325123fbe7095ad59e28
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Översikt över policytillämpning

När dataanvändningsetiketter har tillämpats på [!DNL Platform] [!DNL Data Governance] datauppsättningar och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med hjälp av funktioner tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

Det finns två metoder för policytillämpning som tillhandahålls av [!DNL Data Governance] funktioner på [!DNL Platform]: API-baserad tillämpning och automatisk tillämpning.

## API-baserad tillämpning

API:t innehåller [!DNL Policy Service] slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning.

I självstudiekursen om [policytillämpning](api-enforcement.md) finns anvisningar om hur du utvärderar principer med API:t.

## Automatisk kontroll

Vissa program som är byggda ovanpå [!DNL Experience Platform] (till exempel [!DNL Real-time Customer Data Platform]) har automatisk tillämpning av dataanvändningsprinciper. Varje program har en egen metod för att hantera överträdelser av policyer och innehåller åtgärder för att lösa problem.

Automatisk policytillämpning i realtid CDP utnyttjar funktioner för datalänkning, dataklassificering och policyhantering för att utvärdera och upptäcka överträdelser av policyer. Mer information finns i [realtidsöversikten](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) för CDP Data Governance.