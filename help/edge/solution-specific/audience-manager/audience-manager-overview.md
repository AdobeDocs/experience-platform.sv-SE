---
title: Skicka data till Adobe Audience Manager
seo-title: Skicka data till Adobe Audience Manager med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] på [!DNL Experience Platform Edge Network]

Adobe Experience Platform [!DNL Web SDK] är integrerat med Adobe Audience Manager och har stöd för att skicka och ta emot data från [!DNL Audience Manager], cookies- och URL-mål samt synkning av ID.

## Aktivering [!DNL Audience Manager]

Du måste göra följande för att [!DNL Audience Manager] kunna aktivera:

- Aktivera [!DNL Audience Manager] i [edge-konfigurationen](../../fundamentals/edge-configuration.md).
- Aktivera eller inaktivera cookie- och URL-mål.
- Ange ID-synkroniseringsbehållaren för externa partnersynkroniseringar (valfritt)

## Synkroniserar identiteter

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via kommandot [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Välj dina namnutrymmen från [identitetstjänstens namnutrymmen](../../../identity/../identity-service/namespaces.md) för att ange i vilken kontext en identitet relateras, genom att använda värdena i kolumnen Identitetssymbol:

![Vy över namnutrymmesgränssnittet](../../../assets/edge_namespaceUI_identity-symbol.png)

Som Audience Manager-kund använder du alla befintliga datakällor som använder ID-typ: Enhetsövergripande enheter har automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande Identity Namespace för Audience Manager-datakällan loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

Ny [!DNL Audience Manager] datakälla som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande [!DNL Audience Manager] datakälla, men observera att syncIdentity-metoden endast stöder Namespace Identity Symbols.
