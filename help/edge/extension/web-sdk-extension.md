---
title: Adobe Experience Platform Web SDK-tillägg
seo-title: Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
description: Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
seo-description: Adobe Experience Platform Web SDK Extension Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# Adobe Experience Platform Web SDK-tillägg för Platform Launch

Adobe Experience Platform Web SDK Extension skickar data till Adobe Experience Cloud från webbegenskaper via Adobe Experience Platform Edge Network. Med Adobe Experience Platform Web SDK-tillägget kan du strömma data till olika plattformar, synkronisera identiteter, anmäla dig och automatiskt samla in kontextdata.

## Konfigurera AEP Web SDK-tillägget

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar Adobe Experience Platform Web SDK-tillägget.

Om Adobe Experience Platform Web SDK-tillägget inte är installerat ännu öppnar du din egenskap, väljer **[!UICONTROL Extensions > Catalog]**, hovrar över Adobe Experience Platform Web SDK-tillägget och väljer **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken **[!UICONTROL Extensions]**, håller pekaren över tillägget och väljer **[!UICONTROL Configure]**.

![](./assets/ext-aep-config.png)

### Instansnamn

Tillägget Adobe Experience Platform Web SDK har stöd för flera instanser på sidan. Detta används för att skicka data till flera organisationer med en enda Adobe Experience Platform Launch-konfiguration. **[!UICONTROL Name]** är som standard legerat. Du kan dock ändra instansnamnet till ett giltigt JavaScript-objektnamn. Adobe Experience Platform-tillägget kräver att alla instanser har olika **[!UICONTROL Config ID]** och olika **[!UICONTROL Organization ID]**.

## **[!UICONTROL Config ID]**

**[!UICONTROL Config ID]** är vad som anger för Adobe Experience Platform var data ska dirigeras och vilka konfigurationer som ska användas på servern. Detta krävs för att Adobe Experience Platform-tillägget ska fungera. Du kan få ett konfigurations-ID genom att kontakta kundtjänst.


### **[!UICONTROL Organization ID]**

**[!UICONTROL Organization ID]** är den organisation som du vill att data skickas till på Adobe. För det mesta bör du använda standardvärdet som fylls i automatiskt. När du har flera instanser på sidan fyller du i värdet för den andra organisationen som du vill skicka data till.

### **[!UICONTROL Edge Domain]**

**[!UICONTROL Edge Domain]** är den domän som Adobe Experience Platform-tillägget skickar och tar emot data från. Tillägget kräver att du använder en CNAME från första part för produktionstrafik. Standarddomänen från tredje part fungerar för utvecklingsmiljöer men är inte lämplig för produktionsmiljöer. Instruktioner om hur du konfigurerar en CNAME från en annan leverantör finns [här](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Enable Errors]**

Om ett fel med tillägget uppstår loggas felet som standard i konsolen. Om du vill dölja felen i en produktionsmiljö kan du avmarkera kryssrutan **[!UICONTROL Enable Errors]**. Fel skrivs fortfarande ut när felsökning är aktiverat i Platform Launch.

### **[!UICONTROL Enable Opt-in]**

Om **[!UICONTROL Enable Opt-in]** är aktiverat kan AEP Web SDK-tillägget hålla träffar tills anmälan tas emot. Tillägget visar en åtgärd för att ange inställningar för deltagande.

### **[!UICONTROL Enable Migrate ECID]**

Tillägget AEP Web SDK använder en ny cookie för att lagra ECID:t. Den här inställningen möjliggör kompatibilitet mellan den nya cookien och den gamla cookien för migreringsändamål. Adobe rekommenderar starkt att detta aktiveras, såvida du inte har några befintliga besökare med ett ECID.

### **[!UICONTROL Use 3rd Party Cookies]**

Adobe Experience Platform kommer alltid att lagra en cookie i den första domänen. Med det här alternativet kan du använda en cookie-uppsättning från tredje part på demdex.net utöver cookien på förstahandsdomänen. Detta kan vara praktiskt när du har användare som förflyttar sig mellan flera domäner. Detta inaktiverar anrop till demdex.net.

### **[!UICONTROL Context]**

Tillägget samlar automatiskt in information om innehållet i begäran (till exempel information om URL:en och webbläsaren). Du kan inaktivera detta genom att avmarkera specifika kontexter.

- **[!UICONTROL web]** - Information om webbsidan, t.ex. url, referent osv.
- **[!UICONTROL device]** - Information om enheten, t.ex. skärmorientering, skärmhöjd och skärmbredd.
- **[!UICONTROL environment]** - Information om datormiljön (webbläsare, anslutning osv.)
- **[!UICONTROL location]** - Begränsad information om var användaren befinner sig

## Vad händer nu?

1. Ange [åtgärdstyper](action-types.md).
2. Ange [dataelementtyper](data-element-types.md).
