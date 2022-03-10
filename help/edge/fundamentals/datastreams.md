---
title: Konfigurera ditt datastream för Experience Platform Web SDK
description: 'Lär dig hur du konfigurerar datastreams. '
keywords: konfiguration;datastreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 0d23576097b113fa3b24857467658bdf745be427
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 0%

---

# Konfigurera ett datastream

En datastream representerar konfigurationen på serversidan när Adobe Experience Platform Web och Mobile SDK implementeras. Med [konfigurera, kommando](configuring-the-sdk.md) i SDK styr saker som måste hanteras på klienten (till exempel `edgeDomain`) hanterar datastreams alla andra konfigurationer för SDK. När en begäran skickas till Adobe Experience Platform Edge Network `edgeConfigId` används för att referera till datastream. På så sätt kan du uppdatera konfigurationen på serversidan utan att behöva göra kodändringar på webbplatsen.

Det här dokumentet innehåller stegen för hur du konfigurerar ett datastam i användargränssnittet för datainsamling.

>[!NOTE]
>
>Din organisation måste etableras för den här funktionen för att kunna komma åt den i användargränssnittet. Om du inte har tillgång till tjänsten kontaktar du din Customer Success Manager (CSM) för att komma igång med tillåtelselista.

## Öppna [!UICONTROL Datastreams] arbetsyta

Du kan skapa och hantera datastammar i användargränssnittet för datainsamling genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen.

![Fliken Datastreams i användargränssnittet för datainsamling](../images/datastreams/datastreams-tab.png)

>[!NOTE]
>
>Medan du kan komma åt [!UICONTROL Datastreams] oavsett om du använder plattformens tagghanteringsfunktioner eller inte måste du ha utvecklarbehörighet för att kunna hantera dataströmmar själva. Se [användarbehörigheter](../../tags/ui/administration/user-permissions.md) artikel i taggdokumentationen om du vill ha mer information.

