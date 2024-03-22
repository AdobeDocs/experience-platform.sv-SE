---
title: Amazon Ads
description: Amazon Ads erbjuder en rad alternativ som hjälper er att nå era annonsmål för registrerade säljare, leverantörer, bokleverantörer, KDP-författare (Kindle Direct Publishing), apputvecklare och/eller byråer. Integreringen av Amazon Ads med Adobe Experience Platform ger körklar integrering med Amazon Ads-produkter, inklusive Amazon DSP (ADSP). Med Amazon Ads-destinationen i Adobe Experience Platform kan man definiera målgrupper för annonsörer för målinriktning och aktivering i Amazon DSP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 8e34e5488ab80cd1f3c8086bf7c16d3f22527540
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 1%

---

# (Beta) Amazon Ads-anslutning {#amazon-ads}

## Översikt {#overview}

[!DNL Amazon Ads] erbjuder en mängd alternativ som hjälper er att nå era annonsmål för registrerade säljare, leverantörer, bokleverantörer, KDP-författare (Kindle Direct Publishing), apputvecklare och/eller byråer.

The [!DNL Amazon Ads] integrering med Adobe Experience Platform ger nyckelfärdig integrering med [!DNL Amazon Ads] -produkter, inklusive Amazon DSP (ADSP) och Amazon Marketing Cloud (AMC).

Använda [!DNL Amazon Ads] i Adobe Experience Platform kan man definiera annonsörernas målgrupper för målgruppsanpassning och aktivering i Amazon DSP.  Dessutom kan användare överföra sina data till [!DNL Amazon Marketing Cloud] för att förstå målgruppens resultat, tillhandahåller annonsörer dimensioner, medlemskap i Amazon-segment eller andra signaler som är tillgängliga i AMC. När annonsörer har överförts till AMC kan användarna använda [!DNL Amazon Marketing Cloud] för att ändra, förbättra eller lägga till material till målgrupper med Amazon-signaler inifrån [!DNL Amazon Marketing Cloud].

AMC sammanför unika signaler från olika Amazon-ägda och styrda kanaler, som omfattar alla medier, inklusive visning, video, direktuppspelad TV, ljud och sponsrade annonser. Användare kan enkelt skicka kuraterade segment från Adobe Experience Platform till AMC för att förbättra inlärningen, som målgruppernas marknadsgrupper, livsstilskohorter och varumärkesinteraktionsmönster. Augmenterade segment kan sedan användas för att optimera medieaktiveringar i Amazon DSP.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Amazon Ads]* team. Detta är för närvarande en betaprodukt och funktionaliteten kan komma att ändras. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *`amc-support@amazon.com`.*

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda *[!DNL Amazon Ads]* mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda denna destination.

### Aktivering och målinriktning {#activation-and-targeting}

Tack vare integreringen med Amazon DSP kan [!DNL Amazon Ads] annonsörer för att skicka annonsörer CDP-målgrupper från Adobe Experience Platform till Amazon DSP för att skapa annonsörer för målgruppsanpassning. Målgrupper kan väljas i Amazon-DSP för positiv målinriktning och negativ målinriktning (undertryckning).

### Analyser och mätningar {#analytics-and-measurement}

Integreringen med [!DNL Amazon Marketing Cloud] (AMC) tillåter [!DNL Amazon Ads] annonsörer skicka CDP-segment från Adobe Experience Platform-formulär till AMC. Annonsörer kan sedan ansluta CDP-indata med [!DNL Amazon Ads] signalera och utföra anpassade analyser i ämnen som mediernas inverkan, målgruppssegment och kundresor i sekretessformat. En annonsör kan t.ex. ladda upp en lista över sina befintliga kunder för att förstå hur den samlade marknadsföringskampanjen fungerar, eller aggregerad statistik över konverteringshändelser på Amazon, som att visa en produktinformationssida, lägga en produkt i en kundvagn eller köpa en produkt.

### Annonsoptimering

Integreringen med [!DNL Amazon Marketing Cloud] (AMC) tillåter annonsörer att ladda upp sina egna kundlistor och använda [!DNL Amazon Marketing Cloud] SQL, utför återkommande överlappningsanalyser, undertryckningar, tillägg eller optimeringar till målgrupper innan ni skapar en aktiveringsfärdig målgrupp i Amazon DSP för målinriktning.

## Förutsättningar {#prerequisites}

Använd [!DNL Amazon Ads] anslutning till Adobe Experience Platform måste användarna först ha tillgång till ett Amazon DSP Advertiser-konto eller [!DNL Amazon Marketing Cloud] -instans. Om du vill etablera dessa förekomster går du till följande sida på sidan [!DNL Amazon Ads] webbplats:

