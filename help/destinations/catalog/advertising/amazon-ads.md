---
title: Amazon Ads
description: Amazon Ads erbjuder en rad alternativ som hjälper er att nå era annonsmål för registrerade säljare, leverantörer, bokleverantörer, KDP-författare (Kindle Direct Publishing), apputvecklare och/eller byråer. Integreringen av Amazon Ads med Adobe Experience Platform ger körklar integrering med Amazon Ads-produkter, inklusive Amazon DSP (ADSP). Med Amazon Ads-destinationen i Adobe Experience Platform kan man definiera målgrupper för annonsörer för målinriktning och aktivering i Amazon DSP.
last-substantial-update: 2025-01-07T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 546ef0f9a5a9c37de3891aba02491540a5c6f8c9
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 1%

---

# Amazon Ads-anslutning {#amazon-ads}

## Översikt {#overview}

[!DNL Amazon Ads] erbjuder en rad alternativ som hjälper dig att nå dina annonsmål för registrerade säljare, leverantörer, bokleverantörer, KDP-författare (Kindle Direct Publishing), apputvecklare och/eller byråer.

Integreringen av [!DNL Amazon Ads] med Adobe Experience Platform ger körklar integrering med [!DNL Amazon Ads]-produkter, inklusive Amazon DSP (ADSP) och Amazon Marketing Cloud (AMC).

Med målplatsen [!DNL Amazon Ads] i Adobe Experience Platform kan användare definiera annonsörgrupper för målinriktning och aktivering i Amazon DSP.  Dessutom kan användare överföra sina data till [!DNL Amazon Marketing Cloud] för att förstå målgruppens prestanda, annonsörens tillhandahållna dimensioner, medlemskap i Amazon-segment eller andra signaler som är tillgängliga i AMC. När annonsörer har överförts till AMC kan användare använda [!DNL Amazon Marketing Cloud] för att ändra, förbättra eller lägga till i målgruppsmedlemmar med hjälp av Amazon-signaler inifrån [!DNL Amazon Marketing Cloud].

