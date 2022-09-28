---
title: Översikt över Common Analytics-tillägg
description: Läs mer om taggtillägget för Common Analytics i Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Översikt över tillägg för Common Analytics-plugin-program

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Använd den här referensen för information om hur du konfigurerar tillägget Common Analytics Plugins och de alternativ som är tillgängliga när du använder det här tillägget för att förstärka [!DNL Adobe Analytics] Tillägg.

## Konfigurera tillägget för Common Analytics-plugin-program

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar tillägget Common Analytics-plugin-program.

>[!IMPORTANT]
>
>Tillägget Common Analytics Plugins utökar [!DNL Adobe Analytics] tillägg. Du måste ha [!DNL Adobe Analytics] tillägget är installerat på din egenskap för att det ska fungera. Dessutom måste du göra spåraren globalt åtkomlig i dialogrutan [!DNL Adobe Analytics] tillägg.

Ingen ytterligare konfiguration krävs på tilläggsnivån.

## Lägga till plugin-program i [!DNL Adobe Analytics] extension

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

Dessa åtgärder initierar det specifika plugin-program som du tänker använda individuellt. Om du vill initiera alla plugin-program som du vill använda i egenskapen lägger du bara till motsvarande åtgärd i regeln och sparar regeln. Även om det är lite svårare att konfigurera tillägget på det här sättet ger det bättre kodeffektivitet. Adobe rekommenderar därför detta tillvägagångssätt.

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
>Mer information om plugin-programmen ovan finns i [Analysdokumentation](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html).
