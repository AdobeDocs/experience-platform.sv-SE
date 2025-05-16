---
keywords: Google customer match;Google customer match;Google Customer Match
title: Google Customer Match Connection
description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Google egna och styrda egendomar som Search, Shopping och Gmail.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: ce205622260f4252d1a7db7c5011366fb2ed4d3c
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 1%

---

# [!DNL Google Customer Match]-anslutning

>[!IMPORTANT]
>
> Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de kompatibilitetskrav och medgivanderelaterade krav som definieras i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i EU ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). Tvingande av dessa ändringar av medgivandekraven gäller från och med den 6 mars 2024.
><br/>
>För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe verktygen som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.
><br/>
>Kunder som har köpt Adobe sekretess- och säkerhetssköld och har konfigurerat en [medgivandeprincip](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för att filtrera bort profiler som inte godkänts behöver inte vidta några åtgärder.
><br/>
>Kunder som inte har köpt Adobe sekretess- och säkerhetssköld måste använda [segmentdefinitionsfunktionerna](../../../segmentation/home.md#segment-definitions) i [Segment Builder](../../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, så att de kan fortsätta använda Real-Time CDP Google-destinationer utan avbrott.

Med [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) kan du använda dina online- och offlinedata för att nå och återengagera dina kunder via egenskaper som ägs och hanteras av Google, till exempel: [!DNL Search], [!DNL Shopping] och [!DNL Gmail].

>[!TIP]
>
>Om du vill nå kunder på [!DNL YouTube] lager använder du [Google kundmatchning + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) som använder Google Audience Partner API.

![Google kundmatchningsmål i Adobe Experience Platform-gränssnittet.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Google Customer Match] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa med den här funktionen.

### Använd skiftläge 1

Ett sportklädmärke vill nå befintliga kunder genom [!DNL Google Search] och [!DNL Google Shopping] för att personalisera erbjudanden och objekt baserat på deras tidigare köp och webbhistorik. Det klädvarumärket kan importera e-postadresser från sin egen CRM till Experience Platform och bygga målgrupper utifrån sina egna offlinedata. Sedan kan de skicka dessa målgrupper till [!DNL Google Customer Match] för användning i [!DNL Search] och [!DNL Shopping], vilket optimerar deras annonsutgifter.

### Använd skiftläge 2

>[!TIP]
>
>Om du vill köra det här användningsfallet för [!DNL YouTube]-lager använder du det nya [Google kundmatchning + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)-målet, som använder Google Audience Partner API.

Ett framstående teknikföretag lanserade en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Målgrupper skapas baserat på kunder som äger äldre telefonmodeller. Därefter skickas målgrupper till [!DNL Google Customer Match], så att företaget kan inrikta sig på befintliga kunder, kunder som äger äldre telefonmodeller och liknande kunder på [!DNL YouTube].

## Datastyrning för [!DNL Google Customer Match] mål {#data-governance}

Vissa destinationer i Experience Platform har vissa regler och skyldigheter för data som skickas till eller tas emot från målplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs mer](../../../data-governance/labels/overview.md) om verktyg och principer för datastyrning.

## Identiteter som stöds {#supported-identities}

[!DNL Google Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| `IDFA` | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| `phone_sha256_e.164` | Telefonnummer i E164-format, hashas med algoritmen SHA256 | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `email_lc_sha256` | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `user_id` | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |
| `address_info_first_name` | Användarens förnamn | Den här målidentiteten är avsedd att användas tillsammans med `address_info_last_name`, `address_info_country_code` och `address_info_postal_code` när du vill skicka e-postadressdata till ditt mål. <br><br>Om du vill vara säker på att Google matchar adressen måste du mappa alla fyra adressfälten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) och se till att inga av dessa fält saknar data i de exporterade profilerna. <br> Om något fält antingen är omappat eller innehåller data som saknas matchar inte Google adressen. |
| `address_info_last_name` | Användarens efternamn | Den här målidentiteten är avsedd att användas tillsammans med `address_info_first_name`, `address_info_country_code` och `address_info_postal_code` när du vill skicka e-postadressdata till ditt mål. <br><br>Om du vill vara säker på att Google matchar adressen måste du mappa alla fyra adressfälten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) och se till att inga av dessa fält saknar data i de exporterade profilerna. <br> Om något fält antingen är omappat eller innehåller data som saknas matchar inte Google adressen. |
| `address_info_country_code` | Landskod för användaradress | Den här målidentiteten är avsedd att användas tillsammans med `address_info_first_name`, `address_info_last_name` och `address_info_postal_code` när du vill skicka e-postadressdata till ditt mål. <br><br>Om du vill vara säker på att Google matchar adressen måste du mappa alla fyra adressfälten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) och se till att inga av dessa fält saknar data i de exporterade profilerna. <br> Om något fält antingen är omappat eller innehåller data som saknas matchar inte Google adressen. <br><br>Godkänt format: landskoder med gemener och två bokstäver i formatet [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) . |
| `address_info_postal_code` | Postnummer för användaradress | Den här målidentiteten är avsedd att användas tillsammans med `address_info_first_name`, `address_info_last_name` och `address_info_country_code` när du vill skicka e-postadressdata till ditt mål. <br><br>Om du vill vara säker på att Google matchar adressen måste du mappa alla fyra adressfälten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) och se till att inga av dessa fält saknar data i de exporterade profilerna. <br> Om något fält antingen är omappat eller innehåller data som saknas matchar inte Google adressen. |

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

