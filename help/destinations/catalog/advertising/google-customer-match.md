---
keywords: Google customer match;Google customer match;Google Customer Match
title: Google Customer Match Connection
description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Google egna och styrda egendomar som Search, Shopping, Gmail och YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 0%

---

# [!DNL Google Customer Match] anslutning

## Översikt {#overview}

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) Med kan ni använda era online- och offlinedata för att nå ut till och återinteragera med era kunder via Google egna och driftsatta egendomar, som: [!DNL Search], [!DNL Shopping], [!DNL Gmail]och [!DNL YouTube].

![Google kundmatchningsmål i Adobe Experience Platform användargränssnitt.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Google Customer Match] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa med den här funktionen.

### Använd skiftläge 1

Ett sportklädmärke vill nå befintliga kunder genom [!DNL Google Search] och [!DNL Google Shopping] för att personalisera erbjudanden och objekt baserat på deras tidigare inköp och webbhistorik. Kläddervarumärket kan importera e-postadresser från sin egen CRM till Experience Platform och bygga målgrupper utifrån sina egna offlinedata. Sedan kan de skicka dessa målgrupper till [!DNL Google Customer Match] ska användas tvärs över [!DNL Search] och [!DNL Shopping], optimera deras annonsutgifter.

### Använd skiftläge 2

Ett framstående teknikföretag lanserade en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Målgrupper skapas baserat på kunder som äger äldre telefonmodeller. Sedan skickas målgrupperna till [!DNL Google Customer Match]så att företaget kan inrikta sig på befintliga kunder, kunder som äger äldre telefonmodeller och liknande kunder på [!DNL YouTube].

## Datastyrning för [!DNL Google Customer Match] mål {#data-governance}

Vissa destinationer i Experience Platform har vissa regler och skyldigheter för data som skickas till eller tas emot från destinationsplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs mer](../../../data-governance/labels/overview.md) om verktyg och policyer för datastyrning.

## Identiteter som stöds {#supported-identities}

