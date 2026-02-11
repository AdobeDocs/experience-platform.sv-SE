---
title: Anpassade byggkomponenter
description: Skapa en anpassad Web SDK-version som inaktiverar funktioner som minskar byggstorleken.
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---

# Anpassade byggkomponenter

SDK-biblioteket för webben innehåller flera moduler för olika funktioner som personalisering, identitet, länkspårning med mera. Beroende på hur du använder dem kanske du bara behöver specifika funktioner i stället för hela biblioteket. Om du inaktiverar byggkomponenter kan du bara använda de moduler du behöver, vilket minskar biblioteksstorleken och förbättrar prestanda.

När du inaktiverar en komponent kan du inte längre redigera inställningarna för den komponenten. Om du använder flera Web SDK-instanser gäller de valda byggkomponenterna alla instanser.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Expandera dragspelet **[!UICONTROL Custom build components]** högst upp.

>[!WARNING]
>
>Felaktiga ändringar av dessa inställningar kan leda till oönskade resultat, inklusive dataförlust. Testa implementeringen i en utvecklingsmiljö noggrant innan du publicerar dessa ändringar i produktionen.

Adobe kan inaktivera följande byggkomponenter för Web SDK:

| Komponenten Build | Beskrivning | Beroende funktioner |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Möjliggör automatisk länkinsamling och Activity Map tracking. | |
| **[!UICONTROL Advertising]** | Möjliggör integrering av Adobe Advertising med Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Stöder integrering med Adobe Audience Manager, t.ex. ID-synk. | |
| **[!UICONTROL Brand concierge]** | Möjliggör integrering med varumärkesprofilering. |
| **[!UICONTROL Consent]** | Möjlighet att använda funktioner för samtycke. | [[!UICONTROL Set consent]](../actions/set-consent.md)-åtgärd |
| **[!UICONTROL Event merge]** | Föråldrat. | [[!UICONTROL Event merge ID]](../data-element-types.md) dataelement (utgått) <br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md)-åtgärd (utgått) |
| **[!UICONTROL Media Analytics bridge]** | Stöder integrering med äldre Media Analytics. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md)-åtgärd |
| **[!UICONTROL Personalization]** | Stöder integreringar med Adobe Target och Adobe Journey Optimizer. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md)-åtgärd |
| **[!UICONTROL Push notifications]** | Aktiverar push-meddelanden för Adobe Journey Optimizer. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md)-åtgärd |
| **[!UICONTROL Rules engine]** | Aktiverar enhetsbeslut med Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) åtgärd <br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) händelse |
| **[!UICONTROL Streaming media]** | Stöder integrering med direktuppspelad mediainsamling. | [[!UICONTROL Send media event]](../actions/send-media-event.md)-åtgärd |
