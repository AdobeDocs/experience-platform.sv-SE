---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Komma igång med innehåll och handel med AI
topic: Getting started
description: Innehåll och AI för handel använder Adobe I/O API:er. För att kunna ringa anrop till Adobe I/O API:er och I/O-konsolintegreringen måste du först slutföra självstudiekursen om autentisering.
translation-type: tm+mt
source-git-commit: 2be04547b96e1a6c293cc63e782fe1b3259619ba
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Komma igång med innehåll och handel med AI

>[!NOTE]
>
>Innehåll och handel AI är i betaversion. Dokumentationen kan komma att ändras.

[!DNL Content and Commerce AI] använder Adobe I/O API:er. För att kunna ringa anrop till Adobe I/O API:er och I/O-konsolintegreringen måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md).

När du kommer till steget **Lägg till API** finns API:t under Experience Cloud i stället för Adobe Experience Platform, vilket visas i följande skärmbild:

![lägga till innehåll och handel med AI](./images/add-api.png)

När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Adobe I/O API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Skapa en Postman-miljö (valfritt)

När du har konfigurerat ditt projekt och API i Adobe Developer Console kan du välja att hämta en miljöfil för Postman. Välj under **[!UICONTROL APIs]** den vänstra listen i ditt projekt **[!UICONTROL Content and Commerce AI]**. En ny flik öppnas med ett kort med etiketten &quot;[!DNL Try it out]&quot;. Välj **Hämta för Postman** om du vill hämta en JSON-fil som används för att konfigurera postmanmiljön.

![ladda ned för postman](./images/add-to-postman.png)

När du har hämtat filen öppnar du Postman och väljer **kugghjulsikonen** i det övre högra hörnet för att öppna dialogrutan **Hantera miljöer** .

![kugghjulsikon](./images/select-gear-icon.png)

Välj sedan **Importera** från dialogrutan **Hantera miljöer** .

![import](./images/import.png)

Du omdirigeras och uppmanas att välja en miljöfil på datorn. Markera JSON-filen som du hämtade tidigare och välj sedan **Öppna** för att läsa in miljön.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Du omdirigeras tillbaka till fliken *Hantera miljöer* med ett nytt miljönamn ifyllt. Markera miljönamnet om du vill visa och redigera variablerna som är tillgängliga i Postman. Du måste fortfarande fylla i `JWT_TOKEN` och `ACCESS_TOKEN`. Dessa värden borde ha inhämtats när [självstudiekursen](../../tutorials/authentication.md)för autentisering slutfördes.

![](./images/re-direct.png)

När du är klar bör variablerna se ut som skärmbilden nedan. Välj **Uppdatera** för att slutföra konfigurationen av miljön.

![](./images/final-environment.png)

Nu kan du välja din miljö i listrutan i det övre högra hörnet och automatiskt fylla i sparade värden. Redigera om värdena när du vill för att uppdatera alla API-anrop.

![exempel](./images/select-environment.png)

Mer information om hur du arbetar med Adobe I/O API:er med Postman finns i posten Medium om hur du [använder Postman för JWT-autentisering i Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

När du har alla dina autentiseringsuppgifter är du redo att konfigurera en anpassad arbetare för [!DNL Content and Commerce AI]. Följande dokument hjälper till att förstå Extensibility Framework och miljöinställningar.

Om du vill veta mer om Extensibility Framework börjar du med att läsa [introduktionen till utökningsdokumentet](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . I det här dokumentet beskrivs förutsättningarna och etableringskraven.

Om du vill veta mer om hur du konfigurerar en miljö för [!DNL Content and Commerce AI]börjar du med att läsa guiden för [att konfigurera en utvecklarmiljö](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html). Det här dokumentet innehåller konfigurationsinstruktioner som gör att du kan utveckla för tjänsten Asset compute.