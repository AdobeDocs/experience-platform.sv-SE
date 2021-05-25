---
keywords: facebook-anslutning;facebook-anslutning;facebook-mål;facebook;instagram;messenger;facebook messenger
title: Facebook-anslutning
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: d82eb1a839518dbd9831808485d9d5029e3dcaf5
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---

# [!DNL Facebook] anslutning

## Översikt {#overview}

Aktivera profiler för [!DNL Facebook]-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hash-kodade e-postmeddelanden.

Du kan använda det här målet för målgrupper i alla [!DNL Facebook’s]-appar som stöds av [!DNL Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] och [!DNL Messenger]. Det program som ni valt att köra kampanjen mot anges av placeringsnivån i [!DNL Facebook Ads Manager].

![Facebook-mål i Adobe Experience Platform användargränssnitt](../../assets/catalog/social/facebook/catalog.png)

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda [!DNL Facebook]-målet finns det två exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

### Använd skiftläge 1

En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga segment utifrån sina egna offlinedata och skicka dessa segment till den sociala plattformen [!DNL Facebook] för att optimera annonsutgifterna.

### Använd skiftläge 2

Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare företaget har för dessa kunder är medlems-ID och e-postadresser.

För att rikta in dem på sociala medier kan de lägga in kunddata från sina CRM i Adobe Experience Platform med e-postadresserna som identifierare.

Därefter kan de använda sina offlinedata, inklusive tillhörande medlemskaps-ID:n och kundnivåer, för att skapa nya målgruppssegment som de kan rikta sig mot via målet [!DNL Facebook].

## Identiteter som stöds {#supported-identities}

[!DNL Facebook Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [kraven för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för normal text respektive hashade telefonnummer. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [kraven för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i Facebook-destinationen.

## Krav för facebook-konto {#facebook-account-prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Facebook] måste du kontrollera att du uppfyller följande krav:

- Ditt [!DNL Facebook]-användarkonto måste ha behörigheten **[!DNL Manage campaigns]** aktiverad för det annonskonto som du tänker använda.
- Företagskontot **Adobe Experience Cloud** måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.
   >[!IMPORTANT]
   >
   > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer**. Behörighet krävs för [!DNL Adobe Experience Platform]-integreringen.
- Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. Om du vill göra det går du till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför kan målgrupper som är aktiverade för [!DNL Facebook] vara avstängda från *hash*-identifierare, till exempel e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Kraven för hashning av telefonnummer {#phone-number-hashing-requirements}

Det finns två sätt att aktivera telefonnummer i [!DNL Facebook]:

- **Hämtar råtelefonnummer**: du kan importera råa telefonnummer i  [!DNL E.164] formatet till  [!DNL Platform]. De hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina raw-telefonnummer till namnutrymmet `Phone_E.164`.
- **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du tar dig in i  [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hashade telefonnummer till namnutrymmet `Phone_SHA256`.

>[!NOTE]
>
>Telefonnummer som är inkapslade i namnområdet `Phone` kan inte aktiveras i [!DNL Facebook].


## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser i klartext i Experience Platform, och låta [!DNL Platform] hash-koda dem när de aktiveras.

Om du vill veta mer om att importera e-postadresser i Experience Platform kan du läsa översikten [över gruppimporten](/help/ingestion/batch-ingestion/overview.md) och översikten [över direktuppspelningsförslag](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

- Trimma alla inledande och avslutande blanksteg från e-poststrängen. exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
- När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   - Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
- Kontrollera att den hash-kodade strängen är i gemener
   - Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktiveringen.
> Attributkälldata hashas inte automatiskt. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen.
> Alternativet **[!UICONTROL Apply transformation]** visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Transformering av identitetsmappning](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda namnutrymmet `Extern_ID` för att skicka data till [!DNL Facebook] måste du synkronisera dina egna identifierare med [!DNL Facebook Pixel]. Mer information finns i [Facebook officiella dokumentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers).

## Anslut till målet {#connect-destination}

Mer information om hur du ansluter till [!DNL Facebook]-målet finns i [Arbetsflöde för autentisering av sociala mål](./workflow.md).

I videon nedan visas också stegen för att konfigurera ett [!DNL Facebook]-mål och aktivera segment.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Aktivera segment till [!DNL Facebook] {#activate-segments}

Instruktioner om hur du aktiverar segment till [!DNL Facebook] finns i [Aktivera data till mål](../../ui/activate-destinations.md).

I steget **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL Origin of audience] när du skickar segment till [!DNL Facebook Custom Audiences].

![Facebook Origin of Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Exporterade data {#exported-data}

För [!DNL Facebook] innebär en lyckad aktivering att en [!DNL Facebook] anpassad målgrupp skapas programmatiskt i [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL Facebook] har stöd för historiska efterfyllningar av målgrupper. Alla historiska segmentkvalifikationer skickas till [!DNL Facebook] när du aktiverar segmenten till målet.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du aktiverar segment till [!DNL Facebook] kan du få följande fel:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kunder använder nyligen skapade konton och [!DNL Facebook]-behörigheterna inte är aktiva ännu.

Om du får felmeddelandet `400 Bad Request` efter att du har följt stegen i [Facebook-kontoförutsättningarna](#facebook-account-prerequisites), tillåt några dagar innan behörigheterna [!DNL Facebook] börjar gälla.