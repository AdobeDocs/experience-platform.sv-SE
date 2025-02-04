---
title: API-tillägg för konvertering av Adobe Snapchat
description: Med Adobe Experience Platform webbevent-API kan du dela webbplatsinteraktioner direkt med Snapchat.
last-substantial-update: 2025-01-20T00:00:00Z
source-git-commit: 6403c339b2407410e282a25a0382845214bb6a95
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Snapchat] för konverterings-API

Konverterings-API-tillägget [!DNL Snap] är ett säkert [Edge Network Server-API](/help/server-api/overview.md) som gör att du kan dela information med [!DNL Snapchat] direkt om användaråtgärder på dina webbplatser. Du kan utnyttja reglerna för vidarebefordran av händelser för att skicka data från **[!DNL Adobe Experience Platform Edge Network]** till **[!DNL Snapchat]** med hjälp av tillägget **[!DNL Snap]** för konverterings-API.

## Krav för [!DNL Snapchat] {#prerequisites}

Om du vill använda konverterings-API:t [!DNL Snapchat] måste du ha en [händelsevidarebefordringsegenskap](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started) konfigurerad i Adobe Experience Platform och de [nödvändiga behörigheterna](https://experienceleague.adobe.com/en/docs/experience-platform/collection/permissions) för att kunna redigera egenskapen.

Skapa en [dataström](/help/tags/ui/event-forwarding/getting-started.md) och lägg till tjänsten [Händelsevidarebefordran](/help/tags/ui/event-forwarding/getting-started#enable-event-forwarding) i den.

Ett **[!DNL Snapchat]** [Business Manager](https://business.snapchat.com/)-konto krävs för att använda konverterings-API:t. Business Manager hjälper annonsörer att integrera marknadsföringsaktiviteter från **[!DNL Snapchat]** i sina företag och med externa partner. Se artikeln **[!DNL Snapchat]** [Help center](https://businesshelp.snapchat.com/s/article/get-started?language=en_US) om hur du skapar ett Business Manager-konto om du inte har ett.

En **[!DNL Snap Pixel]**(https://businesshelp.snapchat.com/s/article/pixel-website-install?language=en_US) måste konfigureras i Snapchat Ads Manager och du måste ha åtkomst för att kunna visa `Pixel ID`. `Pixel ID` finns i avsnittet **[!UICONTROL Events Manager]**(https://businesshelp.snapchat.com/s/article/events-manager?language=en_US).

Du behöver en statisk, långlivad API-token. Se [[!DNL Snapchat] Konverterings-API-dokumentationen](https://developers.snap.com/api/marketing-api/Conversions-API/GetStarted#access-token) för att hämta denna token.

## Installera och konfigurera API-tillägget för [!DNL Snapchat]-webbhändelser {#install}

Navigera till **[!UICONTROL Data Collection]**>**[!UICONTROL Event Forwarding]** om du vill installera tillägget. Välj den egenskap där du vill installera tillägget.

Följ de här stegen när du har valt önskad egenskap:

1. Välj **[!UICONTROL Extensions]** i den vänstra navigeringspanelen.
2. Sök efter **[!UICONTROL Snap Conversion API Extension]** och välj **[!UICONTROL Install]**.

   ![Installationsknappen ](../../../images/extensions/server/snap/install.png) visas i bilden.

3. Ange följande värden på konfigurationsskärmen:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL API Token]**

När du är klar väljer du **[!UICONTROL Save]**.

![Bild som visar Pixel-ID och API-tokenknapp](../../../images/extensions/server/snap/configure.png).
<!-- 
![[!DNL Snap] configuration screen for the [!DNL Snap] conversion API extension.](../../../images/extensions/server/snap/configure.png) -->

## Skapa dataelement {#create-data-elements}

Om du vill skicka datapunkter som parametrar till API-tillägget [!DNL Snapchat] för konvertering måste du skapa [dataelement](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding#create-an-event-forwarding-data-element) för varje datapunkt. Följ de här stegen:

1. Navigera till **[!UICONTROL Authoring]**>**[!UICONTROL Data Elements]** på egenskapens **[!UICONTROL Property Info]**-skärm och välj sedan **[!UICONTROL Add Data Element]**.

   ![Bilden visar knappen för att lägga till dataelement](../../../images/extensions/server/snap/add_data_element.png).

2. Ange ett namn för dataelementet.

3. Välj **[!UICONTROL Core]** som tillägg och **[!UICONTROL Path]** som dataelementtyp.

4. I listrutan väljer du lämpligt alternativ och fyller i fältet [!UICONTROL Path] på den högra panelen för att referera till önskade data i ditt schema.

   ![Bild som visar skärmen för att skapa dataelement](../../../images/extensions/server/snap/create_data_element.png).

Om du till exempel skapar ett dataelement som refererar till `snapClickId` i schemat som visas nedan:

![Bilden visar schemat ](../../../images/extensions/server/snap/schema.png).

Du måste konfigurera dataelementet eftersom `snapClickId` finns under `_snap.inc.exchange` i XDM-schemat.

![Bild som visar skärmen för redigeringsdataelement](../../../images/extensions/server/snap/edit_data_element.png).

Mer information om hur du skapar dataelement finns i dokumentationen [Egenskaper för vidarebefordran av händelser](/help/tags/ui/event-forwarding/overview#data-elements.md).

## Skapa regler för att skicka konverteringshändelser som ska snabbas {#create-snap-rules}

[Regler](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding#create-an-event-forwarding-rule) används för att utlösa tillägg i plattformen. I det här avsnittet beskrivs hur du skapar regler i egenskapen för vidarebefordring av händelser för att skicka konverteringshändelser till Snap med tillägget för Conversions API.

### Skapa en ny regel

1. Navigera till egenskapen för vidarebefordran av händelser och välj **[!UICONTROL Rules]** på redigeringsmenyn. Klicka sedan på **[!UICONTROL Create New Rule]**.

   ![Bild som visar regler i den vänstra navigeringen](../../../images/extensions/server/snap/create_new_rule.png).

2. Ge regeln ett namn och konfigurera ett villkor för att aktivera Snap-händelsen. Om du till exempel vill skicka en `PURCHASE`-händelse när en händelse innehåller ett ordernummer anger du ett villkor för att kontrollera om användarinteraktionen innehåller ett giltigt inköpsordernummer.

   ![Bilden visar konfigurationsskärmen för villkor](../../../images/extensions/server/snap/action_configuration.png).

3. När du har sparat villkoret lägger du till en åtgärd som utlöser API:t för fästkonvertering. I den vänstra panelen:

   * Ställ in listrutemenyn [!UICONTROL Extension] på [!UICONTROL Snap Conversions API Extension].

   * Ställ in listrutemenyn [!UICONTROL Action Type] på [!UICONTROL Report Web Conversions].

   * Namnge regeln därefter.

   ![Bilden visar åtgärdskonfigurationsskärmen](../../../images/extensions/server/snap/action_configuration.png).

4. Konfigurera de [CAPI-parametervärden](https://developers.snap.com/api/marketing-api/Conversions-API/Parameters) som du vill skicka för händelsen i avsnittet **[!UICONTROL Data Bindings]** på den högra panelen. Fälten i tillägget mappas till CAPI-parametrar enligt nedan. Mer information om de olika parametrarna finns i [API-dokumentationen för Snapchat-konverteringar](https://developers.snap.com/api/marketing-api/Conversions-API/Parameters).

| Databindningsfält | Snap CAPI-parameter |
| --- | --- |
| Händelsetyp (obligatoriskt) | `event_name` |
| E-post | `em` |
| Telefonnummer | `ph` |
| Användaragent | `client_user_agent` |
| IP-adress | `client_ip_address` |
| Klicka på ID | `sc_click_id` |
| Cookie1 | `so_cookie1` |
| Förnamn | `fn` |
| Efternamn | `ln` |
| Kön | `ge` |
| Ort | `ph` |
| Läge | `st` |
| Postnummer | `zp` |
| Land | `country` |
| Externt ID | `external_id` |
| Partner-ID | `partner_id` |
| Prenumerations-ID | `subscription_id` |
| Lead-ID | `lead_id` |
| Artikel eller kategori | `content_category` |
| Innehållsnamn | `content_ids` |
| Innehållstyp | `content_name` |
| Innehåll | `contents` |
| Beskrivning | `description` |
| Händelsetagg | `event_tag` |
| Antal objekt | `num_items` |
| Pris | `value` |
| Valuta | `currency` |
| Transaktions-ID | `order_id` (skickas även för `event_id` i stället för `client dedup idD`) |
| Förutsedd LTV | `predicted_ltv` |
| Söksträng | `search_string` |
| Registreringsmetod | `sign_up_method` |
| Klientens avlämnings-ID | `event_id` |
| Begränsad dataanvändning | `data_processing_options` |
| Sidadress | `event_source_url` |

### Obligatoriska och valfria fält

* Obligatoriska fält:

   * Alla händelser har `event_source` inställt på `WEB`.

   * Minst ett av följande fält eller kombinationer krävs för matchning:

      * E-post
      * Telefonnummer
      * IP-adress och användaragent

**Ytterligare information:**

* För `Purchase` händelser krävs fälten `Currency` och `Price`.

* Om du aktiverar kryssrutan **[!UICONTROL Test Mode]** skickas händelser som testhändelser, som visas i verktyget för testhändelser i stället för som standardrapporter. Mer information finns i den här [hjälpartikeln för företag](https://businesshelp.snapchat.com/s/article/capi-event-testing?language=en_US#:~:text=Snap&#39;s%20Conversions%20API%20(CAPI)%20Test,being%20processed%20as%20production%20results.).

* Parametern `contents` ska vara en JSON-sträng som innehåller minst ett av följande fält:

   * `id`
   * `item_category`
   * `brand`
   * `delivery_category`
   * `item_price`
   * `quantity`

Exempel:

```json
{
  "id": "id1",
  "brand": "brand1",
  "delivery_category": "c1",
  "item_price": 2.00,
  "quantity": 2
}
```

Om du vill använda [anpassade konverteringsvärden och ROAS-rapportering](https://businesshelp.snapchat.com/s/article/custom-conversions-value-roas?language=en_US) inkluderar du relevanta parametrar i fältet `contents`. Exempel: `brand`, `item_price`, `id`.

Exempelkonfiguration för en `Purchase`-händelse:

[Bild som visar databindningar](../../../images/extensions/server/snap/data_bindings.png)

De valfria fälten kan anges enligt följande:

[Bild som visar valfria fält](../../../images/extensions/server/snap/optional_fields.png)

När du har angett regelns namn, villkor och åtgärd enligt beskrivningen ovan, sparar du regeln och kontrollerar att den är aktiverad.

[Bild som visar aktiverad regel](../../../images/extensions/server/snap/enabled_rule.png)

Du kan nu publicera dessa ändringar i din egenskap. Mer information finns i dokumentationen om [publiceringsflödet](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview).

## Felsökning {#troubleshoot}

Om du vill felsöka och optimera konfigurationen kan du läsa rekommendationerna för [händelsekvalitet](https://businesshelp.snapchat.com/s/article/event-quality-score) för att försäkra dig om att dina händelser uppnår högsta möjliga matchningsfrekvens och prestandatillgångar.

Om du får problem med din **händelsekvalitet** kan du läsa mer om våra rekommendationer om hur du kan förbättra den [här](https://businesshelp.snapchat.com/s/article/esq-issues-recommendations?language=en_US).

## Nästa steg {#next-steps}

I den här guiden beskrivs hur du skickar händelsedata på serversidan till **[!DNL Snap]** med tillägget **[!DNL Snap Conversions API]**. Mer information om funktioner för att vidarebefordra händelser i plattformen finns i [Översikt över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
