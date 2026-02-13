---
title: Konfigurationsinställningar för Adobe Advertising
description: Aktivera eller inaktivera funktioner för DSP (Demand-side Platform).
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Konfigurationsinställningar för Adobe Advertising {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising för webben: SDK är för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Konfigurera inställningar för Adobe Advertising-integreringar. Observera att ingen annonskonfiguration behövs för att aktivera klickmätningar. Klienter med sökfunktioner, sociala medier och Commerce har inga ytterligare åtgärder som behöver vidtas. Användare av DSP (Demand-side Platform) måste dock konfigurera annonsörer i det här avsnittet för att kunna mäta genomskinliga konverteringar."

I avsnittet **[!UICONTROL Adobe Advertising]** kan du aktivera eller inaktivera DSP-funktioner (Demand-side Platform) om de används i implementeringen. Du behöver bara ange det här fältet om implementeringen använder en DSP.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Adobe Advertising]**.

Det finns för närvarande ett alternativ.

## [!UICONTROL Adobe Advertising DSP]

En nedrullningsbar meny som aktiverar eller inaktiverar DSP-funktioner för Adobe Advertising.

* **[!UICONTROL Enabled]**: Aktiverar vyövergripande spårning.
* **[!UICONTROL Disabled]**: Inaktiverar genomskinlighetsspårning.

När det här alternativet är aktiverat är följande inställningar tillgängliga:

* **[!UICONTROL Advertisers]**: De annonsörer som genomsiktsspårning ska aktiveras för.
* **[!UICONTROL ID5 partner ID]**: Valfritt. Organisationens ID5-partner-ID. Med den här inställningen kan Web SDK samla in universella ID:n för ID5.
* **[!UICONTROL RampID JavaScript path]**: Valfritt. Sökvägen till din organisations [!DNL LiveRamp RampID] JavaScript-kod (`ats.js`).  Med den här inställningen kan Web SDK samla in [!DNL RampID] universella ID:n.
