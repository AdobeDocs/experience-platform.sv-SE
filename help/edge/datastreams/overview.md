---
title: Översikt över dataströmmar
description: Koppla samman er integrering med Experience Platform SDK på klientsidan med Adobe-produkter och tredjepartsmål.
keywords: konfiguration;datastreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destination;url Destinations;Analytics Settings Blockreport suite;Data Prep för datainsamling;Data Prep;Mapper;XDM Mapper;Mapper on Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 3690a32f32c6cfa25120e9af44fe559122e779a0
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 1%

---

# Översikt över datastreams

En datastream representerar konfigurationen på serversidan när Adobe Experience Platform Web och Mobile SDK implementeras. Med [konfigurera, kommando](../fundamentals/configuring-the-sdk.md) i SDK styr saker som måste hanteras på klienten (till exempel `edgeDomain`) hanterar datastreams alla andra konfigurationer för SDK. När en begäran skickas till Adobe Experience Platform Edge Network `edgeConfigId` används för att referera till datastream. På så sätt kan du uppdatera konfigurationen på serversidan utan att behöva göra kodändringar på webbplatsen.

Det här dokumentet innehåller stegen för hur du konfigurerar ett datastam i användargränssnittet för datainsamling.

## Öppna [!UICONTROL Datastreams] arbetsyta

Du kan skapa och hantera datastammar i användargränssnittet för datainsamling genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen.

![Fliken Datastreams i användargränssnittet för datainsamling](../images/datastreams/overview/datastreams-tab.png)

