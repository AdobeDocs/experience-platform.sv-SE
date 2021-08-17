---
keywords: länkad anslutning;länkad anslutning;länkade destinationer;länkad;
title: Länkad matchad målgruppsanslutning
description: Aktivera profiler för era LinkedIn-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hashad-e-post.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# [!DNL LinkedIn Matched Audiences] anslutning

## Översikt {#overview}

Aktivera profiler för era [!DNL LinkedIn]-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hash-kodade e-postmeddelanden och mobil-ID:n.

![linkedIn-mål i Adobe Experience Platform användargränssnitt](../../assets/catalog/social/linkedin/catalog.png)

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL LinkedIn Matched Audiences] finns det ett användningsexempel som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

Ett programvaruföretag organiserar en konferens och vill hålla kontakt med deltagarna och visa dem personliga erbjudanden baserat på deras konferensstatus. Företaget kan importera e-postadresser eller mobilenhets-ID:n från sina egna [!DNL CRM] till Adobe Experience Platform. Sedan kan de bygga segment utifrån sina egna offlinedata och skicka dessa segment till den sociala plattformen [!DNL LinkedIn], vilket optimerar deras annonsutgifter.

## Identiteter som stöds {#supported-identities}

[!DNL LinkedIn Matched Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [kraven för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashad e-post. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |


## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer och andra) som används i  [!DNL LinkedIn Matched Audiences] målet.

## Krav för linkedIn-konton {#LinkedIn-account-prerequisites}

Innan du kan använda målet [!UICONTROL LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar dina [!DNL LinkedIn Campaign Manager]-användarbehörigheter finns i [Lägg till, redigera och ta bort användarbehörigheter för annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför kan målgrupper som är aktiverade för [!DNL LinkedIn Matched Audiences] vara avstängda från *hash*-identifierare, till exempel e-postadresser eller mobila enhets-ID:n.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser i klartext i Experience Platform, och låta [!DNL Platform] hash-koda dem när de aktiveras.

Om du vill veta mer om att importera e-postadresser i Experience Platform kan du läsa översikten [över gruppimporten](/help/ingestion/batch-ingestion/overview.md) och översikten [över direktuppspelningsförslag](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. Till exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktiveringen.
> Attributkälldata hashas inte automatiskt.
> 
> Om källfältet innehåller ohstreckade attribut ska du under steget [Identitetsmappning](../../ui/activate-destinations.md#mapping) kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen.
> 
> Alternativet **[!UICONTROL Apply transformation]** visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Transformering av identitetsmappning](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

I videon nedan visas också stegen för att konfigurera ett [!DNL LinkedIn Matched Audiences]-mål och aktivera segment.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i [självstudiekursen för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: en beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: din  [!DNL LinkedIn Campaign Manager Account ID]. Du hittar detta ID i ditt [!DNL LinkedIn Campaign Manager]-konto.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till mål.

## Exporterade data {#exported-data}

En lyckad aktivering innebär att en [!DNL LinkedIn]-anpassad målgrupp skapas programmatiskt i [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL LinkedIn Matched Audiences] har stöd för historiska efterfyllningar av målgrupper. Alla historiska segmentkvalifikationer skickas till [!DNL LinkedIn] när du aktiverar segmenten till målet.
