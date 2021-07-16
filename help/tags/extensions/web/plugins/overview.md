---
title: Översikt över Common Analytics-tillägg
description: Lär dig mer om taggtillägget för Common Analytics i Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Översikt över tillägg för Common Analytics-plugin-program

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Använd den här referensen för information om hur du konfigurerar tillägget Common Analytics Plugins och de alternativ som är tillgängliga när du använder det här tillägget för att förstärka tillägget [!DNL Adobe Analytics].

## Konfigurera tillägget för Common Analytics-plugin-program

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar tillägget för Common Analytics-plugin-program.

>[!IMPORTANT]
>
>Tillägget för Common Analytics-plugin utökar tillägget [!DNL Adobe Analytics]. Tillägget [!DNL Adobe Analytics] måste vara installerat på egenskapen för att det ska fungera. Dessutom måste du göra spåraren globalt åtkomlig i tillägget [!DNL Adobe Analytics].

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

I den här åtgärden kan du välja varje plugin som du vill ta med i implementeringen och spara ändringarna. Välj så många eller så få som du vill använda under implementeringen. Länkar till dokumentation om hur du använder varje plugin-program och en kort beskrivning finns i Analytics [Plug-ins overview](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html).

### Initiera plugin-program

Dessa åtgärder initierar det specifika plugin-program som du tänker använda individuellt. Om du vill initiera alla plugin-program som du vill använda i egenskapen lägger du bara till motsvarande åtgärd i regeln och sparar regeln. Även om det är lite svårare att konfigurera tillägget på det här sättet ger det bättre kodeffektivitet. Adobe rekommenderar därför detta tillvägagångssätt.

## Dataelement för tillägg till Common Analytics-plugin-program

I det här avsnittet beskrivs de dataelement som finns i tillägget Plugin-program för Common Analytics.

### getGeoCoordinates

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling i Adobe Experience Platform för att konfigurera och konfigurera plugin-programmet getGeoCoordinates.

### getNewRepeat

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getNewRepeat.

### getPageName

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getPageName.

### getResponsiveLayout

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getResponsiveLayout.

### getTimeParting

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getTimeParting.

### getTimeSinceLastVisit

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getTimeSinceLastVisit.

### getVisitDuration

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getVisitDuration.

### getVisitNum

Användare kan utnyttja det inbyggda användargränssnittet för datainsamling för att konfigurera och konfigurera plugin-programmet getVisitNum.
