---
keywords: Reklam.
title: Microsoft Bing-anslutning
description: Med anslutningsmålet Microsoft Bing kan ni genomföra återannonsering och riktade digitala kampanjer för målgrupper i hela Microsoft Advertising-nätverket, inklusive webbannonsering, sökannonsering och inbyggt webbmaterial.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# [!DNL Microsoft Bing] anslutning {#bing-destination}

## Översikt {#overview}

Använd [!DNL Microsoft Bing] mål för att skicka profildata till hela [!DNL Microsoft Advertising Network], inklusive [!DNL Display Advertising], [!DNL Search]och [!DNL Native].

The [!DNL Microsoft Bing] mål skapar *[!DNL Custom Audiences]* i Microsoft. Dessa finns tillgängliga båda i [!DNL Microsoft Search Network] och [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) enligt listan i [Dokumentation för Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Skicka profildata till [!DNL Microsoft Bing]måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda målgrupper som är inbyggda i [!DNL Microsoft Advertising IDs] rikta sig till användare via displayannonsering eller sökannonsering över [!DNL Microsoft Advertising] kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Bing] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Identitet | Beskrivning |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

**[!DNL Audience Export]** - du exporterar alla medlemmar i en publik till [!DNL Microsoft Bing] mål.

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en publik till [!DNL Microsoft Bing] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID Service (med Adobe Audience Manager eller andra program), kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL Microsoft Bing] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: det här är [!DNL Bing Ads CID], i heltalsformat.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Fyll i målinformation {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: din [!DNL Bing Ads Customer ID] (CID) Ditt CID är ett heltal som finns i URL:en när du loggar in [!DNL Microsoft Advertising].

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Mappnings-ID"
>abstract="Ange det numeriska Bing-målgrupps-ID som du vill mappa det markerade segmentet till. Om det anges [!UICONTROL Mapping ID] motsvarar inte ett målgrupps-ID i Bing-målet. Du kommer inte att se förväntade målgruppsdata i ditt Bing-konto."

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I [Målgruppsschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa målgruppsnamnet i [!UICONTROL Mapping ID] fält. Detta garanterar att målgruppsmetadata skickas till [!DNL Bing].

![Användargränssnittsbild som visar målgruppens tidsplaneringsskärm med ett exempel på hur målgruppsnamnet mappas till Bing Mapping ID.](../../assets/catalog/advertising/bing/mapping-id.png)

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL Microsoft Bing] mål, kontrollera [!DNL Microsoft Bing Ads] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
