---
keywords: Experience Platform;hem;populära ämnen;etikettidentiteter
solution: Experience Platform
title: Märk ett fält som en identitet
description: Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av etiketteringen av fältet.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Märk ett fält som en identitet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde i ett identitetsfält tolkas som en identitet av [!DNL Identity Service]. Identitetens namnutrymme anges som en del av etiketteringen av fältet.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

- Endast strängtypsfält kan användas för identitet
- Identiteter känns bara igen i post- och tidsseriedata
- Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du använder API:t för schematabell för att märka ett fält som en identitet finns i [slutpunktshandboken för beskrivningar](../../xdm/api/descriptors.md#create).

## Nästa steg

Gå till nästa självstudiekurs för att [lista klusteridentiteter](./list-cluster-identites.md)
