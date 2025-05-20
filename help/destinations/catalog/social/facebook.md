---
keywords: Facebook-anslutning;facebook-anslutning;facebook-mål;facebook;instagram;messenger;facebook messenger
title: Facebook-anslutning
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# [!DNL Facebook]-anslutning

## Översikt {#overview}

Aktivera profiler för dina [!DNL Facebook]-kampanjer för målgruppsanpassning, personalisering och undertryckning baserat på hash-kodade e-postmeddelanden.

Du kan använda det här målet för målgrupper över [!DNL Facebook's]-appfamiljen som stöds av [!DNL Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] och [!DNL Messenger]. Markeringen av programmet som du vill köra kampanjen mot anges på placeringsnivån i [!DNL Facebook Ads Manager].

![Facebook-mål i Adobe Experience Platform-gränssnittet.](../../assets/catalog/social/facebook/catalog.png)

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Facebook] finns det två exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

### Använd skiftläge 1

En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till den sociala [!DNL Facebook]-plattformen, vilket optimerar deras annonsutgifter.

### Använd skiftläge 2

Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare som företaget har om dessa kunder är medlems-ID och e-postadresser.

För att rikta in dem på sociala medier kan de lägga in kunddata från sina CRM i Adobe Experience Platform med e-postadresserna som identifierare.

Därefter kan de använda sina offlinedata, inklusive tillhörande medlemskaps-ID:n och kundnivåer, för att skapa nya målgrupper som de kan rikta sig till via målet [!DNL Facebook].

## Identiteter som stöds {#supported-identities}

