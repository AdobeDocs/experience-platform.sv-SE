---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service developer guide
description: Använd RESTful API för att hantera personuppgifter för dina registrerade i olika Adobe Experience Cloud-program
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# [!DNL Privacy Service] utvecklarhandbok

Adobe Experience Platform [!DNL Privacy Service] har ett RESTful-API och användargränssnitt som gör att du kan hantera (komma åt och ta bort) personuppgifter för dina registrerade (kunder) i alla Adobe Experience Cloud-program. [!DNL Privacy Service] har också en central mekanism för granskning och loggning som gör att du kan komma åt status och resultat för jobb som innefattar [!DNL Experience Cloud] program.

I den här handboken beskrivs hur du använder [!DNL Privacy Service] API:t. Mer information om hur du använder användargränssnittet finns i översikten över användargränssnittet för [Privacy Service](../ui/overview.md). En fullständig lista över alla tillgängliga slutpunkter i [!DNL Privacy Service] API finns i [API-referensen](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande [!DNL Experience Platform] funktioner:

* [[!DNL-Privacy Service]](../home.md): Tillhandahåller ett RESTful-API och användargränssnitt som gör att du kan hantera förfrågningar från registrerade (kunder) i olika Adobe Experience Cloud-program.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa Privacy Service-API:t.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md) i [!DNL Experience Platform] felsökningsguiden.

## Samla in värden för obligatoriska rubriker

För att kunna anropa API:t måste du först samla in dina inloggningsuppgifter och använda dem i obligatoriska rubriker: [!DNL Privacy Service]

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Detta innebär att du måste skaffa utvecklarbehörigheter för [!DNL Experience Platform] i Adobe Admin Console och sedan generera autentiseringsuppgifterna i Adobe Developer Console.

### Få utvecklare åtkomst till [!DNL Experience Platform]

Följ de inledande stegen i självstudiekursen för autentisering av [!DNL Platform]Experience Platform för att få utvecklaråtkomst till [](../../tutorials/authentication.md). När du kommit till steget&quot;Generera autentiseringsuppgifter för åtkomst i Adobe Developer Console&quot; går du tillbaka till den här självstudiekursen för att generera autentiseringsuppgifter för [!DNL Privacy Service].

### Generera autentiseringsuppgifter för åtkomst

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ditt `{IMS_ORG}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida API-anrop. Ditt `{ACCESS_TOKEN}` är dock tillfälligt och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

#### Engångskonfiguration

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om hur du [skapar ett tomt projekt](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt klickar du **[!UICONTROL Add API]** på _[!UICONTROL Project Overview]_skärmen.

![](../images/api/getting-started/add-api-button.png)

Skärmen visas _[!UICONTROL Add an API]_. Välj **[!UICONTROL Privacy Service API]**i listan med tillgängliga API:er innan du klickar på&#x200B;**[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Skärmen visas _[!UICONTROL Configure API]_. Välj alternativet att **[!UICONTROL Generate a key pair]**markera och klicka sedan **[!UICONTROL Generate keypair]**i det nedre högra hörnet.

![](../images/api/getting-started/generate-key-pair.png)

Nyckelparet genereras automatiskt och en ZIP-fil som innehåller en privat nyckel och ett offentligt certifikat hämtas till din lokala dator (som kan användas i ett senare steg). Välj **[!UICONTROL Save configured API]** för att slutföra konfigurationen.

![](../images/api/getting-started/key-pair-generated.png)

När API:t har lagts till i projektet visas projektsidan igen på _Privacy Service-API:ts översiktssida_ . Här bläddrar du nedåt till _[!UICONTROL Service Account (JWT)]_avsnittet som innehåller följande åtkomstautentiseringsuppgifter som krävs för alla anrop till[!DNL Privacy Service]API:

* **[!UICONTROL CLIENT ID]**: Klient-ID är det som krävs `{API_KEY}` för detta måste anges i x-api-key-huvudet.
* **[!UICONTROL ORGANIZATION ID]**: Organisations-ID är det `{IMS_ORG}` värde som måste användas i rubriken x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autentisering för varje session

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`, som används i auktoriseringshuvudet. Till skillnad från värdena för `{API_KEY}` och `{IMS_ORG}`måste en ny token genereras var 24:e timme för att kunna fortsätta använda [!DNL Platform] API:er.

Om du vill skapa en ny `{ACCESS_TOKEN}`nyckel öppnar du den tidigare hämtade privata nyckeln och klistrar in innehållet i textrutan bredvid _[!UICONTROL Generate access token]_innan du klickar **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för det obligatoriska auktoriseringshuvudet och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Nästa steg

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till [!DNL Privacy Service] API:t. Dokumentet om [sekretessjobb](privacy-jobs.md) går igenom de olika API-anrop du kan göra med [!DNL Privacy Service] API:t. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.
