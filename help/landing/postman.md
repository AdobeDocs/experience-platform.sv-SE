---
keywords: Experience Platform;startsida;populära ämnen;Adobe Experience Platform;api guide;platform api guide;introduktion till plattform;utvecklarguide
solution: Experience Platform
title: POSTMAN i ADOBE EXPERIENCE PLATFORM
description: Det här dokumentet innehåller steg som beskriver hur du konfigurerar en Postman-miljö, importerar Postman-samlingar och en lista över tillgängliga samlingar för varje plattformstjänst.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# POSTMAN i ADOBE EXPERIENCE PLATFORM

Postman är en samarbetsplattform för API-utveckling som gör att du kan konfigurera miljöer med förinställda variabler, dela API-samlingar, effektivisera CRUD-begäranden och mycket annat. De flesta Platform API-tjänster har Postman-samlingar som kan användas för att göra API-anrop.

## Konfigurera en Postman-miljö för Experience Platform

Följande videoguide visar hur du skapar och konfigurerar din Postman-miljö. En Postman-miljö innehåller alla de rubriker du behöver för att göra API-anrop till de olika samlingarna nedan. När du har konfigurerat det kan du uppdatera det aktuella värdet i miljön när ett värde upphör att gälla (till exempel `ACCESS_TOKEN`) och det nya värdet används i alla dina samlingar.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-samlingar {#collections}

En mapp som innehåller alla tillgängliga Postman-samlingar finns på [Experience Platform Postman-exempeldatabasen ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). En Postman-samlingslänk kan också hittas i varje enskild swagger-fil i [API-referensdokumentationen](https://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

Om du vill hämta en Postman-samling väljer du **[!DNL Raw]** på GitHub-sidan för att läsa in JSON-råfilen på en ny flik. Högerklicka sedan och välj **[!DNL Save as]** för att spara filen på ett lokalt mål som du väljer.

![rå JSON](./images/api-guide/raw-collection.PNG)

## Importera en Postman-samling {#import}

För att kunna använda en [Postman-samling](#collections) måste du ha en miljö konfigurerad. När du har slutfört miljökonfigurationen väljer du **[!DNL Manage Environments]**-väljaren i det övre högra hörnet.

![hantera miljöväljare](./images/api-guide/environment-selector.png)

En pover visas och visar alla dina aktuella miljöer. Om du vill importera en samling väljer du **[!DNL import]** .

![importknapp](./images/api-guide/import-collection.png)

Du uppmanas att välja en fil som ska importeras. Markera den Postman-samlingsfil som du vill importera. När du har valt samlingen fylls den i i den vänstra listen på fliken Samlingar.

![fylld samling](./images/api-guide/imported-collection.png)

Varje samling har olika nyckelvärdepar som kan behövas för att utföra en lyckad CRUD-åtgärd. Läs tjänstens [API-utvecklarhandbok](api-guide.md#api-guides) om du vill veta mer om obligatoriska värden, tips och se exempel.

Mer information om användargränssnittet i Postman och dess tillgängliga funktioner finns i [Postman-dokumentationen](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generera en åtkomsttoken med Postman för icke-produktionsbruk

>[!WARNING]
>
>Som framgår av Postman-samlingen för Identity Management-tjänsten (IMS) är de angivna genereringsmetoderna lämpliga för **icke-produktionsanvändning**. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

I videon nedan används Postman-samlingen [Identity Management Service (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) som kan hämtas från den offentliga GitHub-databasen.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nästa steg

I det här dokumentet introducerades Postman-miljöer, samlingar och hur du importerar samlingar. Nu när du är klar med Postman kan du gå till [handboken Komma igång för plattformen](api-guide.md) och få information om vilka sidhuvuden, exempel och en lista över [API-guider](api-guide.md#api-guides) som är tillgängliga för respektive plattformstjänst.
