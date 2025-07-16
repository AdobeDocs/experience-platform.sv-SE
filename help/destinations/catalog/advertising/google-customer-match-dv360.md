---
title: Google Customer Match + Display & Video 360 connection
description: Med Google kundmatchning + Display & Video 360-destinationskoppling kan du använda dina online- och offlinedata från Experience Platform för att nå och återengagera dina kunder i Google egna och driftsatta egendomar som Search, Shopping, Gmail och YouTube.
badge: Begränsad tillgänglighet
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: efdec64dee4c5857d0df008c2d1242674f9d0b49
workflow-type: tm+mt
source-wordcount: '2309'
ht-degree: 1%

---

# [!DNL Google Customer Match + Display & Video 360]-anslutning

>[!NOTE]
>
>**Begränsad tillgänglighet för Google Customer Match + DV360-kontakten**<br> När vi går igenom hela mognadsperioden för den här integreringen med Google ser vi data som pekar på svagheter i implementeringen som behöver korrigeras innan mer omfattande implementering kan ske. På grund av detta har Adobe minskat synligheten för destinationen till ett begränsat antal kunder. Vi har aktiva samtal med Google för att förbättra produktupplevelsen. Vi förstår att det här kan vara en besvikelse, men vi anser att det är det ansvarsfulla tillvägagångssättet för att säkerställa en högkvalitativ, tillförlitlig upplevelse för våra kunder.</br>

Använd det här målet om du vill aktivera dina egna PII-baserade [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en)-listor direkt till [!DNL Google Display & Video 360]-egenskaper som [!DNL Search], [!DNL YouTube], [!DNL Gmail] och [!DNL Google Display Network].

Vissa Google-integrerade tredje parter, som Adobe Real-Time CDP, kan använda [!DNL Google Audience Partner API] för att skapa [!DNL Customer Match]-målgrupper direkt i kundens [!DNL Display & Video 360]-konto.

Med den nyligen introducerade möjligheten att kunna använda [!DNL Customer Matched] målgrupper i [!DNL Display & Video 360] kan du nu rikta in dig på målgrupper i en utökad lista med inventeringskällor.

![Google kundmatchning + DV360-mål i Adobe Experience Platform användargränssnitt.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Viktigt meddelande om ändringar av Google destinationer i samband med uppdaterade krav på medgivande i Europeiska unionen

>[!IMPORTANT]
>
> Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de kompatibilitetskrav och medgivanderelaterade krav som definieras i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i EU ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). Tvingande av dessa ändringar av medgivandekraven gäller från och med den 6 mars 2024.
> &#x200B;><br/>
> &#x200B;>För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe verktygen som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.
> &#x200B;><br/>
> &#x200B;>Kunder som har köpt Adobe sekretess- och säkerhetssköld och har konfigurerat en [medgivandeprincip](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för att filtrera bort profiler som inte godkänts behöver inte vidta några åtgärder.
> &#x200B;><br/>
> &#x200B;>Kunder som inte har köpt Adobe sekretess- och säkerhetssköld måste använda [segmentdefinitionsfunktionerna](../../../segmentation/home.md#segment-definitions) i [Segment Builder](../../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, så att de kan fortsätta använda Real-Time CDP Google-destinationer utan avbrott.

## När ska det här målet användas

Flera integreringar med Google finns i målkatalogen och det kan vara svårt att förstå när man ska använda var och en av Google tillgängliga destinationer. Förstå de olika användningsfallen genom att läsa informationen i tabellen nedan:

