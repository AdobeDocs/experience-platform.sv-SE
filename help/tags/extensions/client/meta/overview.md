---
title: Översikt över tillägget Meta Pixel
description: Läs om tillägget Meta Pixel i Adobe Experience Platform.
source-git-commit: 87376172f89858bfa883084461544a2c50ba5009
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# [!DNL Meta Pixel] tilläggsöversikt

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) är ett JavaScript-baserat analysverktyg som gör att du kan spåra besökaraktivitet på din webbplats. Besökaråtgärder som du spårar (konverteringar) skickas till [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) där de kan användas för att mäta effektiviteten hos era annonser, kampanjer, konverteringsverktyg och mycket annat.

The [!DNL Meta Pixel] taggtillägg gör att du kan använda [!DNL Pixel] funktioner i klientens taggbibliotek. Det här dokumentet beskriver hur du installerar tillägget och använder dess funktioner i en [regel](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## Förutsättningar

För att kunna använda tillägget måste du ha ett giltigt [!DNL Meta] konto med tillgång till [!DNL Ads Manager]. Du måste [skapa en ny [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) och kopiera [!DNL Pixel ID] så att tillägget kan konfigureras för ditt konto. Om du redan har en befintlig [!DNL Meta Pixel]kan du använda dess ID i stället.

## Installera tillägget

Så här installerar du [!DNL Meta Pixel] navigerar du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Tags]** från vänster navigering. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen väljer du **[!UICONTROL Catalog]** -fliken. Sök efter [!UICONTROL Meta Pixel] kort, välj **[!UICONTROL Install]**.

![The [!UICONTROL Install] knappen som markeras för [!UICONTROL Meta Pixel] i användargränssnittet för datainsamling.](../../../images/extensions/client/meta/install.png)

I konfigurationsvyn som visas måste du ange [!DNL Pixel] ID som du kopierade tidigare för att länka tillägget till ditt konto. Du kan klistra in ID:t direkt i indata eller markera ett befintligt dataelement i stället.

>[!TIP]
>
>Om du använder ett dataelement kan du ändra [!DNL Pixel] ID som används beroende på andra faktorer som byggmiljön. Se avsnittet om bilagan [använda olika [!DNL Pixel] ID för olika miljöer](#id-data-element) för mer information.

Du kan också ange ett händelse-ID att koppla till tillägget med. Detta används för att ta bort identiska händelser mellan [!DNL Meta Pixel] och [!DNL Meta Conversions API]. Se [!DNL Meta] dokumentation om [hantering av dubblett [!DNL Pixel] och [!DNL Conversions API] händelser](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) för mer information.

När du är klar väljer du **[!UICONTROL Save]**

![The [!DNL Pixel] ID som anges som ett dataelement i tilläggskonfigurationsvyn.](../../../images/extensions/client/meta/configure.png)

Tillägget är installerat och du kan nu använda dess olika åtgärder i taggreglerna.

## Konfigurera en taggregel {#rule}

[!DNL Meta Pixel] accepterar en uppsättning fördefinierade [standardhändelser](https://www.facebook.com/business/help/402791146561655), vart och ett med sina egna kontexter och godkända egenskaper. Regelåtgärder från [!DNL Pixel] tillägg korrelerar med dessa händelsetyper, vilket gör att du enkelt kan kategorisera och konfigurera händelsen som skickas till [!DNL Meta] enligt dess typ.

I det här avsnittet visas hur du skapar en regel som skickar en sidvisningshändelse till [!DNL Meta].

Börja skapa en ny taggregel och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Meta Pixel]** för tillägget väljer du **[!UICONTROL Send Page View]** för åtgärdstypen.

![The [!UICONTROL Send Page View] åtgärdstypen som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/client/meta/select-action.png)

Det krävs ingen ytterligare konfiguration för [!UICONTROL Send Page View] åtgärd. Välj **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny tagg [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar i biblioteket.

## Bekräfta att [!DNL Meta] tar emot data

När den uppdaterade versionen har distribuerats till webbplatsen kan du bekräfta om data skickas som förväntat genom att generera konverteringshändelser i webbläsaren och kontrollera om dessa händelser visas i [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL Meta] med [!DNL Meta Pixel] taggtillägg. Mer information om taggar i Experience Platform finns i [taggöversikt](../../../home.md).

## Bilaga: Använd olika [!DNL Pixel] ID för olika miljöer {#id-data-element}

Om du vill testa implementeringen i utvecklings- eller staging-miljöer samtidigt som du behåller din produktion [!DNL Meta Pixel] analyserna är intakta kan du använda ett dataelement för att dynamiskt välja ett lämpligt [!DNL Pixel] ID beroende på vilken miljö som används.

Du kan uppnå detta genom att använda en [!UICONTROL Custom Code] dataelement (tillhandahålls av [[!UICONTROL Core] extension](../core/overview.md)) i kombination med [`turbine` kostnadsfri variabel](../../../extension-dev/turbine.md). I dataelementets JavaScript-kod använder du `turbine` objekt för att hitta den aktuella miljöscenen och sedan returnera ett lämpligt [!DNL Pixel] ID baserat på resultatet.

I följande exempel returneras ett falskt produktions-ID `exampleProductionKey` när det används i produktionsmiljön, och ett annat ID `exampleTestKey` när någon annan miljö används. Ersätt varje värde med den faktiska produktionen och testet när du implementerar koden [!DNL Pixel] ID:n.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```

