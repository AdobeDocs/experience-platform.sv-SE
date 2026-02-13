---
title: Skicka händelse
description: Skicka data till Adobe Experience Platform Edge Network.
exl-id: 4ac7750e-48ab-4eb6-873d-bb2556dbf788
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Skicka händelse

Åtgärden **[!UICONTROL Send event]** skickar en nyttolast till en datastam på Adobe Experience Platform Edge Network. Det är en av grundfunktionerna för datainsamling och personalisering. Nästan alla organisationer använder den här åtgärden som en del av sin Web SDK-implementering.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Send event]**.

## Allmänna fält

![Användargränssnittsbild för Experience Platform-taggar visar instansinställningarna för åtgärdstypen Skicka händelse.](../assets/instance-settings.png)

* **[!UICONTROL Instance]**: Den SDK-instans som åtgärden gäller för. Den här nedrullningsbara menyn är inaktiverad om implementeringen använder en enda SDK-instans.
* **[!UICONTROL Use guided events]**: Aktivera det här alternativet för att automatiskt fylla i eller dölja vissa fält för att aktivera ett visst användningsfall. Den här inställningen kan bidra till att minska bruset i tillgängliga alternativ när du ställer in åtgärden för varje syfte, och följer Adobe bästa praxis för [Sidhändelser upptill/nedtill](/help/collection/use-cases/personalization/top-bottom-page-events.md). Om du aktiverar den här kryssrutan visas följande alternativknappar:
   * **[!UICONTROL Request personalization]**: Hämta de senaste personaliseringsbesluten utan att spela in en Adobe Analytics-händelse. Den anropas oftast överst på sidan. När den här alternativknappen är markerad anger den följande fält:
      * [!UICONTROL Type] är låst till [!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions] är låst för att aktiveras
      * [!UICONTROL Automatically send a display event] är låst för att inaktiveras
   * **[!UICONTROL Collect analytics]**: Spela in en händelse utan att fatta personaliseringsbeslut. Det anropas oftast längst ned på sidan. När den här alternativknappen är markerad anger den följande fält:
      * [!UICONTROL Include rendered propositions] är låst för att aktiveras

## Datafält

![Användargränssnittsbild för Experience Platform-taggar visar dataelementinställningarna för åtgärdstypen Skicka händelse.](../assets/data.png)

* **[!UICONTROL Type]**: Händelsetypen. Du kan välja bland en fördefinierad uppsättning värden eller definiera ett eget värde. Mer information finns i [Godkända värden för `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype). JavaScript-biblioteket som motsvarar det här fältet är [`eventType`](/help/collection/js/commands/sendevent/eventtype.md).
* **[!UICONTROL XDM]**: Den XDM-nyttolast som du vill skicka till Adobe. Du kan antingen använda ett [XDM-objekt](../data-element-types.md#xdm-object) eller [Variabel](../data-element-types.md#variable) i det här fältet. Om du har regler som fyller i flera XDM-objekt kan du använda [Sammanfogade objekt](../../core/overview.md#merged-objects) för att kombinera dem.
* **[!UICONTROL Data]**: Datanyttolasten som du vill skicka till Adobe. Vissa program och tjänster kräver inte att du följer ett XDM-schema, till exempel Adobe Analytics eller Adobe Target. Använd ett [variabelt](../data-element-types.md#variable)-dataelementtyp för det här fältet.
* **[!UICONTROL Include rendered propositions]**: Aktivera den här kryssrutan för att använda den här händelsen som en visningshändelse, inklusive de förslag som återges när&quot;automatiskt skicka en visningshändelse&quot; avmarkerades. XDM-fältet `_experience.decisioning` innehåller information om återgiven personalisering.
* **[!UICONTROL Document will unload]**: Aktivera den här kryssrutan för att se till att händelsen når servern även om användaren navigerar bort från sidan. Med den här inställningen kan händelser nå servern, men svar från Edge Network ignoreras.
* **[!UICONTROL Merge ID]** _(Borttagen)_: Fyller i `eventMergeId` XDM-fältet.

## Fält för personalisering

![Användargränssnittsbild för Experience Platform-taggar visar Personalization-inställningarna för åtgärdstypen Skicka händelse.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: En matris med omfattningar som du uttryckligen vill begära från personalisering. Du kan ange omfattningarna manuellt eller ange ett dataelement. När du anger scope manuellt representerar varje fält ett omfång. Välj **[!UICONTROL Add scope]** om du vill lägga till fler scope i åtgärden.
* **[!UICONTROL Surfaces]**: En array med ytor att fråga efter med händelsen. Mer information finns i [Skapa webbupplevelser](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) i Adobe Journey Optimizer-dokumentationen. När du anger ytor manuellt representerar varje fält en yta. Välj **[!UICONTROL Add surface]** om du vill lägga till fler ytor i åtgärden.
* **Återge beslut om visuell personalisering:** En kryssruta som, när den är aktiverad, låter dig återge anpassat innehåll på sidan. Mer information finns i [Återge DOM-åtgärder automatiskt](/help/collection/use-cases/personalization/render-auto-pers-content.md).
* **[!UICONTROL Request default personalization]**: Kontrollerar om det sidomfattande omfånget och standardytan har begärts. Som standard begärs den automatiskt under det första `sendEvent` anropet av sidinläsningen. JavaScript-biblioteket som motsvarar dessa alternativknappar är [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md). Du kan välja mellan följande alternativ:
   * **[!UICONTROL Automatic]**: Standardbeteendet. Begär endast standardanpassning när den ännu inte har begärts.
   * **[!UICONTROL Enabled]**: Begär sidomfånget och standardytan explicit. Detta uppdaterar SPA-vycachen.
   * **[!UICONTROL Disabled]**: Undertrycker explicit begäran för sidomfånget och standardytan.
* **[!UICONTROL Decision context]**: Ett nyckelvärdesschema som används vid utvärdering av Adobe Journey Optimizer-regler för enhetsbeslut. Du kan ange beslutskontexten manuellt eller via ett dataelement.

## Advertising

![Gränssnittet för Experience Platform-taggar visar annonsinställningar för åtgärden Skicka händelse](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**: Avgör när (eller om) biblioteket lägger till annonsinformation i XDM-nyttolasten. Du kan välja mellan följande alternativ:
   * **[!UICONTROL Automatic]**: Alla annonsdata som är tillgängliga vid tidpunkten för händelsen läggs till i händelsens nyttolast.
   * **[!UICONTROL Wait]**: Fördröj sändning av händelsen tills annonsdata tas emot.
   * **[!UICONTROL Disabled]**: Lägg inte till annonsdata i händelsens nyttolast. Välj det här alternativet om implementeringen inte använder Adobe Analytics eller Customer Journey Analytics.

## Åsidosättningar av dataströmskonfiguration

Det här kommandot har stöd för åsidosättningar av dataströmskonfigurationer, vilket ger dig kontroll över vilka program och tjänster som tar emot dessa data. När du anger en åsidosättning av en datastream-konfiguration i både ett enskilt kommando och i inställningarna för taggtilläggskonfigurationen, prioriteras det enskilda kommandot. Mer information finns i [Åsidosättningar av dataströmskonfiguration](../configure/configuration-overrides.md).
