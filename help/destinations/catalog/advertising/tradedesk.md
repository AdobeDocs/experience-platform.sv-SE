---
keywords: Reklam. skrivbordet, reklamavdelning
title: The Trade Desk connection
description: Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer för olika annonser, videoklipp och mobila inventeringskällor.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# [!DNL The Trade Desk] anslutning

## Översikt {#overview}

[!DNL The Trade Desk] mål hjälper dig att skicka profildata till  [!DNL The Trade Desk].

[!DNL The Trade Desk] är en självbetjäningsplattform för annonsköpare som vill genomföra återannonsering och målgruppsanpassade digitala kampanjer för alla annonser, videoklipp och mobila inventeringskällor.

Om du vill skicka profildata till [!DNL Trade Desk] måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Trade Desk IDs] eller enhets-ID:n för att skapa återmarknadsföring eller målgruppsanpassade digitala kampanjer.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| The Trade Desk ID | Advertiser ID i Trade Desk-plattformen |

## Exporttyp {#export-type}

**[!DNL Segment export]** - du exporterar alla medlemmar i ett segment (publik) till målet.

## Förutsättningar {#prerequisites}

Om du vill skapa ditt första mål med [!DNL The Trade Desk] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL The Trade Desk]-integreringar i Audience Manager överförs ID-synkroniseringarna du har konfigurerat till Platform.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Fråga din  [!DNL Trade Desk] representant vilken regional server du ska använda. Det här är de tillgängliga regionala servrarna du kan välja mellan:
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

I steget [Segmentschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa dina segment till deras motsvarande ID eller egna namn på målplattformen.

När du mappar segment rekommenderar vi att du använder namnet på plattformssegmentet eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt plattformskonto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

Om du använder flera enhetsmappningar (cookie-ID, [!DNL IDFA], [!DNL GAID]) måste du använda samma mappningsvärde för alla tre mappningarna. [!DNL The Trade Desk] sammanfogar alla till ett enda segment med en uppdelning på enhetsnivå.

![Segmentmappnings-ID](../../assets/common/segment-mapping-id.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Trade Desk]-konto om du vill verifiera om data har exporterats till [!DNL The Trade Desk]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
