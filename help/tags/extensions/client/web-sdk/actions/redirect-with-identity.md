---
title: Omdirigera med identitet
description: Tillåter delning av en besökaridentifierare i organisationens domäner.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Omdirigera med identitet

Åtgärdstypen **[!UICONTROL Redirect with identity]** gör att du kan dela en besökaridentifierare från den aktuella sidan till en annan domän som din organisation äger. Den är utformad för att användas med en klickhändelse och ett värdejämförelsevillkor. Det fungerar ungefär som kommandot [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) i JavaScript-biblioteket.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Redirect with identity]**.

## Användningsfall

* **Identifiera en individ över domäner**: Om en besökare klickar från en domän till en annan som ägs av din organisation kan du använda den här åtgärden så att de fortfarande betraktas som samma individ. Den här identifieringsmetoden är särskilt användbar om du har rapporter som kombinerar data från flera domäner, vilket förhindrar att besökarna blir uppblåsta.
* **Identifiera en individ från en mobilapp till en webbapp**: Om en besökare finns i din mobilapp och klickar på en länk till din webbapp kan du använda den här åtgärden så att Web SDK godkänner att den är samma individ. Det här arbetsflödet ger en enhetlig upplevelse för rapportering och personalisering.

## Tillgängliga fält

* **[!UICONTROL Instance]**: Den SDK-instans som åtgärden gäller för. Den här nedrullningsbara menyn är inaktiverad om implementeringen använder en enda SDK-instans.
* **[!UICONTROL Datastream configuration overrides]**: Det här kommandot har stöd för åsidosättningar av dataströmskonfigurationer, vilket ger dig kontroll över vilka program och tjänster som tar emot dessa data. När du anger en åsidosättning av en datastream-konfiguration i både ett enskilt kommando och i inställningarna för taggtilläggskonfigurationen, prioriteras det enskilda kommandot. Mer information finns i [Åsidosättningar av dataströmskonfiguration](../configure/configuration-overrides.md).

## Exempelregel

Det här kommandot används vanligtvis med en viss regel som lyssnar efter klickningar och kontrollerar vilka domäner du vill använda.

+++Villkor för regelhändelse

Utlöses när någon klickar på en ankartagg med egenskapen `href`.

* **[!UICONTROL Extension]**: Kärna
* **[!UICONTROL Event type]**: Klicka
* **[!UICONTROL When the user clicks on]**: Specifika element
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Regelhändelse](../assets/id-sharing-event-configuration.png)

+++

+++Regelvillkor

Utlöses bara på önskade domäner.

* **[!UICONTROL Logic type]**: Normal
* **[!UICONTROL Extension]**: Kärna
* **[!UICONTROL Condition Type]**: Värdejämförelse
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Matchar Regex
* **[!UICONTROL Right Operand]**: Ett reguljärt uttryck som matchar de önskade domänerna. Exempel: `adobe.com$|behance.com$`

![Regelvillkor](../assets/id-sharing-condition-configuration.png)

+++

+++Regelåtgärd

Lägg till identiteten i URL:en.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Omdirigera med identitet

![Regelåtgärd](../assets/id-sharing-action-configuration.png)

+++
