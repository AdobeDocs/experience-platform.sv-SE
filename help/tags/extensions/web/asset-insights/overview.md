---
title: AEM Asset Insights Extension - översikt
description: Läs om tillägget AEM Asset Insights i Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Översikt över tillägget AEM tillgångsinsikter

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Det här tillägget är avsett att användas tillsammans med [AEM tillgångsinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). Mer specifikt ersätter den processen&quot;pageTracker&quot; och bäddar in kod. När det är konfigurerat skickar det här tillägget mått *Impression* och *Klicka på* till Adobe Analytics, varefter de importeras till AEM Asset Insights-rapporter. Måtten på tillgångarna kan sedan rapporteras med hjälp av AEM eller Adobe Analytics Project Workspaces.

## Förutsättningar för tillägg

### Analytics 

Rapporterna om AEM i Analytics innehåller tre AEM:

* Tillgångs-ID
* Resurskälla
* Klickad resurs

Det finns också två mätvärden:
* Resursimpression
* Resursklick.

Rapporterna måste aktiveras med Analytics Administrator (välj **[!UICONTROL Analytics]> [!UICONTROL Admin] > [!UICONTROL Report Suites] > `<report suite>` > [!UICONTROL Edit Settings] > [!UICONTROL AEM] >[!UICONTROL AEM Assets Reporting]**) innan de kan fyllas i med det här tillägget.

Taggtillägget &quot;*Adobe Analytics*&quot; för Adobe Experience Platform måste installeras i samma webbegenskap.

### Adobe Experience Manager (AEM)

1. Aktivera [AEM tillgångsinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). I AEM väljer du **[!UICONTROL Tools > Assets]** och öppnar sedan panelen **[!UICONTROL Insights Configuration]**.

1. Inaktivera UUID-spårning.

   >[!IMPORTANT]
   >
   >Det här tillägget *fungerar inte* om AEM Resurskonfigurationsinställningen **[!UICONTROL Disable UUID Tracking]** är markerad. Den är avmarkerad som standard.

   ![Inaktivera UUID-spårning](images/disableassets.jpg)

## Konfigurera Adobe Experience Manager (AEM)

I det här avsnittet beskrivs hur du konfigurerar AEM med taggar i Adobe Experience Platform, hur du aktiverar Asset Insight i AEM och hur du aktiverar UUID-spårning för Assets.

### Integrera AEM med taggar

Den rekommenderade integreringen av [Platform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) med Adobe Experience Manager görs via Adobe I/O.

