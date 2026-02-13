---
title: Konfigurationsinställningar för Brand Concierge
description: Konfigurera sessionsbeständighet och tidsgränser för direktuppspelning för Brand Concierge-chatt.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---

# Konfigurationsinställningar för Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge för webben: SDK är för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Konfigurationsinställningar när du använder Brand Concierge på din egenskap."

I avsnittet **[!UICONTROL Brand Concierge]** kan du styra hur Brand Concierge chattsessioner fungerar i webbtaggtillägget för SDK.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Brand Concierge]**.

Följande alternativ är tillgängliga:

## [!UICONTROL Sticky conversation session]

En kryssruta som återger Brand Concierge-sessioner på olika sidor läses in med hjälp av en sessionscookie. Det här alternativet är inaktiverat som standard. Se [`conversation`](/help/collection/js/commands/configure/conversation.md) i dokumentationen för JavaScript-biblioteket för vägledning om hur du anger det här värdet.

## [!UICONTROL Stream timeout (seconds)]

Maximal tid, i sekunder, för att vänta på konversationsströmavbrott innan ett timeout-fel utlöses. Standardvärdet är `10` sekunder.
