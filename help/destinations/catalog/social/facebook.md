---
keywords: facebook-anslutning;facebook-anslutning;facebook-mål;facebook;instagram;messenger;facebook messenger
title: Facebook-anslutning
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 357916aa925c7b3ada4abe64a2bc6ad090d70cc0
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 1%

---

# [!DNL Facebook] anslutning

## Översikt {#overview}

Aktivera profiler för [!DNL Facebook] kampanjer för målgruppsanpassning, personalisering och undertryckande baserat på hashad-e-post.

Du kan använda det här målet för målgruppsanpassning över [!DNL Facebook’s] program som stöds av [!DNL Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]och [!DNL Messenger]. Det program som ni valt att köra kampanjen mot anges av placeringsnivån i [!DNL Facebook Ads Manager].

![Facebook-mål i Adobe Experience Platform användargränssnitt](../../assets/catalog/social/facebook/catalog.png)

## Användningsfall

För att du bättre ska förstå hur och när du ska använda [!DNL Facebook] mål, här är två exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

### Använd skiftläge 1

En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga segment utifrån sina egna offlinedata och skicka dessa segment till [!DNL Facebook] social plattform, optimera deras annonsutgifter.

### Använd skiftläge 2

Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare företaget har för dessa kunder är medlems-ID och e-postadresser.

För att rikta in dem på sociala medier kan de lägga in kunddata från sina CRM i Adobe Experience Platform med e-postadresserna som identifierare.

Därefter kan de använda sina offlinedata, inklusive tillhörande medlemskaps-ID:n och kundnivåer, för att skapa nya målgruppssegment som de kan rikta sig till via [!DNL Facebook] mål.

## Identiteter som stöds {#supported-identities}

[!DNL Facebook Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade telefonnummer. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

## Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i Facebook-destinationen.

## Krav för facebook-konton {#facebook-account-prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Facebook]måste du uppfylla följande krav:

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

* **Inmatning av råtelefonnummer**: du kan importera råa telefonnummer i [!DNL E.164] formatera till [!DNL Platform]. De hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina råa telefonnummer till `Phone_E.164` namnutrymme.
* **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du tar dig in i [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hash-kodade telefonnummer till `Phone_SHA256` namnutrymme.

>[!NOTE]
>
>Telefonnummer som hämtas till `Phone` namnutrymmet kan inte aktiveras i [!DNL Facebook].


## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du hämtar dem till Adobe Experience Platform, eller använda e-postadresser utan att märka dem i Experience Platform, och du kan [!DNL Platform] hash-koda dem vid aktiveringen.

Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](/help/ingestion/batch-ingestion/overview.md) och [översikt över direktuppspelning](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktivering.
> Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.
> The **[!UICONTROL Apply transformation]** -alternativet visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Transformering av identitetsmappning](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda `Extern_ID` namnutrymme som data skickas till [!DNL Facebook]måste du synkronisera dina egna identifierare med [!DNL Facebook Pixel]. Se [Facebook officiella dokumentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) för detaljerad information.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

I videon nedan visas även hur du konfigurerar en [!DNL Facebook] mål och aktivera segment.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: din [!DNL Facebook Ad Account ID]. Du hittar detta ID i din [!DNL Facebook Ads Manager] konto. När du anger detta ID ska du alltid prefix det med `act_`.

## Aktivera segment till den här destinationen {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Målgruppens ursprung"
>abstract="Välj hur kunddata i segmentet ursprungligen samlades in. Data visas i Facebook när en användare anges av segmentet"
>additional-url="http://www.adobe.com/go/destinations-facebook-activate-section-en" text="Läs mer i dokumentationen"

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

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

I **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL Origin of audience] när segment skickas till [!DNL Facebook Custom Audiences].

![Facebook Origin of Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

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
* Välj `IDFA` eller `GAID` namnutrymmen som målidentitet när källnamnutrymmena är `IDFA` eller `GAID`.
* Välj `Extern_ID` namespace som target identity när källnamnutrymmet är ett anpassat.

>[!IMPORTANT]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktivering.
> 
>Attributkälldata hashas inte automatiskt. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.

![Identitetsmappning](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Exporterade data {#exported-data}

För [!DNL Facebook], innebär en lyckad aktivering att [!DNL Facebook] anpassade målgrupper skapas programmatiskt i [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL Facebook] har stöd för historiska efterfyllningar av målgrupper. Alla historiska segmentkvalifikationer skickas till [!DNL Facebook] när du aktiverar segmenten till målet.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kunder använder nyligen skapade konton och [!DNL Facebook] behörigheter är ännu inte aktiva.

Om du får `400 Bad Request` felmeddelande efter att ha följt stegen i [Krav för facebook-konton](#facebook-account-prerequisites), kan du vänta i några dagar för [!DNL Facebook] tillstånd att träda i kraft.
