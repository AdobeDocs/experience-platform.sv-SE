---
title: Händelsevidarebefordringstillägg för Google Cloud-plattform
description: Det här tillägget för vidarebefordran av Adobe Experience Platform-händelser skickar Adobe Experience Edge Network-händelser till Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 7e26ebe6d40796174ca48367f826c7c6f1512abf
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# [!DNL Google Cloud Platform] tillägg för händelsevidarebefordran

[[!DNL Google Cloud Platform]](https://cloud.google.com/) är en plattform för cloud computing som erbjuder ett brett utbud av tjänster som distribuerad datorhantering, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP) för företag.

The [!DNL Google Cloud Platform] [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) utbyggnadsutfall [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL Google Cloud Platform] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förutsättningar

För att kunna använda det här tillägget måste du ha en [!DNL Google Cloud Platform] konto med ett befintligt [!DNL Cloud Pub/Sub] ämne. Om du inte har något ämne som redan finns kan du läsa [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) dokumentation om hur du skapar och hanterar ämnen.

### Skapa en hemlighet och ett dataelement

Skapa först en ny `Google OAuth 2` [händelsevidarebefordringshemlighet](../../../ui/event-forwarding/secrets.md), som används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

Nästa, [skapa ett dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) med **[!UICONTROL Core]** tillägg och en **[!UICONTROL Secret]** dataelementtyp som refererar till `Google OAuth 2` hemlighet du nyss skapade.

## Installera och konfigurera [!DNL Google Cloud Platform] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller välj en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** flik, välja **[!UICONTROL Install]** på kortet för [!DNL Google Cloud Platform] tillägg.

![Katalogen [!DNL Google Cloud Platform] tillägg som markerar installationen.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

På konfigurationsskärmen anger du dataelementets hemlighet som du skapade tidigare i **[!UICONTROL Access Token]** fält. Dataelementets hemlighet innehåller din [!DNL Google Cloud Platform] OAuth 2-token. Välj **[!UICONTROL Save]** när du är klar.

![The [!DNL Google Cloud Platform] konfigurationssida för tillägg.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Skapa en [!DNL Send Data to Cloud Pub/Sub] regel {#tracking-rule}

Skapa en ny vidarebefordring av händelser när tillägget har installerats [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du **[!UICONTROL Google Cloud Platform]** tillägg, välj **[!UICONTROL Send Data to Cloud Pub/Sub]** för åtgärdstypen.

![Åtgärdskonfigurationsvyn för [!UICONTROL Google Cloud Platform], med funktionsmakrot markerat och [!UICONTROL Send Data to Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Topic] | Det ämne som ska ta emot händelser från händelsevidarebefordran. Värdet måste ha formatet `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] | Det här fältet innehåller de data som ska vidarebefordras till [!DNL Cloud Pub/Sub] ämne i JSON-format.<br><br>Under **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet, eller så kan du välja dataelementsikonen (![Ikon för datauppsättning](../../../images/extensions/server/aws/data-element-icon.png)) för att välja från en lista med befintliga dataelement som ska representera data.<br><br>Du kan också använda **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en UI-redigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |
| [!UICONTROL Attributes] | Det här fältet innehåller JSON-objektet med extra attribut som ska skickas tillsammans med meddelandet.<br><br>Under **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet, eller så kan du välja dataelementsikonen (![Ikon för datauppsättning](../../../images/extensions/server/aws/data-element-icon.png)) för att välja från en lista med befintliga dataelement som ska representera data.<br><br>Du kan också använda **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en UI-redigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |

{style="table-layout:auto"}

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL Cloud Pub/Sub] med [!DNL Google Cloud Platform] tillägg för händelsevidarebefordran. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).