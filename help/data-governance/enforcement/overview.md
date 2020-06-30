---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över policytillämpning
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Översikt över policytillämpning

När dataanvändningsetiketter har tillämpats på [!DNL Platform] [!DNL Data Governance] datauppsättningar och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med hjälp av funktioner tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

Det finns två metoder för policytillämpning som tillhandahålls av [!DNL Data Governance] funktioner på [!DNL Platform]: **API-baserad tillämpning** och **automatisk tillämpning**.

## API-baserad tillämpning

API:t innehåller [!DNL Policy Service] slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning.

I självstudiekursen om [policytillämpning](api-enforcement.md) finns anvisningar om hur du utvärderar principer med API:t.

## Automatisk kontroll

Vissa program som är byggda ovanpå [!DNL Experience Platform] (till exempel [!DNL Real-time Customer Data Platform]) har automatisk tillämpning av dataanvändningsprinciper. Varje program har en egen metod för att hantera överträdelser av policyer och innehåller åtgärder för att lösa problem.

Mer information om automatisk tillämpning av dataanvändningsprinciper finns i dokumentationen för det [!DNL Platform]baserade programmet som du använder. Information om automatisk policytillämpning i CDP i realtid finns i CDP-översikten [i](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)realtid.