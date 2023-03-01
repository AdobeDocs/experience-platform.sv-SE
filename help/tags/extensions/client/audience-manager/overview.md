---
title: Adobe Audience Manager Extension - översikt
description: Lär dig om Adobe Audience Manager-taggtillägget i Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Översikt över Adobe Audience Manager-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Med taggtillägget Audience Manager kan du integrera DIL-koden som används av Audience Manager med dina egenskaper i Adobe Experience Platform.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

>[!NOTE]
>
>Tillägget är inte avsett för händelsevidarebefordran av Adobe Analytics-data. Om du vill vidarebefordra en händelse använder du [Adobe Analytics-tillägg](../analytics/overview.md).

## Konfigurera Adobe Audience Manager-tillägget

Om Adobe Audience Manager-tillägget inte är installerat ännu öppnar du din egenskap och väljer **[!UICONTROL Extensions > Catalog]** hovra över Adobe Audience Manager-tillägget och välj **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du [!UICONTROL Extensions] hovra över tillägget och välj **[!UICONTROL Configure]**.

### Inställningar för DIL

Konfigurera inställningarna för DIL. Följande konfigurationsalternativ är tillgängliga:

![](../../../images/ext-aam-config.png)

#### DIL version

Visar Datans Integration Library (DIL) version.

Den här inställningen kan inte ändras.

#### Uteslut särskilda sökvägar

Om URL:en matchar någon av de uteslutna sökvägarna läses tillägget inte in.

Välj **[!UICONTROL Add Path]** för att ange en exkluderad URL.

Aktivera Regex om URL:en är ett reguljärt uttryck.

#### Använd DIL Site Catalyst-modulen

The [Modulen SiteCatalyst](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html) fungerar med DIL för att skicka Analytics-taggelement till Audience Manager.

Använd kodredigeraren för att konfigurera filen siteCatalyst.init.

Du kan också skapa en anteckning som innehåller information om den här konfigurationen.

#### Använd modulen DIL Google Analytics

Aktivera [Modulen Google Analytics](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html).

#### DIL.skapa initieringsegenskaper

Lägg till initieringsegenskaper som används av [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) och delegenskapen namespace för [visitorService-objekt](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html). Det finns två exempel på användning i kodkommentarerna i kodredigeraren.

Välj **[!UICONTROL Choose an Item]** om du vill lägga till ytterligare egenskaper.

Håll muspekaren över ikonerna för att se vad varje egenskap gör. Mer information om egenskaperna finns i [Dokumentation för Audience Manager DIL](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html).

Välj **[!UICONTROL Save]** när du har konfigurerat tillägget.

## Åtgärdstyper för Adobe Audience Manager-tillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i tillägget Audience Manager.

Tillägget Adobe Audience Manager innehåller följande åtgärder i delen Sedan i en regel:

### Kör anpassad kod

Kör den anpassade koden som är konfigurerad i kodredigeraren.

Ange önskad kod i kodredigeraren och ange sedan ett namn för koden. Den här koden blir tillgänglig i delen Sedan i regelbyggaren.

![](../../../images/ext-aam-then.png)

Du kan också lägga till en anteckning med information om konfigurationen.
