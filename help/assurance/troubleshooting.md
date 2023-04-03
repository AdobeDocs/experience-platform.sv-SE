---
title: Adobe Experience Platform Assurance - felsökningsguide
description: I det här dokumentet beskrivs lösningar på vanliga problem när du använder Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---


# Felsöka Adobe Experience Platform Assurance

Om du har problem med att få Assurance att fungera kan du läsa förslagen under följande problemämnen för att lösa vanliga problem.

För att möjliggöra en smidigare implementering och för att upptäcka eventuella problem måste du ha aktiverat SDK-loggning per [Aktivera felsökningsloggning](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) i avsnittet Komma igång.

Du kan ändra SDK-loggnivåer med [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problem med appar på enheten

### QR-koden öppnar inte appen

* Öppna länken direkt. Kopiera länken från **Sessionsinformation**. Klistra in den i webbläsarens adressfält på enheten för att öppna den. Om den inte öppnas, se avsnittet [Programmet öppnar inte länken](#app-does-not-open-link).
* Använd en annan QR-läsare. För iOS 11 eller senare använder du fotoappen för att läsa QR-koden.

### Programmet öppnar inte länken

* Kontrollera att implementeringen av djuplänkarna är korrekt konfigurerad i appen.
   * **Android:** Djupa länkar (applänkar)
      * [Skapa djupa länkar till appsammanhang](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Anpassat URL-schema eller universella länkar
      * [Definiera ett anpassat URL-schema för din app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Stöd för universella länkar i din app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>För Android är `startSession` API behöver inte anropas explicit. För iOS använder du API:t enligt beskrivningen i [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Autentiseringsövertäckning visas, men appen kan inte ansluta

* Kontrollera enhetens internetanslutning via enhetens webbläsare.
* Om appen aldrig har anslutit till Assurance-tjänsten kontrollerar du att den är korrekt konfigurerad för Assurance. Se instruktionerna för hur du installerar [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK-bibliotek.
* Kontrollera att sessionen matchar länken och att den har angetts korrekt för den förväntade sessionen. Se [Loggmeddelandet&quot;OrgID-information är inte tillgänglig&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (detta är ovanligt och relevant endast om du har tillgång till mer än en ORG-instans).

### Adobe Analytics Debugging

**Status för efterbearbetning - ingen felsökningsflagga**

I vyn Analyshändelser kan det hända att din aktuella Adobe Analytics- eller Assurance SDK-version inte stöder felsökningsfunktionen om händelser inte fungerar med statusen &quot;Ingen felsökningsflagga&quot; efter bearbetning.
Uppgradera Adobe Analytics- och Assurance SDK-tilläggen till de senaste versionerna för att lösa problemet.

| Minsta versionskrav | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Säkerhet | > 1.0.0 | > 1.0.0 |

### Kompatibilitet med inbyggda MobileCore och AEPAssurance

| AEP Assurance-version | Mobile Core-version | Installera instruktion |
| --------------------- | ------------------- | ------------------- |
| response-native-aepsurance v2.x.x | [reaktionsnative-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| response-native-aepsurance v3.x.x | [reaktionsnative-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Om du använder `react-native-acpcore` Med Assurance kan React Native-programmet inte byggas med något av följande felmeddelanden:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

eller

```
AppDelegate: AEPAssurance.h file not found
```

**Lösning**

Om det inträffar ska du nedgradera `react-native-aepassurance` med följande npm-kommando:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Det här felet inträffar eftersom `react-native-acpcore` tillägget är **endast** kompatibel med `react-native-aepassurance` version 2.x.x och tidigare.