* [Kom igång med Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Kom igång med Amazon Marketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identiteter som stöds {#supported-identities}

The *[!DNL Amazon Ads]* anslutningen stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service//features/namespaces.md). Mer information om vilka identiteter som stöds av [!DNL Amazon Ads], går till [Amazon DSP Support Center](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i *[!DNL Amazon Ads]* mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

Du kommer till [!DNL Amazon Ads] anslutningsgränssnitt där du först väljer de annonseringskonton som du vill ansluta till. När du ansluter omdirigeras du tillbaka till Adobe Experience Platform med en ny anslutning som medföljer ID:t för det Advertiser-konto du har valt. Välj lämpligt Advertiser-konto på målkonfigurationsskärmen för att fortsätta.

* **[!UICONTROL Bearer token]**: Fyll i bearer-token för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Amazon Ads Connection]**: Välj ID för målet [!DNL Amazon Ads] konto som används för målet.

>[!NOTE]
>
>När du har sparat målkonfigurationen kan du inte ändra [!DNL Amazon Ads] Advertiser-ID:t, även om du autentiserar igen via ditt Amazon-konto. Så här använder du en annan [!DNL Amazon Ads] Advertiser ID, du måste skapa en ny målanslutning.

* **[!UICONTROL Advertiser Region]**: Välj lämplig region där annonsören finns. Mer information om vilka marknadsplatser som stöds i respektive region finns på [Amazon Ads-dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Konfigurera nytt mål](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

The [!DNL Amazon Ads] anslutningen stöder hash-kodad e-postadress och hashade telefonnummer för identitetsmatchning. Skärmbilden nedan innehåller ett exempel på matchning som är kompatibel med [!DNL Amazon Ads] anslutning:

![Mappning av Adobe till Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Om du vill mappa hash-kodade e-postadresser väljer du `Email_LC_SHA256` identitetsnamnområde som ett källfält.
* Om du vill mappa hash-kodade telefonnummer väljer du `Phone_SHA256` identitetsnamnområde som ett källfält.
* Om du vill mappa ohashade e-postadresser eller telefonnummer markerar du motsvarande ID-namnutrymmen som källfält och kontrollerar `Apply Transformation` möjlighet att låta Platform hash-koda identiteterna vid aktiveringen.

Du väljer bara ett angivet målfält en gång i en destinationskonfiguration för [!DNL Amazon Ads] koppling.  Om du till exempel skickar e-post för företag kan du inte heller mappa personlig e-post i samma målkonfiguration.

Vi rekommenderar att du mappar så många fält du har. Om bara ett källattribut är tillgängligt kan du mappa ett enskilt fält. The [!DNL Amazon Ads] destinationen använder alla mappade fält för mappningsändamål, vilket ger högre matchningsfrekvens om fler fält anges. Mer information om godkända identifierare finns på [Hjälpsidan för Amazon Ads hashed-målgrupper](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Exporterade data/Validera dataexport {#exported-data}

När målgruppen har överförts kan du validera att målgruppen har skapats och överförts korrekt enligt följande steg:

**För Amazon DSP**

Navigera till **[!UICONTROL Advertiser ID]** > **[!UICONTROL Audiences]** > **[!UICONTROL Advertiser Audiences]**. Om målgruppen skapades och uppfyller det minsta antalet målgruppsmedlemmar visas statusvärdet för `Active`. Mer information om er målgruppsstorlek och räckvidd finns i den prognostiserade panelen Reach till höger om Amazon DSP användargränssnitt.

![Validering av målgrupp DSP Amazon](../../assets/catalog/advertising/amazon_ads_image_3.png)

**För[!DNL Amazon Marketing Cloud]**

I den vänstra schemaläsaren hittar du målgruppen under **[!UICONTROL Advertiser Uploaded]** > **[!UICONTROL aep_audiences]**. Du kan sedan fråga din målgrupp i AMC SQL-redigeraren med följande sats:

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Validering av målgrupper i Amazon Marketing Cloud](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information finns här: [!DNL Amazon Ads] hjälpresurser:

* [Amazon DSP Help Center](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Mars 2024 | Funktioner och dokumentation | Lagt till alternativet att exportera målgrupper som ska användas i [!DNL Amazon Marketing Cloud] (AMC). |
| Maj 2023 | Funktioner och dokumentation | <ul><li>Stöd för markering av reklamregion har lagts till i [arbetsflöde för målanslutning](#destination-details).</li><li>Uppdaterad dokumentation som återspeglar tillägget av Advertiser Region. Mer information om hur du väljer rätt annonsregion finns i [Amazon-dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Mars 2023 | Inledande version | Ursprunglig målrelease och dokumentation publicerad. |

{style="table-layout:auto"}

+++
