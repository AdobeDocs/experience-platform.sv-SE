---
title: Adobe Commerce Destination Connector
description: Läs om hur Adobe Commerce- och Real-Time CDP-handlare kan personalisera shoppingupplevelsen genom att leverera relevant webbinnehåll och kampanjer, anpassade till kundgrupper som byggts och hanteras inom Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 276224303c7a65a53ff859bcbf47f64a6925bf77
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---

# Adobe Commerce Connection {#adobe-commerce}

## Översikt {#overview}

The [!DNL Adobe Commerce] med målanslutning kan du välja en eller flera Real-Time CDP-målgrupper att aktivera för [!DNL Adobe Commerce] för att leverera en dynamisk personaliserad upplevelse till era kunder. Inom [!DNL Adobe Commerce]kan ni sedan välja de Real-Time CDP-målgrupperna för att personalisera unika erbjudanden i kundvagnen, till exempel&quot;köp 2 få 1 utan kostnad&quot;. Ni kan också visa hjältebanners och ändra produktpriserna genom kampanjerbjudanden som alla är anpassade för Adobe Real-Time CDP målgrupper.

## Förutsättningar {#prerequisites}

Den här kontakten är tillgänglig i målkatalogen för kunder som har köpt Real-Time CDP Prime eller Ultimate och Adobe Commerce.

Om du vill använda den här målanslutningen måste du ha åtkomst till:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Med tillgång till utvecklarkonsolen kan du visa tjänstkonto- och autentiseringsuppgifter som behövs för att [slutföra konfigurationen](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) av tillägget i Adobe Commerce.
- [Adobe Commerce Cloud version 2.4.4 eller senare](https://business.adobe.com/products/magento/magento-commerce.html)

I Experience Platform skapar du följande:

- [Schema](../../../xdm/schema/composition.md). Schemat som du skapar representerar de data som du tänker importera från Adobe Commerce. [Läs mer](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) om hur du skapar ett schema som innehåller handelsspecifika fältgrupper.
- [Datauppsättning](../../../catalog/datasets/user-guide.md#create). En datauppsättning är en lagrings- och hanteringskonstruktion för en datainsamling. Du skapar den här datauppsättningen från schemat som du skapade ovan.
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
- **[!UICONTROL Datastream ID]**: Detta avgör vilken datainsamling som innehåller de målgrupper som ingår i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Se [Konfigurera ett datastream](../../../edge/datastreams/overview.md) för mer information.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper för [!DNL Commerce] mål {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-edge-personalization-destinations.md) för instruktioner om att aktivera målgrupper för [!DNL Commerce] mål.

## Nästa steg i [!DNL Adobe Commerce]

Nu när du har konfigurerat [!DNL Commerce] i Experience Platform måste du installera [!DNL Audience Activation] tillägg i [!DNL Commerce] och konfigurera [!DNL Commerce Admin] för att importera de Real-Time CDP-målgrupper du har skapat. Se [[!DNL Commerce] dokumentation](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) om du vill veta mer.

## Validera målgruppsaktivering i Commerce {#exported-data}

När du har aktiverat Real-Time CDP-målgrupper för [!DNL Adobe Commerce] kommer du att se vilka målgrupper som är tillgängliga när du går till _Administratör_ sidebar, gå sedan till **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**.

![Real-Time CDP Auditions Dashboard](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
