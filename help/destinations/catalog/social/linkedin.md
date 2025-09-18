---
keywords: länkad anslutning;länkad anslutning;länkade destinationer;länkad;
title: Länkad matchad målgruppsanslutning
description: Aktivera profiler för era LinkedIn-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hash-kodade e-postmeddelanden.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 653f43ac6afb25445fe8ef3c2832be8f1c4723fe
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences]-anslutning

## Översikt {#overview}

Aktivera profiler för dina [!DNL LinkedIn]-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hash-kodade e-postmeddelanden och mobil-ID:n.

![LinkedIn-mål i Adobe Experience Platform-gränssnittet](../../assets/catalog/social/linkedin/catalog.png)

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL LinkedIn Matched Audiences] finns det ett användningsexempel som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

Ett programvaruföretag organiserar en konferens och vill hålla kontakt med deltagarna och visa dem personliga erbjudanden baserat på deras konferensstatus. Företaget kan importera e-postadresser eller mobilenhets-ID:n från sina egna [!DNL CRM] till Adobe Experience Platform. Sedan kan de bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till den sociala [!DNL LinkedIn]-plattformen, vilket optimerar deras annonsutgifter.

## Identiteter som stöds {#supported-identities}

[!DNL LinkedIn Matched Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
>
>Från och med september 2025 har målet [!DNL LinkedIn Matched Audiences] inte längre stöd för [!DNL IDFA]-identiteter (identifierare för annonsörer).  Den här ändringen beror på LinkedIn:s krav och är inte relaterad till några uppgraderingar av Experience Platform destinationstjänst.


| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet [ID-matchningskrav](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashad e-post. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |

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
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer och andra) som används i målet [!DNL LinkedIn Matched Audiences]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Krav för LinkedIn-konto {#LinkedIn-account-prerequisites}

Innan du kan använda målet [!UICONTROL LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar användarbehörigheter för [!DNL LinkedIn Campaign Manager] finns i [Lägg till, redigera och ta bort användarbehörigheter för Advertising-konton](https://www.linkedin.com/help/lms/answer/5753) i dokumentationen för LinkedIn.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför kan målgrupper som är aktiverade för [!DNL LinkedIn Matched Audiences] inaktiveras för *hashed*-identifierare, som e-postadresser eller mobila enhets-ID:n.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser som är tydliga i Experience Platform, och få [!DNL Experience Platform] hash-kodade adresser när de aktiveras.

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [gruppimporten](/help/ingestion/batch-ingestion/overview.md) och översikten över [direktuppspelningsinläsningen](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. Till exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Experience Platform] vid aktiveringen.
>&#x200B;> Attributkälldata hashas inte automatiskt.
> 
> Om källfältet innehåller ohstreckade attribut ska du under steget [Identitetsmappning](../../ui/activate-segment-streaming-destinations.md#mapping) kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen.
> 
> Alternativet **[!UICONTROL Apply transformation]** visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Omvandling av identitetsmappning](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I videon nedan visas också stegen för att konfigurera ett [!DNL LinkedIn Matched Audiences]-mål och aktivera målgrupper.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform användargränssnitt uppdateras ofta och kan ha ändrats sedan den här videon spelades in. Den senaste informationen finns i [självstudiekursen för målkonfiguration](../../ui/connect-destination.md).

### Autentisera till mål {#authenticate}

1. Hitta [!DNL LinkedIn Matched Audiences]-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Ange dina inloggningsuppgifter för LinkedIn och välj **Logga in**.

### Uppdatera autentiseringsuppgifter {#refresh-authentication-credentials}

LinkedIn-tokens går ut var 60:e dag. Du kan övervaka förfallotiden för dina tokens från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** eller **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)**.

När token har gått ut slutar dataexporten till målet att fungera. Du kan förhindra detta genom att utföra följande steg:

1. Navigera till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Valfritt) Använd de tillgängliga filtren på sidan om du bara vill visa LinkedIn-konton.
   ![Filtrera så att endast LinkedIn-konton visas](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. Markera det konto som du vill uppdatera, markera ellipsen och välj **[!UICONTROL Edit details]**.
   ![Välj kontrollen Redigera information](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. I det modala fönstret väljer du **[!UICONTROL Reconnect OAuth]** och autentiserar igen med dina LinkedIn-inloggningsuppgifter.
   ![Modalt fönster med alternativet Återanslut OAuth](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Dina autentiseringsuppgifter uppdateras och deras förfallotid återställs till 60 dagar.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Konto-ID"
>abstract="Ditt konto-ID för LinkedIn Campaign Manager. Du hittar detta ID i ditt LinkedIn Campaign Manager-konto."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL LinkedIn Campaign Manager Account ID]. Du kan hitta det här ID:t i ditt [!DNL LinkedIn Campaign Manager]-konto.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

En lyckad aktivering innebär att en anpassad [!DNL LinkedIn]-målgrupp skapas programmatiskt i [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Målgruppsmedlemskapet justeras eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade målgrupperna.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL LinkedIn Matched Audiences] har stöd för tidigare målgruppsåsidosättningar. Alla historiska målgruppskvalifikationer skickas till [!DNL LinkedIn] när du aktiverar målgrupperna till målet.
