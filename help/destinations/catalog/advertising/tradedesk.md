---
keywords: annonsering, reklamavdelning, reklamavdelning
title: The Trade Desk connection
description: Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för webbannonsering, video och mobilannonslager.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 0954b5f22d609b0b12352de70f6c618cc88757c8
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---

# [!DNL The Trade Desk]-anslutning

## Översikt {#overview}

>[!IMPORTANT]
>
>* Från och med den 31 juli 2025 kan du se två **[!DNL The Trade Desk]**-kort sida vid sida i målkatalogen. Det här beror på en intern uppgradering av måltjänsten. Den befintliga **[!DNL The Trade Desk]**-målkopplingen har bytt namn till **[!UICONTROL (Deprecated) The Trade Desk]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL The Trade Desk]**.
>* Använd den nya **[!UICONTROL The Trade Desk]**-anslutningen i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till målet **[!UICONTROL (Deprecated) The Trade Desk]** uppdateras de automatiskt, så ingen åtgärd krävs från dig.
>* Om du skapar dataflöden via [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:
>   * Flödesspecifikation-id: `86134ea1-b014-49e8-8bd3-689f4ce70578`
>   * Anslutningsspecifikation-id: `1029798b-a97f-4c21-81b2-e0301471166e`

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
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| ECID | EXPERIENCE CLOUD ID | Den här identiteten är obligatorisk för att integreringen ska fungera korrekt, men den används inte för målgruppsaktivering. |
| The Trade Desk ID | Advertiser-ID på plattformen [!DNL The Trade Desk] | Använd den här identiteten när du aktiverar målgrupper baserat på varumärkets egna ID. |

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
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL The Trade Desk] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL The Trade Desk]-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

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

Alla målidentiteter som beskrivs i avsnittet [identiteter som stöds](#supported-identities) är obligatoriska och måste mappas under målgruppsaktiveringen. Detta inkluderar:

* **GAID** (Google Advertising ID)
* **IDFA** (Apple ID för annonsörer)
* **ECID** (Experience Cloud-ID)
* **Trade Desk-ID**

Om det inte går att mappa alla nödvändiga identiteter kommer målgruppsaktiveringen inte att lyckas till [!DNL The Trade Desk]. Varje identitet har ett specifikt syfte i integreringen och alla krävs för att målet ska fungera korrekt.

![Skärmbild med obligatoriska mappningar](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL The Trade Desk]-konto om du vill verifiera om data har exporterats till målet [!DNL The Trade Desk]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
