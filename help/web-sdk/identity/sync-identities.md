---
title: Synkronisera identiteter mellan Audience Manager och Adobe Experience Platform med hjälp av Platform Web SDK
description: Lär dig hur du synkroniserar identiteter mellan Audience Manager och Adobe Experience Platform med hjälp av Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: målgruppshanterare;aam;identities;sync identities;namespace;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Synkronisera identiteter mellan Audience Manager och Experience Platform

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via [sendEvent](./overview.md#syncing-identities) -kommando.

Välj namnutrymmen på [Identitetstjänstens namnutrymmen](../../identity/../identity-service/features/namespaces.md) om du vill ange sammanhanget som en identitet relaterar till, genom att använda värdena i kolumnen Identitetssymbol:

![Vy över namnutrymmesgränssnittet](../assets/identity/edge_namespaceUI_identity-symbol.png)

Som Audience Manager-kund har alla befintliga datakällor som använder ID-typ: Enhetsöverskridande har automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande Identity Namespace för Audience Manager-datakällan loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

Alla nya [!DNL Audience Manager] Datakälla som använder ID-typ: Enheten genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande [!DNL Audience Manager] Datakälla men observera att metoden syncIdentity bara stöder identitetssymboler för namnområde.
