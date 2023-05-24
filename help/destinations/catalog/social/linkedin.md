---
keywords: länkad anslutning;länkad anslutning;länkade destinationer;länkad;
title: Länkad matchad målgruppsanslutning
description: Aktivera profiler för era LinkedIn-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hashad-e-post.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] anslutning

## Översikt {#overview}

Aktivera profiler för [!DNL LinkedIn] kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hashad-e-post och mobila ID:n.

![linkedIn-mål i Adobe Experience Platform användargränssnitt](../../assets/catalog/social/linkedin/catalog.png)

## Användningsfall

För att du bättre ska förstå hur och när du ska använda [!DNL LinkedIn Matched Audiences] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa med den här funktionen.

Ett programvaruföretag organiserar en konferens och vill hålla kontakt med deltagarna och visa dem personliga erbjudanden baserat på deras konferensstatus. Företaget kan importera e-postadresser eller mobilenhets-ID:n från sina egna [!DNL CRM] till Adobe Experience Platform. Sedan kan de skapa segment utifrån sina egna offlinedata och skicka dessa segment till [!DNL LinkedIn] social plattform, optimera deras annonsutgifter.

## Identiteter som stöds {#supported-identities}

[!DNL LinkedIn Matched Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [Krav för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text och hashad e-post. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer och andra) som används i [!DNL LinkedIn Matched Audiences] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Krav för linkedIn-konton {#LinkedIn-account-prerequisites}

Innan du kan använda [!UICONTROL LinkedIn Matched Audience] mål, se till att [!DNL LinkedIn Campaign Manager] kontot har [!DNL Creative Manager] behörighet eller högre.

Så här redigerar du [!DNL LinkedIn Campaign Manager] användarbehörigheter, se [Lägg till, redigera och ta bort användarbehörigheter på annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL LinkedIn Matched Audiences] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller mobilenhets-ID.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för e-posthashning {#email-hashing-requirements}

Du kan hash-koda e-postadresser innan du hämtar dem till Adobe Experience Platform, eller använda e-postadresser utan att märka dem i Experience Platform, och du kan [!DNL Platform] hash-koda dem vid aktiveringen.

Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](/help/ingestion/batch-ingestion/overview.md) och [översikt över direktuppspelning](/help/ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. Till exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.

>[!NOTE]
>
>Data från namnutrymmen som inte är hash-kodade hashas automatiskt av [!DNL Platform] vid aktivering.
> Attributkälldata hashas inte automatiskt.
> 
> Under [Identitetsmappning](../../ui/activate-segment-streaming-destinations.md#mapping) om källfältet innehåller ohashade attribut ska du kontrollera **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.
> 
> The **[!UICONTROL Apply transformation]** -alternativet visas bara när du väljer attribut som källfält. Den visas inte när du väljer namnutrymmen.

![Transformering av identitetsmappning](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I videon nedan visas även hur du konfigurerar en [!DNL LinkedIn Matched Audiences] mål och aktivera segment.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Autentisera till mål {#authenticate}

1. Hitta [!DNL LinkedIn Matched Audiences] mål i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Ange dina LinkedIn-uppgifter och välj **Logga in**.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Konto-ID"
>abstract="Ditt konto-ID för LinkedIn Campaign Manager. Du hittar detta ID i ditt LinkedIn Campaign Manager-konto."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL LinkedIn Campaign Manager Account ID]. Du hittar detta ID i din [!DNL LinkedIn Campaign Manager] konto.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

En lyckad aktivering innebär att [!DNL LinkedIn] anpassade målgrupper skapas programmatiskt i [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

>[!TIP]
>
>Integrationen mellan Adobe Experience Platform och [!DNL LinkedIn Matched Audiences] har stöd för historiska efterfyllningar av målgrupper. Alla historiska segmentkvalifikationer skickas till [!DNL LinkedIn] när du aktiverar segmenten till målet.
