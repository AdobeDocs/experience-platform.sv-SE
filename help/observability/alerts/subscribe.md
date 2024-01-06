---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Prenumerera på händelsemeddelanden från Adobe I/O
description: Det här dokumentet innehåller anvisningar om hur du prenumererar på händelsemeddelanden i Adobe I/O för Adobe Experience Platform-tjänster. Referensinformation om tillgängliga händelsetyper tillhandahålls också, tillsammans med länkar till ytterligare dokumentation om hur man tolkar returnerade händelsedata för varje tillämplig [!DNL Platform] service.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: eccd53a8b2076fe23a65aa2e933a7cb871e97f72
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# Prenumerera på händelsemeddelanden i Adobe I/O

[!DNL Observability Insights] gör att du kan prenumerera på Adobe I/O-händelsemeddelanden om Adobe Experience Platform-aktiviteter. Dessa händelser skickas till en konfigurerad webkrok för att underlätta effektiv automatisering av aktivitetsövervakning.

Det här dokumentet innehåller anvisningar om hur du kan prenumerera på händelsemeddelanden i Adobe I/O för Adobe Experience Platform-tjänster. Referensinformation om tillgängliga händelsetyper finns också, tillsammans med länkar till ytterligare dokumentation om hur du kan tolka returnerade händelsedata för varje tillämplig typ [!DNL Platform] service.

## Komma igång

Det här dokumentet kräver en fungerande förståelse för webbhooks och hur du ansluter en webkrok från ett program till ett annat. Se [[!DNL I/O Events] dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) för en introduktion till webbhooks.

## Skapa en webkrok

För att få [!DNL I/O Event] meddelanden måste du registrera en webkrok genom att ange en unik webkroks-URL som en del av din information om händelseregistrering.

Du kan konfigurera din webkrok med valfri klient. En temporär webbkrokadress som du kan använda som del av kursen finns på [Webkrok.webbplats](https://webhook.site/) och kopiera den unika URL-adressen som anges.

![](../images/notifications/webhook-url.png)

Under den inledande valideringsprocessen [!DNL I/O Events] skickar en `challenge` frågeparameter i en GET-begäran till webkroken. Du måste konfigurera webkroken så att den returnerar värdet för den här parametern i svarsnyttolasten. Om du använder Webkrok.site väljer du **[!DNL Edit]** i det övre högra hörnet och sedan ange `$request.query.challenge$` under **[!DNL Response body]** före markering **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Skapa ett nytt projekt i Adobe Developer Console

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i dokumentationen för Adobe Developer Console.

## Prenumerera på event

>[!NOTE]
>
>Inmatningsmeddelandet för data kommer att tas bort från Adobe IO-prenumerationen. I stället bör du använda **Körningsinformation för källflöde** I/O-händelse.

När du har skapat ett nytt projekt går du till projektets översiktsskärm. Välj **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

En dialogruta visas där du kan lägga till en händelseleverantör i ditt projekt:

* Om du prenumererar på Experience Platform-aviseringar väljer du **[!UICONTROL Platform notifications]**
* Om du prenumererar på Adobe Experience Platform [!DNL Privacy Service] meddelanden, välja **[!UICONTROL Privacy Service Events]**

När du har valt en händelseleverantör väljer du **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

På nästa skärm visas en lista med händelsetyper att prenumerera på. Välj de händelser du vill prenumerera på och välj sedan **[!UICONTROL Next]**.

>[!NOTE]
>
>Om du är osäker på vilka händelser du ska prenumerera på för den tjänst du arbetar med kan du läsa följande dokumentation:
>
>* [Plattformsmeddelanden](./rules.md)
>* [Privacy Service-meddelanden](../../privacy-service/privacy-events.md)

![](../images/notifications/choose-event-subscriptions.png)

Nästa skärm uppmanar dig att skapa en JSON Web Token (JWT). Du kan välja att automatiskt generera ett nyckelpar eller överföra en egen offentlig nyckel som genererats i terminalen.

I den här självstudiekursen används det första alternativet. Markera alternativrutan för **[!UICONTROL Generate a key pair]** väljer du **[!UICONTROL Generate keypair]** i det nedre högra hörnet.

![](../images/notifications/generate-keypair.png)

När nyckelparet genereras hämtas det automatiskt av webbläsaren. Du måste lagra den här filen själv eftersom den inte sparas i Developer Console.

På nästa skärm kan du granska informationen om det nya nyckelparet. Välj **[!UICONTROL Next]** för att fortsätta.

![](../images/notifications/keypair-generated.png)

På nästa skärm anger du ett namn och en beskrivning för händelseregistreringen i [!UICONTROL Event registration details] -avsnitt. Det bästa sättet är att skapa ett unikt, enkelt identifierbart namn som hjälper till att skilja den här evenemangsregistreringen från andra i samma projekt.

![](../images/notifications/registration-details.png)

Gå längre ned på samma skärm under [!UICONTROL How to receive events] kan du välja att konfigurera hur händelser ska tas emot. **[!UICONTROL Webhook]** gör att du kan ange en anpassad webbkrosadress för att ta emot händelser, medan **[!UICONTROL Runtime action]** låter dig göra samma sak med [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

För den här självstudiekursen väljer du **[!UICONTROL Webhook]** och ange webbadressen till den webbkrok du skapade tidigare. När du är klar väljer du **[!UICONTROL Save configured events]** för att slutföra registreringen av evenemanget.

![](../images/notifications/receive-events.png)

Informationssidan för den nyligen skapade händelseregistreringen visas, där du kan redigera dess konfiguration, granska mottagna händelser, utföra felsökningsspårning och lägga till nya händelseproviders.

![](../images/notifications/registration-complete.png)

## Nästa steg

Genom att följa den här självstudiekursen har du registrerat en webkrok som du vill ta emot [!DNL I/O Event] meddelanden om [!DNL Experience Platform] och/eller [!DNL Privacy Service]. Mer information om tillgängliga händelser och hur du tolkar meddelandenyttolaster för varje tjänst finns i följande dokumentation:

* [[!DNL Privacy Service] meddelanden](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] meddelanden](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (källor) meddelanden](../../sources/notifications.md)

Se [[!DNL Observability Insights] översikt](../home.md) för mer information om hur du kan övervaka dina aktiviteter på [!DNL Experience Platform] och [!DNL Privacy Service].
