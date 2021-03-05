---
keywords: Experience Platform;startsida;populära ämnen;Adobe Experience Platform;api guide;platform api guide;introduktion till plattform;utvecklarguide
solution: Experience Platform
title: Postman i Adobe Experience Platform
topic: api guide
description: Det här dokumentet innehåller steg som beskriver hur du konfigurerar en Postman-miljö, importerar Postman-samlingar och en lista över tillgängliga samlingar för varje plattformstjänst.
translation-type: tm+mt
source-git-commit: effc8fef666ffbf62c2e0874d048245f19c12111
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Postman i Adobe Experience Platform

Postman är en samarbetsplattform för API-utveckling som gör att du kan konfigurera miljöer med förinställda variabler, dela API-samlingar, effektivisera CRUD-begäranden och mycket annat. De flesta Platform API-tjänster har Postman-samlingar som kan användas för att göra API-anrop.

## Så här konfigurerar du en Postman-miljö för Experience Platform

Följande videoguide visar hur du skapar och konfigurerar Postman-miljön. En Postman-miljö innehåller alla de rubriker som behövs för att du ska kunna göra API-anrop till de olika samlingarna nedan. När du har konfigurerat det kan du när som helst uppdatera det aktuella värdet i miljön när ett värde förfaller (till exempel `ACCESS_TOKEN`) och det nya värdet används i alla dina samlingar.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-samlingar {#collections}

En mapp som innehåller alla tillgängliga Postman-samlingar finns på [Experience Platform Postman samples GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). En Postman-samlingslänk kan också hittas i varje enskild swagger-fil i [API-referensdokumentationen](http://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

Om du vill hämta en Postman-samling väljer du **[!DNL Raw]** på GitHub-sidan för att läsa in raw-JSON-filen på en ny flik. Högerklicka sedan och välj **[!DNL Save as]** för att spara filen på ett lokalt mål som du väljer.

![råformat JSON](./images/api-guide/raw-collection.PNG)

## Importera en Postman-samling {#import}

För att kunna använda en [Postman-samling](#collections) måste du ha en miljö konfigurerad. När du är klar med konfigurationen av miljön väljer du **[!DNL Manage Environments]**-väljaren i det övre högra hörnet.

![hantera miljöväljare](./images/api-guide/environment-selector.png)

En pover visas och visar alla dina aktuella miljöer. Om du vill importera en samling väljer du **[!DNL import]** .

![importknapp](./images/api-guide/import-collection.png)

Du uppmanas att välja en fil som ska importeras. Markera den Postman-samlingsfil som du vill importera. När du har valt samlingen fylls den i i den vänstra listen på fliken Samlingar.

![populär samling](./images/api-guide/imported-collection.png)

Varje samling har olika nyckelvärdepar som kan behövas för att utföra en lyckad CRUD-åtgärd. Läs tjänstens [API-utvecklarguide](api-guide.md#api-guides) om du vill veta mer om obligatoriska värden, tips och se exempel.

Läs mer om Postman-gränssnittet och dess tillgängliga funktioner i [Postman-dokumentationen](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generera en åtkomsttoken med Postman för icke-produktionsbruk

>[!WARNING]
>
>Som noterades i Postman-samlingen för Adobe I/O-åtkomsttoken är de angivna genereringsmetoderna lämpliga för **icke-produktionsanvändning**. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

I videon nedan används [Adobe I/O-åtkomsttokengenereringssamlingen](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) som kan hämtas från den offentliga GitHub-databasen.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nästa steg

I det här dokumentet introducerades Postman-miljöer, samlingar och hur du importerar samlingar. Nu när du är klar med Postman kan du gå till [guiden ](api-guide.md) Komma igång med plattformen om du vill ha information om obligatoriska rubriker, exempel och en lista över [API-guider](api-guide.md#api-guides) som är tillgängliga för respektive plattformstjänst.