---
title: Skicka data till Adobe Audience Manager
seo-title: Skicka data till Adobe Audience Manager med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager på Experience Platform Edge-nätverket

Adobe Experience Platform Web SDK är integrerat med Adobe Audience Manager och har stöd för att skicka och ta emot data från Audience Manager, Cookie och URL-destinationer samt synkning av ID.

## Aktivera Audience Manager

För att aktivera Audience Manager måste du göra följande:

- Aktivera Audience Manager i [kantkonfigurationen](../../fundamentals/edge-configuration.md).
- Aktivera eller inaktivera cookie- och URL-mål.
- Ange ID-synkroniseringsbehållaren för externa partnersynkroniseringar (valfritt)

## Synkroniserar identiteter

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via [SyncIdentity](../../fundamentals/identity.md) .

SynsyncIdentity-metoden använder [Identity Service Namespaces](../../../identity/../identity-service/namespaces.md) för att ange kontexten som en identitet relaterar till. Som Audience Manager-kund använder du alla befintliga datakällor som använder ID-typ: Enhetsöverskridande enheter får automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande ID-namnområde för Audience Manager-datakällan loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

![Vy över namnutrymmesgränssnittet](../../../assets/edge_configuration_identity.png)

Här kan du söka efter Audience Manager-datakällan efter namn. Metoden syncIdentity använder identitetssymbolen för att ange namnutrymmet.

Ny Audience Manager-datakälla som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Alla Identity Namespace som skapas i Adobe Experience Platform genererar dessutom en motsvarande Audience Manager-datakälla, men observera att syncIdentity-metoden bara stöder Namespace Identity Symbols.
