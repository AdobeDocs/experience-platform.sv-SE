---
keywords: 'Reklam. Vedning. '
title: Microsoft Bing-anslutning
description: Med anslutningsmålet för Microsoft Bing kan ni genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 1%

---

# [!DNL Microsoft Bing] anslutning {#bing-destination}

## Översikt {#overview}

Med [!DNL Microsoft Bing]-målet kan du skicka profildata till [!DNL Microsoft Display Advertising].

Om du vill skicka profildata till [!DNL Microsoft Bing] måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Microsoft Advertising IDs] för att rikta in användare via webbannonsering i [!DNL Microsoft Advertising]-kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Bing] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| MAID | Microsoft Advertising ID |

## Exporttyp {#export-type}

**[!DNL Segment Export]** - du exporterar alla medlemmar i ett segment (publik) till  [!DNL Microsoft Bing] målet.

## Förutsättningar {#prerequisites}

Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Microsoft Bing]-integreringar i Audience Manager överförs ID-synkroniseringarna du har konfigurerat till Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: detta är ditt  [!DNL Bing Ads CID]heltalsformat.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Bing Ads CID].

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till mål.

I steget [Segmentschema](../../ui/activate-destinations.md#segment-schedule) måste du manuellt mappa dina segment till deras motsvarande ID eller egna namn i målet.

När du mappar segment rekommenderar vi att du använder segmentnamnet [!DNL Platform] eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt [!DNL Platform]-konto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Microsoft Bing Ads]-konto för att kontrollera om data har exporterats till [!DNL Microsoft Bing]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
