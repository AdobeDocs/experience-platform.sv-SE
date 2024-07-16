---
title: Översikt över tillägget Meta Pixel
description: Läs om tillägget Meta Pixel i Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) är ett JavaScript-baserat analysverktyg som gör att du kan spåra besökaraktivitet på din webbplats. Besöksåtgärder som du spårar (kallas konverteringar) skickas till [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager), där de kan användas för att mäta effektiviteten hos dina annonser, kampanjer, konverteringstrattar med mera.

Med taggtillägget [!DNL Meta Pixel] kan du utnyttja [!DNL Pixel]-funktioner i klientens taggbibliotek. Det här dokumentet beskriver hur du installerar tillägget och använder dess funktioner i en [regel](../../../ui/managing-resources/rules.md).

## Förhandskrav

Du måste ha ett giltigt [!DNL Meta]-konto med åtkomst till [!DNL Ads Manager] för att kunna använda tillägget. Du måste [skapa en ny [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) och kopiera dess [!DNL Pixel ID] så att tillägget kan konfigureras för ditt konto. Om du redan har en befintlig [!DNL Meta Pixel] kan du använda dess ID i stället.

Vi rekommenderar starkt att du använder [!DNL Meta Pixel] i kombination med [!DNL Meta Conversions API] för att dela och skicka samma händelser från klientsidan respektive serversidan, eftersom detta kan hjälpa till att återställa händelser som inte plockats upp av [!DNL Meta Pixel]. I guiden för [[!DNL Meta Conversions API] tillägget för vidarebefordran av händelser](../../client/meta/overview.md) finns anvisningar om hur du integrerar det i implementeringar på serversidan. Observera att din organisation måste ha åtkomst till [vidarebefordran av händelser](../../../ui/event-forwarding/overview.md) för att kunna använda tillägget på serversidan.

## Installera tillägget

Om du vill installera tillägget [!DNL Meta Pixel] går du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Tags]** i den vänstra navigeringen. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Catalog]**. Sök efter kortet [!UICONTROL Meta Pixel] och välj sedan **[!UICONTROL Install]**.

![Knappen [!UICONTROL Install] som väljs för tillägget [!UICONTROL Meta Pixel] i användargränssnittet för datainsamling.](../../../images/extensions/client/meta/install.png)

I konfigurationsvyn som visas måste du ange det [!DNL Pixel]-ID som du kopierade tidigare för att kunna länka tillägget till ditt konto. Du kan klistra in ID:t direkt i indata eller markera ett befintligt dataelement i stället.

>[!TIP]
>
>Om du använder ett dataelement kan du ändra det [!DNL Pixel]-ID som används dynamiskt beroende på andra faktorer, till exempel byggmiljön. Mer information finns i bilagan om [att använda olika [!DNL Pixel] ID:n för olika miljöer](#id-data-element).

Du kan också ange ett händelse-ID att koppla till tillägget med. Detta används för att deduplicera identiska händelser mellan [!DNL Meta Pixel] och [!DNL Meta Conversions API]. Mer information finns i avsnittet om [händelseborttagning](../../server/meta/overview.md#event-deduplication) i översikten över tillägget [!DNL Conversions API].

När du är klar väljer du **[!UICONTROL Save]**

![Det [!DNL Pixel]-ID som anges som ett dataelement i tilläggskonfigurationsvyn.](../../../images/extensions/client/meta/configure.png)

Tillägget är installerat och du kan nu använda dess olika åtgärder i taggreglerna.

## Konfigurera en taggregel {#rule}

[!DNL Meta Pixel] accepterar en uppsättning fördefinierade [standardhändelser](https://www.facebook.com/business/help/402791146561655), var och en med egna kontexter och godkända egenskaper. Regelåtgärderna som tillhandahålls av tillägget [!DNL Pixel] korrelerar till de här händelsetyperna, vilket gör att du enkelt kan kategorisera och konfigurera händelsen som skickas till [!DNL Meta] utifrån dess typ.

I det här avsnittet visas hur du skapar en regel som skickar en sidvyhändelse till [!DNL Meta].

Börja skapa en ny taggregel och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Meta Pixel]** som tillägg och sedan **[!UICONTROL Send Page View]** som åtgärdstyp.

![Åtgärdstypen [!UICONTROL Send Page View] som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/client/meta/select-action.png)

Det krävs ingen ytterligare konfiguration för åtgärden [!UICONTROL Send Page View]. Välj **[!UICONTROL Keep Changes]** om du vill lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny tagg, [build](../../../ui/publishing/builds.md), för att aktivera ändringarna i biblioteket.

## Bekräfta att [!DNL Meta] tar emot data

När den uppdaterade versionen har distribuerats till webbplatsen kan du bekräfta om data skickas som förväntat genom att generera konverteringshändelser i webbläsaren och kontrollera om dessa händelser visas i [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Nästa steg

I den här guiden beskrivs hur du skickar data till [!DNL Meta] med taggtillägget [!DNL Meta Pixel]. Om du planerar att även skicka händelser på serversidan till [!DNL Meta] kan du nu fortsätta installera och konfigurera tillägget [[!DNL Conversions API] för vidarebefordran av händelser](../../server/meta/overview.md).

Mer information om taggar i Experience Platform finns i [taggöversikten](../../../home.md).

## Bilaga: Använd olika [!DNL Pixel]-ID:n för olika miljöer {#id-data-element}

Om du vill testa implementeringen i utvecklings- eller staging-miljöer samtidigt som [!DNL Meta Pixel]-analysen för produktionen förblir intakt, kan du använda ett dataelement för att dynamiskt välja ett lämpligt [!DNL Pixel]-ID beroende på vilken miljö som används.

Du kan uppnå detta genom att använda ett [!UICONTROL Custom Code]-dataelement (tillhandahålls av [[!UICONTROL Core] extension](../core/overview.md)) i kombination med den [`turbine` kostnadsfria variabeln ](../../../extension-dev/turbine.md). I dataelementets JavaScript-kod använder du objektet `turbine` för att hitta den aktuella miljöfasen och returnerar sedan ett lämpligt [!DNL Pixel]-ID baserat på resultatet.

I följande exempel returneras det falska produktions-ID:t `exampleProductionKey` när det används i produktionsmiljön och ett annat ID `exampleTestKey` när någon annan miljö används. När du implementerar den här koden ska du ersätta varje värde med din faktiska produktion och testa [!DNL Pixel]-ID:n.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
