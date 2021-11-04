---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Översikt över tvingande av policy
topic-legacy: guide
description: När dataanvändningsetiketter har tillämpats på Adobe Experience Platform datauppsättningar, och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser. Det finns två metoder för policytillämpning som tillhandahålls av datastyrningsfunktioner på plattformen, API-baserad tillämpning och automatisk tillämpning.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Översikt över policytillämpning

När dataanvändningsetiketter har tillämpats på datauppsättningar, och dataanvändningsprinciper har definierats för marknadsföringsåtgärder mot dessa etiketter, kan du med Adobe Experience Platform Data Governance tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

Det finns två metoder för policystyrning som tillhandahålls av datastyrningsfunktioner för [!DNL Platform]: API-baserad tillämpning och automatisk tillämpning.

## API-baserad tillämpning

The [!DNL Policy Service] API innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några policyöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning.

Se självstudiekursen om [API-baserad tillämpning](./api-enforcement.md) för steg om hur du utvärderar principer med API:t.

## Automatisk kontroll

Experience Platform utnyttjar funktioner för datalinje, dataklassificering och policyhantering för att automatiskt utvärdera och upptäcka överträdelser av policyer. Se översikten på [automatisk policytillämpning](./auto-enforcement.md) för mer information.
