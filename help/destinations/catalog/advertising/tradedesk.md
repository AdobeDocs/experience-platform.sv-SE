---
keywords: Reklam. skrivbordet, reklamavdelning
title: The Trade Desk connection
description: Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer för olika annonser, videoklipp och mobila inventeringskällor.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# [!DNL The Trade Desk] anslutning

## Översikt {#overview}

[!DNL The Trade Desk] mål hjälper dig att skicka profildata till [!DNL The Trade Desk].

[!DNL The Trade Desk] är en självbetjäningsplattform för annonsköpare som vill genomföra återannonsering och målgruppsanpassade digitala kampanjer för alla annonser, videoklipp och mobila inventeringskällor.

Skicka profildata till [!DNL Trade Desk]måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Trade Desk IDs] eller enhets-ID:n för att skapa återannonsering eller målgruppsanpassade digitala kampanjer.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| The Trade Desk ID | Advertiser ID i Trade Desk-plattformen |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) till målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL The Trade Desk] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Adobe Audience Manager eller andra program), kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL The Trade Desk] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Fråga [!DNL Trade Desk] representerar vilken regional server du bör använda. Det här är de tillgängliga regionala servrarna du kan välja mellan:
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

I [Segmentschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa dina segment till deras motsvarande ID eller egna namn på målplattformen.

När du mappar segment rekommenderar vi att du använder namnet på plattformssegmentet eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt plattformskonto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

Om du använder flera enhetsmappningar (cookie-ID:n) [!DNL IDFA], [!DNL GAID]) måste du använda samma mappningsvärde för alla tre mappningarna. [!DNL The Trade Desk] sammanfogar alla till ett enda segment med en uppdelning på enhetsnivå.

![Segmentmappnings-ID](../../assets/common/segment-mapping-id.png)

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL The Trade Desk] mål, kontrollera [!DNL Trade Desk] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