The [!UICONTROL Datastreams] På -fliken visas en lista med befintliga dataströmmar, inklusive deras egna namn, ID och senaste ändringsdatum. Välj namnet på en datastream som [visa information och konfigurera tjänster](#view-details).

Välj ikonen &quot;mer&quot; (**...**) för en viss datastream för att visa fler alternativ. Välj **[!UICONTROL Edit]** för att uppdatera [grundläggande konfiguration](#configure) för datastream, eller välj **[!UICONTROL Delete]** för att ta bort datastream.

![Alternativ för redigering eller borttagning och befintlig datastream](../images/datastreams/edit-datastream.png)

## Skapa ett nytt datastream {#create}

Om du vill skapa ett datastream börjar du med att välja **[!UICONTROL New Datastream]**.

![Välj nytt datastream](../images/datastreams/new-datastream-button.png)

### [!UICONTROL Configure] {#configure}

Arbetsflödet för att skapa en datastam visas med början i konfigurationssteget. Härifrån måste du ange ett namn och en valfri beskrivning för datastream.

Om du konfigurerar det här dataflödet för användning i Experience Platform och använder Platform Web SDK måste du även välja en [händelsebaserat XDM-schema (Experience Data Model)](../../xdm/classes/experienceevent.md) för att representera de data du planerar att använda vid inhämtning.

![Grundkonfiguration för ett datastream](../images/datastreams/configure.png)

Resten av det här avsnittet fokuserar på stegen för att mappa data till ett valt plattformshändelseschema. Om du använder Mobile SDK eller på annat sätt inte konfigurerar ditt datastream för Platform väljer du **[!UICONTROL Save]** innan du går vidare till nästa avsnitt på [lägga till tjänster i datastream](#add-services).

### Dataförberedelse för datainsamling {#data-prep}

>[!IMPORTANT]
>
>Data Prep för datainsamling stöds för närvarande inte för implementeringar av Mobile SDK.

Data Prep är en Experience Platform-tjänst som gör att du kan mappa, omvandla och validera data till och från Experience Data Model (XDM). När du konfigurerar en plattformsaktiverad datastream kan du använda dataprep-funktioner för att mappa dina källdata till XDM när du skickar dem till Platform Edge Network.

Underavsnitten nedan beskriver de grundläggande stegen för att mappa data i användargränssnittet för datainsamling. Mer utförlig vägledning om alla funktioner för dataförberedelser, inklusive omformningsfunktioner för beräknade fält, finns i följande dokumentation:

* [Översikt över datapreflight](../../data-prep/home.md)
* [Funktioner för datapersonmappning](../../data-prep/functions.md)
* [Hantera dataformat med Data Prep](../../data-prep/data-handling.md)

#### [!UICONTROL Select data]

Välj **[!UICONTROL Save and Add Mapping]** när du har slutfört [grundläggande konfigurationssteg](#configure)och **[!UICONTROL Select data]** visas. Härifrån måste du ange ett exempel på ett JSON-objekt som representerar strukturen för de data som du planerar att skicka till Platform. Du kan välja att överföra objektet som en fil eller klistra in raw-objektet i den angivna textrutan i stället.

>[!IMPORTANT]
>
>JSON-objektet måste ha en enda rotnod `data` för att validera.

Om JSON är giltig visas ett förhandsgranskningsschema i den högra panelen. Välj **[!UICONTROL Next]** för att fortsätta.

![JSON-exempel på förväntade inkommande data](../images/datastreams/select-data.png)

#### [!UICONTROL Mapping]

The **[!UICONTROL Mapping]** visas så att du kan mappa fälten i källdata till målhändelseschemats fält i Platform. För att komma igång väljer du **[!UICONTROL Add new mapping]** för att skapa en ny mappningsrad.

![Lägga till en ny mappning](../images/datastreams/add-new-mapping.png)

Välj källikon (![Källikon](../images/datastreams/source-icon.png)) och i den dialogruta som visas väljer du det källfält som du vill mappa på den angivna arbetsytan. När du har valt ett fält använder du **[!UICONTROL Select]** för att fortsätta

![Markera fältet som ska mappas i källschemat](../images/datastreams/source-mapping.png)

Välj sedan schemaikonen (![Schemaikon](../images/datastreams/schema-icon.png)) för att öppna en liknande dialogruta för målhändelseschemat. Välj det fält som du vill mappa data till innan du bekräftar med **[!UICONTROL Select]**.

![Markera fältet som ska mappas i målschemat](../images/datastreams/target-mapping.png)

Mappningssidan visas igen med den ifyllda fältmappningen. The **[!UICONTROL Mapping progress]** avsnittsuppdateringar för att återspegla det totala antalet fält som har mappats.

![Fältet har mappats med förloppet speglat](../images/datastreams/field-mapped.png)

Följ stegen ovan för att mappa resten av fälten till målschemat. Även om du inte behöver mappa alla tillgängliga källfält, måste alla fält i målschemat som har angetts som obligatoriska mappas för att det här steget ska kunna slutföras. The **[!UICONTROL Required fields]** anger hur många obligatoriska fält som ännu inte har mappats i den aktuella konfigurationen.

När antalet obligatoriska fält har nått noll och du är nöjd med mappningen väljer du **[!UICONTROL Save]** för att slutföra ändringarna.

![Mappningen är klar](../images/datastreams/mapping-complete.png)

## Visa information om dataström {#view-details}

När du har konfigurerat en ny datastam eller valt en befintlig som ska visas, visas informationssidan för den datastream. Här finns mer information om datastream, inklusive dess ID.

![Informationssida för ett datastream som skapats](../images/datastreams/view-details.png)

På informationsskärmen kan du [lägg till tjänster](#add-services) för att aktivera funktioner från de Adobe Experience Cloud-produkter du har tillgång till.

## Lägga till tjänster i ett datastream {#add-services}

På informationssidan för ett datastream väljer du **[!UICONTROL Add Service]** för att börja lägga till tillgängliga tjänster för den aktuella datastream.

![Välj Lägg till tjänst för att fortsätta](../images/datastreams/add-service.png)

På nästa skärm använder du listrutemenyn för att välja en tjänst som ska konfigureras för det här dataflödet. Endast de tjänster som du har åtkomst till visas i den här listan.

![Välj en tjänst i listan](../images/datastreams/service-selection.png)

Välj önskad tjänst, fyll i de konfigurationsalternativ som visas och välj sedan **[!UICONTROL Save]** för att lägga till tjänsten i datastream. Alla tillagda tjänster visas i informationsvyn för datastream.

![Tjänster som lagts till i ett datastream](../images/datastreams/services-added.png)

Underavsnitten nedan beskriver konfigurationsalternativen för varje tjänst.

>[!NOTE]
>
>Varje tjänstkonfiguration innehåller en **[!UICONTROL Enabled]** som aktiveras automatiskt när tjänsten väljs. Om du vill inaktivera den valda tjänsten för den här datastreamen väljer du **[!UICONTROL Enabled]** växla igen.

### Adobe Analytics-inställningar

Den här tjänsten kontrollerar om och hur data skickas till Adobe Analytics. Mer information finns i guiden på [skicka data till Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../images/datastreams/analytics-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Report Suite ID] | **(Obligatoriskt)** ID:t för analysrapportsviten som du vill skicka data till. Detta ID finns i användargränssnittet i Adobe Analytics under [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Om flera rapportsviter anges kopieras data till varje rapportserie. |

### Adobe Audience Manager-inställningar

Den här tjänsten kontrollerar om och hur data skickas till Adobe Audience Manager. Allt som behövs för att skicka data till Audience Manager är att aktivera det här avsnittet. De andra inställningarna är valfria men rekommenderas.

![Inställningsblock för hantering av målgruppshantering i Adobe](../images/datastreams/audience-manager-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Cookie Destinations Enabled] | Gör att SDK kan dela segmentinformation via [cookie-destinationer](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) från [!DNL Audience Manager]. |
| [!UICONTROL URL Destinations Enabled] | Gör att SDK kan dela segmentinformation via [URL-mål](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) från [!DNL Audience Manager]. |

### Adobe Experience Platform-inställningar

>[!IMPORTANT]
>
>När du aktiverar en datastream för plattformen bör du tänka på den plattformssandlåda som du använder, som visas på den översta menyfliken i användargränssnittet för datainsamling.
>
>![Markerad sandlåda](../images/datastreams/platform-sandbox.png)
>
>Sandlådor är virtuella partitioner i Adobe Experience Platform som gör att du kan isolera data och implementeringar från andra i din organisation. När en datastream har skapats kan dess sandlåda inte ändras. Mer information om sandlådornas roll i Experience Platform finns i [dokumentation för sandlådor](../../sandboxes/home.md).

Den här tjänsten kontrollerar om och hur data skickas till Adobe Experience Platform.

![Adobe Experience Platform inställningsblock](../images/datastreams/platform-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Event Dataset] | **(Obligatoriskt)** Välj den plattformsdatauppsättning som kundhändelsedata ska direktuppspelas till. Det här schemat måste använda [Klassen XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profile Dataset] | Välj den plattformsdatauppsättning som kundattributdata ska skickas till. Det här schemat måste använda [Klassen XDM Individuell profil](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Markera den här kryssrutan om du vill aktivera Offer decisioning för en implementering av en Platform Web SDK. Se guiden [använda Offer decisioning med Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) om du vill ha mer information om implementeringen. Mer information om Offer decisioning finns i [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html). |
| [!UICONTROL Edge Segmentation] | Markera den här kryssrutan för att aktivera [kantsegmentering](../../segmentation/ui/edge-segmentation.md) för denna datastream. När SDK skickar data via en datastam som är aktiverad för kantsegmentering, skickas alla uppdaterade segmentmedlemskap för den aktuella profilen tillbaka som svar.<br><br>Det här alternativet kan användas i kombination med [!UICONTROL Personalization Destinations] for [exempel på användning av personalisering på nästa sida](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | Vid användning i kombination med [!UICONTROL Edge Segmentation] kan datastream ansluta till personaliseringsmotorer som Adobe Target. Se måldokumentationen för specifika steg om [konfigurera personaliseringsmål](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target-inställningar

Den här tjänsten kontrollerar om och hur data skickas till Adobe Target.

![Adobe Target inställningsblock](../images/datastreams/target-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Property Token] | [!DNL Target] låter kunderna styra behörigheter genom att använda egenskaper. Mer information om egenskaper finns i handboken [konfigurera företagsbehörigheter](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) i [!DNL Target] dokumentation.<br><br>Egenskapstoken finns i Adobe Target-gränssnittet under [!UICONTROL Setup] > [!UICONTROL Properties]. |
| [!UICONTROL Target Environment ID] | [Miljöer i Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) hjälper er att hantera implementeringen i alla utvecklingsfaser. Den här inställningen anger vilken miljö du tänker använda med den här datastream.<br><br>Det bästa sättet är att ange detta på olika sätt för var och en av dina `dev`, `stage`och `prod` datastream-miljöer för att hålla saker och ting enkla. Om du redan har definierat Adobe Target-miljöer kan du använda dessa. |
| [!UICONTROL Target Third Party ID namespace] | Identitetsnamnrymden för `mbox3rdPartyId` som du vill använda för den här datastream. Se guiden [implementera `mbox3rdPartyId` med Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) för mer information. |

### [!UICONTROL Event Forwarding] inställningar

Den här tjänsten kontrollerar om och hur data skickas till [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md).

![Avsnittet Händelsevidarebefordran i konfigurationsgränssnittet](../images/datastreams/event-forwarding-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Launch Property] | **(Obligatoriskt)** Egenskapen för vidarebefordran av händelser som du vill skicka data till. |
| [!UICONTROL Launch Environment] | **(Obligatoriskt)** Den miljö i den valda egenskapen som du vill skicka data till. |

>[!NOTE]
>
>Du kan välja **[!UICONTROL Manually enter IDs]** om du vill skriva i egenskaps- och miljönamnen i stället för att använda listrutemenyer.

### [!UICONTROL Third Party ID Sync] inställningar

Avsnittet med tredje parts-ID är det enda avsnitt som alltid är aktivt. Det finns två tillgängliga inställningar: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; och &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Synkroniseringsavsnittet för tredjeparts-ID i konfigurationsgränssnittet](../images/datastreams/third-party-id-sync-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Third Party ID Sync Container ID] | ID-synkroniseringar kan grupperas i behållare så att olika ID-synkroniseringar kan köras vid olika tidpunkter. Detta styr vilken behållare för ID-synk som körs för den här datastream. |

## Nästa steg

I den här guiden beskrivs hur du konfigurerar ett datastam i användargränssnittet för datainsamling. Mer information om hur du installerar och konfigurerar Web SDK när du har konfigurerat ett datastream finns i [E2E-guide för datainsamling](../../collection/e2e.md#install).
