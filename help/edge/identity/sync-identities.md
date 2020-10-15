---
title: Synkronisera identiteter med Audience Manager och Adobe Experience Platform
seo-title: Synkronisera identiteter med Audience Manager och Adobe Experience Platform med Adobe Experience Platform Web SDK
description: Lär dig hur du synkroniserar identiteter med Adobe Audience Manager med Experience Platform Web SDK
seo-description: Lär dig hur du synkroniserar identiteter med Adobe Audience Manager med Experience Platform Web SDK
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 290792cd507248c41690c493cc18daaab869db50
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Synkroniserar identiteter

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via kommandot [sendEvent](./overview.md#syncing-identities) .

Välj dina namnutrymmen från [identitetstjänstens namnutrymmen](../../identity/../identity-service/namespaces.md) för att ange i vilken kontext en identitet relateras, genom att använda värdena i kolumnen Identitetssymbol:

![Vy över namnutrymmesgränssnittet](../../assets/edge_namespaceUI_identity-symbol.png)

Som Audience Manager-kund använder du alla befintliga datakällor som använder ID-typ: Enhetsövergripande enheter har automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande Identity Namespace för Audience Manager-datakällan loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

Ny [!DNL Audience Manager] datakälla som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande [!DNL Audience Manager] datakälla, men observera att syncIdentity-metoden endast stöder Namespace Identity Symbols.
