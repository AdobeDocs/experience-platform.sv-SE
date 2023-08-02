---
keywords: Reklam.
title: Microsoft Bing-anslutning
description: Med anslutningsmålet Microsoft Bing kan ni genomföra återannonsering och riktade digitala kampanjer för målgrupper i hela Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# [!DNL Microsoft Bing] anslutning {#bing-destination}

## Översikt {#overview}

The [!DNL Microsoft Bing] mål hjälper dig att skicka profildata till [!DNL Microsoft Display Advertising].

Skicka profildata till [!DNL Microsoft Bing]måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda målgrupper som är inbyggda i [!DNL Microsoft Advertising IDs] målgruppsanpassning via webbannonsering [!DNL Microsoft Advertising] kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Bing] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| MAID | Microsoft Advertising ID |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Detta mål stöder aktivering av alla målgrupper som genererats via Experience Platform [Segmenteringstjänst](../../../segmentation/home.md).

*Dessutom* stöder denna destination även aktivering av målgrupper som beskrivs i tabellen nedan.

| Målgruppstyp | Beskrivning |
---------|----------|
| Anpassade överföringar | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

**[!DNL Audience Export]** - du exporterar alla medlemmar i en publik till [!DNL Microsoft Bing] mål.

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en publik till [!DNL Microsoft Bing] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Adobe Audience Manager eller andra program), kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL Microsoft Bing] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: det här är [!DNL Bing Ads CID], i heltalsformat.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

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
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I [Målgruppsschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa målgruppsnamnet i [!UICONTROL Mapping ID] fält. Detta garanterar att målgruppsmetadata skickas till [!DNL Bing].

![Användargränssnittsbild som visar målgruppens tidsplaneringsskärm med ett exempel på hur målgruppsnamnet mappas till Bing Mapping ID.](../../assets/catalog/advertising/bing/mapping-id.png)

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL Microsoft Bing] mål, kontrollera [!DNL Microsoft Bing Ads] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
