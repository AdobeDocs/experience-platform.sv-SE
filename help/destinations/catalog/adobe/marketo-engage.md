---
title: Marketo Engage Destination
description: Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c57a519b5a230dc62699808cf5c020d48cc79083
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---

# Marketo Engage destination {#beta-marketo-engage-destination}

## Destinationsändringslogg {#changelog}

>[!IMPORTANT]
>
>I och med att [den förbättrade Marketo V2-målanslutningen](/help/release-notes/2022/july-2022.md#destinations) har släppts visas nu två Marketo-kort i målkatalogen.
>* Om du redan aktiverar data till målet **[!UICONTROL Marketo V1]**: Skapa nya dataflöden till målet **[!UICONTROL Marketo V2]** och ta bort befintliga dataflöden till målet **[!UICONTROL Marketo V1]** senast i februari 2023. Från och med det datumet tas **[!UICONTROL Marketo V1]**-målkortet bort.
>* Om du ännu inte har skapat några dataflöden till målet **[!UICONTROL Marketo V1]** använder du det nya **[!UICONTROL Marketo V2]**-kortet för att ansluta till och exportera data till Marketo.

![Bild av de två Marketo-målkorten i en sida vid sida-vy.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Förbättringar av Marketo V2-destinationen omfattar:

* I steget **[!UICONTROL Schedule segment]** i aktiveringsarbetsflödet behövde du i Marketo V1 lägga till ett **Mappnings-ID** manuellt för att kunna exportera data till Marketo. Det här manuella steget behövs inte längre i Marketo V2.
* I steget **[!UICONTROL Mapping]** i aktiveringsarbetsflödet kunde du i Marketo V1 mappa XDM-fält till endast tre målfält i Marketo: `firstName`, `lastName` och `companyName`. Med Marketo V2 kan du mappa XDM-fält till många fler fält i Marketo. Mer information finns i avsnittet [Attribut som stöds](#supported-attributes) nedan.

## Översikt {#overview}

[!DNL Marketo Engage] är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.

Målgruppen gör det möjligt för marknadsförare att skicka målgrupper som skapats i Adobe Experience Platform till Marketo där de visas som statiska listor.

## Identiteter och attribut som stöds {#supported-identities-attributes}

>[!NOTE]
>
>I [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i arbetsflödet för aktivering av mål är det *obligatoriskt* att mappa identiteter och *valfritt* att mappa attribut. Att mappa e-post och/eller ECID från fliken Identity Namespace är det viktigaste att göra för att se till att personen matchas i Marketo. Mappning av e-post ger högsta matchningsfrekvens.

### Identiteter som stöds {#supported-identities}

| Målidentitet | Beskrivning |
|---|---|
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |

{style="table-layout:auto"}

### Attribut som stöds {#supported-attributes}

Du kan mappa attribut från Experience Platform till alla attribut som din organisation har tillgång till i Marketo. I Marketo kan du använda [Beskriv API-begäran](https://developers.marketo.com/rest-api/lead-database/leads/#describe) för att hämta de attributfält som din organisation har åtkomst till.

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
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-post, ECID) som används i målet [!DNL Marketo Engage]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Ställ in mål och aktivera målgrupper {#set-up}

>[!IMPORTANT]
> 
>* Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions).
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Mer information om hur du konfigurerar målet och aktiverar målgrupper finns i [Push an Adobe Experience Platform Audience to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) i dokumentationen för Marketo.

I videon nedan visas också stegen för att konfigurera ett Marketo-mål och aktivera målgrupper.

>[!IMPORTANT]
>
>Videon återspeglar inte helt den aktuella funktionen. Den mest aktuella informationen finns i guiden ovan. Följande delar av videon är inaktuella:
> 
>* Målkortet som du bör använda i Experience Platform-gränssnittet är **[!UICONTROL Marketo V2]**.
>* I videon visas inte det nya **[!UICONTROL Person creation]**-väljarfältet i arbetsflödet för anslutning till mål. Om du vill använda det fältet måste du mappa både förnamn och efternamn under steget för attributmappning.
>* De två begränsningar som anges i videon gäller inte längre. Du kan nu mappa många andra profilattributfält utöver den information om målgruppsmedlemskap som stöddes när videon spelades in. Du kan också exportera målgruppsmedlemmar till Marketo som ännu inte finns i dina statiska Marketo-listor, och dessa läggs till i listorna.
>* I **[!UICONTROL Schedule audience step]** av aktiveringsarbetsflödet behövde du i Marketo V1 lägga till en **[!UICONTROL Mapping ID]** manuellt för att kunna exportera data till Marketo. Det här manuella steget behövs inte längre i Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Bildskärmsmål {#monitor-destination}

När du har anslutit till målet och etablerat ett måldataflöde kan du använda [övervakningsfunktionen](/help/dataflows/ui/monitor-destinations.md) i Real-Time CDP för att få omfattande information om de profilposter som är aktiverade för målet i varje dataflödeskörning.

Övervakningsinformationen för anslutningen [!DNL Marketo Engage] innehåller information på målgruppsnivå om aktiverade, uteslutna och misslyckade identiteter i varje dataflöde och dataflöde. [Läs mer](/help/dataflows/ui/monitor-destinations.md#segment-level-view) om funktionaliteten.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [översikten över datastyrning](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

