---
title: Adobe Audience Manager Extension - översikt
description: Lär dig om Adobe Audience Manager-taggtillägget i Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 3%

---

# Översikt över Adobe Audience Manager-tillägg

Med taggtillägget Audience Manager kan du integrera den DIL-kod som används av Audience Manager med dina egenskaper i Adobe Experience Platform.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

>[!NOTE]
>
>Det här tillägget är inte avsett att användas för händelsevidarebefordran av Adobe Analytics-data. Använd [Adobe Analytics-tillägget](../analytics/overview.md) för vidarebefordran av händelser.

## Konfigurera Adobe Audience Manager-tillägget

Om Adobe Audience Manager-tillägget ännu inte är installerat öppnar du din egenskap, väljer **[!UICONTROL Extensions > Catalog]**, håller pekaren över Adobe Audience Manager-tillägget och väljer **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken [!UICONTROL Extensions], håller pekaren över tillägget och väljer **[!UICONTROL Configure]**.

### DIL-inställningar

Konfigurera dina DIL-inställningar. Följande konfigurationsalternativ är tillgängliga:

![](../../../images/ext-aam-config.png)

#### DIL Version

Visar Data Integration Library-versionen (DIL).

Den här inställningen kan inte ändras.

#### Uteslut särskilda sökvägar

Om URL:en matchar någon av de uteslutna sökvägarna läses tillägget inte in.

Välj **[!UICONTROL Add Path]** om du vill ange en exkluderad URL.

Aktivera Regex om URL:en är ett reguljärt uttryck.

#### Använd DIL Site Catalyst-modulen

[SiteCatalyst-modulen](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html) fungerar med DIL för att skicka Analytics-taggelement till Audience Manager.

Använd kodredigeraren för att konfigurera filen siteCatalyst.init.

Du kan också skapa en anteckning som innehåller information om den här konfigurationen.

#### Använd DIL Google Analytics-modulen

Aktivera [Google Analytics-modulen](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html).

#### DIL.create Initialization Properties

Lägg till initieringsegenskaper som används av [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) och namnutrymmesunderegenskapen för [visitorService-objektet](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html). Det finns två exempel på användning i kodkommentarerna i kodredigeraren.

Välj **[!UICONTROL Choose an Item]** om du vill lägga till fler egenskaper.

Håll muspekaren över ikonerna för att se vad varje egenskap gör. Mer information om egenskaperna finns i [Audience Manager DIL-dokumentationen](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html).

Välj **[!UICONTROL Save]** när du har slutfört konfigurationen av tillägget.

## Åtgärdstyper för Adobe Audience Manager-tillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Audience Manager-tillägget.

Tillägget Adobe Audience Manager innehåller följande åtgärder i delen Sedan i en regel:

### Kör anpassad kod

Kör den anpassade koden som konfigurerats i kodredigeraren.

Ange önskad kod i kodredigeraren och ange sedan ett namn för koden. Den här koden blir tillgänglig i delen Sedan i regelbyggaren.

![](../../../images/ext-aam-then.png)

Du kan också lägga till en anteckning med information om konfigurationen.
