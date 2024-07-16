---
title: Adobe Experience Platform Assurance - felsökningsguide
description: I det här dokumentet beskrivs lösningar på vanliga problem när du använder Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Felsöka Adobe Experience Platform Assurance

Om du har problem med att få Assurance att fungera kan du läsa förslagen under följande problemämnen för att lösa vanliga problem.

För att möjliggöra en smidigare implementering och för att upptäcka eventuella problem måste du ha aktiverat SDK-loggning per [Aktivera felsökningsloggning](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) i avsnittet Komma igång.

Du kan ändra SDK-loggnivåer med API:t [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel).

## Problem med appar på enheten

### QR-koden öppnar inte appen

* Öppna länken direkt. Kopiera länken från **sessionsinformation**. Klistra in den i webbläsarens adressfält på enheten för att öppna den. Om den inte öppnas kan du läsa avsnittet [Länken ](#app-does-not-open-link) öppnas inte i appen.
* Använd en annan QR-läsare. För iOS 11 eller senare använder du fotoappen för att läsa QR-koden.

### Appen öppnar inte länken

* Kontrollera att implementeringen av djuplänkarna är korrekt konfigurerad i appen.
   * **Android:** Djupa länkar (applänkar)
      * [Skapa djupa länkar till appkontext](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Anpassat URL-schema eller universella länkar
      * [Definiera ett anpassat URL-schema för din app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Supporting Universal Links in your app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>För Android behöver `startSession`-API:t inte anropas explicit. För iOS använder du API:t enligt beskrivningen i [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Autentiseringsövertäckning visas, men appen kan inte ansluta

* Kontrollera enhetens internetanslutning via enhetens webbläsare.
* Om appen aldrig har anslutit till Assurance-tjänsten kontrollerar du att den är korrekt konfigurerad för Assurance. Se instruktionerna om hur du installerar [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK-biblioteket.
* Kontrollera att sessionen matchar länken och att den har angetts korrekt för den förväntade sessionen. Se [Loggmeddelandet &quot;OrgID-information är inte tillgänglig&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (detta är ovanligt och relevant endast om du har tillgång till mer än en ORG-instans).

### Adobe Analytics Debugging

**Bearbetningsstatus för Post - ingen felsökningsflagga**

I vyn Analyshändelser kan det hända att din nuvarande Adobe Analytics- eller Assurance SDK-version inte stöder felsökningsfunktionen om händelser inte fungerar med Post-processstatus &quot;Ingen felsökningsflagga&quot;.
Uppgradera Adobe Analytics- och Assurance SDK-tilläggen till de senaste versionerna för att lösa problemet.

| Minsta versionskrav | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Säkerhet | > 1.0.0 | > 1.0.0 |

### Kompatibilitet med React Native MobileCore och AEPAssurance

| AEP Assurance-version | Mobile Core-version | Installera instruktion |
| --------------------- | ------------------- | ------------------- |
| response-native-aepsurance v2.x.x | [response-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| response-native-aepsurance v3.x.x | [response-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Om du använder `react-native-acpcore` med Assurance kan React Native-programmet inte byggas med något av följande felmeddelanden:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

eller

```
AppDelegate: AEPAssurance.h file not found
```

**Lösning**

Om det inträffar, bör du nedgradera `react-native-aepassurance` med följande npm-kommando:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Det här felet inträffar eftersom tillägget `react-native-acpcore` är **endast** kompatibelt med `react-native-aepassurance` version 2.x.x och tidigare.
