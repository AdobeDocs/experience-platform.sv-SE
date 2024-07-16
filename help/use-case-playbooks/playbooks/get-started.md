---
solution: Experience Platform
title: Kom igång med Use Case Playbooks
description: Lär dig hur du kommer igång med funktionen Använd fallspelningsböcker.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Kom igång

Lär dig hur du konfigurerar ditt konto för Use Case Playbooks, som är utformat för Real-time Customer Data Platform och Adobe Journey Optimizer om det inte konfigureras automatiskt. De tre huvudsakliga konfigurationsstegen är:

* Skapa en sandlåda
* Konfigurera användarbehörigheter
* Konfigurera Journey Optimizer-kanalytor för e-post-, push- och SMS-meddelanden (om du tänker använda Journey Optimizer spelböcker)

## Konfigurera användningsfallsspelböcker - videogenomgång {#video}

I den här videon får du lära dig mer om hur du skapar sandlådan, konfigurerar behörigheter och konfigurerar kanalytor för e-post, push-meddelanden och SMS-meddelanden i Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Skapa en utvecklingssandlåda {#create-development-sandbox}

Använd Case Playbooks använder en särskild typ av utvecklingssandlåda. Om du vill komma igång och få åtkomst till funktionen [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md) skapar du [en ny utvecklingssandlåda](/help/sandboxes/ui/user-guide.md#create) (se till att du inte väljer en produktionssandlåda) med namnet (inte titeln) som innehåller antingen `-ucp` eller `-UCP` i suffixet, vilket visas nedan.

>[!IMPORTANT]
>
>När du skapar en ny utvecklingssandlåda måste du se till att namnet innehåller `-ucp` eller `-UCP` i suffixet.


![Skapa en utvecklingssandlåda för fallspelningsböcker](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Du bör nu se [!UICONTROL Playbooks] i den vänstra listen under [!UICONTROL Use Case Playbooks].

![Använd fallspelningsböcker i användargränssnittet när du har skapat sandlådan.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Om du inte ser [!UICONTROL Playbooks] i den vänstra listen som visas ovan kan du använda den här länken `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` för att navigera dit direkt. I länken är `<YOUR_ORG>` namnet på din organisation och `<YOUR_SANDBOX_NAME>` är namnet på den utvecklingssandlåda som du skapade.

## Ge teamet de behörigheter som krävs {#grant-access-permissions}

För att komma igång med [!UICONTROL Use Case Playbooks] behöver medlemmarna i ditt marknadsföringsteam rätt behörigheter så att de kan visa listan med skapade spelböcker eller skapa själva spelböcker.

**Nödvändiga behörigheter**

Om du vill lägga till de nödvändiga behörigheterna inkluderar du den nya fallspelningsbokssandlådan för användning i [roller som du redan har konfigurerat](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), inklusive de som används för andra utvecklingssandlådor.

![Spelbokssandlådan för roller som redan konfigurerats](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Konfigurera en roll för Playbooks:**

Du kan också överväga att lägga till nya roller med [de behörigheter som krävs](/help/access-control/home.md#sandboxes-and-permissions).

[Konfigurera en ny roll](/help/access-control/abac/ui/permissions.md) med de behörigheter som krävs för viktiga spelboksuppgifter. Skapa en roll och lägg till den nya sandlådan i den enligt nedan.

![Skapa en roll och lägg till den i sandlådan](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Behörigheter för spelboksinstanser**

Som en del av Use Case Playbooks skapar du olika resurser som scheman, målgrupper, destinationer och resor. Du och andra användare måste ha rätt behörighet för att skapa de här objekten.

**Behörigheter för scheman**

Om du vill skapa och hantera scheman använder du datamodelleringsbehörigheterna: **[!UICONTROL Manage Schemas]**, **[!UICONTROL View Schemas]**, **[!UICONTROL Manage Relationships]**, **[!UICONTROL Manage Identity Metadata]**

**Behörigheter för mål**

Om du vill skapa och hantera mål använder du målbehörigheter: **[!UICONTROL Manage]**, **[!UICONTROL Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL Manage and Activate Dataset Destination]**, **[!UICONTROL Destination Authoring]**.

**Behörigheter för resor**

Om du vill skapa och hantera resor använder du behörigheterna Resor: **[!UICONTROL Manage Journeys]**, **[!UICONTROL View Journeys]**, **[!UICONTROL View Journeys Report]**, **[!UICONTROL Manage Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions]**, **[!UICONTROL View Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions, Publish Journeys]**.

Bilden nedan visar en ögonblicksbild av de rekommenderade behörigheterna för användare att visa, skapa och hantera spelböcker och de resurser som genereras av spelböcker.

![Ögonblicksbild av alla behörighetsobjekt som behövs för att skapa alla instanser av spelböckerna](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Lägg till användare i rollen**

När du har [skapat en ny roll](/help/access-control/abac/ui/permissions.md#managing-users-for-role) enligt ovan lägger du till dig själv som användare. Om du skapar en roll med begränsad åtkomst för en annan uppsättning användare med endast behörighet att visa, ska du bara ta med de nödvändiga vyobjekt som är kopplade till dessa behörigheter.

## Konfigurera sandbox- och kanalytor i Journey Optimizer {#configure-channel-surfaces}

Om din organisation har licens för [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) och du vill använda de spelböcker som är utformade för Journey Optimizer, måste du konfigurera kanalförinställningarna i sandlådan, som definierar de tekniska parametrar som krävs för dina meddelanden. [Lär dig hur du ställer in kanalytor i Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Om du vill skapa instanser av spelböcker i Journey Optimizer måste du konfigurera kanalytor för e-post-, push- och SMS-meddelanden.

### E-postkanalens yta

Gå till `Channels` i Journey Optimizer-gränssnittet. Konfigurera separata underdomäner och IP-pooler för marknadsföringsmeddelanden och transaktionsmeddelanden, om de inte redan har konfigurerats. Det här är de bästa sätten att se till att transaktionsmeddelanden, som e-postmeddelanden med orderbekräftelse, når fram till dina kunder. Ange namn, e-postadresser och andra inställningar. Välj **Skicka** längst upp till höger på sidan för att skapa marknadskanalsytan. Läs dokumentationen om [hur du konfigurerar e-postkanalsytor](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-kanalsyta

Om du vill skapa en SMS-kanalyta skapar du först en SMS API-autentiseringsuppgift och väljer önskad leverantör (till exempel Sinch). Ge SMS-kanalen ett namn (till exempel SMS Marketing), markera konfigurationen och ange ett avsändarnummer. Välj **Skicka** längst upp till höger på sidan om du vill spara SMS-kanalens yta. Läs dokumentationen om [hur du konfigurerar SMS-kanalsytor](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=en#message-preset-sms).

Konfigurera även kanaler för spelböcker som innehåller transaktionsmeddelanden som orderbekräftelser.

### Tryck kanalyta

Bekräfta att appytorna är konfigurerade från Experience Platform eller datainsamlingsgränssnittet. Så här ser appytorna ut i datainsamlingsmiljön.

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Välj sedan kanal, plattformar och program som du tittade på i appytskonfigurationerna. Välj **Skicka** för att skapa den push-kanalens yta.

Läs dokumentationen om [hur du ställer in push-kanalsytor](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Nästa steg {#next-steps}

Nu när du har följt alla steg i det här dokumentet bör du ha skapat en utvecklingssandlåda med Använd fallspelningsböcker i den vänstra navigeringen. Nu vet du också hur du ger teammedlemmarna de behörigheter som krävs för att visa och hantera spelböcker och generera resurser. Som ett nästa steg ska du läsa om hur du [väljer rätt spelbok](/help/use-case-playbooks/playbooks/choose.md) åt dig och sedan [skapar instanser från den](/help/use-case-playbooks/playbooks/create-share-reuse.md).
