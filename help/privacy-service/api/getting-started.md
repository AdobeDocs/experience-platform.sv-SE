---
title: Autentisera och få åtkomst till Privacy Services-API
description: Lär dig hur du autentiserar till Privacy Service-API:t och hur du tolkar exempel-API-anrop i dokumentationen.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# Autentisera och få åtkomst till Privacy Services-API

Den här guiden ger en introduktion till de centrala koncept du måste känna till innan du försöker ringa anrop till Adobe Experience Platform Privacy Service API.

## Förutsättningar {#prerequisites}

Den här guiden kräver en fungerande förståelse av [Privacy Service](../home.md) och hur det gör det möjligt att hantera förfrågningar från registrerade (kunder) i olika Adobe Experience Cloud-program.

För att kunna skapa åtkomstautentiseringsuppgifter för API:t måste en administratör i organisationen tidigare ha konfigurerat produktprofiler för Privacy Service inom Adobe Admin Console. Den produktprofil som du tilldelar en API-integrering avgör vilka behörigheter som integreringen har för att komma åt Privacy Servicens funktioner. Se guiden på [hantera behörigheter för Privacy Service](../permissions.md) för mer information.

## Samla in värden för obligatoriska rubriker {#gather-values-required-headers}

För att kunna anropa Privacy Service-API:t måste du först samla in dina inloggningsuppgifter och använda dem i obligatoriska rubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dessa värden genereras med [Adobe Developer Console](https://developer.adobe.com/console). Dina `{ORG_ID}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida API-anrop. Men `{ACCESS_TOKEN}` är tillfälligt och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

### Engångskonfiguration {#one-time-setup}

Gå till [Adobe Developer Console](https://developer.adobe.com/console) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i Developer Console-dokumentationen.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add to Project]** och välja **[!UICONTROL API]** i listrutan.

![Det API-alternativ som väljs på menyn [!UICONTROL Add to Project] listruta från sidan med projektinformation i Developer Console](../images/api/getting-started/add-api-button.png)

#### Markera Privacy Service-API:t {#select-privacy-service-api}

The **[!UICONTROL Add an API]** visas. Välj **[!UICONTROL Experience Cloud]** om du vill begränsa listan med tillgängliga API:er väljer du kort för **[!UICONTROL Privacy Service API]** före markering **[!UICONTROL Next]**.

![Privacy Service-API-kortet som väljs i listan över tillgängliga API:er](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Välj **[!UICONTROL View docs]** alternativ för att navigera i ett separat webbläsarfönster till det fullständiga [Referenshandbok för Privacy Services-API](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

Välj sedan autentiseringstypen för att generera åtkomsttoken och få åtkomst till Privacy Service-API:t.

>[!IMPORTANT]
>
>Välj **[!UICONTROL OAuth Server-to-Server]** eftersom det här är den enda metod som stöds för att gå framåt. The **[!UICONTROL Service Account (JWT)]** -metoden är inaktuell. Även om integreringar med JWT-autentiseringsmetoden fortsätter att fungera fram till 1 januari 2025 rekommenderar Adobe starkt att du migrerar befintliga integreringar till den nya OAuth Server-till-Server-metoden före detta datum. Hämta mer information i avsnittet [!BADGE Föråldrat]{type=negative}[Generera en JSON-webbtoken (JWT)](/help/landing/api-authentication.md#jwt).

![Välj autentiseringsmetoden OAuth Server-to-Server.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Tilldela behörigheter via produktprofiler {#product-profiles}

Det sista konfigurationssteget är att välja de produktprofiler som den här integreringen ska ärva sina behörigheter från. Om du väljer mer än en profil kombineras deras behörighetsgrupper för integreringen.

>[!NOTE]
>
Produktprofiler och de detaljerade behörigheter de ger skapas och hanteras av administratörer via Adobe Admin Console. Se guiden på [Behörigheter för Privacy Service](../permissions.md) för mer information.

När du är klar väljer du **[!UICONTROL Save configured API]**.

![En enskild produktprofil väljs från listan innan konfigurationen sparas](../images/api/getting-started/select-product-profiles.png)

När API:t har lagts till i projektet **[!UICONTROL Privacy Service API]** På projektsidan visas följande autentiseringsuppgifter som krävs för alla anrop till API:er för Privacy Service:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![Integreringsinformation när du har lagt till ett API i Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Autentisering för varje session {#authentication-each-session}

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`, som används i auktoriseringshuvudet. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda API:t.

I allmänhet finns det två metoder för att generera en åtkomsttoken:

* [Generera token manuellt](#manual-token) för testning och utveckling.
* [Automatisera generering av token](#auto-token) för API-integreringar.

#### Generera en token manuellt {#manual-token}

Generera en ny `{ACCESS_TOKEN}`, navigera till **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** och markera **[!UICONTROL Generate access token]**, vilket visas nedan.

![En skärminspelning av hur en åtkomsttoken genereras i användargränssnittet för utvecklarkonsolen.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för det obligatoriska [!DNL Authorization] och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

#### Automatisera generering av token {#auto-token}

Du kan också använda en Postman-miljö och en samling för att generera åtkomsttoken. Läs mer om [använda Postman för att autentisera och testa API-anrop](/help/landing/api-authentication.md#use-postman) i autentiseringsguiden för Experience Platform API.

## Läser exempel-API-anrop {#read-sample-api-calls}

Varje slutpunktshandbok innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/api-guide.md#sample-api) i komma igång-guiden för Platform API:er.

## Nästa steg {#next-steps}

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till Privacy Service-API:t. Välj någon av slutpunktsguiderna för att komma igång:

* [Sekretessjobb](./privacy-jobs.md)
* [Godkännande](./consent.md)
