---
keywords: annonsering, reklamavdelning, reklamavdelning
title: The Trade Desk connection
description: Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för webbannonsering, video och mobilannonslager.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: e145dc91fca471078cf94d84ce1012f659d70293
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 0%

---

# [!DNL The Trade Desk]-anslutning

## Översikt {#overview}


>[!IMPORTANT]
>
> Efter den [interna uppgraderingen](../../../release-notes/2025/july-2025.md#destinations) till måltjänsten från juli 2025 kan du märka en **minskning av antalet aktiverade profiler** i dataflödena till [!DNL The Trade Desk].
> Den här minskningen orsakas av förbättrad synlighet för övervakning. Profiler utan ECID räknas nu korrekt som utelämnade i aktiveringsmåtten. Mer information finns i avsnittet [obligatorisk mappning](#mandatory-mappings) på den här sidan.
>
>**Vad har ändrats:**
>
>* Måltjänsten rapporterar nu korrekt när profiler utan ECID tas bort från aktiveringen.
>* **Viktigt!** Profiler utan ECID har aldrig konverterats till [!DNL The Trade Desk] ens före uppgraderingen. Integreringen har alltid krävt ECID. Den här uppgraderingen åtgärdar ett fel som tidigare förhindrade att dessa fall syntes i mätvärdena.
>
>**Vad du behöver göra:**
>
>* Granska era målgruppsdata för att bekräfta att profilerna har giltiga ECID-värden.
>* Övervaka dina aktiveringsvärden för att verifiera förväntat antal profiler. Lägre antal ger korrekt rapportering, inte en förändring av målbeteendet.

Använd den här målkopplingen för att skicka profildata till [!DNL The Trade Desk]. Den här kopplingen skickar data till den [!DNL The Trade Desk] första partens slutpunkt. Integrationen mellan Adobe Experience Platform och [!DNL The Trade Desk] stöder inte export av data till slutpunkten för [!DNL The Trade Desk] från tredje part.

[!DNL The Trade Desk] är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för webbannonsering, video och mobilannonslager.

Om du vill skicka profildata till [!DNL The Trade Desk] måste du först ansluta till målet, vilket beskrivs i följande avsnitt på den här sidan.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda målgrupper som är inbyggda i [!DNL Trade Desk IDs] eller enhets-ID för att skapa återmarknadsföring eller målgruppsanpassade digitala kampanjer.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Nedan visas de identiteter som stöds av målet [!DNL The Trade Desk]. Dessa identiteter kan användas för att aktivera målgrupper för [!DNL The Trade Desk].

Alla identiteter i tabellen nedan är obligatoriska mappningar.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| [!DNL GAID] | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| [!DNL IDFA] | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| [!DNL ECID] | EXPERIENCE CLOUD ID | Den här identiteten är obligatorisk för att integreringen ska fungera korrekt, men den används inte för målgruppsaktivering. |
| [!DNL Tradedesk] | [!DNL TDID] på plattformen [!DNL The Trade Desk] | Använd den här identiteten när du aktiverar målgrupper baserat på varumärkets egna ID. |

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
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL The Trade Desk] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/sv/docs/id-service/using/id-service-api/methods/idsync) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL The Trade Desk]-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Fråga din [!DNL The Trade Desk]-representant vilken regional server du ska använda. Nedan visas de tillgängliga regionala servrarna som du kan välja mellan:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I steget [Målgruppsschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa dina målgrupper till deras motsvarande ID eller egna namn på målplattformen.

När du kartlägger målgrupper rekommenderar Adobe att du använder Experience Platform målgruppsnamn eller en kortare form av det för att underlätta användningen. Men målgrupps-ID:t eller målnamnet behöver inte matcha det i ditt Experience Platform-konto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

### Obligatoriska mappningar {#mandatory-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Förkonfigurerade mappningsuppsättningar"
>abstract="Vi har förkonfigurerat dessa fyra mappningsuppsättningar åt dig. När du aktiverar data till The Trade Desk behöver de profiler som är kvalificerade för de aktiverade målgrupperna inte nödvändigtvis ha alla fyra identiteterna i profilerna, eftersom detta mål fungerar med någon av de målidentiteter som visas här. <br> För cookie-baserad målinriktning baserat på Trade Desk ID behöver du ett ECID i profilen och en ID-synkroniseringsmappning mellan Trade Desk ID och ECID."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Läs mer om förkonfigurerade mappningar"

Alla målidentiteter som beskrivs i avsnittet [identiteter som stöds](#supported-identities) måste mappas i mappningssteget i arbetsflödet för målgruppsaktivering. Detta inkluderar:

* [!DNL GAID] (Google Advertising-id)
* [!DNL IDFA] (Apple-id för annonsörer)
* [!DNL ECID] (Experience Cloud-ID)
* [!DNL The Trade Desk ID]

![Skärmbild med obligatoriska mappningar](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

Genom att mappa alla målidentiteter säkerställer du att aktiveringen kan dela upp och leverera profiler på rätt sätt med valfri identitet. Det innebär inte att alla identiteter måste finnas i varje profil.

För att exporten till The Trade Desk ska lyckas måste en profil innehålla:

* [!DNL ECID] och
* minst en av: [!DNL GAID], [!DNL IDFA] eller [!DNL The Trade Desk ID]

Exempel:

* Endast [!DNL ECID]: exporteras inte
* [!DNL ECID] + [!DNL The Trade Desk ID]: exporterad
* [!DNL ECID] + [!DNL IDFA]: exporterad
* [!DNL ECID] + [!DNL GAID]: exporterad
* [!DNL IDFA] + [!DNL The Trade Desk ID] (no [!DNL ECID]): exporteras inte

>[!NOTE]
> 
>Efter uppgraderingen [juli 2025](/help/release-notes/2025/july-2025.md#destinations) till måltjänsten rapporteras profiler som saknas [!DNL ECID] korrekt som utelämnade i aktiveringsmått. Detta har alltid varit integreringens beteende - profiler utan [!DNL ECID] har aldrig nåtts [!DNL The Trade Desk] - men dropparna visas nu korrekt i din dataflödesövervakning. Lägre antal aktiveringar ger korrekt rapportering, inte en förändring av målfunktionen.

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL The Trade Desk]-konto om du vill verifiera om data har exporterats till målet [!DNL The Trade Desk]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