The [!UICONTROL Datastreams] På -fliken visas en lista med befintliga dataströmmar, inklusive deras egna namn, ID och senaste ändringsdatum. Välj namnet på en datastream som [visa information och konfigurera tjänster](#view-details).

Välj ikonen &quot;mer&quot; (**...**) för en viss datastream för att visa fler alternativ. Välj **[!UICONTROL Edit]** för att uppdatera [grundläggande konfiguration](#configure) för datastream, eller välj **[!UICONTROL Delete]** för att ta bort datastream.

![Alternativ för redigering eller borttagning och befintlig datastream](../images/datastreams/overview/edit-datastream.png)

## Skapa ett nytt datastream {#create}

Om du vill skapa ett datastream börjar du med att välja **[!UICONTROL New Datastream]**.

![Välj nytt datastream](../images/datastreams/overview/new-datastream-button.png)

Arbetsflödet för att skapa en datastam visas med början i konfigurationssteget. Härifrån måste du ange ett namn och en valfri beskrivning för datastream.

Om du konfigurerar det här dataflödet för användning i Experience Platform och använder Platform Web SDK måste du även välja en [händelsebaserat XDM-schema (Experience Data Model)](../../xdm/classes/experienceevent.md) för att representera de data du planerar att använda vid inhämtning.

![Grundkonfiguration för ett datastream](../images/datastreams/overview/configure.png)

Välj **[!UICONTROL Advanced Options]** om du vill visa ytterligare kontroller för att konfigurera datastream.

![Avancerade konfigurationsalternativ](../images/datastreams/overview/advanced-options.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Geo Location] | Avgör om GPS-sökningar utförs baserat på användarens IP-adress. Standardinställningen **[!UICONTROL None]** inaktiverar GPS-sökningar, medan **[!UICONTROL City]** -inställningen ger GPS-koordinater två decimaler. |
| [!UICONTROL First Party ID Cookie] | När det här alternativet är aktiverat anger den här inställningen att Edge Network ska referera till en angiven cookie när en [enhets-ID för första part](../identity/first-party-device-ids.md)i stället för att leta upp det här värdet i identitetskartan.<br><br>När du aktiverar den här inställningen måste du ange namnet på den cookie där ID:t ska lagras. |
| [!UICONTROL Third Party ID Sync] | ID-synkroniseringar kan grupperas i behållare så att olika ID-synkroniseringar kan köras vid olika tidpunkter. När den här inställningen är aktiverad kan du ange vilken ID-synkroniseringsbehållare som ska köras för den här datastream-filen. |
| [!UICONTROL Access Type] | Definierar autentiseringstypen som [!DNL Edge Network] accepterar för datastream. <ul><li>**[!UICONTROL Mixed Authentication]**: När det här alternativet är markerat godkänns både autentiserade och oautentiserade begäranden i Edge Network. Välj det här alternativet när du tänker använda Web SDK eller [Mobile SDK](https://aep-sdks.gitbook.io/docs/), tillsammans med [Server-API](../../server-api/overview.md). </li><li>**[!UICONTROL Authenticated Only]**: När det här alternativet är markerat accepterar Edge Network endast autentiserade begäranden. Välj det här alternativet när du bara vill använda Server-API:t och vill förhindra att oautentiserade begäranden behandlas av [!DNL Edge Network]. </li></ul> |

Om du konfigurerar ditt datastream för Experience Platform följer du självstudiekursen på [Dataförberedelse för datainsamling](./data-prep.md) för att mappa dina data till ett plattformshändelseschema innan du återgår till den här guiden. Annars väljer du **[!UICONTROL Save]** och fortsätta till nästa avsnitt.

## Visa information om dataström {#view-details}

När du har konfigurerat en ny datastam eller valt en befintlig som ska visas, visas informationssidan för den datastream. Här finns mer information om datastream, inklusive dess ID.

![Informationssida för ett datastream som skapats](../images/datastreams/overview/view-details.png)

På informationsskärmen kan du [lägg till tjänster](#add-services) för att aktivera funktioner från de Adobe Experience Cloud-produkter du har tillgång till. Du kan även redigera datastreams [grundläggande konfiguration](#create), uppdatera [mappningsregler](./data-prep.md), [kopiera datastream](#copy)eller ta bort den helt.

## Lägga till tjänster i ett datastream {#add-services}

På informationssidan för ett datastream väljer du **[!UICONTROL Add Service]** för att börja lägga till tillgängliga tjänster för den aktuella datastream.

![Välj Lägg till tjänst för att fortsätta](../images/datastreams/overview/add-service.png)

På nästa skärm använder du listrutemenyn för att välja en tjänst som ska konfigureras för det här dataflödet. Endast de tjänster som du har åtkomst till visas i den här listan.

![Välj en tjänst i listan](../images/datastreams/overview/service-selection.png)

Välj önskad tjänst, fyll i de konfigurationsalternativ som visas och välj sedan **[!UICONTROL Save]** för att lägga till tjänsten i datastream. Alla tillagda tjänster visas i informationsvyn för datastream.

![Tjänster som lagts till i ett datastream](../images/datastreams/overview/services-added.png)

Underavsnitten nedan beskriver konfigurationsalternativen för varje tjänst.

>[!NOTE]
>
>Varje tjänstkonfiguration innehåller en **[!UICONTROL Enabled]** som aktiveras automatiskt när tjänsten väljs. Om du vill inaktivera den valda tjänsten för den här datastreamen väljer du **[!UICONTROL Enabled]** växla igen.

### Adobe Analytics-inställningar {#analytics}

Den här tjänsten kontrollerar om och hur data skickas till Adobe Analytics. Mer information finns i guiden på [skicka data till Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../images/datastreams/overview/analytics-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Report Suite ID] | **(Obligatoriskt)** ID:t för analysrapportsviten som du vill skicka data till. Detta ID finns i användargränssnittet i Adobe Analytics under [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Om flera rapportsviter anges kopieras data till varje rapportserie. |

### Adobe Audience Manager-inställningar {#audience-manager}

Den här tjänsten kontrollerar om och hur data skickas till Adobe Audience Manager. Allt som behövs för att skicka data till Audience Manager är att aktivera det här avsnittet. De andra inställningarna är valfria men rekommenderas.

![Inställningsblock för hantering av målgruppshantering i Adobe](../images/datastreams/overview/audience-manager-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Cookie Destinations Enabled] | Gör att SDK kan dela segmentinformation via [cookie-destinationer](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) från [!DNL Audience Manager]. |
| [!UICONTROL URL Destinations Enabled] | Gör att SDK kan dela segmentinformation via [URL-mål](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) från [!DNL Audience Manager]. |

### Adobe Experience Platform-inställningar {#aep}

>[!IMPORTANT]
>
>När du aktiverar en datastream för plattformen bör du tänka på den plattformssandlåda som du använder, som visas på den översta menyfliken i användargränssnittet för datainsamling.
>
>![Markerad sandlåda](../images/datastreams/overview/platform-sandbox.png)
>
>Sandlådor är virtuella partitioner i Adobe Experience Platform som gör att du kan isolera data och implementeringar från andra i din organisation. När en datastream har skapats kan dess sandlåda inte ändras. Mer information om sandlådornas roll i Experience Platform finns i [dokumentation för sandlådor](../../sandboxes/home.md).

Den här tjänsten kontrollerar om och hur data skickas till Adobe Experience Platform.

![Adobe Experience Platform inställningsblock](../images/datastreams/overview/platform-config.png)

| Inställning | Beskrivning |
|---| --- |
| [!UICONTROL Event Dataset] | **(Obligatoriskt)** Välj den plattformsdatauppsättning som kundhändelsedata ska direktuppspelas till. Det här schemat måste använda [Klassen XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profile Dataset] | Välj den plattformsdatauppsättning som kundattributdata ska skickas till. Det här schemat måste använda [Klassen XDM Individuell profil](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Markera den här kryssrutan om du vill aktivera Offer decisioning för en implementering av en Platform Web SDK. Se guiden [använda Offer decisioning med Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) om du vill ha mer information om implementeringen. Mer information om Offer decisioning finns i [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html). |
| [!UICONTROL Edge Segmentation] | Markera den här kryssrutan för att aktivera [kantsegmentering](../../segmentation/ui/edge-segmentation.md) för denna datastream. När SDK skickar data via en datastam som är aktiverad för kantsegmentering, skickas alla uppdaterade segmentmedlemskap för den aktuella profilen tillbaka som svar.<br><br>Det här alternativet kan användas i kombination med [!UICONTROL Personalization Destinations] for [exempel på användning av personalisering på nästa sida](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | När du har aktiverat detta efter att du har aktiverat [!UICONTROL Edge Segmentation] kryssrutan tillåter det här alternativet att datastream ansluter till personaliseringsmål, som [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md). Se måldokumentationen för specifika steg om [konfigurera personaliseringsmål](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target-inställningar {#target}

Den här tjänsten kontrollerar om och hur data skickas till Adobe Target.

![Adobe Target inställningsblock](../images/datastreams/overview/target-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Property Token] | [!DNL Target] låter kunderna styra behörigheter genom att använda egenskaper. Mer information om egenskaper finns i handboken [konfigurera företagsbehörigheter](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) i [!DNL Target] dokumentation.<br><br>Egenskapstoken finns i Adobe Target-gränssnittet under [!UICONTROL Setup] > [!UICONTROL Properties]. |
| [!UICONTROL Target Environment ID] | [Miljöer i Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) hjälper er att hantera implementeringen i alla utvecklingsfaser. Den här inställningen anger vilken miljö du tänker använda med den här datastream.<br><br>Det bästa sättet är att ange detta på olika sätt för var och en av dina `dev`, `stage`och `prod` datastream-miljöer för att hålla saker och ting enkla. Om du redan har definierat Adobe Target-miljöer kan du använda dessa. |
| [!UICONTROL Target Third Party ID namespace] | Identitetsnamnrymden för `mbox3rdPartyId` som du vill använda för den här datastream. Se guiden [implementera `mbox3rdPartyId` med Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) för mer information. |

### [!UICONTROL Event Forwarding] inställningar

Den här tjänsten kontrollerar om och hur data skickas till [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md).

![Avsnittet Händelsevidarebefordran i konfigurationsgränssnittet](../images/datastreams/overview/event-forwarding-config.png)

| Inställning | Beskrivning |
| --- | --- |
| [!UICONTROL Launch Property] | **(Obligatoriskt)** Egenskapen för vidarebefordran av händelser som du vill skicka data till. |
| [!UICONTROL Launch Environment] | **(Obligatoriskt)** Den miljö i den valda egenskapen som du vill skicka data till. |

>[!NOTE]
>
>Du kan välja **[!UICONTROL Manually enter IDs]** om du vill skriva i egenskaps- och miljönamnen i stället för att använda listrutemenyer.

## Kopiera ett datastream {#copy}

Du kan skapa en kopia av ett befintligt datastream och ändra informationen efter behov.

>[!NOTE]
>
>Datastreams kan bara kopieras inom samma [sandlåda](../../sandboxes/home.md). Du kan alltså inte kopiera en datastam från en sandlåda till en annan.

Från huvudsidan i [!UICONTROL Datastreams] väljer du ellips (**....**) för den aktuella datastream-filen och välj **[!UICONTROL Copy]**.

![Bilden visar [!UICONTROL Copy] det alternativ som väljs i datastreams listvy](../images/datastreams/overview/copy-datastream-list.png)

Du kan också välja **[!UICONTROL Copy Datastream]** från detaljvyn för en viss datastream.

![Bilden visar [!UICONTROL Copy] alternativ som väljs från datastream-informationsvyn](../images/datastreams/overview/copy-datastream-details.png)

En bekräftelsedialogruta visas där du uppmanas att ange ett unikt namn för den nya datastream som ska skapas, tillsammans med information om de konfigurationsalternativ som ska kopieras. Välj **[!UICONTROL Copy]**.

![Bild av bekräftelsedialogrutan för kopiering av ett datastream](../images/datastreams/overview/copy-datastream-confirm.png)

Huvudsidan i [!UICONTROL Datastreams] arbetsytan visas igen med den nya datastream som visas.

## Nästa steg

I den här guiden beskrivs hur du hanterar datastölar i användargränssnittet för datainsamling. Mer information om hur du installerar och konfigurerar Web SDK när du har konfigurerat ett datastream finns i [E2E-guide för datainsamling](../../collection/e2e.md#install).
