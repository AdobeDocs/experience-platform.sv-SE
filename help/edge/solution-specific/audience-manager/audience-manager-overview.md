---
title: Skicka data till Adobe Audience Manager
seo-title: Skicka data till Adobe Audience Manager med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] på [!DNL Experience Platform Edge Network]

Adobe Experience Platform [!DNL Web SDK] är integrerat med Adobe Audience Manager och stöder sändning och mottagning av data från [!DNL Audience Manager]Cookie- och URL-destinationer samt ID-synkronisering.

## Aktivering [!DNL Audience Manager]

Du måste göra följande för att [!DNL Audience Manager] kunna aktivera:

- Aktivera [!DNL Audience Manager] i [edge-konfigurationen](../../fundamentals/edge-configuration.md).
- Aktivera eller inaktivera cookie- och URL-mål.
- Ange ID-synkroniseringsbehållaren för externa partnersynkroniseringar (valfritt)

## Synkroniserar identiteter

Adobe Experience Platform [!DNL Web SDK] kan deklarera kund-ID:n och deras autentiseringstillstånd via [SyncIdentity](../../fundamentals/identity.md) -kommandot.

SynsyncIdentity-metoden använder [Identity Service Namespaces](../../../identity/../identity-service/namespaces.md) för att ange kontexten som en identitet relaterar till. Som [!DNL Audience Manager] kund använder alla befintliga datakällor som använder ID-typ: Enhetsöverskridande enheter får automatiskt en motsvarande [!DNL Identity Namespace]. Om du vill hitta motsvarande [!DNL Identity Namespace] fil [!DNL Audience Manager Data Source]loggar du in på Adobe Experience Platform och går till [!DNL Identities] avsnittet.

![Vy över namnutrymmesgränssnittet](../../../assets/edge_configuration_identity.png)

Här kan du söka efter din [!DNL Audience Manager] datakälla efter namn. Metoden syncIdentity använder identitetssymbolen för att ange namnutrymmet.

Ny [!DNL Audience Manager] datakälla som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande [!DNL Audience Manager] datakälla, men observera att syncIdentity-metoden bara stöder Namespace Identity Symbols.
