---
title: (Beta) Adobe Commerce Destination Connector
description: Läs om hur Adobe Commerce- och Real-Time CDP-handlare kan personalisera shoppingupplevelsen genom att leverera relevant webbplatsinnehåll och kampanjer, anpassade till kundsegment som skapats och hanteras inom Real-Time CDP.
source-git-commit: 51c5458f444220fb526eb9e82417ae6456857de6
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (Beta) Adobe Commerce-anslutning {#adobe-commerce}

## Översikt {#overview}

>[!IMPORTANT]
> 
>The **[!UICONTROL Adobe Commerce]** anslutningsprogrammet är i betaversion och endast tillgängligt för ett visst antal kunder.

The [!DNL Adobe Commerce] med målanslutningen kan du markera ett eller flera Experience Platform-segment som ska aktiveras för [!DNL Adobe Commerce] för att leverera en dynamisk personaliserad upplevelse till era kunder. Inom [!DNL Adobe Commerce]kan du sedan välja de Adobe Experience Platform-segmenten för att personalisera unika erbjudanden i kundvagnen, till exempel&quot;köp 2 få 1 utan kostnad&quot;. Ni kan också visa hjältebanners och ändra produktpriserna med hjälp av kampanjerbjudanden som alla är anpassade efter Adobe Experience Platform segment.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för utvalda betakunder som har köpt CDP Prime eller Ultimate i realtid och Adobe Commerce.

Beta-kunder bör ha tillgång till:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud version 2.4.3 eller senare](https://business.adobe.com/products/magento/magento-commerce.html)

I Experience Platform skapar du följande:

- [Schema](../../../xdm/schema/composition.md). Schemat som du skapar representerar de data som du tänker importera från Adobe Commerce. [Läs mer](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) om hur du skapar ett schema som innehåller handelsspecifika fältgrupper.
- [Datauppsättning](../../../catalog/datasets/user-guide.md#create). En datauppsättning är en lagrings- och hanteringskonstruktion för en datainsamling. Du måste skapa den här datauppsättningen från schemat som du skapade ovan.
- [Datastream](../../../edge/datastreams/overview.md#create). ID som gör att data kan flöda från Adobe Experience Platform till andra Adobe DX-produkter. Detta ID måste kopplas till en specifik webbplats i din specifika Adobe Commerce-instans. När du skapar den här dataströmmen anger du XDM-schemat som du skapade ovan.

När du är klar med kraven ansluter du till [!DNL Commerce] mål.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Ansluta till [!DNL Adobe Commerce] mål:

1. I [Plattformsgränssnitt](https://experience.adobe.com/platform/), gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Välj **[!UICONTROL Personalization]**.
1. Markera Adobe Commerce-målet och välj sedan **[!UICONTROL Set up]**.
1. Följ stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

- **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
- **[!UICONTROL Integration alias]**: Värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
- **[!UICONTROL Datastream ID]**: Detta anger i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Se [Konfigurera ett datastream](../../../edge/datastreams/overview.md) för mer information.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment för [!DNL Commerce] mål {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) för instruktioner om hur målgruppssegment aktiveras för [!DNL Commerce] mål.

## Nästa steg i [!DNL Adobe Commerce]

Nu när du har konfigurerat [!DNL Commerce] mål inom Experience Platform måste du konfigurera [!DNL Commerce Admin] för att importera de CDP-segment i realtid som du har skapat. Se [[!DNL Commerce] dokumentation](https://docs.magento.com/user-guide/marketing/customer-segment-rtcdp.html) om du vill veta mer.

## Validera dataexport {#exported-data}

När du har aktiverat Real-Time CDP-segment för [!DNL Adobe Commerce] kommer du att se vilka segment som är tillgängliga i [!DNL Admin] när du skapar en kundprisregel:

![Adobe Commerce Admin](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
