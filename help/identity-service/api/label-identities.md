---
keywords: Experience Platform;home;popular topics;label identities
solution: Experience Platform
title: Ange etikett för ett fält som identitet
topic: api guide
description: Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av fältets etikett.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# Ange etikett för ett fält som identitet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av [!DNL Identity Service]. Identitetens namnutrymme anges som en del av fältets etikett.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

- Endast strängtypsfält kan användas för identitet
- Identiteter känns bara igen i post- och tidsseriedata
- Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du använder API:t för schematabell för att märka ett fält som en identitet finns i [Skapa en beskrivning](../../xdm/api/descriptors.md).

## Nästa steg

Gå till nästa självstudiekurs för att [lista klusteridentiteter](./list-cluster-identites.md)