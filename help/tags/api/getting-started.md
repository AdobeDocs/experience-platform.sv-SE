---
title: Autentisera och få åtkomst till Reactor API
description: Lär dig hur du kommer igång med Reaktors-API, inklusive steg för att generera nödvändiga inloggningsuppgifter.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Autentisera och få åtkomst till Reactor API

För att kunna använda [Reaktors-API](https://developer.adobe.com/experience-platform-apis/references/reactor/) Om du vill skapa och hantera taggtillägg måste varje begäran innehålla följande autentiseringsrubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Den här guiden beskriver hur du använder Adobe Developer Console för att samla in värdena för vart och ett av dessa rubriker så att du kan börja anropa Reactor API.

## Få utvecklare tillgång till Adobe Experience Platform {#gain-developer-access}

Innan du kan generera autentiseringsvärden för Reactor API måste du ha utvecklaråtkomst till Experience Platform. Följ de inledande stegen i dialogrutan för att få utvecklaråtkomst [Självstudiekurs om autentisering av Experience Platform](/help/landing/api-authentication.md). När du är klar med [Få användaråtkomst](/help/landing/api-authentication.md#gain-user-access) går du tillbaka till den här självstudiekursen för att generera de specifika autentiseringsuppgifterna för Reactor API.

## Generera autentiseringsuppgifter {#generate-access-credentials}

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Organisationens ID (`{ORG_ID}`) och API-nyckel (`{API_KEY}`) kan återanvändas i framtida API-anrop efter att de ursprungligen har skapats. Din åtkomsttoken (`{ACCESS_TOKEN}`) är tillfälligt och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

### Engångskonfiguration {#one-time-setup}

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i Developer Console-dokumentationen.

När du har skapat ett projekt väljer du **Lägg till API** på **Projektöversikt** skärm.

![](../images/api/getting-started/add-api-button.png)

The **Lägg till ett API** visas. Välj **EXPERIENCE PLATFORM LAUNCH API** i listan med tillgängliga API:er innan du väljer **Nästa**.

![](../images/api/getting-started/add-launch-api.png)

Välj sedan autentiseringstypen för att generera åtkomsttoken och få åtkomst till Experience Platform-API:t.

>[!IMPORTANT]
>
>Välj **[!UICONTROL OAuth Server-to-Server]** eftersom det här är den enda metod som stöds för att gå framåt. The **[!UICONTROL Service Account (JWT)]** -metoden är inaktuell. Även om integreringar med JWT-autentiseringsmetoden fortsätter att fungera fram till 1 januari 2025 rekommenderar Adobe starkt att du migrerar befintliga integreringar till den nya OAuth Server-till-Server-metoden före detta datum. Hämta mer information i avsnittet [!BADGE Föråldrat]{type=negative}[Generera en JSON-webbtoken (JWT)](/help/landing/api-authentication.md#jwt) i självstudiekursen om autentisering av plattforms-API.

Välj **Nästa** för att fortsätta.

![Välj autentiseringsmetoden OAuth Server-till-server.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

På nästa skärm får du en uppmaning om att välja en eller flera produktprofiler som ska associeras med API-integreringen.

>[!NOTE]
>
Produktprofiler hanteras av er organisation via Adobe Admin Console och innehåller specifika behörighetsgrupper för detaljfunktioner. Produktprofiler och deras behörigheter kan bara hanteras av användare med administratörsbehörighet inom organisationen. Om du är osäker på vilka produktprofiler du ska välja för API kontaktar du administratören.

Välj önskade produktprofiler i listan och välj sedan **Spara konfigurerat API** för att slutföra API-registreringen.

![](../images/api/getting-started/select-product-profile.png)

### Samla in inloggningsuppgifter {#gather-credentials}

När API:t har lagts till i projektet **[!UICONTROL Experience Platform API]** På projektsidan visas följande autentiseringsuppgifter som krävs för alla anrop till API:er för Experience Platform:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![Integreringsinformation när du har lagt till ett API i Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Generera en åtkomsttoken {#generate-access-token}

Nästa steg är att skapa en `{ACCESS_TOKEN}` autentiseringsuppgifter för användning i API-anrop för plattformar. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda Platform API:er.

>[!TIP]
>
Dessa token upphör att gälla efter 24 timmar. Om du använder den här integreringen för ett program är det en bra idé att hämta din innehavartoken programmatiskt inifrån programmet.

Det finns två alternativ för att generera åtkomsttoken, beroende på hur du använder dem:

* [Generera tokens manuellt](#manual)
* [Automatisera generering av token](#auto-token)

#### Generera åtkomsttoken manuellt {#manual}

Generera en ny `{ACCESS_TOKEN}`, navigera till **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** och markera **[!UICONTROL Generate access token]**, vilket visas nedan.

![Skärminspelning av hur och åtkomsttoken genereras i användargränssnittet för Developer Console.](/help/tags/images/api/getting-started/generate-access-token.gif)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för det obligatoriska auktoriseringshuvudet och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

#### Automatisera generering av token {#auto-token}

Du kan också använda en Postman-miljö och en samling för att generera åtkomsttoken. Läs mer om [använda Postman för att autentisera och testa API-anrop](/help/landing/api-authentication.md#use-postman) i autentiseringsguiden för Experience Platform API.

## Testa API-autentiseringsuppgifter {#test-api-credentials}

Om du följer stegen i den här självstudiekursen bör du ha giltiga värden för `{ORG_ID}`, `{API_KEY}`och `{ACCESS_TOKEN}`. Du kan nu testa dessa värden genom att använda dem i en enkel cURL-begäran till Reactor API.

Börja med att försöka göra ett API-anrop till [lista alla företag](./endpoints/companies.md#list).

>[!NOTE]
>
Du kanske inte har några företag i din organisation, och då är svaret HTTP-status 404 (Hittades inte). Så länge du inte får ett 403-fel (Ej tillåtet) är dina inloggningsuppgifter giltiga och fungerar.

När du har bekräftat att dina inloggningsuppgifter fungerar kan du fortsätta att utforska den andra API-referensdokumentationen och lära dig API:ts många funktioner.

## Läser exempel-API-anrop {#read-sample-api-calls}

Varje slutpunktshandbok innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/api-guide.md#sample-api) i komma igång-guiden för Platform API:er.

## Nästa steg {#next-steps}

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till Reaktors API. Välj någon av slutpunktsguiderna för att komma igång:

* [Referenshandbok för Reaktors-API](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Översikt över API-guide för reaktor](/help/tags/api/overview.md)
