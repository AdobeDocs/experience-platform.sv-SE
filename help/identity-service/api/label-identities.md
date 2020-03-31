---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ange etikett för ett fält som identitet
topic: api guide
translation-type: tm+mt
source-git-commit: 40ce232e39f62f1ee478ef05229dd2fc125ee4c0

---


# Ange etikett för ett fält som identitet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av fältets etikett.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

- Endast strängtypsfält kan användas för identitet
- Identiteter känns bara igen i post- och tidsseriedata
- Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du använder API:t för schematabell för att märka ett fält som en identitet finns i [Skapa en beskrivning](../../xdm/api/descriptors.md).

## Nästa steg

Gå till nästa självstudiekurs för att [lista klusteridentiteter](./list-cluster-identites.md)