1. [Koppla AEM med taggar med Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [Skapa en Adobe Experience Platform-Cloud Service-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### Aktivera tillgångsinsikt i AEM

Instruktioner om hur du aktiverar tillgångsinsikter finns i användarhandboken för [Experience Manager 6.5 Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html).

### Aktivera UUID-spårning för resurser

Spåra resurser i Analytics med hjälp av UUID för resursen i AEM.

Om du vill aktivera spårning med objektets UUID öppnar du komponentprincipkonsolen för den redigerbara mallen och avmarkerar egenskapen Inaktivera UUID-spårning. (Som standard kontrolleras den här egenskapen för OOTB-bildkomponenten.)

![](images/uuid.png)

När du har aktiverat UUID bör du se dataelementet&quot;data-asset-id&quot; som fylls med objektets UUID. Analytics spårar klickningen eller intrycket av resursen med detta UUID.

![](images/uuid-code.png)

## Tilläggsanvändning

Tillägget har två händelser och en åtgärd.

* **Klickad resurs:** En  __ händelse som utlöses när besökaren väljer en AEM som är aktiverad för spårning och har ett mål (href-attribut).

* **Klickad resurs (ingen destination):** En  __ händelse som utlöses när besökaren väljer en AEM resurs som är aktiverad för spårning och som inte har något mål (inget href-attribut).

* **Ange AA-variabler:** En  __ åtgärd som anger vilka Analytics-variabler som är reserverade för AEM Assets (kontextdatavariabler  `a.assets.source`och  `a.assets.idlist`   `a.asset.clickedid`) beroende på vilken händelse som användes och hur händelsen och åtgärden konfigureras. Det här tillägget använder inte några Analytics-händelser, -props eller -variabler.

### Resursavtryck

Lägg till åtgärden Ange AA-variabler i en ny eller befintlig taggregel som aktiveras på varje sida och skickar en förfrågan om Analytics-bild. Åtgärden Ange AA-variabler måste visas **före** åtgärden Adobe Analytics - skicka Beacon. Ytterligare åtgärder kan läggas till efter behov.

På konfigurationssidan **[Ange A-variabler]** väljer du alternativet **[Visade resurser]** (standard). Detta ställer bara in Impressions-händelsen för resurser som faktiskt visas av besökaren.

>[!NOTE]
>
>Även om det inte rekommenderas stöder åtgärden Ange AA-variabler även ett inläst alternativ, som skickar materialavbildningar för varje resurs på sidan, oavsett om besökaren såg dem eller inte.

![Impressions](images/sendImpressions.jpg)


### Klickningar på resurs

Konfigurera en andra regel med hjälp av händelsen Klickad resurs och åtgärden Ange AA-variabler. Händelsen &quot;Resurs klickad&quot; bör konfigureras så att &quot;Bildbegäran klickad på resurs&quot; är inställd på &quot;Vid sidinläsning&quot; (standard). Den här regeln kräver inga Adobe Analytics-åtgärder (som Skicka Beacon) eftersom resurs-ID sparas i `sessionStorage` och skickas av den efterföljande Impressions-regeln.

Händelsen &quot;Klickad resurs&quot; stöder även inställningen &quot;Bildbegäran klickad på resurs&quot; som &quot;Vid klickning&quot;. Detta skickar klickmätningen till Analytics omedelbart och kräver även en Analytics-åtgärd,&quot;Send Beacon&quot;.

![Resursklickningar vid sidinläsning](images/sendClickOnPageload.jpg)

Konfigurera en tredje regel som utlöses när det finns resurser på sidor som inte har något mål (inget `href`-attribut). Den nya regeln måste minst använda händelsen&quot;Klickad resurs (inget mål)&quot; samt åtgärderna&quot;Ange AA-variabler&quot; och&quot;Adobe Analytics - skicka signal&quot;. Ytterligare villkor och åtgärder kan läggas till efter behov.

![Resursklickning på inget mål](images/sendClickOnClickNoDestination.jpg)

### Tips för tilläggstestning

Konfigurera tre regler enligt beskrivningen ovan:

* Resursimpression
* Resursklickningar
* Resursklick utan mål

**Impressions**

1. Navigera till en sida som innehåller AEM resurser.

1. Om det inte finns några resurser synliga i webbläsaren rullar du tills du kan se minst en resurs och välja den resursen, eller bara navigera till en annan sida.

1. Titta på Analytics-bildförfrågan.

   Om `a.assets.idlist` innehåller de resurs-ID:n som kunde visas på föregående sida fungerar regeln korrekt.

   Om `a.assets.idlist` inte finns med i bildbegäran är det troligen en av två orsaker:

   * Det fanns aldrig någon resurs i webbläsarens visningsområde

   * Det fanns inga resurser på sidan som konfigurerats med [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) aktiverade i AEM.

**Klickningar**

1. Navigera till en sida som innehåller AEM resurser.

1. Välj en av resurserna.

Om `a.assets.idlist` har resurs-ID:n på målsidan och `a.assets.clickedid` har resurs-ID:n på den ursprungliga sidan fungerar regeln korrekt i den resulterande Analytics-bildförfrågan (från nästa sida).

Om `a.assets.clickedid` inte ingår i avbildningsbegäran är det mest troligt eftersom den valda resursen inte har [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) aktiverat i AEM.

**Klickningar utan mål**

1. Navigera till en sida som innehåller minst en AEM resurs som inte har något mål (inget `href`-attribut).

1. Välj den resursen.

I den resulterande Analytics-bildbegäran fungerar regeln korrekt om `a.assets.clickedid` har resurs-ID:t.

Om `a.assets.clickedid` inte ingår i avbildningsbegäran är det mest troligt eftersom den valda resursen inte har [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) aktiverat i AEM.
