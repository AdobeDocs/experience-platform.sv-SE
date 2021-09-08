---
keywords: mobiler, bromsa, meddelanden,
title: Braze connection
description: Braze är en heltäckande plattform för kundengagemang som driver relevanta och minnesvärda upplevelser mellan kunder och de varumärken de älskar.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# [!DNL Braze] anslutning

## Översikt {#overview}

Med [!DNL Braze]-målet kan du skicka profildata till [!DNL Braze].

[!DNL Braze] är en heltäckande plattform för kundengagemang som driver relevanta och minnesvärda upplevelser mellan kunder och varumärken de älskar.

Om du vill skicka profildata till [!DNL Braze] måste du först ansluta till målet.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Braze]-målet:

* [!DNL Adobe Experience Platform] segment exporteras till  [!DNL Braze] under  `AdobeExperiencePlatformSegments` attributet.

>[!NOTE]
>
>Tänk på att om du skickar ytterligare anpassade attribut till [!DNL Braze] kan det leda till ökad datapunktsförbrukning för [!DNL Braze]. Kontakta din kontohanterare för [!DNL Braze] innan du skickar ytterligare anpassade attribut.

## Användningsfall {#use-cases}

Som marknadsförare vill jag rikta in mig på användare i ett mål för mobilengagemang, med segment inbyggda i [!DNL Adobe Experience Platform]. Dessutom vill jag leverera personaliserade upplevelser till dem, baserat på attribut från deras [!DNL Adobe Experience Platform]-profiler, så snart segment och profiler uppdateras i [!DNL Adobe Experience Platform].

## Identiteter som stöds {#supported-identities}

[!DNL Braze] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| external_id | Anpassad [!DNL Braze]-identifierare som stöder mappning av alla identiteter. | Du kan skicka alla [identiteter](../../../identity-service/namespaces.md) till [!DNL Braze]-målet, förutsatt att du mappar den till [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Exporttyp {#export-type}

**[!DNL Profile-based]** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn) och/eller identiteter enligt fältmappningen.
[!DNL Adobe Experience Platform] segment exporteras till  [!DNL Braze] under  `AdobeExperiencePlatformSegments` attributet.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Braze account token]**: Det här är din  [!DNL Braze] [!DNL API] nyckel. Här finns detaljerade anvisningar om hur du får tag i din [!DNL API]-nyckel: [REST API Key Overview](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Name]**: Ange ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: Ange en beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Endpoint Instance]**: fråga din  [!DNL Braze] representant vilken slutpunktsinstans du ska använda.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

## Mappningsöverväganden {#mapping-considerations}

För att kunna skicka målgruppsdata från [!DNL Adobe Experience Platform] till [!DNL Braze]-målet måste du gå igenom fältmappningssteget.

Mappningen består av att skapa en länk mellan [!DNL Experience Data Model]-schemafälten (XDM) i ditt [!DNL Platform]-konto och deras motsvarande motsvarigheter från målmålet.

Följ de här stegen för att mappa dina XDM-fält till målfälten för [!DNL Braze]:

Klicka på **[!UICONTROL Add new mapping]** i steget [!UICONTROL Mapping].

![Lägg till mappning för Braze-mål](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klicka på pilknappen bredvid det tomma fältet i [!UICONTROL Source Field]-avsnittet.

![Mappning av Braze-målkälla](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

I fönstret [!UICONTROL Select source field] kan du välja mellan två kategorier med XDM-fält:
* [!UICONTROL Select attributes]: Använd det här alternativet om du vill mappa ett specifikt fält från XDM-schemat till ett  [!DNL Braze] attribut.

![Källattribut för Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Använd det här alternativet om du vill mappa ett  [!DNL Platform] identitetsnamnutrymme till ett  [!DNL Braze] namnutrymme.

![Namnområde för Braze Destination Source](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Välj källfält och klicka sedan på **[!UICONTROL Select]**.

Klicka på mappningsikonen till höger om fältet i [!UICONTROL Target Field]-avsnittet.

![Målmappning för Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

I fönstret [!UICONTROL Select target field] kan du välja mellan två kategorier av målfält:
* [!UICONTROL Select identity namespace]: Använd det här alternativet om du vill mappa  [!DNL Platform] identitetsnamnutrymmen till  [!DNL Braze] identitetsnamnutrymmen.
* [!UICONTROL Select custom attributes]: Använd det här alternativet om du vill mappa XDM-attribut till anpassade  [!DNL Braze] attribut som du har definierat i ditt  [!DNL Braze] konto. <br> Du kan också använda det här alternativet för att byta namn på befintliga XDM-attribut till  [!DNL Braze]. Om du till exempel mappar ett `lastName` XDM-attribut till ett anpassat `Last_Name`-attribut i [!DNL Braze], skapas attributet `Last_Name` i [!DNL Braze], om det inte redan finns, och mappas XDM-attributet till det.`lastName`

![Mappningsfält för mål för Braze](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Välj målfält och klicka sedan på **[!UICONTROL Select]**.

Nu bör du se fältmappningen i listan.

![Mappning av Braze-mål har slutförts](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Upprepa föregående steg om du vill lägga till fler mappningar.

## Mappningsexempel {#mapping-example}

Säg att ditt XDM-profilschema och din [!DNL Braze]-instans innehåller följande attribut och identiteter:

|  | XDM-profilschema | [!DNL Braze] Instans |
|---|---|---|
| Attribut | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>Telefonnummer</code></li></ul> |
| Identiteter | <ul><li>E-post</code></li><li>Google Ad ID (GAID)</code></li><li>Apple-ID för annonsörer (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Den korrekta mappningen skulle se ut så här:

![Exempel på Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Braze]-konto för att kontrollera om data har exporterats till [!DNL Braze]-målet. [!DNL Adobe Experience Platform] segment exporteras till  [!DNL Braze] under  `AdobeExperiencePlatformSegments` attributet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] verkställer datastyrning finns i [Datastyrningsöversikt](../../../data-governance/home.md).
