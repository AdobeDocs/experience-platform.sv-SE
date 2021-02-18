---
title: Synkronisera identiteter mellan Audience Manager och Adobe Experience Platform med hjälp av Platform Web SDK
description: Lär dig hur du synkroniserar identiteter mellan Audience Manager och Adobe Experience Platform med hjälp av Platform Web SDK
seo-description: Lär dig hur du synkroniserar identiteter med Adobe Audience Manager med Experience Platform Web SDK
keywords: målgruppshanterare;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Synkronisera identiteter mellan Audience Manager och Experience Platform

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via kommandot [sendEvent](./overview.md#syncing-identities).

Välj dina namnutrymmen i [identitetstjänstens namnutrymmen](../../identity/../identity-service/namespaces.md) för att ange kontexten som en identitet relaterar till genom att använda värdena i kolumnen Identitetssymbol:

![Vy över namnutrymmesgränssnittet](../../assets/edge_namespaceUI_identity-symbol.png)

Som Audience Manager-kund använder du alla befintliga datakällor som använder ID-typ: Enhetsövergripande enheter har automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande Identity Namespace för Audience Manager-datakällan loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

Ny datakälla i [!DNL Audience Manager] som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande [!DNL Audience Manager]-datakälla, men observera att syncIdentity-metoden endast stöder Namespace Identity Symbols.