[!DNL Facebook Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

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
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i Facebook-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Krav för Facebook-konto {#facebook-account-prerequisites}

Innan du kan skicka dina målgrupper till [!DNL Facebook] måste du kontrollera att du uppfyller följande krav:

* Ditt [!DNL Facebook]-användarkonto måste ha fullständig åtkomst till [!DNL Facebook Business Account] som äger det annonskonto som du använder.
* Ditt [!DNL Facebook]-användarkonto måste ha behörigheten **[!DNL Manage campaigns]** aktiverad för annonskontot som du tänker använda.
* Affärskontot **Adobe Experience Cloud** måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i dokumentationen för Facebook.

  >[!IMPORTANT]
  >
  > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer**. Behörighet krävs för integreringen av [!DNL Adobe Experience Platform].

* Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. Om du vill göra det går du till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`, där `accountID` är din [!DNL Facebook Ad Account ID]. Kontrollera att avsnittet `business_id=206617933627973` finns i URL:en när du signerar användarvillkoren.

  >[!IMPORTANT]
  >
  >När du signerar [!DNL Facebook Custom Audiences]-användarvillkoren måste du se till att använda samma användarkonto som du använde för att autentisera i Facebook API.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför kan målgrupper som är aktiverade för [!DNL Facebook] inaktiveras för *hashed*-identifierare, som e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två metoder för att aktivera telefonnummer i [!DNL Facebook]:

* **Hämtar råtelefonnummer**: du kan importera råa telefonnummer i formatet [!DNL E.164] till [!DNL Experience Platform]. De hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till namnutrymmet `Phone_E.164`.
* **Inkommande hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du lägger in dem i [!DNL Experience Platform]. Om du väljer det här alternativet måste du alltid importera dina hashade telefonnummer till namnutrymmet `Phone_SHA256`.

>[!NOTE]
>
>Telefonnummer som är inkapslade i namnområdet `Phone` kan inte aktiveras i [!DNL Facebook].

## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser som är tydliga i Experience Platform, och få [!DNL Experience Platform] hash-kodade adresser när de aktiveras.

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [gruppimporten](/help/ingestion/batch-ingestion/overview.md) och översikten över [direktuppspelningsinläsningen](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen, exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Experience Platform] vid aktiveringen.
> Attributkälldata hashas inte automatiskt. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen.
> Alternativet **[!UICONTROL Apply transformation]** visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Använd omformningskontroll markerat i mappningssteget.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda namnområdet `Extern_ID` för att skicka data till [!DNL Facebook] måste du synkronisera dina egna identifierare med [!DNL Facebook Pixel]. Mer information finns i den officiella dokumentationen för [Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers).

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I videon nedan visas också stegen för att konfigurera ett [!DNL Facebook]-mål och aktivera målgrupper.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform användargränssnitt uppdateras ofta och kan ha ändrats sedan den här videon spelades in. Den senaste informationen finns i [självstudiekursen för målkonfiguration](../../ui/connect-destination.md).

### Autentisera till mål {#authenticate}

1. Hitta Facebook-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till Facebook-steget som visas i aktiveringsarbetsflödet.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Ange dina inloggningsuppgifter för Facebook och välj **Logga in**.

### Uppdatera autentiseringsuppgifter {#refresh-authentication-credentials}

Autentiseringstoken för Facebook går ut var 60:e dag. När token har gått ut slutar dataexporten till målet att fungera.

Du kan övervaka dina tokens förfallodatum från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[!UICONTROL Accounts]** eller **[!UICONTROL Browse]**.

![Förfallodatumkolumn för Facebook-kontotoken på fliken Bläddra](../../assets/catalog/social/facebook/account-expiration-browse.png)

![Förfallodatumkolumn för Facebook-kontotoken på fliken Konton](../../assets/catalog/social/facebook/account-expiration-accounts.png)

För att förhindra att en token upphör att gälla och detta orsakar avbrott i aktiveringsdataflödena kan du autentisera igen genom att utföra följande steg:

1. Navigera till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Valfritt) Använd de tillgängliga filtren på sidan om du bara vill visa Facebook-konton.
   ![Filtrera så att endast Facebook-konton visas](/help/destinations/assets/catalog/social/facebook/refresh-oauth-filters.png)
3. Markera det konto som du vill uppdatera, markera ellipsen och välj **[!UICONTROL Edit details]**.
   ![Välj kontrollen Redigera information](/help/destinations/assets/catalog/social/facebook/refresh-oauth-edit-details.png)
4. I det modala fönstret väljer du **[!UICONTROL Reconnect OAuth]** och autentiserar igen med dina Facebook-autentiseringsuppgifter.
   ![Modalt fönster med alternativet Återanslut OAuth](/help/destinations/assets/catalog/social/facebook/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Dina autentiseringsuppgifter uppdateras och deras förfallotid återställs till 60 dagar.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Konto-ID"
>abstract="Ditt Facebook-konto-ID. Du hittar detta ID i ditt Facebook Ads Manager-konto. När du anger detta ID ska du alltid prefix med `act_`."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Facebook Ad Account ID]. Du kan hitta det här ID:t i ditt [!DNL Facebook Ads Manager]-konto. När du anger detta ID ska du alltid prefix med `act_`.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Målgruppens ursprung"
>abstract="Välj hur kunddata i målgruppen ursprungligen samlades in. Data visas på Facebook när en användare är en målanvändare i segmentet"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Målgruppens ursprung"
>abstract="Annonsörer samlade in data direkt från kunderna."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Målgruppens ursprung"
>abstract="Annonsörer samlade in data direkt från sina partners."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Målgruppens ursprung"
>abstract="Annonsörer samlade in data direkt från sina kunder och partners."

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I steget **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL Origin of audience] när du skickar målgrupper till [!DNL Facebook Custom Audiences].

![Audience-listrutans ursprung visas i Facebook-aktiveringssteget.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Mappningsexempel: aktiverar målgruppsdata i [!DNL Facebook Custom Audience] {#example-facebook}

Nedan visas ett exempel på korrekt identitetsmappning när målgruppsdata aktiveras i [!DNL Facebook Custom Audience].

Välja källfält:

* Välj namnutrymmet `Email` som källidentitet om de e-postadresser du använder inte hashas.
* Välj namnutrymmet `Email_LC_SHA256` som källidentitet om du hashas i kundens e-postadresser vid datahämtning till [!DNL Experience Platform], enligt [!DNL Facebook] [e-posthashkraven](#email-hashing-requirements).
* Välj namnutrymmet `PHONE_E.164` som källidentitet om dina data består av telefonnummer som inte är hashas. [!DNL Experience Platform] hash-kodar telefonnumren så att de uppfyller kraven för [!DNL Facebook].
* Välj namnutrymmet `Phone_SHA256` som källidentitet om du hashade telefonnummer vid dataöverföring till [!DNL Experience Platform], enligt [!DNL Facebook] [krav för telefonnummerhashning](#phone-number-hashing-requirements).
* Välj namnutrymmet `IDFA` som källidentitet om dina data består av [!DNL Apple] enhets-ID:n.
* Välj namnutrymmet `GAID` som källidentitet om dina data består av [!DNL Android] enhets-ID:n.
* Välj namnutrymmet `Custom` som källidentitet om dina data består av andra typer av identifierare.

Markera målfält:

* Välj namnutrymmet `Email_LC_SHA256` som målidentitet när källnamnutrymmena är antingen `Email` eller `Email_LC_SHA256`.
* Välj namnutrymmet `Phone_SHA256` som målidentitet när källnamnutrymmena är antingen `PHONE_E.164` eller `Phone_SHA256`.
* Välj namnutrymmena `IDFA` eller `GAID` som mål-ID när källnamnutrymmena är `IDFA` eller `GAID`.
* Välj namnutrymmet `Extern_ID` som målidentitet när källnamnområdet är ett anpassat.

>[!IMPORTANT]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Experience Platform] vid aktiveringen.
> 
>Attributkälldata hashas inte automatiskt. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen.

![Använd omformningskontroll markerat i mappningssteget.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Exporterade data {#exported-data}

För [!DNL Facebook] innebär en lyckad aktivering att en anpassad [!DNL Facebook]-målgrupp skapas programmatiskt i [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Målgruppsmedlemskap läggs till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade målgrupperna.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL Facebook] har stöd för tidigare målgruppsåsidosättningar. Alla historiska målgruppskvalifikationer skickas till [!DNL Facebook] när du aktiverar målgrupperna till målet.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kunder använder nyligen skapade konton och behörigheterna [!DNL Facebook] ännu inte är aktiva.

>[!IMPORTANT]
>
>Kontrollera att du godkänner [!DNL Facebook Custom Audience Terms of Service] under `business ID 206617933627973`, vilket visas i URL-mallen i avsnittet [Kontokrav](#facebook-account-prerequisites).

Om du får felmeddelandet `400 Bad Request` efter att du har följt stegen i [Krav för Facebook-konto](#facebook-account-prerequisites) kan det ta några dagar innan behörigheterna för [!DNL Facebook] börjar gälla.


