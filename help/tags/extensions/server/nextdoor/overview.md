---
title: Nextdoor Conversion API Extension
description: Lär dig hur du använder API-tillägget för konvertering av Nextdoor för att skicka konverteringshändelser för att spåra hur era annonskampanjer fungerar.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 1%

---


# [!DNL Nextdoor] API-tillägg för konvertering - användarhandbok

## Översikt

[!DNL Nextdoor] är en social nätverkstjänst för grannskap som ansluter människor till deras lokala communities. Det är en plattform där grannar kan kommunicera, dela information, hålla sig uppdaterade på lokala event och nyheter samt köpa och sälja artiklar till andra i sina respektive områden.

Använd [[!DNL Nextdoor] konverterings-API-tillägget](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) för att skicka konverteringshändelser direkt till konverterings-API:t för [!DNL Nextdoor's]. Det här tillägget hjälper dig att spåra och mäta prestandan för dina [!DNL Nextdoor]-annonskampanjer genom att skicka konverteringsdata på serversidan.

I den här handboken visas hur du installerar, konfigurerar och använder tillägget [!DNL Nextdoor] för konverterings-API i [regler](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) för vidarebefordran av händelser.

## Förhandskrav {#prerequisites}

Du behöver ett giltigt [!DNL Nextdoor] Ads Manager-konto för att kunna använda det här tillägget. Om du inte redan har en, gå till [[!DNL Nextdoor Ads] registreringssidan](https://ads.nextdoor.com/v2/signup) för att registrera dig och skapa ditt konto.

### Samla nödvändig konfigurationsinformation {#configuration-details}

Om du vill ansluta Experience Platform till [!DNL Nextdoor] behöver du följande information:

| Autentiseringsuppgifter | Beskrivning | Säkerhetsinformation |
| --- | --- | --- |
| Data-Source-ID | Din unika datakällidentifierare från [!DNL Nextdoor], som du kan hitta i ditt [!DNL Nextdoor Ads Manager]-konto genom att gå till sidan Assets > Pixlar och skapa en Nextdoor Pixel. | Det är säkert att dela detta inom din organisation. |
| Åtkomsttoken | Åtkomsttoken för API-autentisering för säker kommunikation. Du kan generera denna token genom att logga in på ditt [!DNL Nextdoor Ads Manager]-konto och komma åt API-inställningarna. | Skydda denna token eftersom den ger åtkomst till ditt konto. |

## Installera och konfigurera tillägget [!DNL Nextdoor] {#install}

Om du vill installera tillägget väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen. Markera **[!UICONTROL Catalog]** på fliken **[!UICONTROL Nextdoor Conversion API Extension]** och välj sedan **[!UICONTROL Install]**.

![Tilläggskatalogen som visar installationen av [!DNL Nextdoor] tilläggskort.](../../../images/extensions/server/nextdoor/install-extension.png)

På nästa skärm anger du de konfigurationsvärden som du genererade från din [!DNL Nextdoor Ads Manager]:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

När du är klar väljer du **[!UICONTROL Save]**.

Konfigurationsskärmen ![[!DNL Nextdoor] för [!DNL Nextdoor]-konverterings-API-tillägget.](../../../images/extensions/server/nextdoor/configure.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till [!DNL Nextdoor].

Skapa en ny [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL Nextdoor Conversion API Extension]**. Om du vill skicka Edge Network-händelser till [!DNL Nextdoor] anger du **[!UICONTROL Action Type]** till **[!UICONTROL Report Web Conversions]**.

![Åtgärdstypen [!UICONTROL Report Web Conversions] som väljs för en [!DNL Nextdoor]-regel i användargränssnittet för datainsamling.](../../../images/extensions/server/nextdoor/select-action.png)

När du har gjort det här valet visas ytterligare kontroller som gör att du kan konfigurera händelsen ytterligare enligt instruktionerna nedan. När du är klar väljer du **[!UICONTROL Keep Changes]** för att spara regeln.

**Huvudinnehållsparametrar**

Dessa huvudparametrar definierar din konverteringshändelse:

| Parameter | Beskrivning | Datatyp | Obligatoriskt | Alternativ/format | Exempel |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Anger vilken typ av konverteringshändelse som spåras. | Sträng (listruta) | Obligatoriskt | <ul><li>Inköp</li><li>Lead</li><li>Registrera dig</li><li>Lägg i kundvagnen</li><li>Initiera utcheckning</li><li>Sidvy</li><li>Sök</li><li>Visa innehåll</li><li>Lägg till i önskelista</li><li>Prenumerera</li><li>Egen</li></li>Konvertering 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Unik identifierare för att förhindra dubblerad händelserapport. Detta genereras automatiskt om det är tomt. | Sträng | Valfritt | Unik strängidentifierare | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Tidsstämpel när konverteringshändelsen inträffade. Standardvärdet är aktuell tid om inget anges. | Heltal | Valfritt | Unik tidsstämpel i sekunder | `1703980800` (30 dec 2023) |
| [!UICONTROL Action Source] | Kanal eller plattform där konverteringen inträffade. | Sträng (listruta) | Obligatoriskt | <ul><li>webbplats</li><li>e-post</li><li>app</li><li>phone_call</li><li>chatta</li><li>physical_store</li><li>system_generated</li><li>övriga</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Åsidosätt det globala datakällans ID för specifika händelser. Ärver från konfigurationen om inget anges. | Sträng | Valfritt | Alfanumerisk sträng | `12345` |
| [!UICONTROL Action Source URL] | Den specifika URL där konverteringen inträffade. | Sträng | Valfritt | Fullständig URL inklusive protokoll | https://example.com/checkout/success |

**Parametrar för sekretess och efterlevnad**

Använd de här parametrarna för att säkerställa sekretess:

| Parameter | Beskrivning | Datatyp | Obligatoriskt | Värden/format | Exempel |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Flagga för att begränsa dataanvändning för sekretess. | Heltal | Valfritt | <ul><li>0 = Inga begränsningar</li><li>1 = Begränsa</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Landspecifika begränsningar för databehandling. | Heltal | Valfritt | 1 = USA (andra koder kan stödjas) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Statsspecifika restriktioner för användare i USA. | Heltal | Valfritt | 1000 = CA, 1001 = CO, osv. | `1000` |
| [!UICONTROL Test Event] | Markerar händelsen som ett test för utveckling/felsökning. | Sträng | Valfritt | Valfri sträng som inte är tom | `test` |

**Parametrar för kundinformation**

>[!IMPORTANT]
>
>Du måste ange minst en kundinformationsparameter för korrekt händelseattribuering och matchning.

| Parameter | Beskrivning | Datatyp | Obligatoriskt | Format | Exempel |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | Kundens e-postadress för identitetsmatchning. | Sträng | Minst ett kundfält krävs | Normal text eller SHA-256-hash | `user@example.com` |
| [!UICONTROL Phone Number] | Kundens telefonnummer för identitetsmatchning. | Sträng | Minst ett kundfält krävs | E.164-format (hashas med SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Kundens förnamn för förbättrad matchning. | Sträng | Minst ett kundfält krävs | Normal text eller SHA-256-hash | `John` |
| [!UICONTROL Last Name] | Kundens efternamn för förbättrad matchning. | Sträng | Minst ett kundfält krävs | Normal text eller SHA-256-hash | `Smith` |
| [!UICONTROL Date of Birth] | Kundens födelsedatum för demografisk matchning. | Sträng | Valfritt | YYYMMDD (SHA-256 hash) | `19900115` |
| [!UICONTROL Gender] | Kundens kön för demografisk målgruppsanpassning. | Sträng | Valfritt | M/F/O (SHA-256 hash) | `M` |
| [!UICONTROL External ID] | Din interna kund-ID. | Sträng | Valfritt | Alla unika strängar | `customer_12345` |
| [!UICONTROL Street Address] | Kundens gatuadress. | Sträng | Valfritt | SHA-256 hash | `123 Main Street` (hash) |
| [!UICONTROL City] | Kundens stad. | Sträng | Valfritt | SHA-256 hash | `San Francisco` (hash) |
| [!UICONTROL State] | Kundens delstat/provins. | Sträng | Valfritt | Kod med två bokstäver (SHA-256 hash) | `CA` (hash) |
| [!UICONTROL Zip Code] | Kundens postnummer. | Sträng | Valfritt | USA:s första fem siffror (SHA-256 hashed) | `94102` (hash) |
| [!UICONTROL Country] | Kundens land. | Sträng | Valfritt | ISO-3166-1 alpha-2 (SHA-256 hashed) | `US` (hash) |
| [!UICONTROL Click ID] | Nextdoor click identifier for attribution. | Sträng | Valfritt | Hämtat från URL-parametern `ndclid` | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | IP-adress till användarens enhet. | Sträng | Valfritt | IPv4- eller IPv6-adress | `192.168.1.1` |
| [!UICONTROL Client User Agent] | Användaragentsträng för webbläsare. | Sträng | Valfritt | Användaragentsträng för Raw-webbläsare | `Mozilla/5.0 (Windows...)` |

**Egna parametrar**

Dessa parametrar ger ytterligare kontext om konverteringshändelsen:

| Parameter | Beskrivning | Datatyp | Obligatoriskt | Format | Exempel |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Totalt värde för inköpstransaktionen. | Sträng | **KRÄVS för inköpshändelser** | ISO 4217 Currency + Amount (inga blanksteg) | `USD123.45` |
| [!UICONTROL Order ID] | Unik transaktions- eller orderidentifierare. | Sträng | Valfritt | Alla unika strängar | `order_12345` |
| [!UICONTROL Delivery Category] | Leveranssätt för produkt/tjänst. | Sträng | Valfritt | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Detaljerad information om köpta produkter. | String (JSON-array) | Valfritt | JSON-array med produktobjekt | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Mobilappsparametrar**

Du måste inkludera de här parametrarna när `Action Source = 'APP'`:

| Parameter | Beskrivning | Datatyp | Obligatoriskt | Format | Exempel |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Identifierare för mobilprogram. | Sträng | **KRÄVS för APP-händelser** | <ul><li>Paket-ID (iOS)</li><li>Paketnamn (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | Medgivandestatus för iOS App Tracking Transparency. | Sträng | **KRÄVS för APP-händelser** | Boolesk sträng | `true` |
| [!UICONTROL Platform] | Mobiloperativsystem. | Sträng | **KRÄVS för APP-händelser** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Version av mobilprogrammet. | Sträng | **KRÄVS för APP-händelser** | Versionssträng enligt appens definition | `2.0.0-beta` |

## Händelsetyper {#event-types}

Följande händelsetyper stöds för olika konverteringsscenarier:

| Händelsenamn | Händelsetyp | Beskrivning | Användningsfall | Obligatoriska fält | Anteckningar |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Standard | Slutförd inköpstransaktion. | E-handelskonverteringar | <ul><li>Händelsenamn</li><li>Ordervärde</li><li>Kundinformation</li></ul> | Viktigast för ROAS-optimering |
| [!UICONTROL Lead] | Standard | Leadgenerering eller förfrågan. | Skicka formulär, kontaktförfrågningar | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Högvärdeskonvertering för B2B |
| [!UICONTROL Sign Up] | Standard | Användarregistrering eller kontoskapande. | Registrering av nyhetsbrev, kontoregistrering | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Funnel populäraste konverteringsspårning |
| [!UICONTROL Add to Cart] | Standard | Produkten läggs till i kundvagnen. | Funnel tracking för e-handel | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Mid-funnel-engagemangssignal |
| [!UICONTROL Initiate Checkout] | Standard | Utcheckningsprocessen har startats. | Spårning av inköpsavsikt | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Indikator för stark inköpsmetod |
| [!UICONTROL Page View] | Standard | Viktig sida besöktes. | Content engagement, landningssidor | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Använd endast för sidor med högt värde |
| [!UICONTROL Search] | Standard | Sök på webbplatsen. | Produkt-/innehållsidentifiering | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Anger aktivt användarengagemang |
| [!UICONTROL View Content] | Standard | Innehåll eller produkt visas. | Vyer av produktsidor, innehållsengagemang | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Användbar för återmarknadsföring |
| [!UICONTROL Add to Wishlist] | Standard | Produkten har lagts till i önskelistan. | Framtida inköpsmetod | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Anger starkt produktintresse |
| [!UICONTROL Subscribe] | Standard | Prenumeration på service/nyhetsbrev. | Återkommande intäkter, engagemang | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Indikator för värde för högsta livstid |
| [!UICONTROL Custom Conversion 1 - 10] | Egen | Affärsspecifik konverteringshändelse. | Definiera din egen konverteringstyp | <ul><li>Händelsenamn</li><li>Kundinformation</li></ul> | Anpassa för unika affärsåtgärder |

## Integrering av dataelement {#data-element}

Alla fält har stöd för dataelement för vidarebefordran av Adobe-händelser. Markera dataelementsikonen ![dataelement](../../../images/extensions/server/nextdoor/data-element-icon.png) bredvid ett fält för att:

* **Välj befintliga dataelement**: Välj bland dataelement som redan har skapats.
* **Lägg till nya dataelement**: Skapa och definiera nya dataelement efter behov.
* **Använd dynamiska värden**: Fyll i fält med dynamiskt innehåll som kommer från din webbplats.

## Bästa praxis {#best-practices}

Följ dessa metodtips för att säkerställa korrekt konverteringsspårning, förbättra datakvaliteten och följa sekretesslagstiftningen. Dessa rekommendationer hjälper dig att maximera effekten av integreringen av konverterings-API:t för [!DNL Nextdoor] och optimera dina annonsresultat.

### Datakvalitet och sekretess

Korrekt datahantering är nödvändigt för att maximera konverteringsattribueringens exakthet samtidigt som användarsekretess och efterlevnad av gällande regelverk upprätthålls. Dessa rutiner hjälper er att säkerställa att era kunddata är korrekt formaterade, behandlas på ett säkert sätt och hanteras i enlighet med sekretesslagstiftningen.

* **Använd konsekvent dataformatering**: Formatera e-post, telefonnummer och andra data på ett konsekvent sätt:

   * **Normalisering av e-post**: Konvertera e-postmeddelanden till gemener, rensa mellanrum och ta bort punkter från [!DNL Gmail] adresser.
   * **Standardisering av telefonnummer**: Använd E.164-format (+1234567890) för internationell kompatibilitet.
   * **Adressnormalisering**: Standardisera gatabbrevieringar (St., Ave., Rd.) och ta bort eventuella extra blanksteg.
   * **Namnformatering**: Konvertera namn till gemener, ta bort extra blanksteg och hantera specialtecken konsekvent.

* **Hash-känsliga data**: Överväg att hash-koda känsliga kunddata innan du skickar dem. Normalisera alltid dina data före hash-kodning för att säkerställa konsekventa hash-värden:

   * Använd SHA-256-hash för telefonnummer, adresser och andra PII-filer.
   * Tillägget kommer automatiskt att skicka e-postmeddelanden med oformaterad text - du kan skicka båda formaten.
   * Hash-koda data på ett enhetligt sätt i alla era uppföljningsimplementationer.
      * **Exempel**: Normalisera&quot;John@Example.COM&quot; →&quot;john@example.com&quot; före hash-kodning.

* **Ange fullständig information**: Inkludera så mycket kundinformation som möjligt för bättre matchning:

   * Inkludera flera identifierare (e-post + telefon eller e-post + namn + adress) när de är tillgängliga.
   * Använd externa kund-ID:n för att länka konverteringshändelser till dina CRM-data.
   * Tillhandahålla demografiska data (ålder, kön) när sådana finns tillgängliga och i enlighet med lagstiftningen om integritetsskydd.

* **Samtyckeshantering**: Kontrollera att du har rätt medgivande för datainsamling:

   * Implementera korrekta mekanismer för samtycke innan ni samlar in kunddata.
   * Respektera användarens avanmälningsinställningar och begäran om borttagning av data.
   * Använd parametrarna för begränsad dataanvändning för användare som har avanmält sig.
   * **Resurser**:
      * [GDPR-efterlevnadshandbok](https://gdpr.eu/compliance/)
      * [CCPA - Integritetskrav](https://oag.ca.gov/privacy/ccpa)

* **Dataminivå**: Skicka bara nödvändiga data för konverteringsspårning:

   * Samla bara in och skicka data som är viktiga för attribuering och optimering.
   * Granska och granska datafälten som du skickar regelbundet.
   * Ta bort onödig kundinformation för att minska sekretessriskerna.

* **Använd korrekta tidsstämplar**: Kontrollera att händelsens tidsstämplar är korrekta för korrekt attribuering.
   * Använd den faktiska tiden när konverteringen inträffade, inte när du bearbetade data.
   * Kontrollera att tidsstämplarna är i Unix Epooch-format (sekunder sedan 1 januari 1970).
   * Konto för tidszonsskillnader i tidsstämpelberäkningar.

### Händelseborttagning

Förhindra dubbla konverteringshändelser för att säkerställa korrekt kampanjmätning och undvika inflationsstatistik. Implementera korrekt borttagning av dubbletter så att varje konvertering bara räknas en gång, vilket ger tillförlitliga data för era optimeringsbeslut.

* **Ange unika händelse-ID:n**: Använd alltid unika händelse-ID:n för att förhindra dubblettkonverteringar.
* **Använd konsekvent namngivning**: Använd konsekvent namngivning av händelser i hela implementeringen.

### Hastighetsbegränsning

Konverterings-API:t [!DNL Nextdoor] omfattas av hastighetsbegränsning. Den aktuella hastighetsgränsen är **100 förfrågningar/minut** per annonsörer. Om du överskrider hastighetsgränsen returnerar API:t en `HTTP 429 Too Many Requests`-felkod.

## Slutsats {#conclusion}

Konverterings-API-tillägget [!DNL Nextdoor] är ett kraftfullt sätt att spåra konverteringar och mäta effektiviteten för dina [!DNL Nextdoor] -annonskampanjer. Genom att följa den här guiden och implementera de bästa metoderna kan ni säkerställa korrekt konverteringsspårning och optimera annonsresultatet.

Den senaste informationen och ytterligare resurser finns på [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Nästa steg {#next-steps}

Den här guiden visar hur du skickar händelsedata på serversidan till [!DNL Nextdoor] med hjälp av [!DNL Nextdoor]-tillägget för konverterings-API. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
