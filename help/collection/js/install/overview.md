---
title: Web SDK - installationsöversikt
description: Lär dig installera Experience Platform Web SDK.
keywords: web sdk-installation;installera web sdk;Internet Explorer;promise;npm-paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Web SDK - installationsöversikt

Det finns tre sätt att använda Adobe Experience Platform Web SDK:

1. **[Webbtaggtillägg för SDK](/help/tags/extensions/client/web-sdk/overview.md)**: Adobe rekommenderar att du använder den här metoden. Installera en tagginläsare på webbplatsen och använd sedan användargränssnittet för Adobe Experience Platform Data Collection för att konfigurera implementeringen.
1. **[Webbbibliotek för SDK JavaScript](library.md)**: Referera till en CDN-värdbiblioteksfil eller använd din egen infrastruktur som värd för biblioteksfilen. Ring till biblioteket i koden på din webbplats.
1. **[NPM](npm.md)**: Installera Web SDK på din webbplats med NPM-pakethanteraren.

## Förhandskrav

Innan du använder eller installerar Web SDK måste du uppfylla följande krav:

* Arkitekturen i Adobe Experience Platform måste konfigureras först. Dessa inställningar innehåller nödvändiga scheman, identiteter och datastreams.
* Du måste ha rätt behörighet konfigurerad för att komma åt rätt verktyg. Om din organisation till exempel bestämmer sig för att använda taggtillägget måste du ha rätt behörighet för att komma åt användargränssnittet för datainsamlingen. Mer information finns i [Behörigheter för datainsamling](../../permissions.md).
* Vi rekommenderar att du har en CNAME-domän. Om du redan har en CNAME för Adobe Analytics kan du använda den. Testning under utveckling fungerar utan CNAME, men Adobe rekommenderar att du gör det innan du publicerar till produktion. Mer information finns i [Enhet-ID för första part](../../use-cases/identity/first-party-device-ids.md).
