---
title: Komma igång med Privacy Services-API
description: Lär dig hur du autentiserar till Privacy Service-API:t och hur du tolkar exempel-API-anrop i dokumentationen.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Komma igång med Privacy Services-API

Den här guiden ger en introduktion till de centrala koncept du behöver känna till innan du försöker ringa anrop till Adobe Experience Platform Privacy Service API.

## Förutsättningar

Den här guiden kräver en fungerande förståelse av [Privacy Service](../home.md) och hur det gör det möjligt att hantera förfrågningar från registrerade (kunder) i olika Adobe Experience Cloud-program.

För att kunna skapa åtkomstautentiseringsuppgifter för API:t måste en administratör i organisationen tidigare ha konfigurerat produktprofiler för Privacy Service inom Adobe Admin Console. Den produktprofil som du tilldelar en API-integrering avgör vilka behörigheter som integreringen har för att komma åt Privacy Servicens funktioner. Se guiden [hantera behörigheter för Privacy Service](../permissions.md) för mer information.

## Samla in värden för obligatoriska rubriker

För att kunna anropa Privacy Service-API:t måste du först samla in dina inloggningsuppgifter och använda dem i obligatoriska rubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dessa värden genereras med [Adobe Developer Console](https://developer.adobe.com/console). Dina `{ORG_ID}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida API-anrop. Men `{ACCESS_TOKEN}` är tillfälligt och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

### Engångskonfiguration

Gå till [Adobe Developer Console](https://developer.adobe.com/console) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i Developer Console-dokumentationen.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add to Project]** och välja **[!UICONTROL API]** i listrutan.

![Det API-alternativ som väljs på menyn [!UICONTROL Add to Project] listruta från sidan med projektinformation i Developer Console](../images/api/getting-started/add-api-button.png)

#### Välj ett API och generera ett nyckelpar {#keypair}

The **[!UICONTROL Add an API]** visas. Välj **[!UICONTROL Experience Cloud]** om du vill begränsa listan med tillgängliga API:er väljer du kort för **[!UICONTROL Privacy Service API]** före markering **[!UICONTROL Next]**.

![Privacy Service-API-kortet som väljs i listan över tillgängliga API:er](../images/api/getting-started/add-privacy-service-api.png)

The **[!UICONTROL Configure API]** visas. Välj alternativet att **[!UICONTROL Generate a key pair]** väljer **[!UICONTROL Generate keypair]**.

![The [!UICONTROL Generate a key pair] det alternativ som markeras på [!UICONTROL Configure API] screen](../images/api/getting-started/generate-key-pair.png)

Nyckelparet genereras automatiskt och en ZIP-fil som innehåller en privat nyckel och ett offentligt certifikat hämtas av webbläsaren (används i ett senare steg). Välj **[!UICONTROL Next]** för att fortsätta.

![Det genererade nyckelpar som visas i användargränssnittet, vars värden hämtas automatiskt av webbläsaren](../images/api/getting-started/key-pair-generated.png)

#### Tilldela behörigheter via produktprofiler {#product-profiles}

Det sista konfigurationssteget är att välja de produktprofiler som den här integreringen ska ärva sina behörigheter från. Om du väljer mer än en profil kombineras deras behörighetsgrupper för integreringen.

>[!NOTE]
>
>Produktprofiler och de detaljerade behörigheter de ger skapas och hanteras av administratörer via Adobe Admin Console. Se guiden [Behörigheter för Privacy Service](../permissions.md) för mer information.

När du är klar väljer du **[!UICONTROL Save configured API]**.

![En enskild produktprofil väljs från listan innan konfigurationen sparas](../images/api/getting-started/select-product-profiles.png)

När API:t har lagts till i projektet visas projektsidan igen på sidan **Översikt över Privacy Service-API** sida. Här rullar du nedåt till **[!UICONTROL Service Account (JWT)]** som innehåller följande åtkomstautentiseringsuppgifter som krävs för alla anrop till Privacy Service-API:

* **[!UICONTROL CLIENT ID]**: Klient-ID krävs `{API_KEY}` som ska anges i `x-api-key` header.
* **[!UICONTROL ORGANIZATION ID]**: Organisations-ID är `{ORG_ID}` värde som måste användas i `x-gw-ims-org-id` header.

![Värdena för klient-ID och organisations-ID som de visas på projektöversiktssidan efter att API:t har konfigurerats](../images/api/getting-started/jwt-credentials.png)

### Autentisering för varje session

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`, som används i auktoriseringshuvudet. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda API:t.

I allmänhet finns det två metoder för att generera en åtkomsttoken:

* [Generera token manuellt](#manual-token) för testning och utveckling.
* [Automatisera generering av token](#auto-token) för API-integreringar.

#### Generera en token manuellt {#manual-token}

Generera en ny `{ACCESS_TOKEN}`öppnar du den tidigare hämtade privata nyckeln och klistrar in innehållet i textrutan bredvid **[!UICONTROL Generate access token]** före markering **[!UICONTROL Generate Token]**.

![Tidigare genererad åtkomsttoken klistras in på projektets översiktssida med [!UICONTROL Generate Token] knappen markeras efter](../images/api/getting-started/paste-private-key.png)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för begärd auktoriseringshuvud och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

![Den genererade åtkomsttoken som kopieras från användargränssnittet](../images/api/getting-started/generated-access-token.png)

#### Automatisera generering av token {#auto-token}

Du kan generera nya åtkomsttoken för automatiserade processer genom att skicka en JSON Web Token (JWT) via en POST-begäran till Adobe Identity Management-tjänsten (IMS). Se Developer Console-dokumentet på [JWT-autentisering](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) för detaljerade steg.

## Läser exempel-API-anrop

Varje slutpunktshandbok innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/api-guide.md#sample-api) i komma igång-guiden för Platform API:er.

## Nästa steg

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till Privacy Service-API:t. Välj någon av slutpunktsguiderna för att komma igång:

* [Sekretessjobb](./privacy-jobs.md)
* [Godkännande](./consent.md)
