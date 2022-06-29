---
keywords: 'Reklam. Vedning. '
title: Microsoft Bing-anslutning
description: Med anslutningsmålet Microsoft Bing kan ni genomföra återannonsering och riktade digitala kampanjer för målgrupper i hela Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: cffd689363e71f27a554df31beaf763f9bad37f4
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# [!DNL Microsoft Bing] anslutning {#bing-destination}

## Översikt {#overview}

The [!DNL Microsoft Bing] mål hjälper dig att skicka profildata till [!DNL Microsoft Display Advertising].

Skicka profildata till [!DNL Microsoft Bing]måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Microsoft Advertising IDs] målgruppsanpassning via webbannonsering [!DNL Microsoft Advertising] kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Bing] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| MAID | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

**[!DNL Segment Export]** - du exporterar alla medlemmar i ett segment (publik) till [!DNL Microsoft Bing] mål.

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) till [!DNL Microsoft Bing] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Adobe Audience Manager eller andra program), kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL Microsoft Bing] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: det här är din [!DNL Bing Ads CID], i heltalsformat.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Bing Ads CID].

## Aktivera segment till den här destinationen {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Mappnings-ID"
>abstract="Ange det numeriska Bing-segment-ID som du vill mappa det markerade segmentet till. Om [!UICONTROL Mapping ID] motsvarar inte ett segment-ID i Bing-målet. Du kommer inte att se förväntade målgruppsdata i ditt Bing-konto."

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

I [Segmentschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa dina segment till deras motsvarande numeriska segment-ID i [!DNL Bing] mål. Fyll i det numeriska segmentets ID från [!DNL Bing] i [!UICONTROL Mapping ID] fält.

![Gränssnittsbild som visar segmentmappningsskärmen med ett exempel på Bing Mapping ID](../../assets/catalog/advertising/bing/mapping-id.png)

Om [!UICONTROL Mapping ID] motsvarar inte ett segment-ID i Bing-målet. Du kommer inte att se förväntade målgruppsdata i ditt Bing-konto.

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL Microsoft Bing] mål, kontrollera [!DNL Microsoft Bing Ads] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
