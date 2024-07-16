---
title: Åtgärdstyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika åtgärdstyperna i taggtillägget Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 0%

---


# Åtgärdstyper

När du har konfigurerat taggtillägget [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) måste du konfigurera åtgärdstyperna.

Den här sidan beskriver de åtgärdstyper som stöds av [Adobe Experience Platform Web SDK-taggtillägget](web-sdk-extension-configuration.md).


## Använd svar {#apply-response}

Använd åtgärdstypen **[!UICONTROL Apply response]** när du vill utföra olika åtgärder baserat på ett svar från Edge Network. Den här åtgärdstypen används vanligtvis i hybriddistributioner där servern gör ett första anrop till Edge Network. Den här åtgärdstypen tar svaret från anropet och initierar Web SDK i webbläsaren.

Om du använder den här åtgärdstypen kan klientbelastningstiden för hybridpersonalisering minska.

![Bild av användargränssnittet i Experience Platform som visar typen Använd svarsåtgärd.](assets/apply-response.png)

Den här åtgärdstypen stöder följande konfigurationsalternativ:

* **[!UICONTROL Instance]**: Välj den Web SDK-instans som du använder.
* **[!UICONTROL Response headers]**: Markera det dataelement som returnerar ett objekt som innehåller huvudnycklar och värden som returneras från Edge Network-serveranropet.
* **[!UICONTROL Response body]**: Markera det dataelement som returnerar objektet som innehåller JSON-nyttolasten från Edge Network-svaret.
* **[!UICONTROL Render visual personalization decisions]**: Aktivera det här alternativet för att automatiskt återge det personaliseringsinnehåll som tillhandahålls av Edge Network och dölja innehållet för att förhindra flimmer.

## Skicka händelse {#send-event}

Skickar en händelse till Adobe [!DNL Experience Platform] så att Adobe Experience Platform kan samla in data som du skickar och agera på den informationen. Markera en instans (om du har fler än en). Alla data som du vill skicka kan skickas i fältet **[!UICONTROL XDM Data]**. Använd ett JSON-objekt som överensstämmer med XDM-schemats struktur. Det här objektet kan antingen skapas på sidan eller via en **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Det finns några andra fält i åtgärdstypen Skicka händelse som också kan vara användbara beroende på implementeringen. Observera att alla dessa fält är valfria.

* **Typ:** I det här fältet kan du ange en händelsetyp som ska spelas in i XDM-schemat. Mer information finns i [`type`](/help/web-sdk/commands/sendevent/type.md) i kommandot `sendEvent`.
* **Data:** Data som inte matchar ett XDM-schema kan skickas med det här fältet. Det här fältet är användbart om du försöker uppdatera en Adobe Target-profil eller skicka Target Recommendations-attribut. Mer information finns i [`data`](/help/web-sdk/commands/sendevent/data.md) i kommandot `sendEvent`.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **Datauppsättnings-ID:** Om du behöver skicka data till en annan datauppsättning än den som du angav i din datauppsättning kan du ange detta datauppsättnings-ID här.
* **Dokumentet tas bort:** Markera kryssrutan **[!UICONTROL Document will unload]** om du vill se till att händelserna når servern även om användaren navigerar bort från sidan. Detta gör att händelser kan nå servern, men svaren ignoreras.
* **Återge beslut om visuell anpassning:** Om du vill återge anpassat innehåll på sidan markerar du kryssrutan **[!UICONTROL Render visual personalization decisions]** . Du kan också ange beslutsomfattningar och/eller ytor om det behövs. Mer information om återgivning av anpassat innehåll finns i [anpassningsdokumentationen](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content).

## Ange samtycke {#set-consent}

När du har fått ditt samtycke från din användare måste du meddela Adobe Experience Platform Web SDK genom att använda åtgärdstypen &quot;Ange samtycke&quot;. För närvarande stöds två typer av standarder: &quot;Adobe&quot; och &quot;IAB TCF&quot;. Se [Supporting Customer Consent Preferences](../../../../web-sdk/commands/setconsent.md). När du använder Adobe version 2.0 stöds bara ett dataelementvärde. Du måste skapa ett dataelement som matchar det godkända objektet.

I den här åtgärden får du även ett valfritt fält där du kan inkludera en identitetskarta så att identiteter kan synkroniseras när du har fått ditt samtycke. Synkronisering är användbart när medgivandet har konfigurerats som Väntande eller Ut eftersom det är sannolikt det första anropet som utlöses.

## Uppdatera variabel {#update-variable}