Kontrollera sedan att ditt [!DNL Google]-konto har konfigurerats för en [!DNL Standard] eller högre behörighetsnivå. Mer information finns i [dokumentationen för Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).

### Tillåtelselista {#allowlist}

Innan du skapar [!DNL Google Customer Match]-målet i Experience Platform måste du kontrollera att ditt [!DNL Google Ads]-konto följer [[!DNL Google Customer Match] principen](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunder med kompatibla konton tillåtslista automatiskt av Google.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Google] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför kan målgrupper som är aktiverade för [!DNL Google Customer Match] inaktiveras för *hashed*-identifierare, som e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

### Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två metoder för att aktivera telefonnummer i [!DNL Google Customer Match]:

* **Inkommande råtelefonnummer**: du kan importera råa telefonnummer i formatet [!DNL E.164] till [!DNL Experience Platform], och de hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till namnutrymmet `Phone_E.164`.
* **Inkommande hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du lägger in dem i [!DNL Experience Platform]. Om du väljer det här alternativet måste du alltid importera dina hashade telefonnummer till namnutrymmet `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Telefonnummer som är inkapslade i namnområdet `Phone` kan inte aktiveras i [!DNL Google Customer Match].

### Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser som är tydliga i Experience Platform, och få [!DNL Experience Platform] hash-kodade adresser när de aktiveras.

Mer information om Google hashkrav och andra begränsningar för aktivering finns i följande avsnitt i Google dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] med telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] med ID:n för mobila enheter](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [gruppimporten](../../../ingestion/batch-ingestion/overview.md) och översikten över [direktuppspelningsinläsningen](../../../ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla Google krav som beskrivs i länkarna ovan.

### Hash-krav för adressfält {#address-field-hashing}

När adressrelaterade fält mappas till [!DNL Google Customer Match] kommer Experience Platform **automatiskt att krascha** `address_info_first_name` - och `address_info_last_name`-värdena innan de skickas till Google. Denna automatiska hashning krävs för att uppfylla Google säkerhets- och integritetskrav.

Ange **inte** förhash-värden för `address_info_first_name` eller `address_info_last_name`. Om du redan anger hash-kodade värden misslyckas matchningsprocessen.

### Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda namnområdet `User_ID` för att skicka data till Google måste du synkronisera dina egna identifierare med [!DNL gTag]. Mer information finns i [Google officiella dokumentation](https://support.google.com/google-ads/answer/9199250).

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Videoöversikt {#video-overview}

Se videon nedan för en förklaring av fördelarna och hur du aktiverar data till Google Customer Match.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: ange ett namn för den här målanslutningen
* **[!UICONTROL Description]**: ange en beskrivning för den här målanslutningen
* **[!UICONTROL Account ID]**: ditt [Google Ads-kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Formatet på ID:t är xxx-xxx-xxxx. Använd inte ditt konto-ID om du använder [!DNL Google Ads Manager Account (My Client Center)]. Använd [Google Ads-kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en) i stället.

>[!IMPORTANT]
>
> * Marknadsföringsåtgärden **[!UICONTROL Combine with PII]** är markerad som standard för målet [!DNL Google Customer Match] och kan inte tas bort.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* till mål måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I steget **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL App ID] när du skickar [!DNL IDFA] eller [!DNL GAID] målgrupper till [!DNL Google Customer Match].

![Fältet Google-program-ID för kundmatchning är markerat i segmentschemagrycket i aktiveringsarbetsflödet.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Mer information om hur du hittar [!DNL App ID] finns i [Google officiella dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) eller frågar din Google-representant.

### Mappningsexempel: aktiverar målgruppsdata i [!DNL Google Customer Match] {#example-gcm}

Detta är ett exempel på korrekt identitetsmappning när målgruppsdata aktiveras i [!DNL Google Customer Match].

Välja källfält:

* Välj namnutrymmet `Email` som källidentitet om de e-postadresser du använder inte hashas.
* Välj namnutrymmet `Email_LC_SHA256` som källidentitet om du hashas i kundens e-postadresser vid datahämtning till [!DNL Experience Platform], enligt [!DNL Google Customer Match] [e-posthashkraven](#hashing-requirements).
* Välj namnutrymmet `PHONE_E.164` som källidentitet om dina data består av telefonnummer som inte är hashas. [!DNL Experience Platform] hash-kodar telefonnumren så att de uppfyller kraven för [!DNL Google Customer Match].
* Välj namnutrymmet `Phone_SHA256_E.164` som källidentitet om du hashade telefonnummer vid dataöverföring till [!DNL Experience Platform], enligt [!DNL Facebook] [krav för telefonnummerhashning](#phone-number-hashing-requirements).
* Välj namnutrymmet `IDFA` som källidentitet om dina data består av [!DNL Apple] enhets-ID:n.
* Välj namnutrymmet `GAID` som källidentitet om dina data består av [!DNL Android] enhets-ID:n.
* Välj namnutrymmet `Custom` som källidentitet om dina data består av andra typer av identifierare.

Markera målfält:

* Välj namnutrymmet `Email_LC_SHA256` som målidentitet när källnamnutrymmena är antingen `Email` eller `Email_LC_SHA256`.
* Välj namnutrymmet `Phone_SHA256_E.164` som målidentitet när källnamnutrymmena är antingen `PHONE_E.164` eller `Phone_SHA256_E.164`.
* Välj namnutrymmena `IDFA` eller `GAID` som mål-ID när källnamnutrymmena är `IDFA` eller `GAID`.
* Välj namnutrymmet `User_ID` som målidentitet när källnamnområdet är ett anpassat.

![Identitetsmappning mellan käll- och målfält som visas i mappningssteget i aktiveringsarbetsflödet.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Experience Platform] vid aktiveringen.

Attributkälldata hashas inte automatiskt. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen.

![Använd omvandlingskontroll markerat i mappningssteget i aktiveringsarbetsflödet.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Bildskärmsmål {#monitor-destination}

När du har anslutit till målet och etablerat ett måldataflöde kan du använda [övervakningsfunktionen](/help/dataflows/ui/monitor-destinations.md) i Real-Time CDP för att få omfattande information om de profilposter som är aktiverade för målet i varje dataflödeskörning.

>[!IMPORTANT]
>
>När du mappar de fyra adressrelaterade mål-ID:n (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) räknas de som separata individuella identiteter för varje profil på dataflödets övervakningssida.

## Verifiera att målgruppsaktiveringen lyckades {#verify-activation}

När du har slutfört aktiveringsflödet växlar du till ditt **[!UICONTROL Google Ads]**-konto. De aktiverade målgrupperna visas i ditt Google-konto som kundlistor. Beroende på målgruppens storlek fyller vissa målgrupper inte plats om det inte finns fler än 100 aktiva användare att betjäna.

När en målgrupp mappas till både [!DNL IDFA] och [!DNL GAID] mobil-ID skapas en separat målgrupp för varje ID-mappning i [!DNL Google Customer Match] . Ditt [!DNL Google Ads]-konto visar två olika segment, ett för [!DNL IDFA] och ett för mappningen [!DNL GAID].

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [kraven](#google-account-prerequisites). Om du vill åtgärda det här problemet kontaktar du Google och kontrollerar att ditt konto är tillåtet och konfigurerat för en [!DNL Standard] eller högre behörighetsnivå. Mer information finns i [dokumentationen för Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).