---
title: Konfigurera Adobe Experience Platform Web SDK-tillägget
description: Konfigurera taggtillägget Adobe Experience Platform Web SDK i användargränssnittet för datainsamling.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Konfigurera Adobe Experience Platform Web SDK-tillägget

Adobe Experience Platform Web SDK-taggtillägget skickar data till Adobe Experience Cloud från webbegenskaper via Adobe Experience Platform Edge Network. Tillägget gör att ni kan strömma data till plattformen, synkronisera identiteter, bearbeta kundens medgivandesignaler och automatiskt samla in kontextdata.

Det här dokumentet beskriver hur du konfigurerar tillägget i användargränssnittet för datainsamling.

## Komma igång

Om plattformstillägget för Web SDK redan har installerats för en egenskap öppnar du egenskapen i användargränssnittet för datainsamling och väljer alternativet **[!UICONTROL Extensions]** -fliken. Under Platform Web SDK väljer du **[!UICONTROL Configure]**.

![](../images/extension/overview/configure.png)

Om du inte har installerat tillägget än väljer du **[!UICONTROL Catalog]** -fliken. Leta reda på plattformstillägget för Web SDK i listan över tillgängliga tillägg och välj **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

I båda fallen kommer du till konfigurationssidan för Platform Web SDK. I avsnitten nedan beskrivs tilläggets konfigurationsalternativ.

![](../images/extension/overview/config-screen.png)

## Allmänna konfigurationsalternativ

Konfigurationsalternativen högst upp på sidan anger för Adobe Experience Platform var data ska skickas och vilka konfigurationer som ska användas på servern.

### [!UICONTROL Name]

Tillägget Adobe Experience Platform Web SDK har stöd för flera instanser på sidan. Namnet används för att skicka data till flera organisationer med en taggkonfiguration.

Tilläggets namn är som standard &quot;[!DNL alloy]&quot;. Du kan dock ändra instansnamnet till ett giltigt JavaScript-objektnamn.

### **[!UICONTROL IMS Organization ID]**

The [!UICONTROL IMS Organization ID] är den organisation som du vill att data skickas till i Adobe. För det mesta använder du standardvärdet som fylls i automatiskt. När du har flera instanser på sidan fyller du i det här fältet med värdet för den andra organisationen som du vill skicka data till.

### **[!UICONTROL Edge Domain]**

The [!UICONTROL Edge Domain] är den domän som Adobe Experience Platform-tillägget skickar och tar emot data från. Adobe rekommenderar att du använder en CNAME (1st-party domain) för det här tillägget. Standarddomänen från tredje part fungerar för utvecklingsmiljöer men är inte lämplig för produktionsmiljöer. Instruktioner om hur du konfigurerar en CNAME från en förstahandsleverantör finns i listan [här](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datastreams]

När en begäran skickas till Adobe Experience Platform Edge Network, används ett datastream-ID för att referera till konfigurationen på serversidan. Du kan uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

Se guiden [datastreams](../datastreams/overview.md) för mer information.


## [!UICONTROL Privacy]

![](../images/extension/overview/privacy.png)

The [!UICONTROL Privacy] I kan du konfigurera hur SDK hanterar användares medgivandesignaler från din webbplats. Det gör i synnerhet att du kan välja den standardnivå för samtycke som antas av en användare om ingen annan explicit inställning har angetts. Standardnivån för samtycke sparas inte i användarens profil. I följande tabell visas vad varje alternativ innebär:

| [!UICONTROL Default Consent Level] | Beskrivning |
| --- | --- |
| [!UICONTROL In] | Samla in händelser som inträffar innan användaren ger sitt samtycke. |
| [!UICONTROL Out] | Ignorera händelser som inträffar innan användaren ger sitt medgivande. |
| [!UICONTROL Pending] | Köhändelser som inträffar innan användaren ger sitt samtycke. När du har angett medgivandeinställningar kommer händelserna att samlas in eller tas bort beroende på vilka inställningar som har angetts. |
| [!UICONTROL Provided by data element] | Standardnivån för samtycke bestäms av ett separat dataelement som du definierar. När du använder det här alternativet måste du ange dataelementet med den angivna listrutan. |

Använd Utgående eller Väntande om du kräver uttryckligt användargodkännande för din affärsverksamhet.

## [!UICONTROL Identity]

![](../images/extension/overview/identity.png)

### [!UICONTROL Migrate ECID from VisitorAPI]

Det här alternativet är aktiverat som standard. När den här funktionen är aktiverad kan SDK läsa AMCV- och s_ecid-cookies och ange den AMCV-cookie som används av Visitor.js. Den här funktionen är viktig när du migrerar till Adobe Experience Platform Web SDK eftersom vissa sidor fortfarande kan använda Visitor.js. SDK kan fortsätta att använda samma ECID så att användare inte identifieras som två separata användare.

### [!UICONTROL Use third-party cookies]

Med det här alternativet kan SDK försöka lagra en användaridentifierare i en cookie från tredje part. Om det lyckas identifieras användaren som en enskild användare när han/hon navigerar mellan flera domäner, i stället för att identifieras som en separat användare på varje domän. Om det här alternativet är aktiverat kanske SDK fortfarande inte kan lagra användaridentifieraren i en tredjeparts-cookie om webbläsaren inte stöder cookies från tredje part eller har konfigurerats av användaren så att cookies från tredje part inte tillåts. I det här fallet lagrar SDK bara identifieraren i förstahandsdomänen.

## [!UICONTROL Personalization]

![](../images/extension/overview/personalization.png)

Om du vill dölja vissa delar av webbplatsen när anpassat innehåll läses in, kan du ange vilka element som ska döljas i den fördolda formatredigeraren. Du kan sedan kopiera det fördolda standardfragmentet som du har fått och klistra in det inuti `<head>`-element på din HTML-webbplats.

## [!UICONTROL Data Collection]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL Callback function]

Callback-funktionen som finns i tillägget kallas också [`onBeforeEventSend` function](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) i biblioteket. Med den här funktionen kan du ändra händelser globalt innan de skickas till Adobe Edge Network. Mer detaljerad information om hur funktionen används finns [här](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Click data collection]

SDK kan automatiskt samla in länkklicksinformation åt dig. Som standard är den här funktionen aktiverad men kan inaktiveras med det här alternativet. Länkarna är även märkta som nedladdningslänkar om de innehåller något av de nedladdningsuttryck som finns i [!UICONTROL Download Link Qualifier] textruta. I Adobe finns vissa standardkvalificerare för nedladdningslänk, men dessa kan redigeras när som helst.

### [!UICONTROL Automatically collected context data]

Som standard samlar SDK in vissa kontextdata för enhet, webb, miljö och platskontext. Om du vill se en lista över den information som samlas in av Adobe kan du hitta den [här](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Om du inte vill att dessa data ska samlas in, eller om du bara vill att vissa kategorier av data ska samlas in, kan du ändra de här alternativen.

## [!UICONTROL Advanced Settings]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL Edge base path]

Använd det här fältet om du behöver ändra grundsökvägen som används för att interagera med Adobe Edge Network. Det här behöver inte uppdateras, men om du deltar i en beta eller alfa kan Adobe be dig att ändra det här fältet.
