---
title: Händelsevidarebefordringstillägg för Google Cloud-plattform
description: Det här tillägget för vidarebefordran av Adobe Experience Platform-händelser skickar Edge Network-händelser till Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# [!DNL Google Cloud Platform]-tillägg för händelsevidarebefordring

[[!DNL Google Cloud Platform]](https://cloud.google.com/) är en plattform för cloud computing som erbjuder en mängd olika tjänster, till exempel distribuerad databehandling, databaslagring, innehållsleverans och SaaS-integreringstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP).

Tillägget [!DNL Google Cloud Platform] [Vidarebefordra ](../../../ui/event-forwarding/overview.md) använder [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL Google Cloud Platform] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förhandskrav

Om du vill använda det här tillägget måste du ha ett [!DNL Google Cloud Platform]-konto med ett befintligt [!DNL Cloud Pub/Sub]-ämne. Om du inte har något ämne läser du [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic)-dokumentationen om hur du skapar och hanterar ämnen.

### Skapa en hemlighet och ett dataelement

Skapa först en ny `Google OAuth 2` [händelsevidarebefordringshemlighet](../../../ui/event-forwarding/secrets.md) som används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

Sedan [skapar du ett dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) med tillägget **[!UICONTROL Core]** och dataelementtypen **[!UICONTROL Secret]** som refererar till den `Google OAuth 2`-hemlighet som du nyss skapade.

## Installera och konfigurera tillägget [!DNL Google Cloud Platform] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. På fliken **[!UICONTROL Catalog]** väljer du **[!UICONTROL Install]** på kortet för tillägget [!DNL Google Cloud Platform].

![Installationen av katalogtillägget [!DNL Google Cloud Platform] markeras.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

På konfigurationsskärmen anger du dataelementets hemlighet som du skapade tidigare i fältet **[!UICONTROL Access Token]**. Dataelementets hemlighet innehåller din [!DNL Google Cloud Platform] OAuth 2-token. Välj **[!UICONTROL Save]** när du är klar.

![Konfigurationssidan för [!DNL Google Cloud Platform]-tillägget.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Skapa en [!DNL Send Data to Cloud Pub/Sub]-regel {#tracking-rule}

När tillägget har installerats skapar du en ny händelsevidarebefordrande [regel](../../../ui/managing-resources/rules.md) och konfigurerar villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du tillägget **[!UICONTROL Google Cloud Platform]** och väljer sedan **[!UICONTROL Send Data to Cloud Pub/Sub]** som åtgärdstyp.

![Åtgärdskonfigurationsvyn för [!UICONTROL Google Cloud Platform], med åtgärden markerad och [!UICONTROL Send Data to Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Topic] | Det ämne som ska ta emot händelser från händelsevidarebefordran. Värdet måste ha formatet `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] | Det här fältet innehåller de data som ska vidarebefordras till avsnittet [!DNL Cloud Pub/Sub] i JSON-format.<br><br>Under alternativet **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet. Du kan också markera dataelementsikonen (![Datauppsättningsikonen](/help/images/icons/database.png)) och välja från en lista över befintliga dataelement som ska representera data.<br><br>Du kan också använda alternativet **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en gränssnittsredigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |
| [!UICONTROL Attributes] | Det här fältet innehåller JSON-objektet med extra attribut som ska skickas tillsammans med meddelandet.<br><br>Under alternativet **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet. Du kan också markera dataelementsikonen (![Datauppsättningsikonen](/help/images/icons/database.png)) och välja från en lista över befintliga dataelement som ska representera data.<br><br>Du kan också använda alternativet **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en gränssnittsredigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |

{style="table-layout:auto"}

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL Cloud Pub/Sub] med hjälp av tillägget [!DNL Google Cloud Platform] för vidarebefordran av händelser. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
