---
keywords: Experience Platform;komma igång;innehåll;innehållstaggning
solution: Experience Platform
title: Komma igång med innehållstaggning
description: Innehållstaggning använder Adobe I/O API:er. För att kunna ringa anrop till API:er för Adobe I/O och I/O-konsolintegrering måste du först slutföra självstudiekursen om autentisering.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Komma igång med innehållstaggar

[!DNL Content tagging] använder Adobe I/O API:er. För att kunna ringa anrop till API:er för Adobe I/O och I/O-konsolintegreringen måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en).

När du kommer till steget **Lägg till API** finns API:t under Creative Cloud i stället för Adobe Experience Platform, vilket visas i skärmbilden nedan:

![lägger till innehållstaggning](./images/add-api-updated.png)

När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Adobe I/O API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Skapa en Postman-miljö (valfritt)

När du har konfigurerat ditt projekt och ditt API i Adobe Developer Console kan du välja att hämta en miljöfil för Postman. Välj **[!UICONTROL Content tagging]** under **[!UICONTROL APIs]** till vänster i projektet. En ny flik öppnas med ett kort med etiketten [!DNL Try it out]. Välj **Hämta för Postman** om du vill hämta en JSON-fil som används för att konfigurera postmanmiljön.

![hämta för postman](./images/add-to-postman-updated.png)

När du har hämtat filen öppnar du Postman och väljer **kugghjulsikonen** i det övre högra hörnet för att öppna dialogrutan **Hantera miljöer** .

![kugghjulsikon](./images/select-gear-icon.png)

Välj sedan **Importera** i dialogrutan **Hantera miljöer**.

![importera](./images/import-updated.png)

Du omdirigeras och uppmanas att välja en miljöfil på datorn. Markera JSON-filen som du hämtade tidigare och välj sedan **Öppna** för att läsa in miljön.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Du omdirigeras tillbaka till fliken *Hantera miljöer* med ett nytt miljönamn ifyllt. Markera miljönamnet för att visa och redigera de variabler som är tillgängliga i Postman. Du måste fortfarande fylla i `JWT_TOKEN` och `ACCESS_TOKEN` manuellt. Dessa värden borde ha hämtats när [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering slutfördes.

![](./images/re-direct-updated.png)

När du är klar bör variablerna se ut som skärmbilden nedan. Välj **Uppdatera** för att slutföra konfigurationen av miljön.

![](./images/final-environment-updated.png)

Nu kan du välja din miljö i listrutan i det övre högra hörnet och automatiskt fylla i sparade värden. Redigera om värdena när du vill för att uppdatera alla API-anrop.

![exempel](./images/select-environment-updated.png)

Mer information om hur du arbetar med Adobe I/O-API:er med Postman finns i Medium-posten på [med Postman för JWT-autentisering på Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

När du har alla dina autentiseringsuppgifter kan du konfigurera en anpassad arbetare för [!DNL Content tagging]. Följande dokument hjälper till att förstå Extensibility Framework och miljöinställningar.

Om du vill veta mer om Extensibility Framework börjar du med att läsa dokumentet [introduction to extensibility](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) . I det här dokumentet beskrivs förutsättningarna och etableringskraven.

Om du vill veta mer om hur du konfigurerar en miljö för [!DNL Content tagging] börjar du med att läsa guiden för [konfigurera en utvecklarmiljö](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Det här dokumentet innehåller konfigurationsinstruktioner som gör att du kan utveckla för tjänsten Asset compute.
