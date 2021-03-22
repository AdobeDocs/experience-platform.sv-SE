---
keywords: 'Reklam. Vedning. '
title: Microsoft Bing-anslutning
description: Med anslutningsmålet för Microsoft Bing kan ni genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# [!DNL Microsoft Bing] anslutning  {#bing-destination}

## Översikt {#overview}

Med [!DNL Microsoft Bing]-målet kan du skicka profildata till [!DNL Microsoft Display Advertising].

Om du vill skicka profildata till [!DNL Microsoft Bing] måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Microsoft Advertising IDs] för att rikta in användare via webbannonsering i [!DNL Microsoft Advertising]-kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| MAID | Microsoft Advertising ID |

## Exporttyp {#export-type}

**[!DNL Segment Export]** - du exporterar alla medlemmar i ett segment (publik) till  [!DNL Microsoft Bing] målet.

## Förutsättningar {#prerequisites}

Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Microsoft Bing]-integreringar i Audience Manager överförs ID-synkroniseringarna du har konfigurerat till Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: detta är ditt  [!DNL Bing Ads CID]heltalsformat.

## Anslut till målet {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL Microsoft Bing] och väljer **[!UICONTROL Configure]**.

![Konfigurera Microsoft Bing-mål](../../assets/catalog/advertising/bing/configure.png)

Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

![Aktivera Microsoft Bing-mål](../../assets/catalog/advertising/bing/activate.png)

## Autentiseringssteg {#authentication}

I steget **[!UICONTROL Authentication]** måste du ange information om målanslutningen:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Bing Ads CID].
* **[!UICONTROL Marketing action]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns på sidan [Datastyrning i Adobe Experience Platform](../../../data-governance/policies/overview.md). Mer information om de enskilda Adobe-definierade marknadsföringsåtgärderna finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

![Autentisering av Microsoft Bing-mål](../../assets/catalog/advertising/bing/authentication.png)

Klicka på **[!UICONTROL Create destination]**. Målet har skapats. Du kan klicka på [!UICONTROL Save & Exit] om du vill aktivera segment senare eller klicka på [!UICONTROL Next] om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md#select-attributes).

I steget [Segmentschema](../../ui/activate-destinations.md#segment-schedule) måste du manuellt mappa dina segment till deras motsvarande ID eller egna namn i målet.

När du mappar segment rekommenderar vi att du använder segmentnamnet [!DNL Platform] eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt [!DNL Platform]-konto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

![Segmentmappnings-ID](../../assets/common/segment-mapping-id.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Microsoft Bing Ads]-konto för att kontrollera om data har exporterats till [!DNL Microsoft Bing]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.