---
title: The Trade Desk Real-Time Conversions API Extension Overview
description: Läs mer om API-tillägget Trade Desk Real-Time Conversions för händelsevidarebefordran i Adobe Experience Platform.
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: eb650da02ac69c5afbebfe6ba371cc19617f79d0
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# Översikt över tillägget [!DNL The Trade Desk Real-Time Conversions API]

Du kan använda tillägget [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) om du vill skicka data från Adobe Experience Platform Edge Network till [!DNL The Trade Desk] genom att använda API:ts funktioner i [reglerna för vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).

Med tillägget [!DNL The Trade Desk Real-Time Conversions API] kan du utnyttja API:ts funktioner i reglerna för [ vidarebefordran av händelser](../../../ui/event-forwarding/overview.md) för att skicka data till [!DNL The Trade Desk] från Adobe Experience Platform Edge Network.

Läs det här dokumentet för att lära dig hur du installerar tillägget och använder dess funktioner i en händelsevidarebefordring av [regeln](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Den här tilläggs- och dokumentationssidan underhålls av [!DNL The Trade Desk]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt.

## Förhandskrav {#prerequisites}

Du måste ha ett relevant Advertiser ID, UPixel ID och Tracker ID från ditt [!DNL The Trade Desk]-konto för att kunna konfigurera [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Om du är handlare måste du också skaffa ditt handels-ID.

## Installera och konfigurera API:t för [!DNL The Trade Desk]-realtidskonverteringar {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. På fliken **[!UICONTROL Catalog]** väljer du **[!UICONTROL The Trade Desk]** Real-Time Conversions API-kort och sedan **[!UICONTROL Install]**.

![Tilläggskatalogen som visar installationen av [!DNL The Trade Desk] tilläggskort.](../../../images/extensions/server/tradedesk/install-extension.png)

På nästa skärm anger du [!UICONTROL Advertiser ID] och eventuellt [!UICONTROL Merchant ID]. Du kan klistra in ID:n direkt i dessa indata eller använda ett dataelement i stället. Dessa fungerar som standardvärden som används vid anrop av en händelse till [!DNL The Trade Desk]-API:t för realtidskonverteringar. Välj **[!UICONTROL Save]** när du är klar.

Följ självstudiekursen [Skapa dataelement](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) om du vill lära dig hur du kan skapa dataelement och göra dem tillgängliga för tillägg i din taggegenskap.

![Konfigurationssidan för [!DNL The Trade Desk]-tillägget med fälten [!UICONTROL Advertiser ID] och [!UICONTROL Merchant ID] markerade.](../../../images/extensions/server/tradedesk/configure-extension.png)

Tillägget är installerat och du kan nu använda dess funktioner i reglerna för vidarebefordran av händelser.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

När du har installerat och konfigurerat tillägget kan du börja skapa regler för vidarebefordran av händelser som avgör hur och när händelser skickas till [!DNL The Trade Desk].

Du bör överväga att konfigurera flera regler för att skicka alla godkända [begäranegenskaper](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] och [!DNL The Trade Desk] Real-Time Conversions API.

>[!NOTE]
>
>Händelser bör skickas ut i realtid eller så nära realtid som möjligt.

Skapa en ny händelsevidarebefordring av [regel](../../../ui/managing-resources/rules.md) i din händelsevidarebefordringsegenskap. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL The Trade Desk]**. Välj sedan **[!UICONTROL Real Time Conversion]** för **[!UICONTROL Action Type]**.

![Vyn för egenskapsregler för vidarebefordran av händelser, med de fält som krävs för att lägga till en åtgärdskonfiguration för vidarebefordring av händelser, markerad.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsedata som ska skickas till [!DNL The Trade Desk]. Välj **[!UICONTROL Keep Changes]** om du vill spara regeln.

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
| Typ av annons-ID | Typ av reklam-ID som anges i AD ID-egenskapen: TDID, IDFA, AAID, DAID, NAID, IDL, EUID eller UID2. |
| Impression | En 36-teckensträng (inklusive bindestreck) som fungerar som det unika ID:t för det intryck som händelsen är kopplad till. |
| Order-ID | Händelsens associerade orderidentifierare. |
| td1-td10 | Tio sekventiellt numrerade anpassade dynamiska egenskaper som kan användas för att tillhandahålla ytterligare konverteringsmetadata. |

{style="table-layout:auto"}

![Avsnittet [!DNL Basic Request Properties] som visar exempeldata i fälten.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Mer information om [request properties](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) som accepteras av [!DNL The Trade Desk] Real-Time Conversions API finns i dokumentationen för [!DNL The Trade Desk]-utvecklaren.

**[!UICONTROL Object Request Parameters]**

Ett JSON-objekt som innehåller mer information. Du kan välja att använda en reducerad uppsättning indata för nyckelvärden eller att ange JSON i Raw-format. Dessutom kan du hämta dynamiska data från ett dataelement genom att markera diskarna (![Diskikon](/help/images/icons/database.png)) till höger.


![Avsnittet [!DNL Object Request Parameters] som visar tillgängliga fält.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Mer information om [!UICONTROL Object Request Parameters] och deras egenskaper finns i dokumentationen för [Real-Time Conversions Event](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) .

**[!UICONTROL Configuration Overrides]**

>[!NOTE]
>
>I fälten [!UICONTROL Configuration Overrides] kan du ange olika [!DNL Advertiser ID] och/eller [!DNL Merchant ID] för alla regler.

| Indata | Beskrivning |
| --- | --- |
| Annonsörs-ID | Unik identifierare för annonsören som den här händelsen är associerad med. Ett annat annonsörs-ID kan anges för att åsidosätta det ID som du angav i tilläggskonfigurationen. |
| Affärs-ID | Den unika identifierare som varje handlare anges av [!DNL The Trade Desk] under introduktionsprocessen. Ett annat handels-ID kan anges för att åsidosätta det ID som du angav i tilläggskonfigurationen. |

![Avsnittet [!DNL Configuration Overrides] som visar tillgängliga fält.](../../../images/extensions/server/tradedesk/configure-overrides.png)

När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**. Publicera slutligen en ny händelse som vidarebefordrar [build](../../../ui/publishing/builds.md) för att aktivera ändringar som gjorts i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL The Trade Desk] med API-tillägget [!DNL The Trade Desk] Real-Time Conversions. Här rekommenderas att du utökar integreringen genom att skapa distinkta regler som skickar specifika konverteringshändelser beroende på vilket som är tillämpligt för varje kampanj. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).

Mer information om hur du implementerar integrationen finns i [!DNL The Trade Desk]-dokumentationen om [de effektivaste strategierna för  [!DNL The Trade Desk] API:t för realtidskonverteringar](https://www.facebook.com/business/help/308855623839366?id=818859032317965).

Mer information om hur du felsöker implementeringen med verktyget för felsökning och övervakning av händelsevidarebefordran i Experience Platform finns i [Adobe Experience Platform Debugger-översikten](../../../../debugger/home.md) och [Övervaka aktiviteter i händelsevidarebefordran](../../../ui/event-forwarding/monitoring.md).
