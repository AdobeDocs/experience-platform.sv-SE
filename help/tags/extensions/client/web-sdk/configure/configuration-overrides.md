---
title: Åsidosättningsinställningar för dataströmskonfiguration
description: Ändra konfigurationsinställningar när vissa villkor uppfylls.
exl-id: 68227148-3d74-4807-836c-14acd8a9c1dc
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 2%

---

# Åsidosättningsinställningar för dataströmskonfiguration {#config-overrides}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_overrides"
>title="Åsidosättningar av dataströmskonfiguration"
>abstract="Du kan välja att utlösa olika datastream-beteenden utan att behöva använda ett separat datastream. Om du anger åsidosättningar av dataströmskonfigurationer på klientsidan för en miljö i det här avsnittet åsidosätts alla dynamiska datastream-konfigurationer och regler på serversidan för den miljön."

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK. Med den här funktionen kan du villkorligt utlösa olika datastream-beteenden utan att skapa ett nytt datastream eller ändra befintliga inställningar.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Datastream configuration overrides]**.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av datastream-konfigurationen när [en datastream](/help/datastreams/configure.md) konfigureras i datastreams-gränssnittet. Mer information om hur du konfigurerar åsidosättningar finns i [Åsidosättningar av dataströmskonfigurationer](/help/datastreams/overrides.md) i dokumentationen för datastreams.
1. När du har konfigurerat åsidosättningen av datastream i användargränssnittet för datastreams kan du konfigurera taggtillägget.

Åsidosättningar av dataström måste konfigureras per miljö. Utvecklings-, staging- och produktionsmiljöerna har alla olika åsidosättningar. Du kan kopiera åsidosättningsinställningarna mellan olika miljöer:

![Bild som visar åsidosättningar av dataströmskonfigurationer med hjälp av SDK-taggtilläggssidan för webben.](../assets/datastream-overrides.png)

Som standard är åsidosättningar av dataströmskonfigurationer inaktiverade. Alternativet **[!UICONTROL Match datastream configuration]** är markerat som standard.

![Användargränssnittet för SDK-taggtillägget för webben visar att datastream-konfigurationen åsidosätter standardinställningen.](../assets/datastream-override-default.png)

Om du vill aktivera datastream-åsidosättningar i taggtillägget väljer du **[!UICONTROL Enabled]** i listrutan.

![Användargränssnittet för SDK-taggtillägget för webben visar inställningen för åsidosättande av dataströmskonfigurationen.](../assets/datastream-override-enabled.png)

När du har aktiverat åsidosättningar av dataströmskonfigurationer kan du konfigurera åsidosättningar för varje tjänst som beskrivs nedan. Dessa inställningar åsidosätter alla datastream-konfigurationer och regler på serversidan för den valda miljön.

## Adobe Analytics

Åsidosätt datadirigering till Adobe Analytics-tjänsten.

![Användargränssnittsbild för SDK-taggtillägg för webben visar inställningarna för åsidosättning av Adobe Analytics datastream.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Aktivera eller inaktivera dataroutning till Adobe Analytics.
* **[!UICONTROL Report suites]**: ID för målrapportsviterna i Adobe Analytics. Värdet måste vara en förkonfigurerad åsidosättningsrapportssvit (eller en kommaavgränsad lista över rapportsviter) från din datastream-konfiguration. Den här inställningen åsidosätter den primära rapportsviten.
* **[!UICONTROL Add Report Suite]**: Välj det här alternativet om du vill lägga till ytterligare rapportsviter.

## Adobe Audience Manager

Åsidosätt datadirigering till Adobe Audience Manager.

![Användargränssnittsbild för SDK-taggtillägg för webben visar inställningarna för åsidosättning av Adobe Audience Manager datastream.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Aktivera eller inaktivera dataroutning till Adobe Audience Manager.
* **[!UICONTROL Third-party ID sync container]**: ID:t för målets synkroniseringsbehållare för tredjeparts-ID i Audience Manager. Värdet måste vara en förkonfigurerad sekundär behållare från din datastream-konfiguration och åsidosätter den primära behållaren.

## Adobe Experience Platform

Åsidosätt datadirigering till Adobe Experience Platform.

![Användargränssnittsbild för SDK-taggtillägg för webben visar inställningarna för åsidosättning av Adobe Experience Platform datastream.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Aktivera eller inaktivera dataroutning till Adobe Experience Platform.
* **[!UICONTROL Event dataset]**: ID:t för målhändelsedatauppsättningen i Adobe Experience Platform. Värdet måste vara en förkonfigurerad sekundär datauppsättning från din datastream-konfiguration.
* **[!UICONTROL Offer Decisioning]**: Aktivera eller inaktivera dataroutning till tjänsten [!DNL Offer Decisioning].
* **[!UICONTROL Edge Segmentation]**: Aktivera eller inaktivera dataroutning till tjänsten [!DNL Edge Segmentation].
* **[!UICONTROL Personalization Destinations]**: Aktivera eller inaktivera dataroutning till personaliseringsmål.
* **[!UICONTROL Adobe Journey Optimizer]**: Aktivera eller inaktivera dataroutning till [!DNL Adobe Journey Optimizer].

## Händelsevidarebefordran på Adobe-serversidan

Åsidosätt dataroutning till tjänsten Adobe Server-Side Event Forwarding.

![Användargränssnittsbild för SDK-taggtillägg på webben visar inställningarna för åsidosättning av dataströmmen för händelsespårning på Adobe-serversidan.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Aktivera eller inaktivera dataroutning till tjänsten för händelsevidarebefordran på Adobe-serversidan.

## Adobe Target {#target}

Åsidosätt datadirigering till Adobe Target.

![Användargränssnittsbild för SDK-taggtillägg för webben visar inställningarna för åsidosättning av Adobe Target datastream.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: Aktivera eller inaktivera dataroutning till Adobe Target.
