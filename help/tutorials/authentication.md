---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autentisera och få tillgång till Experience Platform API:er
topic: tutorial
translation-type: tm+mt
source-git-commit: 8c73363e88aab242ae258037deb80eeec872e519
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# Autentisera och få åtkomst till Experience Platform API:er

Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er.

## Autentisera för att göra API-anrop

För att skydda program och användare måste alla förfrågningar till Adobe I/O-API:er autentiseras och auktoriseras med standarder som OAuth och JSON Web Tokens (JWT). JWT används sedan tillsammans med klientspecifik information för att generera din personliga åtkomsttoken.

I den här självstudiekursen beskrivs stegen för autentisering genom att skapa en åtkomsttoken som beskrivs i följande flödesschema:
![](images/authentication/authentication-flowchart.png)

## Förutsättningar

För att kunna anropa Experience Platform API:er krävs följande:

* En IMS-organisation med tillgång till Adobe Experience Platform
* Ett registrerat Adobe ID-konto
* En administratör för Admin Console där du kan lägga till dig som **utvecklare** och som **användare** för en produkt.

I följande avsnitt går vi igenom stegen för att skapa ett Adobe ID och bli utvecklare och användare för en organisation.

### Skapa ett Adobe-ID

Om du inte har något Adobe-ID kan du skapa ett med följande steg:

1. Gå till [Adobe Developer Console](https://console.adobe.io)
2. Klicka på **Skapa ett nytt konto**
3. Slutför registreringsprocessen

## Bli utvecklare och användare av Experience Platform för en organisation

Innan du skapar integreringar på Adobe I/O måste ditt konto ha utvecklarbehörighet för en produkt i en IMS-organisation. Detaljerad information om utvecklarkonton på Admin Console finns i [supportdokumentet](https://helpx.adobe.com/enterprise/using/manage-developers.html) för hantering av utvecklare.

**Få utvecklaråtkomst**

Kontakta en administratör för Admin Console i din organisation för att lägga till dig som utvecklare för en av organisationens produkter med hjälp av [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

Administratören måste tilldela dig som utvecklare minst en produktprofil för att kunna fortsätta.

![](images/authentication/add-developer.png)

När du har utsetts till utvecklare får du behörighet att skapa integreringar på [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Dessa integreringar är en pipeline från externa program och tjänster till Adobe API.

**Få användaråtkomst**

Administratören för Admin Console måste också lägga till dig i produkten som användare.

![](images/authentication/assign-users.png)

På samma sätt som när du lägger till en utvecklare måste administratören tilldela dig till minst en produktprofil för att kunna fortsätta.

![](images/authentication/assign-user-details.png)


## Generera autentiseringsuppgifter för åtkomst i Adobe Developer Console

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ditt `{IMS_ORG}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida API-anrop för plattformen. Ditt `{ACCESS_TOKEN}` är dock tillfälligt och måste genereras om var 24:e timme.

Stegen beskrivs närmare nedan.

### Engångskonfiguration

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med ditt Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om hur du [skapar ett tomt projekt](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt klickar du **[!UICONTROL Add API]** på skärmen _Projektöversikt_ .

![](images/authentication/add-api-button.png)

Skärmen _Lägg till ett API_ visas. Klicka på produktikonen för Adobe Experience Platform och välj sedan **[!UICONTROL Experience Platform API]** innan du klickar på **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

När du har valt Experience Platform som det API som ska läggas till i projektet följer du de steg som beskrivs i självstudiekursen om hur du [lägger till ett API i ett projekt med ett tjänstkonto (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (med början från steget Konfigurera API) för att slutföra processen.

När API:t har lagts till i projektet visas följande autentiseringsuppgifter på sidan _Projektöversikt_ som krävs i alla anrop till Experience Platform API:er:

* `{API_KEY}` (Klient-ID)
* `{IMS_ORG}` (Organisations-ID)

![](./images/authentication/api-key-ims-org.png)

### Autentisering för varje session

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`. Till skillnad från värdena för `{API_KEY}` och `{IMS_ORG}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda plattforms-API:er.

Om du vill skapa en ny `{ACCESS_TOKEN}`variant följer du stegen för att [generera en JWT-token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) i referenshandboken för Developer Console.

## Testa autentiseringsuppgifter

När du har samlat in alla tre nödvändiga autentiseringsuppgifter kan du försöka göra följande API-anrop. Detta anrop listar alla XDM-klasser (Experience Data Model) i schematabellens `global` behållare:

**API-format**

```http
GET /global/classes
```

**Begäran**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Om ditt svar liknar det som visas nedan är dina inloggningsuppgifter giltiga och fungerar. (Det här svaret har trunkerats för utrymme.)

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Använd Postman för JWT-autentisering och API-anrop

[Postman](https://www.getpostman.com/) är ett populärt verktyg för att arbeta med RESTful API:er. I det här [mellanbrevet](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beskrivs hur du kan konfigurera postman så att den automatiskt utför JWT-autentisering och använder den för att använda API:er för Adobe Experience Platform.

## Nästa steg

Genom att läsa det här dokumentet har du samlat in och testat dina autentiseringsuppgifter för plattforms-API:er. Du kan nu följa med i de exempel på API-anrop som finns i [dokumentationen](../landing/documentation/overview.md).

Förutom de autentiseringsvärden du har samlat in i den här självstudiekursen behöver många plattforms-API:er även en giltig `{SANDBOX_NAME}` som rubrik. Mer information finns i översikten över [](../sandboxes/home.md) sandlådor.