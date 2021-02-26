---
title: Adobe Experience Platform Web SDK Extension - översikt
description: Läs mer om Adobe Experience Platform Web SDK-tillägget för Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Adobe Experience Platform Web SDK-tillägg - översikt

Adobe Experience Platform Web SDK-tillägget skickar data till Adobe Experience Cloud från webbegenskaper via Adobe Experience Platform Edge Network. Tillägget gör att ni kan strömma data till plattformen, synkronisera identiteter, bearbeta kundens medgivandesignaler och automatiskt samla in kontextdata.

I det här dokumentet beskrivs hur du konfigurerar tillägget i Adobe Experience Platform Launch användargränssnitt.

## Konfigurera tillägget

Om plattformstillägget för Web SDK redan har installerats för en egenskap öppnar du egenskapen i Platforma launchens användargränssnitt och väljer fliken **[!UICONTROL Extensions]**. Välj **[!UICONTROL Configure]** under Platform Web SDK.

![](../images/extension/overview/configure.png)

Om du inte har installerat tillägget än väljer du fliken **[!UICONTROL Catalog]**. Leta reda på plattformstillägget för Web SDK i listan över tillgängliga tillägg och välj **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

I båda fallen kommer du till konfigurationssidan för Platform Web SDK. I avsnitten nedan beskrivs tilläggets konfigurationsalternativ.

![](../images/extension/overview/config-screen.png)

## Allmänna konfigurationsalternativ

Konfigurationsalternativen högst upp på sidan anger för Adobe Experience Platform var data ska skickas och vilka konfigurationer som ska användas på servern.

### [!UICONTROL Name]

Tillägget Adobe Experience Platform Web SDK har stöd för flera instanser på sidan. Detta används för att skicka data till flera organisationer med en enda konfiguration för Platform launch.

Tilläggets namn är som standard &quot;[!DNL alloy]&quot;. Du kan dock ändra instansnamnet till ett giltigt JavaScript-objektnamn.

### **[!UICONTROL IMS Organization ID]**

[!UICONTROL IMS Organization ID] är den organisation som du vill att data skickas till på Adobe. För det mesta bör du använda standardvärdet som fylls i automatiskt. När du har flera instanser på sidan fyller du i det här fältet med värdet för den andra organisationen som du vill skicka data till.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain] är den domän som Adobe Experience Platform-tillägget skickar och tar emot data från. Tillägget kräver att du använder en CNAME från första part för produktionstrafik. Standarddomänen från tredje part fungerar för utvecklingsmiljöer men är inte lämplig för produktionsmiljöer. Instruktioner om hur du konfigurerar en CNAME från en annan leverantör finns [här](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge Configurations]

När en begäran skickas till Adobe Experience Platform Edge Network används ett edge-konfigurations-ID för att referera till konfigurationen på serversidan. På så sätt kan du uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

Mer information finns i guiden om [kantkonfigurationer](../fundamentals/edge-configuration.md).

## [!UICONTROL Privacy]

I [!UICONTROL Privacy]-avsnittet kan du konfigurera hur SDK hanterar signaler om kundsamtycke från din webbplats. Det gör i synnerhet att du kan välja den standardnivå för samtycke som antas av en kund om ingen annan explicit medgivandepreferens har angetts. I följande tabell visas vad varje alternativ innebär:

| [!UICONTROL Default Consent Level] | Beskrivning |
| --- | --- |
| [!UICONTROL In] | Anmäl dig. Använd det här alternativet om du antar att kunden godkänner det som standard och endast respekterar avanmälningssignaler. |
| [!UICONTROL Pending] | Kunder med &quot;väntande&quot; samtycke antas avanmäla sig tills en anmälningssignal skickas. Använd det här alternativet om du kräver uttryckligt kundgodkännande för din affärsverksamhet. |
| [!UICONTROL Provided by data element] | Standardnivån för samtycke bestäms av ett separat dataelement som du definierar. När du använder det här alternativet måste du ange dataelementet med den angivna listrutan. |