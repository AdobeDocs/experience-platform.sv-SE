---
title: Åtgärdstyper i Adobe Experience Platform Web SDK Extension
description: Läs mer om de olika åtgärdstyperna i taggtillägget Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 19e85ef4dbaeb90712ad9cd6ad4cb9a1a6b0c6a5
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Åtgärdstyper

På den här sidan visas alla åtgärder som stöds i en taggregel. Så här skapar eller redigerar du åtgärder i en taggregel:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och välj sedan önskad [!UICONTROL Action Type].

SDK-taggtillägget för webben erbjuder följande åtgärder:

* [**[!UICONTROL Apply propositions]**](apply-propositions.md): Återge förslag i ensidiga program utan att öka mätvärdena.
* [**[!UICONTROL Apply response]**](apply-response.md): Utför en åtgärd baserat på ett svar från Edge Network.
* [**[!UICONTROL Evaluate rulesets]**](evaluate-rulesets.md): Utlösa en utvärdering av en regeluppsättning manuellt.
* [**[!UICONTROL Get Media Analytics tracker]**](get-media-analytics-tracker.md): Exportera det gamla medie-API:t till ett fönsterobjekt.
* [**[!UICONTROL Redirect with identity]**](redirect-with-identity.md): Tillåter delning av en besökaridentifierare mellan domäner som du äger.
* [**[!UICONTROL Send event]**](send-event.md): Skickar händelsedata till Edge Network.
* [**[!UICONTROL Send media event]**](send-media-event.md): Skickar mediedata till Edge Network.
* [**[!UICONTROL Set consent]**](set-consent.md): Anger önskat samtycke för besökaren.
* [**[!UICONTROL Update variable]**](update-variable.md): Ändrar ett [variabel](../data-element-types.md#variable)-dataelement.
