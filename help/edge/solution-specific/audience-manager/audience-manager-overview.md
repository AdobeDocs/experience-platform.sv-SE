---
title: Skicka data till Adobe Audience Manager
seo-title: Skicka data till Adobe Audience Manager med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Audience Manager med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager på Experience Platform Edge Network

Adobe Experience Platform Web SDK är integrerat med Adobe Audience Manager och har stöd för att skicka och ta emot data från Audience Manager, Cookie- och URL-destinationer och ID-synkronisering.

## Aktivera Audience Manager

Om du vill aktivera Audience Manager måste du göra följande:

- Aktivera Audience Manager i din [edge-konfiguration](../../fundamentals/edge-configuration.md).
- Aktivera eller inaktivera cookie- och URL-mål.
- Ange ID-synkroniseringsbehållaren för externa partnersynkroniseringar (valfritt)

## Synkroniserar identiteter

Adobe Experience Platform Web SDK har stöd för att deklarera kund-ID:n och deras autentiseringstillstånd via [SyncIdentity](../../fundamentals/identity.md) -kommandot.

SynsyncIdentity-metoden använder [Identity Service Namespaces](../../../identity/../identity-service/namespaces.md) för att ange kontexten som en identitet relaterar till. Som Audience Manager-kund använder alla befintliga datakällor som använder ID-typ: Enhetsöverskridande enheter får automatiskt ett motsvarande identitetsnamnutrymme. Om du vill hitta motsvarande Identity Namespace för datakällan i Audience Manager loggar du in på Adobe Experience Platform och navigerar till avsnittet Identiteter.

![Vy över namnutrymmesgränssnittet](../../../assets/edge_configuration_identity.png)

Här kan du söka efter datakällan för Audience Manager utifrån namn. Metoden syncIdentity använder identitetssymbolen för att ange namnutrymmet.

Ny datakälla för Audience Manager som använder ID-typ: Enhetsoberoende genererar ett motsvarande identitetsnamnområde. ID-typerna Cookie och Device Advertising ID stöds för närvarande inte. Dessutom kommer alla identitetsnamnutrymmen som skapas i Adobe Experience Platform att generera en motsvarande datakälla för Audience Manager, men observera att syncIdentity-metoden bara stöder namnområdes-identitetssymboler.
