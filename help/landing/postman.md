---
keywords: Experience Platform;startsida;populära ämnen;Adobe Experience Platform;api guide;platform api guide;introduktion till plattform;utvecklarguide
solution: Experience Platform
title: Postman i Adobe Experience Platform
description: Det här dokumentet innehåller steg som beskriver hur du konfigurerar en Postman-miljö, importerar Postman-samlingar och en lista över tillgängliga samlingar för varje plattformstjänst.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Postman i Adobe Experience Platform

Postman är en samarbetsplattform för API-utveckling som gör att du kan konfigurera miljöer med förinställda variabler, dela API-samlingar, effektivisera CRUD-begäranden och mycket annat. De flesta Platform API-tjänster har Postman-samlingar som kan användas för att göra API-anrop.

## Konfigurera en Postman-miljö för Experience Platform

Följande videoguide visar hur du skapar och konfigurerar din Postman-miljö. En Postman-miljö innehåller alla de rubriker du behöver för att göra API-anrop till de olika samlingarna nedan. När du väl har ställt in ett värde upphör det att gälla (t.ex. `ACCESS_TOKEN`) kan du uppdatera det aktuella värdet i miljön och det nya värdet används i alla dina samlingar.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-samlingar {#collections}

En mapp som innehåller alla Postman-samlingar finns på [Experience Platform Postman-exempel GitHub-databas](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). En Postman-samlingslänk kan också hittas i varje enskild swagger-fil i [API-referensdokumentation](https://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

Om du vill hämta en Postman-samling väljer du **[!DNL Raw]** från GitHub-sidan för att läsa in JSON-råfilen på en ny flik. Högerklicka och välj sedan **[!DNL Save as]** om du vill spara filen på ett lokalt mål.

![råformat JSON](./images/api-guide/raw-collection.PNG)

## Importera en Postman-samling {#import}

För att kunna använda en [Postman Collection](#collections)måste du ha en miljö konfigurerad. När du är klar väljer du **[!DNL Manage Environments]** i det övre högra hörnet.

![hantera miljöväljare](./images/api-guide/environment-selector.png)

En pover visas och visar alla dina aktuella miljöer. Om du vill importera en samling väljer du **[!DNL import]** .

![importknapp](./images/api-guide/import-collection.png)

Du uppmanas att välja en fil som ska importeras. Markera den Postman-samlingsfil som du vill importera. När du har valt samlingen fylls den i i den vänstra listen på fliken Samlingar.

![populär samling](./images/api-guide/imported-collection.png)

Varje samling har olika nyckelvärdepar som kan behövas för att utföra en lyckad CRUD-åtgärd. Granska tjänstens [Utvecklarhandbok för API](api-guide.md#api-guides) om du vill veta mer om obligatoriska värden, tips och se exempel.

Läs mer om Postman användargränssnitt och dess tillgängliga funktioner på [Postman-dokumentation](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generera en åtkomsttoken med Postman för icke-produktionsbruk

>[!WARNING]
>
>Som framgår av Identity Management Service (IMS) Postman Collection är de angivna generationsmetoderna lämpliga för **icke-produktionsbruk**. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

I videon nedan används [Identity Management Service (IMS) Postman-samling](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) som kan hämtas från den offentliga GitHub-databasen.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nästa steg

I det här dokumentet introducerades Postman-miljöer, samlingar och hur du importerar samlingar. Nu när du har Postman klar kan du gå till [Starthandbok för plattformen](api-guide.md) för information om obligatoriska rubriker, exempel och en lista med [API-guider](api-guide.md#api-guides) för varje plattformstjänst.
