---
title: Web SDK - installationsöversikt
description: Lär dig installera Experience Platform Web SDK.
keywords: web sdk-installation;installera web sdk;Internet Explorer;promise;npm-paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Web SDK - installationsöversikt

Det finns tre sätt att använda Adobe Experience Platform Web SDK som stöds:

1. **[Web SDK-taggtillägg](extension.md)**: Adobe rekommenderar att du använder den här metoden. Installera en tagginläsare på webbplatsen och använd sedan användargränssnittet för Adobe Experience Platform Data Collection för att konfigurera implementeringen.
1. **[Web SDK JavaScript-bibliotek](library.md)**: Referera en CDN-värdbaserad biblioteksfil eller använd din egen infrastruktur som värd för biblioteksfilen. Ring till biblioteket i koden på din webbplats.
1. **[NPM](npm.md)**: Installera Web SDK på webbplatsen med NPM-pakethanteraren.

## Förhandskrav

Innan du använder eller installerar Web SDK måste du uppfylla följande krav:

* Arkitekturen i Adobe Experience Platform måste konfigureras först. Dessa inställningar innehåller nödvändiga scheman, identiteter och datastreams.
* Du måste ha rätt behörighet konfigurerad för att komma åt rätt verktyg. Om din organisation till exempel bestämmer sig för att använda taggtillägget måste du ha rätt behörighet för att komma åt användargränssnittet för datainsamlingen. Mer information finns i [behörighetshantering för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=sv-SE).
* Vi rekommenderar att du har en CNAME-domän. Om du redan har en CNAME för Adobe Analytics kan du använda den. Testning under utveckling fungerar utan CNAME, men Adobe rekommenderar att du gör det innan du publicerar till produktion. Mer information finns i [Enhet-ID för första part](../identity/first-party-device-ids.md).
