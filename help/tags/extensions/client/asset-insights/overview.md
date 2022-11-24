---
title: AEM Asset Insights Extension - översikt
description: Läs om tillägget AEM Asset Insights i Adobe Experience Platform.
exl-id: 7d3edd42-09fe-4e40-93dc-1edd2fdbb121
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---

# Översikt över tillägget AEM tillgångsinsikter

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Detta tillägg är avsett att användas tillsammans med [AEM tillgångsinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). Mer specifikt ersätter den processen&quot;pageTracker&quot; och bäddar in kod. Tillägget skickar resurs när det är konfigurerat *Impression* och *Klicka* mått till Adobe Analytics, efter vilka de kommer att importeras till AEM Asset Insights-rapporter. Måtten på tillgångarna kan sedan rapporteras med hjälp av AEM eller Adobe Analytics Project Workspaces.

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

The &quot;*Adobe Analytics*&quot;-taggtillägget för Adobe Experience Platform måste installeras i samma webbegenskap.

### Adobe Experience Manager (AEM)

1. Aktivera [AEM tillgångsinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). I AEM väljer du **[!UICONTROL Tools > Assets]**&#x200B;öppnar du **[!UICONTROL Insights Configuration]** -panelen.

1. Inaktivera UUID-spårning.

   >[!IMPORTANT]
   >
   >Det här tillägget kommer att *not* funktionen om inställningen för konfiguration av AEM **[!UICONTROL Disable UUID Tracking]** är markerad. Den är avmarkerad som standard.

   ![Inaktivera UUID-spårning](images/disableassets.jpg)

## Konfigurera Adobe Experience Manager (AEM)

I det här avsnittet beskrivs hur du konfigurerar AEM med taggar i Adobe Experience Platform, hur du aktiverar Asset Insight i AEM och hur du aktiverar UUID-spårning för Assets.

### Integrera AEM med taggar

Rekommenderad integrering av [Plattform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) med Adobe Experience Manager via Adobe I/O.

1. [Koppla AEM med taggar med Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [Skapa en Adobe Experience Platform Cloud Service-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### Aktivera tillgångsinsikt i AEM

Instruktioner om hur du aktiverar resursinsikter finns i [Användarhandbok för Experience Manager 6.5 Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html).

### Aktivera UUID-spårning för resurser

Spåra resurser i Analytics med hjälp av UUID för resursen i AEM.

Om du vill aktivera spårning med objektets UUID öppnar du komponentprincipkonsolen för den redigerbara mallen och avmarkerar egenskapen Inaktivera UUID-spårning. (Som standard kontrolleras den här egenskapen för OOTB-bildkomponenten.)

![](images/uuid.png)

När du har aktiverat UUID bör du se dataelementet&quot;data-asset-id&quot; som fylls med objektets UUID. Analytics spårar klickningen eller intrycket av resursen med detta UUID.

![](images/uuid-code.png)

## Tilläggsanvändning

Tillägget har två händelser och en åtgärd.

* **Klickad resurs:** An _event_ som aktiveras när besökaren väljer en AEM resurs som är aktiverad för spårning och har ett mål (href-attribut).

* **Klickad resurs (ingen destination):** An _event_ som aktiveras när besökaren väljer en AEM resurs som är aktiverad för spårning och inte har något mål (inget href-attribut).

* **Ange AA-variabler:** An _åtgärd_ som anger Analytics-variabler som är reserverade för AEM Assets (kontextdatavariabler) `a.assets.source`, `a.assets.idlist` och `a.asset.clickedid`) beroende på vilken händelse som användes och hur händelsen och åtgärden konfigureras. Det här tillägget använder inte några Analytics-händelser, -props eller -variabler.

### Resursavtryck

Lägg till åtgärden Ange AA-variabler i en ny eller befintlig taggregel som aktiveras på varje sida och skickar en förfrågan om Analytics-bild. Åtgärden Ange AA-variabler måste visas **före** åtgärden&quot;Adobe Analytics - skicka beacon&quot;. Ytterligare åtgärder kan läggas till efter behov.

I **[Ange AA-variabler]** config page, select the **[Visade resurser]** (standard). Detta ställer bara in Impressions-händelsen för resurser som faktiskt visas av besökaren.

>[!NOTE]
>
>Även om det inte rekommenderas stöder åtgärden Ange AA-variabler även ett inläst alternativ, som skickar materialavbildningar för varje resurs på sidan, oavsett om besökaren såg dem eller inte.

![Impressions](images/sendImpressions.jpg)


### Klickningar på resurs

Konfigurera en andra regel med hjälp av händelsen Klickad resurs och åtgärden Ange AA-variabler. Händelsen &quot;Resurs klickad&quot; bör konfigureras så att &quot;Bildbegäran klickad på resurs&quot; är inställd på &quot;Vid sidinläsning&quot; (standard). Den här regeln kräver inga Adobe Analytics-åtgärder (som Skicka Beacon) eftersom resurs-ID:t sparas i `sessionStorage` och skickas av efterföljande Impressions-regel.

Händelsen &quot;Klickad resurs&quot; stöder även inställningen &quot;Bildbegäran klickad på resurs&quot; som &quot;Vid klickning&quot;. Detta skickar klickmätningen till Analytics omedelbart och kräver även en Analytics-åtgärd,&quot;Send Beacon&quot;.

![Resursklickningar vid sidinläsning](images/sendClickOnPageload.jpg)

Konfigurera en tredje regel som ska utlösas när det finns resurser på sidor som inte har något mål (nej `href` attribut). Den nya regeln måste minst använda händelsen&quot;Klickad resurs (inget mål)&quot; samt åtgärderna&quot;Ange AA-variabler&quot; och&quot;Adobe Analytics - skicka signal&quot;. Ytterligare villkor och åtgärder kan läggas till efter behov.

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

   If `a.assets.idlist` innehåller de resurs-ID:n som kunde visas på föregående sida, så fungerar regeln korrekt.

   If `a.assets.idlist` finns inte i bildbegäran, det är troligen en av två orsaker:

   * Det fanns aldrig någon resurs i webbläsarens visningsområde

   * Det fanns inga resurser på sidan konfigurerade med [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) i AEM.

**Klickningar**

1. Navigera till en sida som innehåller AEM resurser.

1. Välj en av resurserna.

I den resulterande Analytics-bildförfrågan (från nästa sida), om `a.assets.idlist` har resurs-ID:n på målsidan och `a.assets.clickedid` har resurs-ID:t för den resurs som valdes på originalsidan, fungerar regeln korrekt.

If `a.assets.clickedid` finns inte i bildbegäran, det beror troligtvis mest på att den valda resursen inte hade [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) i AEM.

**Klickningar utan mål**

1. Navigera till en sida som innehåller minst en AEM resurs som inte har något mål (ingen `href` attribut).

1. Välj den resursen.

I den resulterande Analytics-bildförfrågan, om `a.assets.clickedid` har resurs-ID:t fungerar regeln korrekt.

If `a.assets.clickedid` finns inte i bildbegäran, det beror troligtvis mest på att den valda resursen inte hade [Resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) i AEM.
