---
title: Moengage connection
description: Moengage är en plattform för kundengagemang som driver kundcentrerade interaktioner mellan konsumenter och varumärken i realtid.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# [!DNL Moengage]-anslutning

## Översikt {#overview}

Använd målet [!DNL Moengage] för att ansluta och mappa dina Adobe-data (användarattribut, segment och händelser) till Motion i realtid. Sedan kan kunderna agera utifrån dessa data och leverera personaliserade, målinriktade upplevelser.

Med Adobe är integreringen mycket enkel och intuitiv. Ta vilken Adobe-användarprofil som helst och mappa den till ett MoEngage-användarattribut.

>[!IMPORTANT]
>
>Den här målanslutningen och dokumentationssidan skapas och underhålls av *Moengage*-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *`https://help.moengage.com/hc/en-us`.*

## Användningsfall {#use-cases}

En marknadsförare vill rikta sig till ett användarsegment (inbyggt i Adobe Experience Platform) via [!DNL Moengage] kampanjer. De vill också personalisera kampanjinnehåll baserat på attribut från Adobe Experience Platform-profiler. Med den här integreringen uppdateras användare och attribut i MoEngage så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Innan du kan skicka dina Adobe Experience Platform-data till [!DNL Moengage] bör du tänka på följande krav:

* Om du vill använda MoEngage-målet med Adobe Experience Platform måste användarna först ha tillgång till sitt [!DNL Moengage]-konto. Gå till följande sida för att registrera dig eller logga in på ditt MoEngage-konto: https://app.moengage.com


## Identiteter som stöds {#supported-identities}

[!DNL Moengage] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Unik identifierare som unikt identifierar en användarprofil i systemet [!DNL Moengage]. | Den här identifieraren stöder strängtyp. Antingen user_id eller anonymous_id krävs |
| anonymous_id | En annan identifierare för en okänd användarprofil - det vill säga en profil som inte finns i systemet. | Den här identifieraren stöder strängtyp. Antingen user_id eller anonymous_id krävs |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (user_id, anonymous_id) tillsammans med anpassade attribut som definieras av dig och som har exporterats till [!DNL Moengage]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL USERNAME]**: DATA APP ID för inställningssidan för [!DNL Moengage]-instrumentpanelen.
* **[!UICONTROL PASSWORD]**: DATA APP KEY från inställningssidan på [!DNL Moengage]-instrumentpanelen.

![Moengage Destination Authentication](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Region]**: Ditt program *datacenter*.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Om du vill skicka målgruppsdata korrekt från [!DNL Adobe Experience Platform] till [!DNL Moengage]-målet måste du gå igenom fältmappningssteget.

Mappningen består av att skapa en länk mellan [!DNL Experience Data Model] (XDM)-schemafälten i ditt [!DNL Experience Platform]-konto och motsvarande motsvarigheter från målmålet.

Följ de här stegen för att mappa dina XDM-fält korrekt till målfälten för [!DNL Moengage]:

Välj **[!UICONTROL Checkbox]** i steget [!UICONTROL Mapping].

![Mappning av måltillägg för Moengage](../../assets/catalog/mobile-engagement/moengage/segments.png)

Välj **[!UICONTROL Add new mapping]** i steget [!UICONTROL Mapping].

![Mappning av måltillägg för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping.png)

I avsnittet [!UICONTROL Source Field] markerar du pilknappen bredvid det tomma fältet.

![Moengage Destination Source Mapping](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

I fönstret [!UICONTROL Select source field] kan du välja mellan två kategorier med XDM-fält:
* [!UICONTROL Select attributes]: använd det här alternativet om du vill mappa ett specifikt fält från XDM-schemat till attributet [!DNL Moengage].

![Source-attribut för målmappning för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Välj källfältet och välj sedan **[!UICONTROL Select]**.

I avsnittet [!UICONTROL Target Field] väljer du mappningsikonen till höger om fältet.

![Målmappning för Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

I fönstret [!UICONTROL Select target field] kan du välja mellan två kategorier av målfält:
* [!UICONTROL Select identity namespace]: Använd det här alternativet om du vill mappa [!DNL Experience Platform] identitetsnamnutrymmen till [!DNL Moengage] identitetsnamnutrymmen.
* [!UICONTROL Select custom attributes]: Använd det här alternativet om du vill mappa XDM-attribut till anpassade [!DNL Moengage]-attribut som du har definierat i ditt [!DNL Moengage]-konto. <br> Du kan också använda det här alternativet om du vill byta namn på befintliga XDM-attribut till [!DNL Moengage]. Om du till exempel mappar ett `lastName` XDM-attribut till ett anpassat `Last_Name`-attribut i [!DNL Moengage] skapas `Last_Name`-attributet i [!DNL Moengage], om det inte redan finns, och `lastName` XDM-attributet mappas till det.

![Mappningsfält för målmål för rörelseinteraktion](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Välj målfältet och välj sedan **[!UICONTROL Select]**.

Nu bör du se fältmappningen i listan.

![Målmappning för Moengage slutförd](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Upprepa föregående steg om du vill lägga till fler mappningar.

## Exporterade data/Validera dataexport {#exported-data}

Gå till användarprofilen i ditt [!DNL Moengage]-konto för att kontrollera om data har exporterats till målet [!DNL Moengage]. Här bör du hitta ett användarattribut med namnet `AEPSegments`, som skapas automatiskt och de andra anpassade attributen som har mappats i tidigare steg i Adobe Experience Platform.

`AEPSegments` är ett matristypsattribut i [!DNL Moengage]. Här listas alla Adobe målgruppsnamn som användaren är kopplad till i Experience Platform.


![Målmappning för Moengage slutförd](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
