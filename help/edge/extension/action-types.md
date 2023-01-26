---
title: Åtgärdstyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika åtgärdstyperna i taggtillägget Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Åtgärdstyper

När du har konfigurerat [Adobe Experience Platform Web SDK-taggtillägg](web-sdk-extension-configuration.md)konfigurerar du åtgärdstyperna.

Den här sidan beskriver de tillgängliga åtgärdstyperna.


## Skicka händelse

Skickar en händelse till Adobe [!DNL Experience Platform] så att Adobe Experience Platform kan samla in de data ni skickar och agera utifrån dessa. Markera en instans (om du har fler än en). Alla data som du vill skicka kan skickas i **[!UICONTROL XDM Data]** fält. Använd ett JSON-objekt som överensstämmer med XDM-schemats struktur. Objektet kan antingen skapas på sidan eller via en **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Det finns några andra fält i åtgärdstypen Skicka händelse som också kan vara användbara beroende på implementeringen. Observera att alla dessa fält är valfria.

- **Typ:** I det här fältet kan du ange en händelsetyp som ska registreras i XDM-schemat. Se [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) om du vill ha mer information om standardhändelsetyperna.
- **Data:** Data som inte matchar ett XDM-schema kan skickas med det här fältet. Det här fältet är användbart om du försöker uppdatera en Adobe Target-profil eller skicka Target Recommendations-attribut. Se exempel i vår [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Datauppsättnings-ID:** Om du behöver skicka data till en annan datauppsättning än den som du angav i din datastream, kan du ange detta datauppsättnings-ID här.
- **Dokumentet tas bort:** Om du vill vara säker på att händelserna når servern även om användaren navigerar bort från sidan, ska du kontrollera **[!UICONTROL Document will unload]** kryssrutan. Detta gör att händelser kan nå servern, men svaren ignoreras.
- **Återge beslut om visuell personalisering:** Om du vill återge anpassat innehåll på sidan ska du kontrollera **[!UICONTROL Render visual personalization decisions]** kryssrutan. Du kan också ange beslutsomfattningar och/eller ytor om det behövs. Se [personaliseringsdokumentation](../personalization/rendering-personalization-content.md#automatically-rendering-content) om du vill ha mer information om återgivning av anpassat innehåll.

## Ange samtycke

När du har fått ditt samtycke från din användare måste du meddela Adobe Experience Platform Web SDK genom att använda åtgärdstypen &quot;Ange samtycke&quot;. För närvarande stöds två typer av standarder: &quot;Adobe&quot; och &quot;IAB TCF.&quot; Se [Stöd för inställningar för kundsamtycke](../consent/supporting-consent.md). När du använder Adobe version 2.0 stöds bara ett dataelementvärde. Du måste skapa ett dataelement som matchar det godkända objektet.

I den här åtgärden får du även ett valfritt fält där du kan inkludera en identitetskarta så att identiteter kan synkroniseras när du har fått ditt samtycke. Synkronisering är användbart när medgivandet har konfigurerats som Väntande eller Ut eftersom det är sannolikt det första anropet som utlöses.

## Återställ ID för händelsesammanfogning

Om du vill återställa ditt ID för händelsesammanfogning på sidan kan du göra det med den här åtgärden. Om du vill återställa ditt ID väljer du det sammanfognings-ID som du vill återställa och startar åtgärden efter behov.

## Vad händer nu?

När du har ställt in dina åtgärder [konfigurera dina dataelementtyper](data-element-types.md).
