---
title: Synkronisera identiteter mellan Audience Manager och Adobe Experience Platform med Experience Platform Web SDK
description: Lär dig synkronisera identiteter mellan Audience Manager och Adobe Experience Platform med Experience Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: målgruppshanterare;aam;identities;sync identities;namespace;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Synkronisera identiteter mellan Audience Manager och Experience Platform

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via kommandot [sendEvent](./overview.md#syncing-identities).

Välj dina namnutrymmen från [Identitetstjänstens namnutrymmen](../../identity/../identity-service/features/namespaces.md) för att ange kontexten som en identitet relaterar till genom att använda värdena i kolumnen Identitetssymbol:

![Vy över namnutrymmesgränssnittet](../assets/identity/edge_namespaceUI_identity-symbol.png)

Som Audience Manager-kund har alla befintliga datakällor som använder ID-typ: Flera enheter har automatiskt ett motsvarande ID-namnområde. Om du vill hitta motsvarande Identity Namespace för din Audience Manager Data Source loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

Alla nya [!DNL Audience Manager]-data-Source som använder ID-typ: Enhetsövergripande genererar ett motsvarande identitetsnamnområde. Source-ID-typerna Cookie och Advertising-ID för enhet stöds för närvarande inte. Dessutom kommer alla Identity Namespace som skapas i Adobe Experience Platform att generera motsvarande [!DNL Audience Manager] Data Source, men observera att syncIdentity-metoden bara stöder Namespace Identity Symbols.
