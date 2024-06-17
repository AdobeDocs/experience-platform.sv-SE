---
title: The Trade Desk Real-Time Conversions API Extension Overview
description: Läs mer om API-tillägget Trade Desk Real-Time Conversions för händelsevidarebefordran i Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d9d185685106ac160dcbefc5e9567a85c8302a73
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# [!DNL The Trade Desk Real-Time Conversions API] tilläggsöversikt

Du kan använda [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) för att skicka data från Adobe Experience Platform Edge Network till [!DNL The Trade Desk] genom att använda API:ts funktioner i [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) regler.

Använda [!DNL The Trade Desk Real-Time Conversions API] kan du utnyttja API:ts funktioner i [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) regler att skicka data till [!DNL The Trade Desk] från Adobe Experience Platform Edge Network.

Läs det här dokumentet för att lära dig hur du installerar tillägget och använder dess funktioner vid en händelsevidarebefordring [regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Den här tilläggs- och dokumentationssidan underhålls av [!DNL The Trade Desk] team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt.

## Förutsättningar {#prerequisites}

Du måste ha ett relevant Advertiser ID, UPixel ID och Tracker ID i din [!DNL The Trade Desk] konto för att konfigurera [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Om du är handlare måste du också skaffa ditt handels-ID.

## Installera och konfigurera [!DNL The Trade Desk] API för konvertering i realtid {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller markera en befintlig egenskap som du vill redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** väljer du **[!UICONTROL The Trade Desk]** API-kort för konvertering i realtid och välj sedan **[!UICONTROL Install]**.

![Tilläggskatalogen med [!DNL The Trade Desk] installation av tilläggskort.](../../../images/extensions/server/tradedesk/install-extension.png)

På nästa skärm anger du [!UICONTROL Advertiser ID]och eventuellt en [!UICONTROL Merchant ID]. Du kan klistra in ID:n direkt i dessa indata eller använda ett dataelement i stället. Dessa fungerar som standardvärden som används vid anrop av en händelse till [!DNL The Trade Desk] API för konvertering i realtid. Välj **[!UICONTROL Save]** när du är klar.

Om du vill lära dig hur du kan skapa dataelement och göra dem tillgängliga för tillägg i taggegenskapen följer du [Skapa dataelement](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) självstudie.

![The [!DNL The Trade Desk] konfigurationssida för tillägg med [!UICONTROL Advertiser ID] och [!UICONTROL Merchant ID] markerade fält.](../../../images/extensions/server/tradedesk/configure-extension.png)

Tillägget är installerat och du kan nu använda dess funktioner i reglerna för vidarebefordran av händelser.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

När du har installerat och konfigurerat tillägget kan du börja skapa regler för vidarebefordran av händelser som avgör hur och när händelser skickas till [!DNL The Trade Desk].

Du bör överväga att konfigurera flera regler för att skicka alla godkända [egenskaper för begäran](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] och [!DNL The Trade Desk] API för konvertering i realtid.

>[!NOTE]
>
>Händelser bör skickas ut i realtid eller så nära realtid som möjligt.

Skapa en ny händelsevidarebefordring [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL The Trade Desk]**. Nästa, välj **[!UICONTROL Real Time Conversion]** för **[!UICONTROL Action Type]**.

![Vyn Egenskapsregler för händelsevidarebefordring, med fälten som krävs för att lägga till en händelsevidarebefordringsregel, markerad.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsedata som ska skickas till [!DNL The Trade Desk]. Välj **[!UICONTROL Keep Changes]** för att spara regeln.

Konfigurationsalternativen är uppdelade i tre huvudavsnitt enligt nedan:

**[!UICONTROL Basic Request Properties]**

| Indata | Beskrivning |
| --- | --- |
| Spårar-ID | Plattforms-ID för händelsespåraren. |
| UPixel-ID | Det universella pixel-ID:t för händelsen. |
| Referent-URL | Webbplats-URL:en som händelsen inträffade från, om sådan finns. |
| Händelsenamn | Den typ av händelse som definieras av partnerplattformen. |
| Värde | Intäktsspårningsvärdet i decimalsträng (till exempel &quot;19.98&quot;). |
| Valuta | Valutakod i ISO-format. |
| Klient-IP | Klientens IPv4- eller IPv6-IP-adress. |
| Annons-ID | Det unika reklam-ID:t för händelsen. |
| Typ av annons-ID | Typ av reklam-ID, som anges i AD ID-egenskapen: TDID, IDFA, AAID, DAID, NAID, IDL, EUID eller UID2. |
| Impression | En 36-teckensträng (inklusive bindestreck) som fungerar som det unika ID:t för det intryck som händelsen är kopplad till. |
| Order-ID | Händelsens associerade orderidentifierare. |
| td1-td10 | Tio sekventiellt numrerade anpassade dynamiska egenskaper som kan användas för att tillhandahålla ytterligare konverteringsmetadata. |

{style="table-layout:auto"}

![The [!DNL Basic Request Properties] som visar exempeldata i fälten.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Se [!DNL The Trade Desk] utvecklardokumentation för mer information om [egenskaper för begäran](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) godkänd av [!DNL The Trade Desk] API för konvertering i realtid.

**[!UICONTROL Object Request Parameters]**

Ett JSON-objekt som innehåller mer information. Du kan välja att använda en reducerad uppsättning indata för nyckelvärden eller att ange JSON i Raw-format. Dessutom kan du hämta dynamiska data från ett dataelement genom att välja diskarna (![Diskikon](../../../images/extensions/server/tradedesk/disk-icon.png)) till höger.


![The [!DNL Object Request Parameters] -sektion som visar tillgängliga fält.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Se [Händelse för konvertering i realtid](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) för mer information om [!UICONTROL Object Request Parameters] och deras egenskaper.

**[!UICONTROL Configuration Overrides]**

>[!NOTE]
>
>The [!UICONTROL Configuration Overrides] kan du ange ett annat [!DNL Advertiser ID] och/eller [!DNL Merchant ID] på alla regler.

| Indata | Beskrivning |
| --- | --- |
| Annonsörs-ID | Unik identifierare för annonsören som den här händelsen är associerad med. Ett annat annonsörs-ID kan anges för att åsidosätta det ID som du angav i tilläggskonfigurationen. |
| Affärs-ID | Den unika identifierare som varje handlare anges av [!DNL The Trade Desk] under introduktionsprocessen. Ett annat handels-ID kan anges för att åsidosätta det ID som du angav i tilläggskonfigurationen. |

![The [!DNL Configuration Overrides] -sektion som visar tillgängliga fält.](../../../images/extensions/server/tradedesk/configure-overrides.png)

När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**. Publicera slutligen en ny händelsevidarebefordring [bygg](../../../ui/publishing/builds.md) för att aktivera ändringar som gjorts i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL The Trade Desk] med [!DNL The Trade Desk] API-tillägg för konvertering i realtid. Här rekommenderas att du utökar integreringen genom att skapa distinkta regler som skickar specifika konverteringshändelser beroende på vilket som är tillämpligt för varje kampanj. Mer information om funktioner för vidarebefordran av händelser finns i [!DNL Adobe Experience Platform], läsa [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).

Se [!DNL The Trade Desk] dokumentation om [de bästa sätten för [!DNL The Trade Desk] API för konvertering i realtid](https://www.facebook.com/business/help/308855623839366?id=818859032317965) om du vill ha mer information om hur ni kan implementera er integrering på ett effektivt sätt.

Mer information om hur du felsöker implementeringen med verktyget för felsökning och övervakning av händelsevidarebefordran i Experience Platform finns i [Adobe Experience Platform Debugger - översikt](../../../../debugger/home.md) och [Övervaka aktiviteter vid händelsevidarebefordran](../../../ui/event-forwarding/monitoring.md).