AMC sammanför unika signaler från olika Amazon-ägda och styrda kanaler, som omfattar alla medier, inklusive visning, video, direktuppspelad TV, ljud och sponsrade annonser. Användare kan enkelt skicka kuraterade segment från Adobe Experience Platform till AMC för att förbättra inlärningen, som målgruppernas marknadsgrupper, livsstilskohorter och varumärkesinteraktionsmönster. Augmenterade segment kan sedan användas för att optimera medieaktiveringar i Amazon DSP.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Amazon Ads]*-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *`amc-support@amazon.com`.*

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet *[!DNL Amazon Ads]* finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Aktivering och målinriktning {#activation-and-targeting}

Tack vare den här integreringen med Amazon DSP kan [!DNL Amazon Ads]-annonsörer skicka CDP-målgrupper från Adobe Experience Platform till Amazon DSP för att skapa marknadsföringsmålgrupper för annonsering. Målgrupper kan väljas inom Amazon DSP för positiv målinriktning och negativ målinriktning (undertryckning).

### Analyser och mätningar {#analytics-and-measurement}

Integrationen med [!DNL Amazon Marketing Cloud] (AMC) gör att [!DNL Amazon Ads] annonsörer kan skicka CDP-segment från Adobe Experience Platform-formulär till AMC. Annonsörer kan sedan ansluta sig till CDP-indata med [!DNL Amazon Ads]-signaler och utföra anpassade analyser på ämnen som mediapåverkan, målgruppssegment och kundresor i sekretessformat. En annonsör kan t.ex. ladda upp en lista över sina befintliga kunder för att förstå hur den samlade marknadsföringskampanjen fungerar, eller aggregerad statistik över konverteringshändelser på Amazon, som att visa en produktinformationssida, lägga en produkt i en kundvagn eller köpa en produkt.

### Advertising-optimering

Tack vare den här integreringen med [!DNL Amazon Marketing Cloud] (AMC) kan annonsörer överföra egna kundlistor och använda [!DNL Amazon Marketing Cloud] SQL för att utföra överlappningsanalyser, undertryckanden, tillägg eller optimeringar till målgrupper med jämna mellanrum innan de skapar en aktiveringsklar målgrupp i Amazon DSP för målgruppsanpassning.

## Förhandskrav {#prerequisites}

Om du vill använda [!DNL Amazon Ads]-anslutningen med Adobe Experience Platform måste användarna först ha tillgång till ett Amazon DSP Advertiser-konto eller en [!DNL Amazon Marketing Cloud]-instans. Om du vill etablera de här instanserna går du till följande sida på webbplatsen [!DNL Amazon Ads]:

* [Kom igång med Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Kom igång med Amazon Marketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identiteter som stöds {#supported-identities}

Anslutningen *[!DNL Amazon Ads]* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service//features/namespaces.md). Mer information om vilka identiteter som stöds av [!DNL Amazon Ads] finns på [Amazon DSP Support Center](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i målet *[!DNL Amazon Ads]*. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

Du dirigeras till [!DNL Amazon Ads]-anslutningsgränssnittet där du först väljer de annonserarkonton som du vill ansluta till. När du ansluter omdirigeras du tillbaka till Adobe Experience Platform med en ny anslutning som medföljer ID:t för det Advertiser-konto du har valt. Välj lämpligt Advertiser-konto på målkonfigurationsskärmen för att fortsätta.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Amazon Ads Connection]**: Välj ID för det [!DNL Amazon Ads]-målkonto som används för målet.

>[!NOTE]
>
>När du har sparat målkonfigurationen kan du inte ändra [!DNL Amazon Ads]-annons-ID, även om du autentiserar igen via ditt Amazon-konto. Om du vill använda ett annat [!DNL Amazon Ads] Advertiser-ID måste du skapa en ny målanslutning. Annonsörer som redan har konfigurerats för en integrering med ADSP måste skapa ett nytt målflöde om de vill att deras målgrupper ska levereras till AMC eller till ett annat ADSP-konto.

* **[!UICONTROL Advertiser Region]**: Välj lämplig region där annonsören finns. Mer information om vilka marknadsplatser som stöds av respektive region finns i [Amazon Ads-dokumentationen](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).

* **[!UICONTROL Amazon Ads Consent Signal]**: Bekräfta att alla data som skickas via den här anslutningen har samtyckt till att använda personuppgifter för annonsändamål. &quot;GRANTED&quot; innebär att Amazon samtycker till att använda kundens personuppgifter för annonsering. Tillåtna värden är &quot;GRANTED&quot; och &quot;DENIED&quot;. Alla poster som skickas via anslutningar med &quot;DENIED&quot; kommer att refuseras för vidare användning inom Amazon Ads.

![Konfigurera nytt mål](../../assets/catalog/advertising/amazon-ads/amazon_ads_consent_input.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

Anslutningen [!DNL Amazon Ads] har stöd för hash-kodade e-postadresser och hashade telefonnummer för identitetsmatchningssyften. Skärmbilden nedan innehåller ett exempel på matchning som är kompatibel med anslutningen [!DNL Amazon Ads]:

![Mappning av Adobe till Amazon Ads](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_2.png)

* Om du vill mappa hash-kodade e-postadresser väljer du identitetsnamnområdet `Email_LC_SHA256` som ett källfält.
* Om du vill mappa hash-kodade telefonnummer markerar du identitetsnamnområdet `Phone_SHA256` som ett källfält.
* Om du vill mappa ohashade e-postadresser eller telefonnummer markerar du motsvarande identitetsnamnutrymmen som källfält och markerar alternativet `Apply Transformation` om du vill att plattformen ska hash-koda identiteterna vid aktiveringen.
* *NYTT från och med versionen från september 2024*: Amazon Ads kräver att du mappar ett fält som innehåller ett `countryCode`-värde i ISO-format med två tecken för att underlätta identitetsmatchningsprocessen (t.ex. USA, GB, MX, CA och så vidare). Anslutningar utan `countryCode` mappningar kommer att få negativ effekt på identitetsmatchningsfrekvenserna.

Du väljer bara ett angivet målfält en gång i en destinationskonfiguration för [!DNL Amazon Ads]-kopplingen.  Om du till exempel skickar e-post för företag kan du inte heller mappa personlig e-post i samma målkonfiguration.

Vi rekommenderar att du mappar så många fält du har. Om bara ett källattribut är tillgängligt kan du mappa ett enskilt fält. Målet [!DNL Amazon Ads] använder alla mappade fält för mappningsändamål, vilket ger högre matchningsfrekvenser om fler fält anges. Mer information om godkända identifierare finns på [hjälpsidan för Amazon Ads hashed-målgrupper](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Exporterade data/Validera dataexport {#exported-data}

När målgruppen har överförts kan du validera att målgruppen har skapats och överförts korrekt enligt följande steg:

**För Amazon DSP**

Navigera till din **[!UICONTROL Advertiser ID]** > **[!UICONTROL Audiences]** > **[!UICONTROL Advertiser Audiences]**. Om målgruppen skapades och uppfyller det minsta antalet målgruppsmedlemmar visas statusen `Active`. Mer information om er målgruppsstorlek och räckvidd finns i den prognostiserade panelen Reach till höger om användargränssnittet i Amazon DSP.

![Verifiering av målgruppsgenerering i Amazon DSP](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_3.png)

**För[!DNL Amazon Marketing Cloud]**

I den vänstra schemaläsaren hittar du målgruppen under **[!UICONTROL Advertiser Uploaded]** > **[!UICONTROL aep_audiences]**. Du kan sedan fråga din målgrupp i AMC SQL-redigeraren med följande sats:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![Verifiering av målgruppsgenerering i Amazon Marketing Cloud](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_5.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare hjälpdokumentation finns på följande [!DNL Amazon Ads] hjälpresurser:

* [Amazon DSP Help Center](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Februari 2025 | Lagt till kravet att lägga till **[!UICONTROL Amazon Ads Consent Signal]** i exportdataflöden och befordrade målet från betaversionen till allmänt tillgängligt. |
| Maj 2024 | Funktioner och dokumentation | Mappningsalternativet har lagts till för att exportera parametern `countryCode` till Amazon Ads. Använd `countryCode` i [mappningssteget](#map) om du vill förbättra identitetsmatchningsfrekvensen med Amazon. |
| Mars 2024 | Funktioner och dokumentation | Lagt till alternativet att exportera målgrupper som ska användas i [!DNL Amazon Marketing Cloud] (AMC). |
| Maj 2023 | Funktioner och dokumentation | <ul><li>Stöd har lagts till för markering av reklamregion i [målanslutningsarbetsflödet](#destination-details).</li><li>Uppdaterad dokumentation som återspeglar tillägget av Advertiser Region. Mer information om hur du väljer rätt annonsregion finns i [Amazon-dokumentationen](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Mars 2023 | Inledande version | Ursprunglig målrelease och dokumentation publicerad. |

{style="table-layout:auto"}

+++
