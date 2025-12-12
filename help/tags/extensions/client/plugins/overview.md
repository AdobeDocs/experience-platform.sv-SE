---
title: Översikt över Common Analytics-tillägg
description: Läs mer om taggtillägget för Common Analytics i Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Översikt över tillägg för Common Analytics-plugin-program

Använd den här referensen för information om hur du konfigurerar tillägget för Common Analytics-plugin-program och de alternativ som är tillgängliga när du använder det här tillägget för att förstärka tillägget [!DNL Adobe Analytics].

## Konfigurera tillägget för Common Analytics-plugin-program

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar tillägget för Common Analytics-plugin-program.

>[!IMPORTANT]
>
>Tillägget för Common Analytics-plugin utökar tillägget [!DNL Adobe Analytics]. Tillägget [!DNL Adobe Analytics] måste vara installerat på din egenskap för att det ska fungera. Dessutom måste du göra spåraren globalt åtkomlig i tillägget [!DNL Adobe Analytics].

Ingen ytterligare konfiguration krävs på tilläggsnivån.

## Lägger till plugin-program i tillägget [!DNL Adobe Analytics]

För att kunna använda de plugin-program som ingår i det här tillägget måste du först initiera de plugin-program som du tänker använda i sin egen regel.

1. Skapa en ny regel.
1. Lägg till händelsen Core - Library Loaded (Page Top).
1. Använd någon av initieringsmetoderna nedan.

## Åtgärdstyper för tillägg för Common Analytics-plugin-program

I det här avsnittet beskrivs de åtgärdstyper som finns i tillägget Plugin-program för Common Analytics.

Tillägget Common Analytics Plugins innehåller följande åtgärder:

* [Initiera](#initialize)
* [Initiera plugin-program](#initialize-plugin)

### Initiera

>[!IMPORTANT]
>
>Denna åtgärd är enklare att implementera, men Adobe Consulting rekommenderar inte att du använder den här åtgärden eftersom plugin-programmets vikt ökar.

I den här åtgärden kan du välja varje plugin som du vill ta med i implementeringen och spara ändringarna. Välj så många eller så få som du vill använda under implementeringen.

### Initiera plugin-program

Dessa åtgärder initierar det specifika plugin-program som du tänker använda individuellt. Om du vill initiera alla plugin-program som du vill använda i egenskapen lägger du bara till motsvarande åtgärd i regeln och sparar regeln. Även om det är lite svårare att konfigurera tillägget på det här sättet ger det bättre kodeffektivitet. Därför rekommenderar Adobe den här metoden.

## Dataelement för tillägg till Common Analytics-plugin-program

Följande dataelement finns i tillägget Common Analytics-plugin-program, som använder taggfunktioner för att konfigurera och konfigurera motsvarande plugin-program i Analytics:

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>Mer information om ovanstående plugin-program finns i [Analytics-dokumentationen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=sv-SE).
