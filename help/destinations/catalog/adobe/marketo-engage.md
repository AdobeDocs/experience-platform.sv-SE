---
title: Marketo Engage destination
description: Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Marketo Engage {#beta-marketo-engage-destination}

## Destinationsändringslogg {#changelog}

>[!IMPORTANT]
>
>Med den nya [förbättrad Marketo V2-målanslutning](/help/release-notes/2022/july-2022.md#destinations)visas nu två Marketo-kort i målkatalogen.
>* Om du redan aktiverar data för **[!UICONTROL Marketo V1]** mål: Skapa nya dataflöden för **[!UICONTROL Marketo V2]** mål och ta bort befintliga dataflöden till **[!UICONTROL Marketo V1]** destination senast i februari 2023. Från och med den dagen **[!UICONTROL Marketo V1]** destinationskortet kommer att tas bort.
>* Om du ännu inte har skapat några dataflöden till **[!UICONTROL Marketo V1]** mål, använd den nya **[!UICONTROL Marketo V2]** för att ansluta till och exportera data till Marketo.


![Bild av de två Marketo-målkorten i en sida vid sida-vy.](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

Förbättringar av Marketo V2-målet omfattar:

* I **[!UICONTROL Schedule segment]** i Marketo V1 behövde du lägga till en **Mappnings-ID** för att exportera data till Marketo. Detta manuella steg behövs inte längre i Marketo V2.
* I **[!UICONTROL Mapping]** i Marketo V1 kunde du mappa XDM-fält till endast tre målfält i Marketo: `firstName`, `lastName`och `companyName`. Med Marketo V2 kan du mappa XDM-fält till många fler fält i Marketo. Mer information finns i [attribut som stöds](#supported-attributes) vidare nedan.

## Översikt {#overview}

[!DNL Marketo Engage] är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.

På så sätt kan marknadsförarna skicka segment som skapats i Adobe Experience Platform till Marketo där de visas som statiska listor.

## Identiteter och attribut som stöds {#supported-identities-attributes}

>[!NOTE]
>
>I [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) för aktiveringsmålarbetsflödet är *obligatoriskt* kartlägga identiteter och *valfri* för att mappa attribut. Att mappa e-post och/eller ECID från fliken Identity Namespace är det viktigaste att göra för att se till att personen matchas i Marketo. Mappning av e-post ger högsta matchningsfrekvens.

### Identiteter som stöds {#supported-identities}

| Målidentitet | Beskrivning |
|---|---|
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Se följande dokument på [ECID](/help/identity-service/ecid.md) för mer information. |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |

{style=&quot;table-layout:auto&quot;}

### Attribut som stöds {#supported-attributes}

Du kan mappa attribut från Experience Platform till alla attribut som din organisation har åtkomst till i Marketo. I Marketo kan du använda [Beskriv API-begäran](https://developers.marketo.com/rest-api/lead-database/leads/#describe) för att hämta de attributfält som din organisation har åtkomst till.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (e-post, ECID) som används i [!DNL Marketo Engage] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Ställ in mål och aktivera segment {#set-up}

>[!IMPORTANT]
> 
>* Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions).
>* Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.


Detaljerade instruktioner om hur du ställer in målet och aktiverar segment finns i [Överför ett Adobe Experience Platform-segment till en Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) i Marketo-dokumentationen.

I videon nedan visas också stegen för att konfigurera ett Marketo-mål och aktivera segment.

>[!IMPORTANT]
>
>Videon återspeglar inte helt aktuell funktion. Den mest aktuella informationen finns i guiden ovan. Följande delar av videon är inaktuella:
> 
>* Målkortet som du ska använda i användargränssnittet för Experience Platform är **[!UICONTROL Marketo V2]**.
>* Videon visar inte det nya **[!UICONTROL Person creation]** väljarfält i arbetsflödet för anslutning till mål.
>* De två begränsningar som anges i videon gäller inte längre. Du kan nu mappa många andra profilattributfält utöver segmentmedlemskapsinformationen som stöddes när videon spelades in. Du kan också exportera segmentmedlemmar till Marketo som ännu inte finns i dina statiska Marketo-listor, och dessa läggs till i listorna.
>* I **[!UICONTROL Schedule segment step]** i Marketo V1 behövde du lägga till en **[!UICONTROL Mapping ID]** för att exportera data till Marketo. Detta manuella steg behövs inte längre i Marketo V2.


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