Använd den här åtgärden om du vill ändra ett XDM-objekt som ett resultat av en händelse. Den här åtgärden är avsedd att skapa ett objekt som senare kan refereras från en **[!UICONTROL Send event]**-åtgärd för att spela in händelsens XDM-objekt.

För att kunna använda den här åtgärdstypen måste du ha definierat ett [variabel](data-element-types.md#variable)-dataelement. När du väljer ett variabeldataelement att ändra visas en redigerare som liknar redigeraren för [XDM-objektets](data-element-types.md#xdm-object) dataelement.

![](assets/update-variable.png)

Det XDM-schema som används för redigeraren är det schema som har valts i dataelementet [!UICONTROL variable]. Du kan ange en eller flera egenskaper för objektet genom att klicka på en av egenskaperna i trädet till vänster och sedan ändra värdet till höger. I skärmbilden nedan ställs egenskapen produceradAv in på dataelementet&quot;Producerad av dataelement&quot;.

![](assets/update-variable-set-property.png)

Det finns vissa skillnader mellan redigeraren i uppdateringen av variabelåtgärden och redigeraren i XDM-objektdataelementet. Först har uppdateringsvariabelåtgärden ett rotnivåobjekt med namnet&quot;xdm&quot;. Om du klickar på det här objektet kan du ange ett dataelement som ska användas för att ställa in hela objektet. För det andra har åtgärden för att uppdatera variabeln kryssrutor för att rensa data från xdm-objektet. Klicka på en av egenskaperna till vänster och markera sedan kryssrutan till höger för att ta bort värdet. Detta rensar det aktuella värdet innan du anger värden för variabeln.

## Skicka mediahändelse {#send-media-event}

Skickar en mediehändelse till Adobe Experience Platform och/eller Adobe Analytics. Den här åtgärden är användbar när du spårar mediahändelser på webbplatsen. Markera en instans (om du har fler än en). Åtgärden kräver en `playerId` som representerar en unik identifierare för en spårad mediesession. Det kräver också ett **[!UICONTROL Quality of Experience]**- och `playhead`-dataelement när en mediesession startas.

![Plattformsgränssnittsbild som visar skärmen för händelsen skicka media.](assets/send-media-event.png)

Åtgärdstypen **[!UICONTROL Send media event]** stöder följande egenskaper:

* **[!UICONTROL Instance]**: Den Web SDK-instans som används.
* **[!UICONTROL Media Event Type]**: Den typ av mediahändelse som spåras.
* **[!UICONTROL Player ID]**: Unik identifierare för mediesessionen.
* **[!UICONTROL Playhead]**: Medieuppspelningens aktuella position i sekunder.
* **[!UICONTROL Media session details]**: När du skickar en mediesändningshändelse måste du ange nödvändig information om mediesessionen.
* **[!UICONTROL Chapter details]**: I det här avsnittet kan du ange kapitelinformation när du skickar en kapitelmediahändelse.
* **[!UICONTROL Advertising details]**: När du skickar en `AdBreakStart` -händelse måste du ange nödvändig annonsinformation.
* **[!UICONTROL Advertising pod details]**: Information om annonseringsområdet när en `AdStart` -händelse skickas.
* **[!UICONTROL Error details]**: Information om det uppspelningsfel som spåras.
* **[!UICONTROL State Update Details]**: Det spelartillstånd som uppdateras.
* **[!UICONTROL Custom Metadata]**: Anpassade metadata om mediahändelsen som spåras.
* **[!UICONTROL Quality of Experience]**: Mediekvaliteten för upplevelsedata som spåras.

## Hämta Media Analytics Tracker {#get-media-analytics-tracker}

Den här åtgärden används för att hämta det gamla API:t för Media Analytics. När åtgärden konfigureras och ett objektnamn anges, exporteras det gamla Media Analytics-API:t till det fönsterobjektet. Om inget anges exporteras den till `window.Media` som det aktuella mediets JS-biblioteket gör.

![Plattformsgränssnittsbild som visar åtgärdstypen Hämta Media Analytics Tracker.](assets/get-media-analytics-tracker.png)

## Omdirigera med identitet {#redirect-with-identity}

Använd den här åtgärdstypen om du vill dela identiteter från den aktuella sidan till andra domäner. Den här åtgärden är utformad för att användas med en **[!UICONTROL click]**-händelsetyp och ett värdejämförelsevillkor. Mer information om hur du använder åtgärdstypen finns i [Lägg till identitet i URL med Web SDK-tillägget](../../../../web-sdk/commands/appendidentitytourl.md#extension).

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du ha en bättre förståelse för hur du konfigurerar dina åtgärder. Läs sedan om hur du [konfigurerar dina dataelementtyper](data-element-types.md).
