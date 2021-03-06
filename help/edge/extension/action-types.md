---
title: Åtgärdstyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika åtgärdstyperna i taggtillägget Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Åtgärdstyper

Konfigurera åtgärdstyperna när du har konfigurerat taggtillägget [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

Den här sidan beskriver de tillgängliga åtgärdstyperna.


## Skicka händelse

Skickar en händelse till Adobe [!DNL Experience Platform] så att Adobe Experience Platform kan samla in de data du skickar och agera på dessa uppgifter. Markera en instans (om du har fler än en). Alla data som du vill skicka kan skickas i fältet **[!UICONTROL XDM Data]**. Använd ett JSON-objekt som överensstämmer med XDM-schemats struktur. Objektet kan antingen skapas på sidan eller via en **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Det finns några andra fält i åtgärdstypen Skicka händelse som också kan vara användbara beroende på implementeringen. Observera att alla dessa fält är valfria.

- **Typ:** I det här fältet kan du ange en händelsetyp som ska registreras i ditt XDM-schema. Mer information om standardhändelsetyperna finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api).
- **Data:** Data som inte matchar ett XDM-schema kan skickas med det här fältet. Det här fältet är användbart om du försöker uppdatera en Adobe Target-profil eller skicka Target Recommendations-attribut. Se till exempel vår [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Datauppsättnings-ID:** Om du behöver skicka data till en annan datauppsättning än den som du angav i din datastream kan du ange detta datauppsättnings-ID här.
- **Dokumentet tas bort:** Markera  **[!UICONTROL Document will unload]** kryssrutan om du vill kontrollera att händelserna når servern även om användaren navigerar bort från sidan. Detta gör att händelser kan nå servern, men svaren ignoreras.
- **Återge beslut om visuell personalisering:** Markera  **[!UICONTROL Render visual personalization decisions]** kryssrutan om du vill återge anpassat innehåll på sidan. Du kan också ange beslutsomfattningar om det behövs. Mer information om återgivning av anpassat innehåll finns i [personaliseringsdokumentationen](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content).

## Ange samtycke

När du har fått ditt samtycke från din användare måste du meddela Adobe Experience Platform Web SDK genom att använda åtgärdstypen &quot;Ange samtycke&quot;. För närvarande stöds två typer av standarder: &quot;Adobe&quot; och &quot;IAB TCF.&quot; Se [Supporting Customer Consent Preferences](../consent/supporting-consent.md). När du använder Adobe version 2.0 stöds bara ett dataelementvärde. Du måste skapa ett dataelement som matchar det godkända objektet.

I den här åtgärden får du även ett valfritt fält där du kan inkludera en identitetskarta så att identiteter kan synkroniseras när du har fått ditt samtycke. Synkronisering är användbart när medgivandet har konfigurerats som Väntande eller Ut eftersom det är sannolikt det första anropet som utlöses.

## Återställ ID för händelsesammanfogning

Om du vill återställa ditt ID för händelsesammanfogning på sidan kan du göra det med den här åtgärden. Om du vill återställa ditt ID väljer du det sammanfognings-ID som du vill återställa och startar åtgärden efter behov.

## Vad händer nu?

När du har angett åtgärderna [konfigurerar du dina dataelementtyper](data-element-types.md).
