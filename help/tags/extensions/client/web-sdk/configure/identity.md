---
title: Inställningar för identitetskonfiguration
description: Definiera hur taggtillägget identifierar besökare.
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Inställningar för identitetskonfiguration {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="Identitet"
>abstract="Definiera hur taggtillägget identifierar besökare."

I det här konfigurationsavsnittet kan du definiera hur Web SDK ska fungera när det gäller att hantera användaridentifiering.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Identity]**.

![Bild som visar identitetsinställningarna för SDK-taggtillägget för webben i användargränssnittet för taggar](../assets/web-sdk-ext-identity.png)

Följande alternativ är tillgängliga:

## [!UICONTROL Migrate ECID from VisitorAPI]

En kryssruta som gör att Web SDK kan läsa cookies i `AMCV` och `s_ecid` och ange cookie-filen `AMCV` som används av `Visitor.js`. Den här funktionen är viktig när du migrerar från bibliotek som använder `VisitorAPI.js` till Web SDK, eftersom vissa sidor fortfarande använder `Visitor.js`. Med det här alternativet kan SDK fortsätta att använda samma ECID så att användare inte identifieras som två separata användare. JavaScript-biblioteket som motsvarar kryssrutan är [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

När det här alternativet är aktiverat försöker Web SDK lagra en användaridentifierare i en cookie från tredje part. Om det lyckas identifieras användaren som en enskild användare när de navigerar mellan flera domäner, i stället för att identifieras som en separat användare på varje domän. Om det här alternativet är aktiverat kan SDK fortfarande inte lagra användaridentifieraren i en tredjeparts-cookie om webbläsaren inte stöder cookies från tredje part eller om den har konfigurerats av användaren att inte tillåta cookies från tredje part. I det här fallet lagrar SDK bara identifieraren i förstahandsdomänen. JavaScript-biblioteket som motsvarar kryssrutan är [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).

>[!IMPORTANT]
>
>Cookies från tredje part är inte kompatibla med funktionen [för första parts enhets-ID](/help/collection/use-cases/identity/first-party-device-ids.md) i Web SDK. Du kan antingen använda enhets-ID:n från en annan leverantör eller använda cookies från tredje part. Du kan inte använda båda funktionerna samtidigt.
