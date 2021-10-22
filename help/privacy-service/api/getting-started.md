---
title: Komma igång med Privacy Services-API
description: Lär dig hur du autentiserar till Privacy Service-API:t och hur du tolkar exempel-API-anrop i dokumentationen.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 6dcbf2df46ba35104abd9c4e6412799e77c9c49f
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Komma igång med Privacy Services-API

Den här guiden ger en introduktion till de centrala koncept du behöver känna till innan du försöker ringa anrop till Privacy Services-API:t.

## Förutsättningar

Handboken kräver en fungerande förståelse av följande funktioner:

* [Adobe Experience Platform Privacy Service](../home.md): Tillhandahåller ett RESTful-API och användargränssnitt som gör att du kan hantera förfrågningar från registrerade (kunder) i olika Adobe Experience Cloud-program.

## Samla in värden för obligatoriska rubriker

För att kunna anropa Privacy Service-API:t måste du först samla in dina inloggningsuppgifter och använda dem i obligatoriska rubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Detta innebär att du måste skaffa utvecklarbehörigheter för Adobe Experience Platform i Adobe Admin Console och sedan generera autentiseringsuppgifterna i Adobe Developer Console.

### Få utvecklare åtkomst till Experience Platform

Få utvecklare åtkomst till [!DNL Platform]följer du de inledande stegen i [Självstudiekurs om autentisering av Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). När du kommer till steget&quot;Generera autentiseringsuppgifter för åtkomst i Adobe Developer Console&quot; går du tillbaka till den här självstudiekursen för att generera autentiseringsuppgifter för Privacy Servicen.

### Generera autentiseringsuppgifter för åtkomst

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Dina `{IMS_ORG}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida API-anrop. Men `{ACCESS_TOKEN}` är tillfälligt och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

#### Engångskonfiguration

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add API]** på **[!UICONTROL Project Overview]** skärm.

![](../images/api/getting-started/add-api-button.png)

The **[!UICONTROL Add an API]** visas. Välj **[!UICONTROL Privacy Service API]** i listan med tillgängliga API:er innan du väljer **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

The **[!UICONTROL Configure API]** visas. Välj alternativet att **[!UICONTROL Generate a key pair]** väljer **[!UICONTROL Generate keypair]** i det nedre högra hörnet.

![](../images/api/getting-started/generate-key-pair.png)

Nyckelparet genereras automatiskt och en ZIP-fil som innehåller en privat nyckel och ett offentligt certifikat hämtas till din lokala dator (som kan användas i ett senare steg). Välj **[!UICONTROL Save configured API]** för att slutföra konfigurationen.

![](../images/api/getting-started/key-pair-generated.png)

När API:t har lagts till i projektet visas projektsidan igen på sidan **Översikt över Privacy Service-API** sida. Här rullar du nedåt till **[!UICONTROL Service Account (JWT)]** som innehåller följande åtkomstautentiseringsuppgifter som krävs i alla anrop till Privacy Service-API:

* **[!UICONTROL CLIENT ID]**: Klient-ID krävs `{API_KEY}` för det måste anges i rubriken x-api-key.
* **[!UICONTROL ORGANIZATION ID]**: Organisations-ID är `{IMS_ORG}` värde som måste användas i huvudet x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autentisering för varje session

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`, som används i auktoriseringshuvudet. Till skillnad från värdena för `{API_KEY}` och `{IMS_ORG}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda [!DNL Platform] API:er.

Så här skapar du en ny `{ACCESS_TOKEN}`öppnar du den tidigare hämtade privata nyckeln och klistrar in innehållet i textrutan bredvid **[!UICONTROL Generate access token]** före markering **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för begärd auktoriseringshuvud och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/api-guide.md#sample-api) i komma igång-guiden för Platform API:er.

## Nästa steg

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till Privacy Service-API:t. Välj någon av slutpunktsguiderna för att komma igång:

* [Sekretessjobb](./privacy-jobs.md)
* [Godkännande](./consent.md)
