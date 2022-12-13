---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Översikt över tvingande av policy
topic-legacy: guide
description: Läs om hur dataanvändningsprinciper tillämpas på Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 6f79b1a03a75558d1a25f0375e8393ad56756d80
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Översikt över policytillämpning

En gång [etiketter för dataanvändning](../labels/overview.md) har tillämpats och [dataanvändningsprinciper](../policies/overview.md) har definierats kan du tillämpa dessa policyer för att förhindra dataåtgärder som utgör policyöverträdelser.

>[!NOTE]
>
>Det här dokumentet fokuserar på efterlevnaden av dataanvändningsprinciper. Mer information om åtkomstkontrollprinciper finns i handboken om [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md).

Det finns två metoder för policytillämpning i Adobe Experience Platform: automatisk tillämpning och API-baserad tillämpning.

## Automatisk kontroll

Experience Platform utnyttjar funktioner för datalinje, dataklassificering och policyhantering för att automatiskt utvärdera och upptäcka överträdelser av policyer. Se översikten på [automatisk policytillämpning](./auto-enforcement.md) för mer information.

## API-baserad tillämpning

The [!DNL Policy Service] API innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan ni sedan skapa protokoll i ert upplevelseprogram för att på ett lämpligt sätt följa regelefterlevnaden för datastyrning.

Se självstudiekursen om [API-baserad tillämpning](./api-enforcement.md) för steg om hur du utvärderar principer med API:t.
