---
keywords: Google customer match;Google customer match;Google Customer Match
title: Google Customer Match Connection
description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Google egna och styrda egendomar som Search, Shopping, Gmail och YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 23828fcbb1257fa093c1e114ee4c2fcb2162d9d6
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 0%

---

# [!DNL Google Customer Match] anslutning

## Översikt {#overview}

[Google kundmatchning](https://support.google.com/google-ads/answer/6379332?hl=en) Med kan ni använda era online- och offlinedata för att nå ut till och återinteragera med era kunder via Google egna och driftsatta egendomar, som: [!DNL Search], [!DNL Shopping], [!DNL Gmail]och [!DNL YouTube].

![Google kundmatchningsmål i Adobe Experience Platform användargränssnitt](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Google Customer Match] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

### Använd skiftläge 1

Ett sportklädmärke vill nå befintliga kunder genom [!DNL Google Search] och [!DNL Google Shopping] för att personalisera erbjudanden och objekt baserat på deras tidigare inköp och webbhistorik. Det klädvarumärket kan importera e-postadresser från sin egen CRM till Experience Platform och bygga segment utifrån sina egna offlinedata. Sedan kan de skicka dessa segment till [!DNL Google Customer Match] ska användas tvärs över [!DNL Search] och [!DNL Shopping], optimera deras annonsutgifter.

### Använd skiftläge 2

Ett framstående teknikföretag lanserade en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Segment skapas baserat på kunder som äger äldre telefonmodeller. Sedan skickas segment till [!DNL Google Customer Match]så att företaget kan inrikta sig på befintliga kunder, kunder som äger äldre telefonmodeller och liknande kunder på [!DNL YouTube].

## Datastyrning för [!DNL Google Customer Match] mål {#data-governance}

Vissa destinationer i Experience Platform har vissa regler och skyldigheter för data som skickas till eller tas emot från destinationsplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs mer](../../../data-governance/labels/overview.md) om verktyg och policyer för datastyrning.

## Identiteter som stöds {#supported-identities}

[!DNL Google Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256_e.164 | Telefonnummer i E164-format som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| user_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer och andra) som används i [!DNL Google Customer Match] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] kontokrav {#google-account-prerequisites}

Innan du konfigurerar en [!DNL Google Customer Match] mål i Experience Platform, se till att du läser och följer Google policy för användning av [!DNL Customer Match], konturerad i [Google supportdokumentation](https://support.google.com/google-ads/answer/6299717).

Kontrollera sedan att [!DNL Google] kontot har konfigurerats för [!DNL Standard] eller högre behörighetsnivå. Se [Google Ads-dokumentation](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) för mer information.

### Tillåtelselista {#allowlist}

Innan du skapar [!DNL Google Customer Match] mål i Experience Platform, se till att [!DNL Google Ads] kontot följer [Google kundmatchningspolicy](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunder med kompatibla konton tillåts automatiskt listade av Google.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Google] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL Google Customer Match] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

### Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två sätt att aktivera telefonnummer i [!DNL Google Customer Match]:

* **Inmatning av råtelefonnummer**: du kan importera råa telefonnummer i [!DNL E.164] formatera till [!DNL Platform]och de hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till `Phone_E.164` namnutrymme.
* **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du tar dig in i [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hash-kodade telefonnummer till `PHONE_SHA256_E.164` namnutrymme.

>[!NOTE]
>
>Telefonnummer som hämtas till `Phone` namnutrymmet kan inte aktiveras i [!DNL Google Customer Match].

### Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du hämtar dem till Adobe Experience Platform, eller använda e-postadresser utan att märka dem i Experience Platform, och du kan [!DNL Platform] hash-koda dem vid aktiveringen.

Mer information om Google hashkrav och andra begränsningar för aktivering finns i följande avsnitt i Google dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Kundmatchning med telefonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Kundmatchning med mobila enhets-ID:n](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](../../../ingestion/batch-ingestion/overview.md) och [översikt över direktuppspelning](../../../ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla Google krav som beskrivs i länkarna ovan.

### Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda `User_ID` namnutrymme för att skicka data till Google, se till att du synkroniserar dina egna identifierare med [!DNL gTag]. Se [Google officiella dokumentation](https://support.google.com/google-ads/answer/9199250) för detaljerad information.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: ange ett namn för den här målanslutningen
* **[!UICONTROL Description]**: ange en beskrivning för den här målanslutningen
* **[!UICONTROL Account ID]**: din [Google Ads, kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Formatet på ID:t är xxx-xxx-xxxx. Om du använder [!DNL Google Ads Manager Account (My Client Center)]använder du inte ditt konto-ID för chef. Använd [Google Ads, kund-ID](https://support.google.com/google-ads/answer/1704344?hl=en) i stället.

>[!IMPORTANT]
>
> * The **[!UICONTROL Combine with PII]** marknadsföringsåtgärd väljs som standard för [!DNL Google Customer Match] och kan inte tas bort.


## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

I **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL App ID] när [!DNL IDFA] eller [!DNL GAID] segment till [!DNL Google Customer Match].

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
* Välj `IDFA` eller `GAID` namnutrymmen som målidentitet när källnamnutrymmena är `IDFA` eller `GAID`.
* Välj `User_ID` namespace som target identity när källnamnutrymmet är ett anpassat.

![Identitetsmappning](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktivering.

Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.

![Transformering av identitetsmappning](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verifiera att segmentaktiveringen lyckades {#verify-activation}

När aktiveringsflödet är klart växlar du till **[!UICONTROL Google Ads]** konto. De aktiverade segmenten visas i ditt Google-konto som kundlistor. Observera att beroende på segmentstorleken fyller vissa målgrupper inte i bilden om det inte finns fler än 100 aktiva användare att betjäna.

När ett segment mappas till båda [!DNL IDFA] och [!DNL GAID] mobil-ID, [!DNL Google Customer Match] skapar ett separat segment för varje ID-mappning. Dina [!DNL Google Ads] kontot visar två olika segment, ett för [!DNL IDFA]och en för [!DNL GAID] mappning.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [krav](#google-account-prerequisites). Kontakta Google och kontrollera att ditt konto är godkänt och konfigurerat för en [!DNL Standard] eller högre behörighetsnivå. Se [Google Ads-dokumentation](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) för mer information.

## Ytterligare resurser {#additional-resources}

* [Integrera Google kundmatchning - videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

