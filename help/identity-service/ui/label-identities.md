---
keywords: Experience Platform;hem;populära ämnen;etikettidentiteter
title: Märk ett fält som en identitet i användargränssnittet
description: Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av identitetstjänsten. Identitetens namnutrymme anges som en del av fältets etikett.
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Ange etikett för ett fält som en identitet i användargränssnittet

Fält som innehåller personligt identifierbar information (PII) kan märkas som identitetsfält. Ett värde som anges i ett identitetsfält tolkas som en identitet av [!DNL Identity Service]. Identitetens namnutrymme anges som en del av fältets etikett.

Följande villkor måste vara uppfyllda för att ett fält ska kunna märkas som identitet:

* Endast strängtypsfält kan användas för identitet
* Identiteter känns bara igen i post- och tidsseriedata
* Endast PII-fält ska markeras som identitet. Om du väljer ett fält som representerar mer generiska data blir relationen mindre exakt och det kan uppstå fel när relaterade identiteter från identitetsdiagrammet används

Instruktioner om hur du etiketterar identitetsfält i användargränssnittet finns i handboken [definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md).

## Nästa steg

Mer information om [!DNL Identity Service], se [[!DNL Identity Service] översikt](../home.md).