[!DNL Google Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256_e.164 | Telefonnummer i E164-format, hashas med algoritmen SHA256 | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| user_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer och andra) som används i [!DNL Google Customer Match] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] kontokrav {#google-account-prerequisites}

Innan du konfigurerar en [!DNL Google Customer Match] mål i Experience Platform, se till att du läser och följer Google policy för användning av [!DNL Customer Match], konturerad i [Google supportdokumentation](https://support.google.com/google-ads/answer/6299717).

Se sedan till att [!DNL Google] kontot har konfigurerats för [!DNL Standard] eller högre behörighetsnivå. Se [Google Ads-dokumentation](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) för mer information.

### Tillåtelselista {#allowlist}

Innan du skapar [!DNL Google Customer Match] mål i Experience Platform, se till att [!DNL Google Ads] kontot följer [[!DNL Google Customer Match] policy](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunder med kompatibla konton tillåts automatiskt listade av Google.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Google] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL Google Customer Match] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

### Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två sätt att aktivera telefonnummer i [!DNL Google Customer Match]:

* **Inmatning av telefonnummer i råformat**: du kan importera råa telefonnummer i [!DNL E.164] formatera till [!DNL Platform]och de hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till `Phone_E.164` namnutrymme.
* **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du lägger in dem i [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hash-kodade telefonnummer till `PHONE_SHA256_E.164` namnutrymme.

>[!NOTE]
>
>Telefonnummer som hämtas till `Phone` namnutrymmet kan inte aktiveras i [!DNL Google Customer Match].

### Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du hämtar dem till Adobe Experience Platform, eller använda e-postadresser utan att märka dem i Experience Platform, och du kan [!DNL Platform] hash-koda dem vid aktiveringen.

Mer information om Google hashkrav och andra begränsningar för aktivering finns i följande avsnitt i Google dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] med telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] med mobilenhets-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](../../../ingestion/batch-ingestion/overview.md) och [översikt över direktuppspelning](../../../ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla Google krav som beskrivs i länkarna ovan.

### Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda `User_ID` namnutrymme för att skicka data till Google, se till att du synkroniserar dina egna identifierare med [!DNL gTag]. Se [Google officiella dokumentation](https://support.google.com/google-ads/answer/9199250) för detaljerad information.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: ange ett namn för den här målanslutningen
* **[!UICONTROL Description]**: ange en beskrivning för den här målanslutningen
* **[!UICONTROL Account ID]**: din [Google Ads, kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Formatet på ID:t är xxx-xxx-xxxx. Om du använder [!DNL Google Ads Manager Account (My Client Center)]använder du inte ditt konto-ID för chef. Använd [Google Ads, kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en) i stället.

>[!IMPORTANT]
>
> * The **[!UICONTROL Combine with PII]** marknadsföringsåtgärd väljs som standard för [!DNL Google Customer Match] och kan inte tas bort.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL App ID] när [!DNL IDFA] eller [!DNL GAID] målgrupper [!DNL Google Customer Match].

![Google program-ID för kundmatchning](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Mer information om hur du hittar [!DNL App ID], se [Google officiella dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Mappningsexempel: aktivera målgruppsdata i [!DNL Google Customer Match] {#example-gcm}

Detta är ett exempel på korrekt identitetsmappning när målgruppsdata aktiveras i [!DNL Google Customer Match].

Välja källfält:

* Välj `Email` namnutrymmet som källidentitet om e-postadresserna du använder inte hashas.
* Välj `Email_LC_SHA256` namnrymd som källidentitet om du har hasarkiverat e-postadresser till kundens inmatning i [!DNL Platform], enligt [!DNL Google Customer Match] [krav på e-posthashning](#hashing-requirements).
* Välj `PHONE_E.164` namnutrymme som källidentitet om dina data består av icke-hash-kodade telefonnummer. [!DNL Platform] kommer att hash-koda telefonnumren för att uppfylla [!DNL Google Customer Match] krav.
* Välj `Phone_SHA256_E.164` namnrymd som källidentitet om du hashade telefonnummer vid datainmatning till [!DNL Platform], enligt [!DNL Facebook] [hashkrav för telefonnummer](#phone-number-hashing-requirements).
* Välj `IDFA` namnutrymme som källidentitet om dina data består av [!DNL Apple] enhets-ID.
* Välj `GAID` namnutrymme som källidentitet om dina data består av [!DNL Android] enhets-ID.
* Välj `Custom` namnutrymme som källidentitet om dina data består av andra typer av identifierare.

Markera målfält:

* Välj `Email_LC_SHA256` namespace som target identity när källnamnutrymmena antingen är `Email` eller `Email_LC_SHA256`.
* Välj `Phone_SHA256_E.164` namespace som target identity när källnamnutrymmena antingen är `PHONE_E.164` eller `Phone_SHA256_E.164`.
* Välj `IDFA` eller `GAID` namnutrymmen som målidentitet när källnamnutrymmen är `IDFA` eller `GAID`.
* Välj `User_ID` namespace som target identity när källnamnutrymmet är ett anpassat.

![Identitetsmappning](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Data från namnutrymmen utan hashning hashas automatiskt av [!DNL Platform] vid aktivering.

Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.

![Transformering av identitetsmappning](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verifiera att målgruppsaktiveringen lyckades {#verify-activation}

När aktiveringsflödet är klart växlar du till **[!UICONTROL Google Ads]** konto. De aktiverade målgrupperna visas i ditt Google-konto som kundlistor. Observera att beroende på målgruppens storlek så fyller vissa målgrupper inte plats om det inte finns fler än 100 aktiva användare att betjäna.

När en målgrupp mappas till båda [!DNL IDFA] och [!DNL GAID] mobil-ID, [!DNL Google Customer Match] skapar en separat målgrupp för varje ID-mappning. Dina [!DNL Google Ads] kontot visar två olika segment, ett för [!DNL IDFA]och en för [!DNL GAID] mappning.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [krav](#google-account-prerequisites). Kontakta Google och kontrollera att ditt konto är godkänt och konfigurerat för en [!DNL Standard] eller högre behörighetsnivå. Se [Google Ads-dokumentation](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) för mer information.

## Ytterligare resurser {#additional-resources}

* [Integrera [!DNL Google Customer Match] - Videokurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

