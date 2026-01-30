---
keywords: annonsering, reklamavdelning, reklamavdelning
title: The Trade Desk connection
description: Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för webbannonsering, video och mobilannonslager.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# [!DNL The Trade Desk]-anslutning

## Översikt {#overview}

Använd den här målkopplingen för att skicka profildata till [!DNL The Trade Desk]. Den här kopplingen skickar data till den [!DNL The Trade Desk] första partens slutpunkt. Integrationen mellan Adobe Experience Platform och [!DNL The Trade Desk] stöder inte export av data till slutpunkten för [!DNL The Trade Desk] från tredje part.

[!DNL The Trade Desk] är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för webbannonsering, video och mobilannonslager.

Om du vill skicka profildata till [!DNL The Trade Desk] måste du först ansluta till målet, vilket beskrivs i följande avsnitt på den här sidan.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda målgrupper som är inbyggda i [!DNL Trade Desk IDs] eller enhets-ID för att skapa återmarknadsföring eller målgruppsanpassade digitala kampanjer.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Nedan visas de identiteter som stöds av målet [!DNL The Trade Desk]. Dessa identiteter kan användas för att aktivera målgrupper för [!DNL The Trade Desk].

Alla identiteter i tabellen nedan är förkonfigurerade och automatiskt mappade under aktiveringen. Du behöver inte konfigurera dessa mappningar manuellt i aktiveringsarbetsflödet.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Aktiveras när det finns ett GAID i profilen. |
| IDFA | Apple ID för annonsörer | Aktiveras när en IDFA finns i profilen. |
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Läs följande dokument på [ECID](/help/identity-service/features/ecid.md) om du vill ha mer information. |
| [!DNL Tradedesk] | [!DNL TDID] på plattformen [!DNL The Trade Desk] | Aktiveras när en profil har ett ECID och en ECID-to-Trade Desk ID-mappning finns i Experience Platform. |

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

Förutsättningar beror på vilka identitetstyper du tänker använda för målgruppsaktivering:

**Det finns inga krav för aktivering av mobilt ID**. Så länge du samlar in och hanterar ID:n (GAID och/eller IDFA) för dina kunder kan du börja aktivera målgrupper till [!DNL The Trade Desk].

**För cookie-baserad målinriktning på[!DNL The Trade Desk]** kontrollerar du att det finns en mappning mellan ECID och [!DNL Trade Desk ID]. Gör så genom att följa stegen nedan:

1. **Aktivera funktionen för ID-synkronisering**: Om det här är första gången du konfigurerar [!DNL The Trade Desk ID]-aktivering och du inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/sv/docs/id-service/using/id-service-api/methods/idsync) i Experience Cloud ID-tjänsten tidigare (med Adobe Audience Manager eller andra program) kontaktar du Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering.
   * Om du tidigare har konfigurerat [!DNL The Trade Desk]-integreringar i Audience Manager överförs dina befintliga ID-synkroniseringar automatiskt till Experience Platform.

2. **Instrumentera dina webbsidor**: Implementera kod på dina webbsidor för att skapa mappningar mellan [!DNL The Trade Desk ID] och Adobe ECID. På så sätt kan Experience Platform koppla Trade Desk-ID:n till kundprofiler.

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

### Förkonfigurerade mappningar {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Förkonfigurerade mappningsuppsättningar"
>abstract="Vi har förkonfigurerat dessa fyra mappningsuppsättningar åt dig. När du aktiverar data till The Trade Desk behöver de profiler som är kvalificerade för de aktiverade målgrupperna inte nödvändigtvis ha alla fyra identiteterna i profilerna, eftersom detta mål fungerar med någon av de målidentiteter som visas här. <br> För cookie-baserad målinriktning baserat på Trade Desk ID behöver du ett ECID i profilen och en ID-synkroniseringsmappning mellan Trade Desk ID och ECID."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Läs mer om förkonfigurerade mappningar"

Följande identitetsmappningar är **förkonfigurerade och fyllda i automatiskt** för dig i arbetsflödet för målgruppsaktivering:

* GAID (Google Advertising-id)
* IDFA (Apple ID för annonsörer)
* ECID (Experience Cloud-ID)
* [!DNL The Trade Desk ID]

![Skärmbild med obligatoriska mappningar](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

De här mappningarna är nedtonade och skrivskyddade. Du behöver inte konfigurera något i det här steget. Välj **[!UICONTROL Next]** om du vill fortsätta.

Experience Platform kontrollerar automatiskt varje profil som tillhör målgrupper som är mappade i aktiveringsarbetsflödet för alla identitetstyper som stöds och aktiverar sedan profilen med hjälp av de identiteter som finns.

### Identitetskrav per aktiveringstyp

**Aktivering av mobilt ID (GAID/IDFA):** Profiler med bara GAID eller IDFA räcker för aktivering. Inga ytterligare identiteter eller krav krävs.

**Cookie-baserad målinriktning ([!DNL Trade Desk ID]):** Kräver båda:

* ECID finns i profilen
* En ID-synkroniseringsmappning mellan [!DNL Trade Desk ID] och ECID (konfigurerad enligt beskrivningen i avsnittet [Krav](#prerequisites))

**Beteende för flera ID:n:** Om en profil innehåller flera identiteter som stöds aktiveras varje identitet separat för [!DNL The Trade Desk]. Detta ger maximal räckvidd och flexibilitet vid målgruppsaktivering.

### Exempel på aktivering

* **Mobile ID-profiler:** Profiler med GAID och/eller IDFA aktiveras med deras respektive reklam-ID. Om en profil innehåller både GAID och IDFA aktiveras varje ID separat.
* **Cookie-baserad profil:** En profil med ECID och motsvarande [!DNL Trade Desk ID]-mappning aktiveras med Trade Desk ID för cookie-baserad målning.
* **Endast ECID-profil:** En profil med endast ECID och ingen [!DNL Trade Desk ID]-mappning exporteras **inte**. ECID räcker inte till för aktivering.

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL The Trade Desk]-konto om du vill verifiera om data har exporterats till målet [!DNL The Trade Desk]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
