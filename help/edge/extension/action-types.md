---
title: Åtgärdstyper för plattforms-SDK-tillägg
description: Åtgärdstyper för Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Åtgärdstyper

När du har konfigurerat [Adobe Experience Platform Web SDK-tillägget](web-sdk-extension.md) för [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfigurerar du åtgärdstyperna.

Den här sidan beskriver de tillgängliga åtgärdstyperna.

## Skicka händelse

Skickar en händelse till Adobe [!DNL Experience Platform] så att Adobe Experience Platform kan samla in de data du skickar och agera på dessa uppgifter. Du måste markera en instans (om du har fler än en). Om händelsen inträffar i början av en sidinläsning eller under en vyändring i ett enkelsidigt program väljer du **[!UICONTROL Occurs at the start of a view]**.

Alla data som du vill skicka kan skickas i fältet **[!UICONTROL XDM Data]**. Detta ska vara ett JSON-objekt som följer strukturen i XDM-schemat. Objektet kan antingen skapas på sidan eller via en **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Ange samtycke

När du har fått ditt samtycke från din användare måste detta meddelas Adobe Experience Platform Web SDK. Det gör du genom att använda åtgärdstypen Ange samtycke. För närvarande stöds två typer av standarder: &quot;Adobe&quot; och &quot;IAB TCF.&quot; Om du använder Adobe-standarden kan du för närvarande ange medgivandet som&quot;In&quot;,&quot;Ut&quot;, eller så kan du ange det med ett dataelement. Om du använder IAB TCF-standarden anger du version och värde som du vill använda samt ytterligare information om GDPR.

I den här åtgärden får du även ett valfritt fält för att inkludera en identitetskarta, så att identiteter kan synkroniseras när samtycke tas emot. Detta kan vara användbart när samtycke har konfigurerats som Väntande eftersom samtalet troligtvis blir det första samtalet som utlöses.

## Återställ ID för händelsesammanfogning

Om du vill återställa ditt ID för händelsesammanfogning på sidan kan du göra det med den här åtgärden. Om du vill återställa ditt ID måste du välja det sammanfognings-ID som du vill återställa och starta åtgärden efter behov.

## Vad händer nu?

När du har angett åtgärdstyper [konfigurerar du dina dataelementtyper](data-element-types.md).