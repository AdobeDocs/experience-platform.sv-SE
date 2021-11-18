---
title: Marketo Engage destination
description: Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 05b97e8bdeb4ffb81a4a671d282d0d8ebc7e870a
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Marketo Engage {#beta-marketo-engage-destination}

## Översikt {#overview}

Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.

På så sätt kan marknadsförarna skicka segment som skapats i Adobe Experience Platform till Marketo där de visas som statiska listor.

## Identiteter som stöds {#supported-identities}

| Målidentitet | Beskrivning |
|---|---|
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Se följande dokument på [ECID](/help/identity-service/ecid.md) för mer information. |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |

>[!NOTE]
>
>I [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) för aktiveringsmålarbetsflödet är *obligatoriskt* kartlägga identiteter och *valfri* för att mappa attribut. Att mappa e-post och/eller ECID från fliken Identity Namespace är det viktigaste att göra för att se till att personen matchas i Marketo. Mappning av e-post ger högsta matchningsfrekvens.

## Exporttyp {#export-type}

Segmentexport - du exporterar alla medlemmar i ett segment (publik) med de identifierare (e-post, ECID) som används i Marketo Engage-målet.

## Ställ in mål och aktivera segment {#set-up}

Detaljerade instruktioner om hur du ställer in målet och aktiverar segment finns i [Överför ett Adobe Experience Platform-segment till en Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) i Marketo-dokumentationen.

I videon nedan visas också stegen för att konfigurera ett Marketo-mål och aktivera segment.

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den mest aktuella informationen finns i guiden ovan.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [datastyrningsöversikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
