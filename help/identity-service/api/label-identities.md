---
keywords: Experience Platform;hem;populära ämnen;etikettidentiteter
solution: Experience Platform
title: Märk ett fält som en identitet
topic: api guide
description: Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av fältets etikett.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# Märk ett fält som en identitet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av [!DNL Identity Service]. Identitetens namnutrymme anges som en del av fältets etikett.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

- Endast strängtypsfält kan användas för identitet
- Identiteter känns bara igen i post- och tidsseriedata
- Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du använder API:t för schemaregister för att märka ett fält som en identitet finns i [slutpunktshandboken för beskrivningar](../../xdm/api/descriptors.md#create).

## Nästa steg

Gå vidare till nästa självstudiekurs för att [visa klusteridentiteter](./list-cluster-identites.md)