---
keywords: Experience Platform;hem;populära ämnen;Autentisera;åtkomst
solution: Experience Platform
title: Autentisera och få åtkomst till Experience Platform API:er
topic-legacy: tutorial
type: Tutorial
description: 'Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er. '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---


# Autentisera och få åtkomst till [!DNL Experience Platform] API:er

Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa till [!DNL Experience Platform] API:er.

## Autentisera för att göra API-anrop

För att skydda program och användare måste alla förfrågningar till Adobe I/O API:er autentiseras och auktoriseras med standarder som OAuth och JSON Web Tokens (JWT). JWT används sedan tillsammans med klientspecifik information för att generera din personliga åtkomsttoken.

I den här självstudiekursen beskrivs stegen för autentisering genom att skapa en åtkomsttoken som beskrivs i följande flödesschema:
![](images/authentication/authentication-flowchart.png)

## Förutsättningar

För att kunna anropa API:er för [!DNL Experience Platform] behöver du följande:

* En IMS-organisation med tillgång till Adobe Experience Platform
* Ett registrerat Adobe ID-konto
* En Admin Console-administratör som lägger till dig som **utvecklare** och **användare** för en produkt.

I följande avsnitt går vi igenom stegen för att skapa en Adobe ID och bli utvecklare och användare för en organisation.

### Skapa en Adobe ID

Om du inte har någon Adobe ID kan du skapa en med följande steg:

1. Gå till [Adobe Developer Console](https://console.adobe.io)
2. Välj **[!UICONTROL create a new account]**
3. Slutför registreringsprocessen

## Bli utvecklare och användare för [!DNL Experience Platform] för en organisation

Innan du skapar integreringar på Adobe I/O måste ditt konto ha utvecklarbehörighet för en produkt i en IMS-organisation. Detaljerad information om utvecklarkonton på Admin Console finns i [supportdokumentet](https://helpx.adobe.com/enterprise/using/manage-developers.html) för hantering av utvecklare.

**Få utvecklaråtkomst**

Kontakta en [!DNL Admin Console]-administratör i din organisation om du vill lägga till dig som utvecklare för någon av organisationens produkter med [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

Administratören måste tilldela dig som utvecklare minst en produktprofil för att kunna fortsätta.

![](images/authentication/add-developer.png)

När du har tilldelats behörighet som utvecklare får du behörighet att skapa integreringar på [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Dessa integreringar är en pipeline från externa program och tjänster till Adobe API.

**Få användaråtkomst**

Din [!DNL Admin Console]-administratör måste också lägga till dig i produkten som en användare.

![](images/authentication/assign-users.png)

På samma sätt som när du lägger till en utvecklare måste administratören tilldela dig till minst en produktprofil för att kunna fortsätta.

![](images/authentication/assign-user-details.png)

## Generera autentiseringsuppgifter för åtkomst i Adobe Developer Console

>[!NOTE]
>
>Om du följer det här dokumentet från [utvecklarhandboken för Privacy Servicen](../privacy-service/api/getting-started.md) kan du nu gå tillbaka till den handboken för att generera autentiseringsuppgifter som är unika för [!DNL Privacy Service].

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Dina `{IMS_ORG}` och `{API_KEY}` behöver bara genereras en gång och kan återanvändas i framtida [!DNL Platform] API-anrop. Din `{ACCESS_TOKEN}` är temporär och måste genereras om var 24:e timme.

Stegen beskrivs närmare nedan.

### Engångskonfiguration

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om att [skapa ett tomt projekt](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add API]** på skärmen **Projektöversikt**.

![](images/authentication/add-api-button.png)

Skärmen **Lägg till ett API** visas. Markera produktikonen för Adobe Experience Platform och välj **[!UICONTROL Experience Platform API]** innan du väljer **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

När du har valt [!DNL Experience Platform] som det API som ska läggas till i projektet följer du stegen som beskrivs i självstudiekursen om hur du lägger till ett API i ett projekt med ett tjänstkonto (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (med början från steget Konfigurera API) för att slutföra processen.[

När API:t har lagts till i projektet visar sidan **Projektöversikt** följande autentiseringsuppgifter som krävs i alla anrop till [!DNL Experience Platform] API:er:

* `{API_KEY}` (Klient-ID)
* `{IMS_ORG}` (Organisations-ID)

![](./images/authentication/api-key-ims-org.png)

### Autentisering för varje session

Den sista obligatoriska autentiseringsuppgifterna som du måste samla in är din `{ACCESS_TOKEN}`. Till skillnad från värdena för `{API_KEY}` och `{IMS_ORG}` måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda [!DNL Platform] API:er.

Om du vill generera en ny `{ACCESS_TOKEN}` följer du stegen för att [generera en JWT-token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) i referenshandboken för Developer Console.

## Testa autentiseringsuppgifter

När du har samlat in alla tre nödvändiga autentiseringsuppgifter kan du försöka göra följande API-anrop. Det här anropet listar alla [!DNL Experience Data Model] (XDM)-klasser i schemaregistrets `global`-behållare:

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

[Postmanis ](https://www.postman.com/) är ett populärt verktyg för att arbeta med RESTful API:er. Detta [medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beskriver hur du kan ställa in postman så att den automatiskt utför JWT-autentisering och använder den för att använda Adobe Experience Platform API:er.

## Nästa steg

Genom att läsa det här dokumentet har du samlat in och testat dina autentiseringsuppgifter för [!DNL Platform] API:er. Du kan nu följa med i de exempel på API-anrop som finns i [dokumentationen](../landing/documentation/overview.md).

Förutom de autentiseringsvärden som du har samlat in i den här självstudiekursen kräver många [!DNL Platform] API:er också en giltig `{SANDBOX_NAME}` som rubrik. Mer information finns i [översikten över sandlådor](../sandboxes/home.md).