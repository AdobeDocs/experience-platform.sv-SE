---
keywords: mobiler, bromsa, meddelanden,
title: Braze connection
description: Braze är en heltäckande plattform för kundengagemang som driver relevanta och minnesvärda upplevelser mellan kunder och de varumärken de älskar.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# [!DNL Braze] anslutning

## Översikt {#overview}

The [!DNL Braze] mål hjälper dig att skicka profildata till [!DNL Braze].

[!DNL Braze] är en heltäckande plattform för kundengagemang som driver relevanta och minnesvärda upplevelser mellan kunder och varumärken de älskar.

Skicka profildata till [!DNL Braze]måste du först ansluta till målet.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Braze] mål:

* [!DNL Adobe Experience Platform] segment exporteras till [!DNL Braze] under `AdobeExperiencePlatformSegments` -attribut.

>[!NOTE]
>
>Tänk på att skicka ytterligare anpassade attribut till [!DNL Braze] kan orsaka ökning av dina [!DNL Braze] datapunktskonsumtion. Kontakta [!DNL Braze] kontohanteraren innan ytterligare anpassade attribut skickas.

## Användningsfall {#use-cases}

Som marknadsförare vill jag rikta in mig på användare i en mobil engagemangsdestination med inbyggda segment [!DNL Adobe Experience Platform]. Dessutom vill jag leverera personaliserade upplevelser till dem utifrån deras attribut [!DNL Adobe Experience Platform] profiler så snart segment och profiler uppdateras i [!DNL Adobe Experience Platform].

## Identiteter som stöds {#supported-identities}

[!DNL Braze] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| external_id | Egen [!DNL Braze] identifierare som stöder mappning av alla identiteter. | Du kan skicka alla [identity](../../../identity-service/namespaces.md) till [!DNL Braze] mål, förutsatt att du mappar det till [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn) och/eller identiteter enligt fältmappningen.[!DNL Adobe Experience Platform] segment exporteras till [!DNL Braze] under `AdobeExperiencePlatformSegments` -attribut. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Braze account token]**: Det här är din [!DNL Braze] [!DNL API] nyckel. Detaljerade instruktioner om hur du får [!DNL API] tangent här: [REST API Key Overview](https://www.braze.com/docs/api/api_key/).

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: Ange en beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Endpoint Instance]**: fråga [!DNL Braze] representerar vilken slutpunktsinstans du ska använda.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Mappningsöverväganden {#mapping-considerations}

Skicka målgruppsdata korrekt från [!DNL Adobe Experience Platform] till [!DNL Braze] mål måste du gå igenom fältmappningssteget.

Mappningen består av att skapa en länk mellan [!DNL Experience Data Model] (XDM) schemafält i [!DNL Platform] och deras motsvarande motsvarigheter från måldestinationen.

Koppla XDM-fälten till [!DNL Braze] målfält, följ dessa steg:

I [!UICONTROL Mapping] steg, klicka **[!UICONTROL Add new mapping]**.

![Lägg till mappning för Braze-mål](../../assets/catalog/mobile-engagement/braze/mapping.png)

I [!UICONTROL Source Field] klickar du på pilknappen bredvid det tomma fältet.

![Mappning av Braze-målkälla](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

I [!UICONTROL Select source field] kan du välja mellan två kategorier med XDM-fält:
* [!UICONTROL Select attributes]: använd det här alternativet för att mappa ett specifikt fält från XDM-schemat till en [!DNL Braze] -attribut.

![Källattribut för Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Använd det här alternativet för att mappa en [!DNL Platform] identity namespace to a [!DNL Braze] namnutrymme.

![Namnområde för Braze Destination Source](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Välj källfält och klicka sedan på **[!UICONTROL Select]**.

I [!UICONTROL Target Field] klickar du på mappningsikonen till höger om fältet.

![Målmappning för Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

I [!UICONTROL Select target field] kan du välja mellan två kategorier av målfält:
* [!UICONTROL Select identity namespace]: Använd det här alternativet för att mappa [!DNL Platform] ID-namnutrymmen till [!DNL Braze] ID-namnutrymmen.
* [!UICONTROL Select custom attributes]: Använd det här alternativet om du vill mappa XDM-attribut till anpassade [!DNL Braze] attribut som du har definierat i [!DNL Braze] konto. <br> Du kan också använda det här alternativet om du vill byta namn på befintliga XDM-attribut till [!DNL Braze]. Du kan till exempel mappa en `lastName` XDM-attribut till en anpassad `Last_Name` attribute in [!DNL Braze], skapar `Last_Name` attribute in [!DNL Braze], om den inte redan finns, och mappa `lastName` XDM-attribut till den.

![Mappningsfält för mål för Braze](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Välj målfält och klicka sedan på **[!UICONTROL Select]**.

Nu bör du se fältmappningen i listan.

![Mappning av Braze-mål har slutförts](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Upprepa föregående steg om du vill lägga till fler mappningar.

## Mappningsexempel {#mapping-example}

Säg ditt XDM-profilschema och ditt [!DNL Braze] -instansen innehåller följande attribut och identiteter:

|  | XDM-profilschema | [!DNL Braze] Instans |
|---|---|---|
| Attribut | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>Telefonnummer</code></li></ul> |
| Identiteter | <ul><li>E-post</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID för annonsörer (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Den korrekta mappningen skulle se ut så här:

![Exempel på Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL Braze] mål, kontrollera [!DNL Braze] konto. [!DNL Adobe Experience Platform] segment exporteras till [!DNL Braze] under `AdobeExperiencePlatformSegments` -attribut.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](../../../data-governance/home.md).
