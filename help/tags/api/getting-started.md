---
title: Autentisera och få åtkomst till Reactor API
description: Lär dig hur du kommer igång med Reaktors-API, inklusive steg för att generera nödvändiga inloggningsuppgifter.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 31e52dce23c558aaba822fe27d2e58ed6a7ce18d
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Autentisera och få åtkomst till Reactor API

Om du vill använda [Reaktors-API](https://developer.adobe.com/experience-platform-apis/references/reactor/) för att skapa och hantera taggtillägg måste varje begäran innehålla följande autentiseringsrubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`
* `Accept: application/vnd.api+json;revision=1`
* `Content-Type: application/vnd.api+json`

Den här guiden beskriver hur du använder Adobe Developer Console för att samla in värdena för vart och ett av dessa rubriker så att du kan börja anropa Reactor API.

## Få utvecklare tillgång till Adobe Experience Platform {#gain-developer-access}

Innan du kan generera autentiseringsvärden för Reactor API måste du ha utvecklaråtkomst till Experience Platform. Följ de inledande stegen i [Experience Platform-självstudiekursen](/help/landing/api-authentication.md) för att få utvecklaråtkomst. När du har slutfört steget [Få tillgång till användare](/help/landing/api-authentication.md#gain-user-access) går du tillbaka till den här självstudiekursen för att generera de specifika autentiseringsuppgifterna för Reactor API.

## Generera autentiseringsuppgifter {#generate-access-credentials}

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Organisationens ID (`{ORG_ID}`) och API-nyckel (`{API_KEY}`) kan återanvändas i framtida API-anrop efter att de först har genererats. Åtkomsttoken (`{ACCESS_TOKEN}`) är tillfällig och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

### Engångskonfiguration {#one-time-setup}

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om att [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i Developer Console-dokumentationen.

När du har skapat ett projekt väljer du **Lägg till API** på skärmen **Projektöversikt**.

![](../images/api/getting-started/add-api-button.png)

Skärmen **Lägg till ett API** visas. Välj **API:t för start av Experience Platform** i listan med tillgängliga API:er innan du väljer **Nästa**.

![](../images/api/getting-started/add-launch-api.png)

Välj sedan autentiseringstypen för att generera åtkomsttoken och få åtkomst till Experience Platform API.

>[!IMPORTANT]
>
>Välj metoden **[!UICONTROL OAuth Server-to-Server]** eftersom det här är den enda metod som stöds för att gå framåt. Metoden **[!UICONTROL Service Account (JWT)]** är föråldrad. Integreringar som använder JWT-autentiseringsmetoden fortsätter att fungera fram till 1 januari 2025, men Adobe rekommenderar starkt att du migrerar befintliga integreringar till den nya OAuth Server-till-Server-metoden före detta datum. Mer information finns i avsnittet [!BADGE Föråldrat]{type=negative} [Generera en JSON-webbtoken (JWT)](/help/landing/api-authentication.md#jwt) i självstudiekursen om Experience Platform API-autentisering.

Välj **Nästa** för att fortsätta.

![Välj autentiseringsmetoden OAuth Server-till-server.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

På nästa skärm får du en uppmaning om att välja en eller flera produktprofiler som ska associeras med API-integreringen.

>[!NOTE]
>
>Produktprofiler hanteras av er organisation via Adobe Admin Console och innehåller specifika behörighetsgrupper för detaljfunktioner. Produktprofiler och deras behörigheter kan bara hanteras av användare med administratörsbehörighet inom organisationen. Om du är osäker på vilka produktprofiler du ska välja för API kontaktar du administratören.

Välj önskade produktprofiler i listan och välj sedan **Spara konfigurerad API** för att slutföra API-registreringen.

![](../images/api/getting-started/select-product-profile.png)

### Samla in inloggningsuppgifter {#gather-credentials}

När API:t har lagts till i projektet visar **[!UICONTROL Experience Platform API]**-sidan för projektet följande autentiseringsuppgifter som krävs i alla anrop till Experience Platform API:er:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![Integreringsinformation när du har lagt till ett API i Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Generera en åtkomsttoken {#generate-access-token}

Nästa steg är att generera en `{ACCESS_TOKEN}`-autentiseringsuppgift som kan användas i Experience Platform API-anrop. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}` måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda Experience Platform API:er.

>[!TIP]
>
>Dessa token upphör att gälla efter 24 timmar. Om du använder den här integreringen för ett program är det en bra idé att hämta din innehavartoken programmatiskt inifrån programmet.

Det finns två alternativ för att generera åtkomsttoken, beroende på hur du använder dem:

* [Generera tokens manuellt](#manual)
* [Automatisera generering av token](#auto-token)

#### Generera åtkomsttoken manuellt {#manual}

Om du vill generera en ny `{ACCESS_TOKEN}` manuellt går du till **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** och väljer **[!UICONTROL Generate access token]** enligt nedan.

![Skärminspelning av hur och åtkomsttoken genereras i Developer Console-gränssnittet.](/help/tags/images/api/getting-started/generate-access-token.gif)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för det obligatoriska auktoriseringshuvudet och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

#### Automatisera generering av token {#auto-token}

Du kan också använda en Postman-miljö och en samling för att generera åtkomsttoken. Mer information finns i avsnittet om att [använda Postman för att autentisera och testa API-anrop](/help/landing/api-authentication.md#use-postman) i autentiseringsguiden för Experience Platform API.

## Testa API-autentiseringsuppgifter {#test-api-credentials}

Om du följer stegen i den här självstudiekursen bör du ha giltiga värden för `{ORG_ID}`, `{API_KEY}` och `{ACCESS_TOKEN}`. Du kan nu testa dessa värden genom att använda dem i en enkel cURL-begäran till Reactor API.

Börja med att försöka göra ett API-anrop till [listan över alla företag](./endpoints/companies.md#list).

>[!NOTE]
>
>Du kanske inte har några företag i din organisation, och då är svaret HTTP-status 404 (Hittades inte). Så länge du inte får ett 403-fel (Ej tillåtet) är dina inloggningsuppgifter giltiga och fungerar.

När du har bekräftat att dina inloggningsuppgifter fungerar kan du fortsätta att utforska den andra API-referensdokumentationen och lära dig API:ts många funktioner.

## Läser exempel-API-anrop {#read-sample-api-calls}

Varje slutpunktshandbok innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/api-guide.md#sample-api) i Komma igång-guiden för Experience Platform API:er.

## Nästa steg {#next-steps}

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till Reaktors API. Välj någon av slutpunktsguiderna för att komma igång:

* [Referenshandbok för reaktors-API](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Översikt över API-guide för reaktor](/help/tags/api/overview.md)
