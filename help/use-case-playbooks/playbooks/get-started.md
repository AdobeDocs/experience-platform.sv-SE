---
solution: Experience Platform
title: Kom igång
description: Lär dig hur du kommer igång med funktionen Använd fallspelningsböcker.
badgeBeta: label="Beta" type="Informative"
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# (Beta) Kom igång

>[!AVAILABILITY]
>
>Den här funktionen finns för närvarande i betaversionen och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Skapa en utvecklingssandlåda {#create-development-sandbox}

För att komma igång och få tillgång till [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md) funktionalitet, [skapa en ny utvecklingssandlåda](/help/sandboxes/ui/user-guide.md#create) (se till att du inte väljer en produktionssandlåda) med namnet (inte titeln) som innehåller antingen `-ucp` eller `-UCP` i suffixet enligt nedan.

![Skapa en utvecklingssandlåda för fallspelningsböcker](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Du bör nu se [!UICONTROL Playbooks] i den vänstra listen under [!UICONTROL Use Case Playbooks] eller under [!UICONTROL Marketer Playground].

![Använd fallspelningsböcker i användargränssnittet när du har skapat sandlådan.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Om du inte ser [!UICONTROL Playbooks] Använd den här länken i den vänstra listen som visas ovan `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` navigera dit direkt. I länken `<YOUR_ORG>` är namnet på din organisation och `<YOUR_SANDBOX_NAME>` är namnet på den utvecklingssandlåda som du skapade.

### Sandlådekonfiguration för Adobe Journey Optimizer-användare {#sandbox-configuration-journey-optimizer}

Om din organisation har licens för [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)måste du konfigurera kanalförinställningarna i sandlådan, som definierar de tekniska parametrar som krävs för dina meddelanden. [Lär dig hur du ställer in kanalytor i Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

## Ge teamet de behörigheter som krävs {#grant-access-permissions}

Så här kommer du igång med [!UICONTROL Use Case Playbooks]behöver medlemmarna i ert marknadsföringsteam rätt behörigheter. Du kan ge ditt team behörigheter enligt följande:

* Medlemmar i marknadsföringsteamet som bara vill bläddra bland spelböckerna kan få **read** behörighet.
* Medlemmar i marknadsföringsteamet som vill skapa instanser från spelböcker kan få **läsa och skriva** behörigheter.

## Nästa steg {#next-steps}

När du har läst det här dokumentet kan du nu komma igång med [!UICONTROL Use Case Playbooks]. Läs sedan hur [hitta rätt spelbok](/help/use-case-playbooks/playbooks/discover.md) för dig och sedan [skapa instanser av den](/help/use-case-playbooks/playbooks/create-share-reuse.md).