| [Google kundmatchning](/help/destinations/catalog/advertising/google-customer-match.md) | [Google Display &amp; Video 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (den här kopplingen) |
|---------|----------|---------|
| Exportera dina PII-baserade målgrupper och nå dem på det tillgängliga lagret i [!DNL Google Customer Match]. | Nå ut till cookie-baserade målgrupper i alla lager som är tillgängliga via [!DNL Google Display & Video 360], i Google egna och driftsatta egenskaper som Youtube och [!DNL Search], och mer därtill. | Skapa PII-baserade målgrupper i [!DNL Google Customer Match] och nå dem i det lager som finns i [!DNL Google Display & Video 360], endast i Google egna och styrda egenskaper. |

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda den här destinationen finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa med den här funktionen.

### Använd skiftläge 1

Ett sportklädmärke vill nå befintliga kunder genom [!DNL Google Search] och [!DNL Google Shopping] för att personalisera erbjudanden och objekt baserat på deras tidigare köp och webbhistorik. Det klädvarumärket kan importera e-postadresser från sin egen CRM till Experience Platform och bygga målgrupper utifrån sina egna offlinedata. Sedan kan de skicka dessa målgrupper till målet [!DNL Google Customer Match + Display & Video 360] som ska användas i alla [!DNL Google Display & Video 360] -egenskaper som [!DNL Search], [!DNL YouTube], [!DNL Gmail] och [!DNL Google Display Network].

### Använd skiftläge 2

Ett framstående teknikföretag har lanserat en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Målgrupper skapas baserat på kunder som äger äldre telefonmodeller. Därefter skickas målgrupper till [!DNL Google Customer Match], så att företaget kan inrikta sig på befintliga kunder, kunder som äger äldre telefonmodeller och liknande kunder på [!DNL Google Display & Video 360]-egenskaper som [!DNL Search], [!DNL YouTube], [!DNL Gmail] och [!DNL Google Display Network].

## Identiteter som stöds {#supported-identities}

[!DNL Google Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256_e.164 | Telefonnummer i E164-format, hashas med algoritmen SHA256 | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer och andra) som används i målet [!DNL Google Customer Match]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match]-kontokrav {#google-account-prerequisites}

Innan du konfigurerar ett [!DNL Google Customer Match]-mål i Experience Platform måste du läsa och följa Google policy för användning av [!DNL Customer Match], som beskrivs i [Google supportdokumentation](https://support.google.com/google-ads/answer/6299717).

Kontrollera sedan att ditt [!DNL Google]-konto har konfigurerats för en [!DNL Standard] eller högre behörighetsnivå. Mer information finns i [dokumentationen för Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1).

### Krav för länkning av konto {#linking}

Innan du konfigurerar den här målanslutningen måste du länka ditt Google-konto-ID till Adobe Google konto-ID: `4641108541`.

Dataexport misslyckas om ditt Google-konto inte är korrekt länkat till Adobe konto-ID.

>[!NOTE]
>
>Adobe har uppdaterat Google Partner-konto-ID från `6219889373` till `4641108541`.
>
>**Om ditt Google-konto är länkat till det gamla Adobe Partner-konto-ID:t (`6219889373`) följer du stegen nedan:**
>
>1. Ta bort länken för ditt Google-konto från det gamla Adobe Partner-konto-ID:t (`6219889373`)
>2. Länka ditt Google-konto till det nya Adobe Partner-konto-ID (`4641108541`)
>3. Ta bort alla målgrupper från era befintliga dataflöden
>4. Skapa nya dataflöden och kartlägga era målgrupper
>
>Om ditt Google-konto redan är länkat till det nya Adobe Partner-konto-ID:t (`4641108541`) krävs ingen åtgärd från dig.

**För organisationer med chefskonton:**

Om din organisation använder ett [manager [!DNL Google] account](https://support.google.com/google-ads/answer/6139186) för att hantera flera klientkonton följer du de här specifika länkningskraven:

* **Så här exporterar du till ett specifikt klientkonto:** Länka det enskilda klientkontot (inte hanterarkontot) till Adobe Google konto-ID: `4641108541`
* **Det räcker inte med enbart kontolänkning för hanterare** och det kan orsaka dataexportfel

### Tillåtelselista {#allowlist}

Innan du skapar [!DNL Google Customer Match]-målet i Experience Platform måste du kontrollera att ditt [!DNL Google Ads]-konto följer [[!DNL Google Customer Match] principen](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunder med kompatibla konton tillåtslista automatiskt av Google.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Google] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför måste målgrupper som är aktiverade för [!DNL Google Customer Match] vara avaktiverade för *hashed*-identifierare, som till exempel hash-kodade e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

### Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två metoder för att aktivera telefonnummer i [!DNL Google Customer Match]:

* **Inkommande råtelefonnummer**: du kan importera råa telefonnummer i formatet [!DNL E.164] till [!DNL Experience Platform], och de hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till namnutrymmet `Phone_E.164`.
* **Inkommande hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du lägger in dem i [!DNL Experience Platform]. Om du väljer det här alternativet måste du alltid importera dina hashade telefonnummer till namnutrymmet `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Telefonnummer som är inkapslade i namnområdet `Phone` kan inte aktiveras för målet [!DNL Google Customer Match + DV360].

### Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser som är tydliga i Experience Platform, och få [!DNL Experience Platform] hash-kodade adresser när de aktiveras.

Mer information om Google hashkrav och andra begränsningar för aktivering finns i följande avsnitt i Google dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] med telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] med ID:n för mobila enheter](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [gruppimporten](../../../ingestion/batch-ingestion/overview.md) och översikten över [direktuppspelningsinläsningen](../../../ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla Google krav som beskrivs i länkarna ovan.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_gcm_dv360_accountID"
>title="Länka Google- och Adobe-konton"
>abstract="Kontrollera att det konto-ID för Google som du anger här redan är länkat till ditt Adobe-konto. Om du har ett hanterarkonto för Google med flera klientkonton och vill exportera data från Experience Platform till ett specifikt klientkonto, måste du länka det klientkontot till ditt Adobe-konto och ange konto-ID här."

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: ange ett namn för den här målanslutningen
* **[!UICONTROL Description]**: ange en beskrivning för den här målanslutningen
* **[!UICONTROL Account ID]**: ditt [Google Ads-kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Formatet på ID:t är xxx-xxx-xxxx. Använd inte ditt konto-ID om du använder [!DNL Google Ads Manager Account (My Client Center)]. Använd [Google Ads-kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en) i stället.
* **[!UICONTROL Account type]**: din kontotyp för Google. Välj ett alternativ, beroende på vilken typ av annonskonto du har hos Google:
   * **[!UICONTROL Display Video Partner]**
   * **[!UICONTROL Display Video Advertiser]**

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* till mål måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](../../assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Mappningsexempel: aktiverar målgruppsdata i [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Detta är ett exempel på korrekt identitetsmappning när målgruppsdata aktiveras i [!DNL Google Customer Match + Display & Video 360].

Välja källfält:

* Välj namnutrymmet `Email` som källidentitet om de e-postadresser du använder inte hashas.
* Välj namnutrymmet `Email_LC_SHA256` som källidentitet om du hashas i kundens e-postadresser vid datahämtning till [!DNL Experience Platform], enligt [!DNL Google Customer Match] [e-posthashkraven](#hashing-requirements).
* Välj namnutrymmet `PHONE_E.164` som källidentitet om dina data består av telefonnummer som inte är hashas. [!DNL Experience Platform] hash-kodar telefonnumren så att de uppfyller kraven för [!DNL Google Customer Match].
* Välj namnutrymmet `Phone_SHA256_E.164` som källidentitet om du hashade telefonnummer vid dataöverföring till [!DNL Experience Platform], enligt [!DNL Facebook] [krav för telefonnummerhashning](#phone-number-hashing-requirements).

Markera målfält:

* Välj namnutrymmet `Email_LC_SHA256` som målidentitet när källnamnutrymmena är antingen `Email` eller `Email_LC_SHA256`.
* Välj namnutrymmet `Phone_SHA256_E.164` som målidentitet när källnamnutrymmena är antingen `PHONE_E.164` eller `Phone_SHA256_E.164`.

![Identitetsmappning mellan käll- och målfält som visas i mappningssteget i aktiveringsarbetsflödet.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Experience Platform] vid aktiveringen.

Attributkälldata hashas inte automatiskt. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen.

![Använd omvandlingskontroll markerat i mappningssteget i aktiveringsarbetsflödet.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Bildskärmsmål {#monitor-destination}

När du har anslutit till målet och etablerat ett måldataflöde kan du använda [övervakningsfunktionen](/help/dataflows/ui/monitor-destinations.md) i Real-Time CDP för att få omfattande information om de profilposter som är aktiverade för målet i varje dataflödeskörning.

Övervakningsinformationen för anslutningen [!DNL Google Customer Match + Display & Video 360] innehåller information på målgruppsnivå om aktiverade, uteslutna och misslyckade identiteter i varje dataflöde och dataflöde. [Läs mer](/help/dataflows/ui/monitor-destinations.md#segment-level-view) om funktionaliteten.

## Verifiera att målgruppsaktiveringen lyckades {#verify-activation}

När du har slutfört aktiveringsflödet växlar du till ditt **[!UICONTROL Google Ads]**-konto. De aktiverade målgrupperna visas i ditt Google-konto som kundlistor. Beroende på målgruppens storlek fyller vissa målgrupper inte plats om det inte finns fler än 1 000 aktiva användare att betjäna. Mer information finns i [Google Audience Partner-dokumentationen](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Observera att du måste be Google om åtkomst till dokumentationen i länken.

## Dataförvaltning

Vissa destinationer i Experience Platform har vissa regler och skyldigheter för data som skickas till eller tas emot från målplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs mer](../../../data-governance/labels/overview.md) om verktyg och principer för datastyrning.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [kraven](#google-account-prerequisites). Om du vill åtgärda det här problemet kontaktar du Google och kontrollerar att ditt konto är tillåtet och konfigurerat för en [!DNL Standard] eller högre behörighetsnivå. Mer information finns i [dokumentationen för Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1).
