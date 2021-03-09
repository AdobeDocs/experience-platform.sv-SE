---
title: Åtgärdstyper i Adobe Experience Platform Web SDK-tillägget
description: Läs mer om de olika åtgärdstyperna i Adobe Experience Platform Web SDK-tillägget i Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Åtgärdstyper

När du har konfigurerat [Adobe Experience Platform Web SDK-tillägget](web-sdk-extension.md) för [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfigurerar du åtgärdstyperna.

Den här sidan beskriver de tillgängliga åtgärdstyperna.

## Skicka händelse

Skickar en händelse till Adobe [!DNL Experience Platform] så att Adobe Experience Platform kan samla in de data du skickar och agera på dessa uppgifter. Markera en instans (om du har fler än en). Om händelsen inträffar i början av en sidinläsning eller under en vyändring i ett enkelsidigt program väljer du **[!UICONTROL Occurs at the start of a view]**.

Alla data som du vill skicka kan skickas i fältet **[!UICONTROL XDM Data]**. Använd ett JSON-objekt som överensstämmer med XDM-schemats struktur. Objektet kan antingen skapas på sidan eller via en **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Ange samtycke

När du har fått ditt samtycke från din användare måste du meddela Adobe Experience Platform Web SDK genom att använda åtgärdstypen &quot;Ange samtycke&quot;. För närvarande stöds två typer av standarder: &quot;Adobe&quot; och &quot;IAB TCF.&quot; Se [Supporting Customer Consent Preferences](../consent/supporting-consent.md). När du använder Adobe version 2.0 stöds bara ett dataelementvärde. Du måste skapa ett dataelement som matchar det godkända objektet.

I den här åtgärden får du även ett valfritt fält där du kan inkludera en identitetskarta så att identiteter kan synkroniseras när du har fått ditt samtycke. Synkronisering är användbart när medgivandet har konfigurerats som Väntande eller Ut eftersom det är sannolikt det första anropet som utlöses.

## Återställ ID för händelsesammanfogning

Om du vill återställa ditt ID för händelsesammanfogning på sidan kan du göra det med den här åtgärden. Om du vill återställa ditt ID väljer du det sammanfognings-ID som du vill återställa och startar åtgärden efter behov.

## Vad händer nu?

När du har angett åtgärdstyper [konfigurerar du dina dataelementtyper](data-element-types.md).