---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Prenumerera på Adobe I/O Event Notifications
description: Det här dokumentet innehåller anvisningar om hur du prenumererar på Adobe I/O händelsemeddelanden för Adobe Experience Platform-tjänster. Referensinformation om tillgängliga händelsetyper finns också, tillsammans med länkar till ytterligare dokumentation om hur du tolkar returnerade händelsedata för varje tillämplig [!DNL Experience Platform] tjänst.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Prenumerera på Adobe I/O händelsemeddelanden

Med [!DNL Observability Insights] kan du prenumerera på Adobe I/O-händelsemeddelanden för Adobe Experience Platform-aktiviteter. Dessa händelser skickas till en konfigurerad webkrok för att underlätta effektiv automatisering av aktivitetsövervakning.

Det här dokumentet innehåller anvisningar om hur du prenumererar på Adobe I/O händelsemeddelanden för Adobe Experience Platform-tjänster. Referensinformation om tillgängliga händelsetyper tillhandahålls också, tillsammans med länkar till ytterligare dokumentation om hur du kan tolka returnerade händelsedata för varje tillämplig [!DNL Experience Platform]-tjänst.

## Komma igång

Det här dokumentet kräver en fungerande förståelse för webbhooks och hur du ansluter en webkrok från ett program till ett annat. Se [[!DNL I/O Events] dokumentationen](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) för en introduktion till webbhooks.

## Skapa en webkrok

För att kunna ta emot [!DNL I/O Event] meddelanden måste du registrera en webkrok genom att ange en unik webkrok-URL som en del av informationen om händelseregistrering.

Du kan konfigurera din webkrok med valfri klient. Om du vill ha en temporär webbkrokadress som du kan använda som en del av den här självstudiekursen besöker du [Webkrok.site](https://webhook.site/) och kopierar den unika webbadress som anges.

![](../images/notifications/webhook-url.png)

Under den inledande valideringsprocessen skickar [!DNL I/O Events] en `challenge`-frågeparameter i en GET-begäran till webbkroken. Du måste konfigurera webkroken så att den returnerar värdet för den här parametern i svarsnyttolasten. Om du använder Webhook.site väljer du **[!DNL Edit]** i det övre högra hörnet och anger sedan `$request.query.challenge$` under **[!DNL Response body]** innan du väljer **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Skapa ett nytt projekt i Adobe Developer Console

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om att [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i Adobe Developer Console-dokumentationen.

## Prenumerera på event

>[!NOTE]
>
>Aviseringshändelsen för dataöverföring har tagits bort i Adobe I/O. I stället bör du använda **Source Flow Run Info** I/O-händelsen.

När du har skapat ett nytt projekt går du till projektets översiktsskärm. Välj **[!UICONTROL Add event]** härifrån.

![](../images/notifications/add-event-button.png)

En dialogruta visas där du kan lägga till en händelseleverantör i ditt projekt:

* Om du prenumererar på Experience Platform-aviseringar väljer du **[!UICONTROL Platform notifications]**
* Om du prenumererar på Adobe Experience Platform [!DNL Privacy Service]-meddelanden väljer du **[!UICONTROL Privacy Service Events]**

Välj **[!UICONTROL Next]** när du har valt en händelseleverantör.

![](../images/notifications/event-provider.png)

På nästa skärm visas en lista med händelsetyper att prenumerera på. Välj de händelser som du vill prenumerera på och välj sedan **[!UICONTROL Next]**.

>[!NOTE]
>
>Om du är osäker på vilka händelser du ska prenumerera på för den tjänst du arbetar med kan du läsa följande dokumentation:
>
>* [Plattformsmeddelanden](./rules.md)
>* [Privacy Service-meddelanden](../../privacy-service/privacy-events.md)

>[!IMPORTANT]
>
>Edge-relaterade aviseringar finns för närvarande i betaversionen och är endast tillgängliga för vissa betatestare.

![](../images/notifications/choose-event-subscriptions.png)

Nästa skärm uppmanar dig att skapa en JSON Web Token (JWT). Du kan välja att automatiskt generera ett nyckelpar eller överföra en egen offentlig nyckel som genererats i terminalen.

I den här självstudiekursen används det första alternativet. Markera alternativrutan för **[!UICONTROL Generate a key pair]** och välj sedan knappen **[!UICONTROL Generate keypair]** i det nedre högra hörnet.

![](../images/notifications/generate-keypair.png)

När nyckelparet genereras hämtas det automatiskt av webbläsaren. Du måste lagra den här filen själv eftersom den inte sparas i Developer Console.

På nästa skärm kan du granska informationen om det nya nyckelparet. Välj **[!UICONTROL Next]** om du vill fortsätta.

![](../images/notifications/keypair-generated.png)

Ange ett namn och en beskrivning för händelseregistreringen i avsnittet [!UICONTROL Event registration details] på nästa skärm. Det bästa sättet är att skapa ett unikt, enkelt identifierbart namn som hjälper till att skilja den här evenemangsregistreringen från andra i samma projekt.

![](../images/notifications/registration-details.png)

Du kan konfigurera hur du vill ta emot händelser längre ned på samma skärm under avsnittet [!UICONTROL How to receive events]. Med **[!UICONTROL Webhook]** kan du ange en anpassad webbkrokadress för att ta emot händelser, medan **[!UICONTROL Runtime action]** låter dig göra det med [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

För den här självstudiekursen väljer du **[!UICONTROL Webhook]** och anger webbadressen till den webbkrok du skapade tidigare. När du är klar väljer du **[!UICONTROL Save configured events]** för att slutföra händelseregistreringen.

![](../images/notifications/receive-events.png)

Informationssidan för den nyligen skapade händelseregistreringen visas, där du kan redigera dess konfiguration, granska mottagna händelser, utföra felsökningsspårning och lägga till nya händelseproviders.

![](../images/notifications/registration-complete.png)

## Nästa steg

Genom att följa den här självstudiekursen har du registrerat en webkrok för att ta emot [!DNL I/O Event] meddelanden för [!DNL Experience Platform] och/eller [!DNL Privacy Service]. Mer information om tillgängliga händelser och hur du tolkar meddelandenyttolaster för varje tjänst finns i följande dokumentation:

* [[!DNL Privacy Service] meddelanden](../../privacy-service/privacy-events.md)
* [[!DNL Flow Service] (källor) meddelanden](../../sources/notifications.md)

Mer information om hur du kan övervaka dina aktiviteter på [!DNL Experience Platform] och [!DNL Privacy Service] finns i [[!DNL Observability Insights] översikten](../home.md).
