---
keywords: facebook-anslutning;facebook-anslutning;facebook-mål;facebook;instagram;messenger;facebook messenger
title: Facebook
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# [!DNL Facebook] anslutning

## Översikt {#overview}

Aktivera profiler för [!DNL Facebook] kampanjer för målgruppsanpassning, personalisering och undertryckande baserat på hashad-e-post.

Du kan använda det här målet för målgruppsanpassning över [!DNL Facebook's] program som stöds av [!DNL Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]och [!DNL Messenger]. Valet av det program som du vill köra kampanjen mot anges på placeringsnivån i [!DNL Facebook Ads Manager].

![Facebook-mål i Adobe Experience Platform användargränssnitt.](../../assets/catalog/social/facebook/catalog.png)

## Användningsfall

För att du bättre ska förstå hur och när du ska använda [!DNL Facebook] mål, här är två exempel på användningsområden som Adobe Experience Platform-kunder kan lösa med den här funktionen.

### Använd skiftläge 1

En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa till [!DNL Facebook] sociala plattformar, optimera deras annonsutgifter.

### Använd skiftläge 2

Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare som företaget har om dessa kunder är medlems-ID och e-postadresser.

För att rikta in dem på sociala medier kan de lägga in kunddata från sina CRM i Adobe Experience Platform med e-postadresserna som identifierare.

Därefter kan de använda sina offlinedata, inklusive tillhörande medlemskaps-ID:n och kundnivåer, för att skapa nya målgrupper som de kan rikta sig till via [!DNL Facebook] mål.

## Identiteter som stöds {#supported-identities}

[!DNL Facebook Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i Facebook-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Krav för facebook-konton {#facebook-account-prerequisites}

Innan du kan skicka dina målgrupper till [!DNL Facebook]ska du kontrollera att du uppfyller följande krav:

* Dina [!DNL Facebook] användarkontot måste ha fullständig åtkomst till [!DNL Facebook Business Account] som äger annonskontot som du använder.
* Dina [!DNL Facebook] användarkontot måste ha **[!DNL Manage campaigns]** behörighet aktiverad för annonskontot som du tänker använda.
* The **Adobe Experience Cloud** företagskonto måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Se [Lägg till partners i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.
  >[!IMPORTANT]
  >
  > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera **Hantera kampanjer** behörighet. Behörighet krävs för [!DNL Adobe Experience Platform] integrering.
* Läs och signera [!DNL Facebook Custom Audiences] Användarvillkor. Om du vill göra det går du till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >När du signerar [!DNL Facebook Custom Audiences] Användarvillkoren måste använda samma användarkonto som du använde för att autentisera i Facebook API.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL Facebook] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två sätt att aktivera telefonnummer i [!DNL Facebook]:

* **Inmatning av telefonnummer i råformat**: du kan importera råa telefonnummer i [!DNL E.164] formatera till [!DNL Platform]. De hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till `Phone_E.164` namnutrymme.
* **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du lägger in dem i [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hash-kodade telefonnummer till `Phone_SHA256` namnutrymme.

>[!NOTE]
>
>Telefonnummer som hämtas till `Phone` namnutrymmet kan inte aktiveras i [!DNL Facebook].

## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du hämtar dem till Adobe Experience Platform, eller använda e-postadresser utan att märka dem i Experience Platform, och du kan [!DNL Platform] hash-koda dem vid aktiveringen.

Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](/help/ingestion/batch-ingestion/overview.md) och [översikt över direktuppspelning](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen, exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen utan hashning hashas automatiskt av [!DNL Platform] vid aktivering.
> Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.
> The **[!UICONTROL Apply transformation]** -alternativet visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Använd omformningskontroll som markeras i mappningssteget.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda `Extern_ID` namnutrymme som data skickas till [!DNL Facebook]måste du synkronisera dina egna identifierare med [!DNL Facebook Pixel]. Se [Facebook officiella dokumentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) för detaljerad information.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I videon nedan visas även hur du konfigurerar en [!DNL Facebook] destinera och aktivera målgrupper.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Autentisera till mål {#authenticate}

1. Hitta Facebook-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till Facebook-steget som visas i aktiveringsarbetsflödet.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Ange dina Facebook-uppgifter och välj **Logga in**.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Konto-ID"
>abstract="Ditt Facebook-konto-ID. Du hittar detta ID i ditt Facebook Ads Manager-konto. När du anger detta ID ska du alltid prefix det med `act_`."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: din [!DNL Facebook Ad Account ID]. Du hittar detta ID i din [!DNL Facebook Ads Manager] konto. När du anger detta ID ska du alltid prefix det med `act_`.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Målgruppens ursprung"
>abstract="Välj hur kunddata i målgruppen ursprungligen samlades in. Data visas i Facebook när en användare anges i segmentet"

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
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL Origin of audience] när målgrupper skickas till [!DNL Facebook Custom Audiences].

![Ursprunget för den meny som visas i Facebook aktiveringssteg.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Mappningsexempel: aktivera målgruppsdata i [!DNL Facebook Custom Audience] {#example-facebook}

Nedan visas ett exempel på korrekt identitetsmappning när målgruppsdata aktiveras i [!DNL Facebook Custom Audience].

Välja källfält:

* Välj `Email` namnutrymmet som källidentitet om e-postadresserna du använder inte hashas.
* Välj `Email_LC_SHA256` namnrymd som källidentitet om du har hasarkiverat e-postadresser till kundens inmatning i [!DNL Platform], enligt [!DNL Facebook] [krav på e-posthashning](#email-hashing-requirements).
* Välj `PHONE_E.164` namnutrymme som källidentitet om dina data består av icke-hash-kodade telefonnummer. [!DNL Platform] kommer att hash-koda telefonnumren för att uppfylla [!DNL Facebook] krav.
* Välj `Phone_SHA256` namnrymd som källidentitet om du hashade telefonnummer vid datainmatning till [!DNL Platform], enligt [!DNL Facebook] [hashkrav för telefonnummer](#phone-number-hashing-requirements).
* Välj `IDFA` namnutrymme som källidentitet om dina data består av [!DNL Apple] enhets-ID.
* Välj `GAID` namnutrymme som källidentitet om dina data består av [!DNL Android] enhets-ID.
* Välj `Custom` namnutrymme som källidentitet om dina data består av andra typer av identifierare.

Markera målfält:

* Välj `Email_LC_SHA256` namespace som target identity när källnamnutrymmena antingen är `Email` eller `Email_LC_SHA256`.
* Välj `Phone_SHA256` namespace som target identity när källnamnutrymmena antingen är `PHONE_E.164` eller `Phone_SHA256`.
* Välj `IDFA` eller `GAID` namnutrymmen som målidentitet när källnamnutrymmen är `IDFA` eller `GAID`.
* Välj `Extern_ID` namespace som target identity när källnamnutrymmet är ett anpassat.

>[!IMPORTANT]
>
>Data från namnutrymmen utan hashning hashas automatiskt av [!DNL Platform] vid aktivering.
> 
>Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.

![Använd omformningskontroll som markeras i mappningssteget.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Exporterade data {#exported-data}

För [!DNL Facebook], innebär en lyckad aktivering att [!DNL Facebook] anpassade målgrupper skulle skapas programmatiskt i [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Målgruppsmedlemskap läggs till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade målgrupperna.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL Facebook] har stöd för historiska efterfyllningar av målgrupper. Alla historiska kvalifikationer skickas till [!DNL Facebook] när du aktiverar målgrupperna till målet.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kunder använder nyligen skapade konton och [!DNL Facebook] behörigheter är ännu inte aktiva.

Om du får `400 Bad Request` felmeddelande efter att ha följt stegen i [Krav för facebook-konton](#facebook-account-prerequisites), kan ta några dagar för [!DNL Facebook] tillstånd att träda i kraft.
