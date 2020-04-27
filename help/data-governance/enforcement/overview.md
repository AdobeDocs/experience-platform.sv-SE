---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över policytillämpning
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# Översikt över policytillämpning

När dataanvändningsetiketter har tillämpats på plattformsdatauppsättningar och dataanvändningspolicyer har definierats för marknadsföringsåtgärder mot dessa etiketter, kan ni med datastyrningsfunktionerna tillämpa dessa policyer och förhindra dataåtgärder som utgör policyöverträdelser.

Det finns två metoder för policytillämpning som tillhandahålls av datastyrningsfunktioner på plattformen: API- **baserad tillämpning** och **automatisk tillämpning**.

## API-baserad tillämpning

API:t för principtjänsten innehåller slutpunkter som gör att du kan testa marknadsföringsåtgärder mot datauppsättningar eller godtyckliga kombinationer av dataanvändningsetiketter för att kontrollera om några principöverträdelser inträffar. Baserat på API-svaret kan du sedan skapa protokoll i ditt upplevelseprogram för att säkerställa regelefterlevnad för dataanvändning.

I självstudiekursen om [policytillämpning](api-enforcement.md) finns anvisningar om hur du utvärderar principer med API:t.

## Automatisk kontroll

Vissa applikationer som bygger på Experience Platform (till exempel Customer Data Platform i realtid) har automatisk tillämpning av dataanvändningsprinciper. Varje program har en egen metod för att hantera överträdelser av policyer och innehåller åtgärder för att lösa problem.

Mer information om automatisk tillämpning av dataanvändningsprinciper finns i dokumentationen för det plattformsbaserade program du använder. Information om automatisk policytillämpning i CDP i realtid finns i CDP-översikten [i](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)realtid.