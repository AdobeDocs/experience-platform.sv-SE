---
title: Adobe Commerce Source Connector
description: Lär dig hur du använder Adobe Commerce-källan för att skicka e-handelsdata till Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 5eaa5e518de72b452d43a9abca3082efe9e4cb32
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce är en flexibel B2B- och B2C-handelsplattform som gör det möjligt för handlare och varumärken att öka intäkterna genom kundcentrerade digitala handelsupplevelser på både webben och fysiska platser.

Adobe Experience Platform Sources har stöd för integrering av Adobe Commerce så att handlare kan skicka butiks- och back office-data till Experience Platform Edge Network, så att andra Adobe Experience Cloud-produkter som Adobe Analytics och Adobe Target kan använda [!DNL Commerce] data.

* **Storefront-händelser**: fånga kundinteraktioner som `View Page`, `View Product`och `Add to Cart`. För B2B-handlare fångar butikshändelser också [rekvisitionslistor](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Back office-händelser**: Hämta information om status för en beställning, t.ex. om en beställning har placerats, annullerats, återbetalats, skickats eller slutförts.

>[!NOTE]
>
>Insamlade data i Adobe Commerce innehåller inte personligt identifierbar information. Alla användaridentifierare, som cookie-ID:n och IP-adresser, är strikt anonymiserade.

## Förutsättningar

För att kunna ansluta Adobe Commerce till Experience Platform måste du ha följande:

* Adobe Commerce 2.4.3 eller senare.
* Ett giltigt Adobe ID- och organisations-ID.
* Åtkomst till [Tillägget Adobe Client Data Layer](../../../tags/extensions/client/client-data-layer/overview.md). Det här tillägget är nödvändigt för att samla in händelsedata för butiken.
* Tillstånd till andra Adobe DX-produkter.

## Onboarding-steg

Följ stegen nedan tillsammans med motsvarande dokumentation för att få ett fullständigt medlemskap i ditt Adobe Commerce-källkonto.

* [Installera [!DNL Data Connection] extension](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) för Adobe Commerce. Du kan hämta anslutningstillägget från [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* När du har installerat anslutningstillägget loggar du in på ditt Adobe-konto i Experience Cloud och [bekräfta ditt organisations-ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Detta ID är kopplat till ditt provisionerade Experience Cloud-företag. Den är formaterad som en 24 tecken lång alfanumerisk sträng och innehåller en obligatorisk `@AdobeOrg`.
* Skapa eller uppdatera sedan XDM-schemat (Experience Data Model) med era handelsspecifika fältgrupper. Detaljerade anvisningar om hur du lägger till handelsspecifika fältgrupper i XDM-schemat finns i guiden [lägga till fältgrupper i ett XDM-schema](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* När schemat har konfigurerats måste du skapa en datauppsättning baserad på ditt nya schema. Den här datauppsättningen innehåller sedan [!DNL Commerce] data som du skickar. Detaljerade anvisningar om hur du skapar en datauppsättning för [!DNL Commerce] data, läs guiden på [skicka data till Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Skapa sedan en datastream och välj det XDM-schema som innehåller dina Commerce-specifika fältgrupper. Mer information om datastreams finns i [datastreams - översikt](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Sedan måste du ansluta Adobe Commerce-instansen till [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). På så sätt kan din Commerce-instans distribueras som SaaS (Software as a Service).
* När alla de tidigare konfigurationerna är klara kan du nu ansluta till Experience Platform genom att konfigurera både Commerce Services Connector och [!DNL Data Connection] tillägg med [!DNL Commerce Admin]. Mer information om det här sista steget finns i guiden [koppla handelsdata till Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
