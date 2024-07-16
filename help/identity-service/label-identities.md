---
keywords: Experience Platform;hem;populära ämnen;etikettidentiteter
title: Märk ett fält som en identitet i användargränssnittet
description: Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av etiketteringen av fältet.
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Ange etikett för ett fält som en identitet i användargränssnittet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde i ett identitetsfält tolkas som en identitet av [!DNL Identity Service]. Identitetens namnutrymme anges som en del av etiketteringen av fältet.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

* Endast strängtypsfält kan användas för identitet
* Identiteter känns bara igen i post- och tidsseriedata
* Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du etiketterar identitetsfält i användargränssnittet finns i handboken [Definiera identitetsfält i användargränssnittet](../xdm/ui/fields/identity.md).

## Nästa steg

Mer information om [!DNL Identity Service] finns i [[!DNL Identity Service] översikten](./home.md).
