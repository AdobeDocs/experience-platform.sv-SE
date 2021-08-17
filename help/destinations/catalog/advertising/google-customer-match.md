---
keywords: Google customer match;Google customer match;Google Customer Match
title: Google Customer Match Connection
description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egenskaper, som Search, Shopping, Gmail och YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# [!DNL Google Customer Match] anslutning

## Översikt {#overview}

[Med Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets kan ni använda era online- och offlinedata för att nå och återengagera era kunder över Googles egna och styrda egenskaper, som:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail]och  [!DNL YouTube].

![Google Customer Match destination in the Adobe Experience Platform UI](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda [!DNL Google Customer Match]-målet finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

### Använd skiftläge 1

Ett sportklädmärke vill nå befintliga kunder via [!DNL Google Search] och [!DNL Google Shopping] för att personalisera erbjudanden och objekt baserat på deras tidigare köp och webbhistorik. Det klädvarumärket kan importera e-postadresser från sin egen CRM till Experience Platform och bygga segment utifrån sina egna offlinedata. Sedan kan de skicka dessa segment till [!DNL Google Customer Match] för användning i [!DNL Search] och [!DNL Shopping], vilket optimerar deras annonsutgifter.

### Använd skiftläge 2

Ett framstående teknikföretag lanserade en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Segment skapas baserat på kunder som äger äldre telefonmodeller. Sedan skickas segment till [!DNL Google Customer Match] så att företaget kan inrikta sig på befintliga kunder, kunder som äger äldre telefonmodeller och liknande kunder på [!DNL YouTube].

## Datastyrning för [!DNL Google Customer Match]-mål {#data-governance}

Vissa destinationer i Experience Platform har vissa regler och skyldigheter för data som skickas till eller tas emot från destinationsplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs ](../../../data-governance/labels/overview.md) mer om verktyg och policyer för datastyrning.

## Identiteter som stöds {#supported-identities}

[!DNL Google Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| phone_sha256_e.164 | Telefonnummer i E164-format som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Följ instruktionerna i [kraven för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för normal text respektive hashade telefonnummer. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i [kraven för ID-matchning](#id-matching-requirements-id-matching-requirements) och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| user_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer och andra) som används i  [!DNL Google Customer Match] målet.

## [!DNL Google Customer Match] kontokrav {#google-account-prerequisites}

Innan du konfigurerar ett [!DNL Google Customer Match]-mål i Experience Platform måste du läsa och följa Googles policy för att använda [!DNL Customer Match], som beskrivs i [Google Support-dokumentationen](https://support.google.com/google-ads/answer/6299717).

Kontrollera sedan att ditt [!DNL Google]-konto är konfigurerat för en [!DNL Standard]-åtkomstnivå eller högre. Mer information finns i [Google Ads-dokumentationen](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).

### Tillåtelselista {#allowlist}

Innan du skapar [!DNL Google Customer Match]-målet i Experience Platform måste du kontrollera att ditt [!DNL Google Ads]-konto är kompatibelt med [Google Customer Match Policy](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunder med kompatibla konton tillåts automatiskt listade av Google.

## Krav för ID-matchning {#id-matching-requirements}

[!DNL Google] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför kan målgrupper som är aktiverade för [!DNL Google Customer Match] vara avstängda från *hash*-identifierare, till exempel e-postadresser eller telefonnummer.

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav.

## Krav för telefonnummerhashning {#phone-number-hashing-requirements}

Det finns två sätt att aktivera telefonnummer i [!DNL Google Customer Match]:

* **Hämtar råtelefonnummer**: kan du importera råa telefonnummer i  [!DNL E.164] formatet till  [!DNL Platform]och de hashas automatiskt när de aktiveras. Om du väljer det här alternativet måste du alltid importera dina raw-telefonnummer till namnutrymmet `Phone_E.164`.
* **Inmatning av hashade telefonnummer**: du kan förhash-koda dina telefonnummer innan du tar dig in i  [!DNL Platform]. Om du väljer det här alternativet måste du alltid importera dina hashade telefonnummer till namnutrymmet `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Telefonnummer som är inkapslade i namnområdet `Phone` kan inte aktiveras i [!DNL Google Customer Match].

## Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller använda e-postadresser i klartext i Experience Platform, och låta [!DNL Platform] hash-koda dem när de aktiveras.

Mer information om Googles hash-krav och andra begränsningar för aktivering finns i följande avsnitt i Googles dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Kundmatchning med telefonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Kundmatchning med mobila enhets-ID:n](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Om du vill veta mer om att importera e-postadresser i Experience Platform kan du läsa översikten [över gruppimporten](../../../ingestion/batch-ingestion/overview.md) och översikten [över direktuppspelningsförslag](../../../ingestion/streaming-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att följa kraven för Google som beskrivs i länkarna ovan.

## Använda anpassade namnutrymmen {#custom-namespaces}

Innan du kan använda namnutrymmet `User_ID` för att skicka data till Google måste du synkronisera dina egna identifierare med [!DNL gTag]. Mer information finns i [Googles officiella dokumentation](https://support.google.com/google-ads/answer/9199250).

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: ange ett namn för den här målanslutningen
* **[!UICONTROL Description]**: ange en beskrivning för den här målanslutningen
* **[!UICONTROL Account ID]**: ditt Google-kundklient-ID. Formatet på ID:t är xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * Marknadsföringsåtgärden **[!UICONTROL Combine with PII]** är markerad som standard för målet [!DNL Google Customer Match] och kan inte tas bort.


## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

I steget **[!UICONTROL Segment schedule]** måste du ange [!UICONTROL App ID] när du skickar segmenten [!DNL IDFA] eller [!DNL GAID] till [!DNL Google Customer Match].

![Google Customer Match App ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Mer information om hur du hittar [!DNL App ID] finns i [Googles officiella dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

## Verifiera att segmentaktiveringen lyckades {#verify-activation}

När aktiveringsflödet är klart växlar du till ditt **[!UICONTROL Google Ads]**-konto. De aktiverade segmenten visas i ditt Google-konto som kundlistor. Observera att beroende på segmentstorleken fyller vissa målgrupper inte i bilden om det inte finns fler än 100 aktiva användare att betjäna.

När du mappar ett segment till både [!DNL IDFA] och [!DNL GAID] mobila ID:n skapar [!DNL Google Customer Match] ett separat segment för varje ID-mappning. Ditt [!DNL Google Ads]-konto visar två olika segment, ett för [!DNL IDFA] och ett för [!DNL GAID]-mappningen.

## Extra resurser {#additional-resources}

* [Integrera Google Customer Match - videosjälvstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
