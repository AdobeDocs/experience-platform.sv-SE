---
title: Adobe Commerce målanslutning
description: Läs om hur Adobe Commerce- och Real-Time CDP-handlare kan personalisera shoppingupplevelsen genom att leverera relevant webbinnehåll och kampanjer, anpassade till kundgrupper som byggts och hanteras inom Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Adobe Commerce Connection {#adobe-commerce}

## Översikt {#overview}

Med [!DNL Adobe Commerce]-målanslutningen kan du välja en eller flera Real-Time CDP-målgrupper som ska aktiveras för ditt [!DNL Adobe Commerce]-konto för att leverera en dynamisk, personlig upplevelse till era kunder. Inom [!DNL Adobe Commerce] kan du sedan välja dessa Real-Time CDP-målgrupper för att anpassa unika erbjudanden i kundvagnen, till exempel&quot;köp 2 få 1 utan kostnad&quot;. Ni kan också visa hjältebanners och ändra produktpriserna genom kampanjerbjudanden som alla är anpassade för Adobe Real-Time CDP målgrupper.

## Förhandskrav {#prerequisites}

Den här kontakten är tillgänglig i målkatalogen för kunder som har köpt Real-Time CDP Prime eller Ultimate och Adobe Commerce.

Om du vill använda den här målanslutningen måste du ha åtkomst till:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Med tillgång till utvecklarkonsolen kan du visa tjänstkonto- och autentiseringsuppgifter-information som behövs för att [slutföra konfigurationen](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=sv-SE#configure-the-extension) av tillägget i Adobe Commerce.
- [Adobe Commerce Cloud version 2.4.4 eller senare](https://business.adobe.com/products/magento/magento-commerce.html)

I Experience Platform skapar du följande:

- [Schema](../../../xdm/schema/composition.md). Schemat som du skapar representerar de data som du tänker importera från Adobe Commerce. [Läs mer](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=sv-SE) om hur du skapar ett schema som innehåller Commerce-specifika fältgrupper.
- [Datauppsättning](../../../catalog/datasets/user-guide.md#create). En datauppsättning är en lagrings- och hanteringskonstruktion för en datainsamling. Du skapar den här datauppsättningen från schemat som du skapade ovan.
- [Datastream](../../../datastreams/overview.md#create). ID som gör att data kan flöda från Adobe Experience Platform till andra Adobe DX-produkter. Detta ID måste kopplas till en specifik webbplats i din specifika Adobe Commerce-instans. När du skapar den här dataströmmen anger du XDM-schemat som du skapade ovan.

När du har slutfört kraven ansluter du till målet [!DNL Commerce].

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Så här ansluter du till målet [!DNL Adobe Commerce]:

1. Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Experience Platform-gränssnittet](https://experience.adobe.com/platform/).
1. Välj **[!UICONTROL Personalization]**.
1. Markera Adobe Commerce-målet för att markera det och välj sedan **[!UICONTROL Set up]**.
1. Följ stegen som beskrivs i [självstudiekursen för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

- **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
- **[!UICONTROL Description]**: Ange en beskrivning för målet. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
- **[!UICONTROL Integration alias]**: Det här värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
- **[!UICONTROL Datastream ID]**: Detta avgör vilka datamängder i datainsamlingen som innehåller de målgrupper som ingår i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Mer information finns i [Konfigurera ett datastream](../../../datastreams/overview.md).

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till målet [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och målgrupper för att profilera mål för begäran](../../ui/activate-edge-personalization-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till målet [!DNL Commerce].

## Nästa steg i [!DNL Adobe Commerce]

Nu när du har konfigurerat målet [!DNL Commerce] i Experience Platform måste du installera tillägget [!DNL Audience Activation] i [!DNL Commerce] och konfigurera [!DNL Commerce Admin] så att de Real-Time CDP-målgrupper du har skapat importeras. Mer information finns i [[!DNL Commerce] dokumentationen](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=sv-SE).

## Validera målgruppsaktivering i Commerce {#exported-data}

När du har aktiverat Real-Time CDP-målgrupper på ditt [!DNL Adobe Commerce]-konto ser du de målgrupperna som är tillgängliga när du går till sidofältet _Admin_ och sedan går du till **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]**.

![Real-Time CDP Audiences Dashboard](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
