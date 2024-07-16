---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Översikt över tvingande av policy
description: Läs om hur dataanvändningsprinciper tillämpas på Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Översikt över policytillämpning

När [dataanvändningsetiketter](../labels/overview.md) har tillämpats och [dataanvändningsprinciper](../policies/overview.md) har definierats, kan du tillämpa dessa profiler för att förhindra dataåtgärder som utgör policyöverträdelser.

>[!NOTE]
>
>Det här dokumentet fokuserar på efterlevnaden av dataanvändningsprinciper. Mer information om åtkomstkontrollprinciper finns i handboken om [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md).

Det finns två metoder för policytillämpning i Adobe Experience Platform: automatisk tillämpning och API-baserad tillämpning.

## Automatisk kontroll

Experience Platform utnyttjar funktioner för datalinje, dataklassificering och policyhantering för att automatiskt utvärdera och upptäcka överträdelser av policyer. Mer information finns i översikten om [automatisk policytillämpning](./auto-enforcement.md).

## API-baserad tillämpning

API:t [!DNL Policy Service] innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några principöverträdelser inträffar. Baserat på API-svaret kan ni sedan skapa protokoll i ert upplevelseprogram för att på ett lämpligt sätt följa regelefterlevnaden för datastyrning.

I självstudiekursen om [API-baserad tillämpning](./api-enforcement.md) finns anvisningar om hur du utvärderar principer med API:t.
