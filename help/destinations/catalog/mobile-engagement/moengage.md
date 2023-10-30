---
title: Moengage connection
description: Moengage är en plattform för kundengagemang som driver kundcentrerade interaktioner mellan konsumenter och varumärken i realtid.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# [!DNL Moengage] anslutning

## Översikt {#overview}

Använd [!DNL Moengage] mål för att ansluta och mappa dina Adobe-data (användarattribut, segment och händelser) till Motion i realtid. Sedan kan kunderna agera utifrån dessa data och leverera personaliserade, målinriktade upplevelser.

Med Adobe är integreringen mycket enkel och intuitiv. Ta vilken användarprofil som helst i Adobe och mappa den till ett MobilEngage-användarattribut.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *Moengage* team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *`https://help.moengage.com/hc/en-us`.*

## Användningsfall {#use-cases}

En marknadsförare vill inrikta sig på ett användarsegment (inbyggt i Adobe Experience Platform) via [!DNL Moengage] kampanjer. De vill också personalisera kampanjinnehåll baserat på attribut från Adobe Experience Platform-profiler. Med den här integreringen uppdateras användare och attribut i MoEngage så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Innan du skickar dina Adobe Experience Platform-data till [!DNL Moengage]Observera följande krav:

* Om du vill använda MoEngage-målet med Adobe Experience Platform måste användarna först ha tillgång till sina [!DNL Moengage] Konto. Gå till följande sida för att registrera dig eller logga in på ditt MoEngage-konto: https://app.moengage.com


## Identiteter som stöds {#supported-identities}

[!DNL Moengage] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Unik identifierare som unikt identifierar en användarprofil i [!DNL Moengage] system. | Den här identifieraren stöder strängtyp. Antingen user_id eller anonymous_id krävs |
| anonymous_id | En annan identifierare för en okänd användarprofil - det vill säga en profil som inte finns i systemet. | Den här identifieraren stöder strängtyp. Antingen user_id eller anonymous_id krävs |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (user_id, anonymous_id) tillsammans med anpassade attribut som du har definierat som exporterade till [!DNL Moengage]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL USERNAME]**: DATA APP ID för inställningssidan för [!DNL Moengage] kontrollpanel.
* **[!UICONTROL PASSWORD]**: DATA APP KEY från inställningssidan för [!DNL Moengage] kontrollpanel.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Region]**: Ditt program *datacenter*.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Skicka målgruppsdata korrekt från [!DNL Adobe Experience Platform] till [!DNL Moengage] mål måste du gå igenom fältmappningssteget.

Mappningen består av att skapa en länk mellan [!DNL Experience Data Model] (XDM) schemafält i [!DNL Platform] och deras motsvarande motsvarigheter från måldestinationen.

Mappa XDM-fälten korrekt till [!DNL Moengage] målfält, följ dessa steg:

I [!UICONTROL Mapping] steg, välja **[!UICONTROL Checkbox]**.

![Lägg till mappning för Moengage-mål](../../assets/catalog/mobile-engagement/moengage/segments.png)

I [!UICONTROL Mapping] steg, välja **[!UICONTROL Add new mapping]**.

![Lägg till mappning för Moengage-mål](../../assets/catalog/mobile-engagement/moengage/mapping.png)

I [!UICONTROL Source Field] markerar du pilknappen bredvid det tomma fältet.

![Mappning av målkälla för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

I [!UICONTROL Select source field] kan du välja mellan två kategorier med XDM-fält:
* [!UICONTROL Select attributes]: använd det här alternativet för att mappa ett specifikt fält från XDM-schemat till [!DNL Moengage] -attribut.

![Källattribut för mappning av mål för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Välj källfält och välj sedan **[!UICONTROL Select]**.

I [!UICONTROL Target Field] markerar du mappningsikonen till höger om fältet.

![Målmappning för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

I [!UICONTROL Select target field] kan du välja mellan två kategorier av målfält:
* [!UICONTROL Select identity namespace]: Använd det här alternativet för att mappa [!DNL Platform] ID-namnutrymmen till [!DNL Moengage] ID-namnutrymmen.
* [!UICONTROL Select custom attributes]: Använd det här alternativet om du vill mappa XDM-attribut till anpassade [!DNL Moengage] attribut som du har definierat i [!DNL Moengage] konto. <br> Du kan också använda det här alternativet om du vill byta namn på befintliga XDM-attribut till [!DNL Moengage]. Du kan till exempel mappa en `lastName` XDM-attribut till en anpassad `Last_Name` attribute in [!DNL Moengage], skapar `Last_Name` attribute in [!DNL Moengage], om den inte redan finns, och mappa `lastName` XDM-attribut till den.

![Mappningsfält för mål för rörelseinteraktion](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Välj målfält och välj sedan **[!UICONTROL Select]**.

Nu bör du se fältmappningen i listan.

![Mappning av Moengage-mål slutförd](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Upprepa föregående steg om du vill lägga till fler mappningar.

## Exporterade data/Validera dataexport {#exported-data}

Verifiera om data har exporterats till [!DNL Moengage] mål, gå till användarprofilen på [!DNL Moengage] konto. Du ser ett användarattribut som kallas AEP-segment.

![Mappning av Moengage-mål slutförd](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
