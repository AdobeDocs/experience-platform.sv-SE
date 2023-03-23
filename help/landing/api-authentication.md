---
keywords: Experience Platform;hem;populära ämnen;Autentisera;åtkomst
solution: Experience Platform
title: Autentisera och få åtkomst till Experience Platform API:er
type: Tutorial
description: Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 1%

---


# Autentisera och få åtkomst till Experience Platform-API:er

Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er. I slutet av den här självstudiekursen kommer du att ha genererat följande autentiseringsuppgifter som krävs för alla API-anrop för plattformen:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

För att skydda program och användare måste alla förfrågningar till Adobe I/O API:er autentiseras och auktoriseras med standarder som OAuth och JSON Web Tokens (JWT). En JWT används tillsammans med klientspecifik information för att generera din personliga åtkomsttoken.

I den här självstudiekursen beskrivs hur du samlar in de nödvändiga autentiseringsuppgifterna för att autentisera API-anrop för plattformar, enligt följande flödesschema:

![](./images/api-authentication/authentication-flowchart.png)

## Förutsättningar

För att kunna anropa Experience Platform API:er måste du ha följande:

* En IMS-organisation med tillgång till Adobe Experience Platform.
* En Admin Console-administratör som kan lägga till dig som utvecklare och som användare för en produktprofil.

Du måste också ha en Adobe ID för att slutföra kursen. Om du inte har någon Adobe ID kan du skapa en med följande steg:

1. Gå till [Adobe Developer Console](https://console.adobe.io).
2. Välj **[!UICONTROL Create a new account]**.
3. Slutför registreringsprocessen.

## Få utvecklare och användare åtkomst till Experience Platform

Innan du skapar integreringar på Adobe Developer Console måste ditt konto ha utvecklar- och användarbehörigheter för en produktprofil för Experience Platform i Adobe Admin Console.

### Få utvecklaråtkomst

Kontakta en [!DNL Admin Console] administratör i din organisation för att lägga till dig som utvecklare i en Experience Platform-produktprofil med hjälp av [[!DNL Admin Console]](https://adminconsole.adobe.com/). Se [!DNL Admin Console] dokumentation för specifika instruktioner om hur man [hantera utvecklaråtkomst för produktprofiler](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

När du har utsetts till utvecklare kan du börja skapa integreringar i [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Dessa integreringar är en pipeline från externa program och tjänster till Adobe-API:er.

### Få användaråtkomst

Dina [!DNL Admin Console] måste administratören också lägga till dig som användare i samma produktprofil. Se guiden [hantera användargrupper i [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) för mer information.

## Generera en API-nyckel, IMS-org-ID och klienthemlighet {#api-ims-secret}

>[!NOTE]
>
>Om du följer det här dokumentet från [API-guide för Privacy Service](../privacy-service/api/getting-started.md)kan du nu gå tillbaka till den guiden för att skapa inloggningsuppgifter som är unika för [!DNL Privacy Service].

När du har fått utvecklare och användare åtkomst till Platform via [!DNL Admin Console]är nästa steg att skapa `{ORG_ID}` och `{API_KEY}` autentiseringsuppgifter i Adobe Developer Console. Dessa autentiseringsuppgifter behöver bara genereras en gång och kan återanvändas i framtida API-anrop för plattformen.

### Lägga till Experience Platform i ett projekt

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add API]** på **[!UICONTROL Project Overview]** skärm.

![](./images/api-authentication/add-api.png)

The **[!UICONTROL Add an API]** visas. Markera produktikonen för Adobe Experience Platform och välj sedan **[!UICONTROL Experience Platform API]** före markering **[!UICONTROL Next]**.

![](./images/api-authentication/platform-api.png)

Följ instruktionerna som beskrivs i självstudiekursen om [lägga till ett API i ett projekt med ett tjänstkonto (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (från steget Konfigurera API) för att slutföra processen.

>[!IMPORTANT]
>
>I ett visst steg under den process som är länkad ovan hämtar webbläsaren automatiskt en privat nyckel och ett tillhörande offentligt certifikat. Observera var den här privata nyckeln lagras på din dator, eftersom den krävs i ett senare steg i den här självstudiekursen.

### Samla in inloggningsuppgifter

När API:t har lagts till i projektet **[!UICONTROL Experience Platform API]** På projektsidan visas följande autentiseringsuppgifter som krävs för alla anrop till API:er för Experience Platform:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

Utöver de ovanstående inloggningsuppgifterna behöver du även de genererade **[!UICONTROL Client Secret]** för ett framtida steg. Välj **[!UICONTROL Retrieve client secret]** för att visa värdet och sedan kopiera det för senare bruk.

![](././images/api-authentication/client-secret.png)

## Generera en JSON-webbtoken (JWT) {#jwt}

Nästa steg är att generera en JSON Web Token (JWT) baserat på dina kontouppgifter. Detta värde används för att generera `{ACCESS_TOKEN}` autentiseringsuppgifter för användning i API-anrop för plattformen, som måste genereras om var 24:e timme.

>[!IMPORTANT]
>
>I den här självstudiekursen beskrivs hur du skapar en JWT-fil i Developer Console i stegen nedan. Denna genereringsmetod bör dock endast användas för testning och utvärdering.
>
>För normal användning måste JWT genereras automatiskt. Mer information om programmässig generering av JWT finns i [autentiseringsguide för tjänstkonto](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) på Adobe Developer.

Välj **[!UICONTROL Service Account (JWT)]** i den vänstra navigeringen väljer du **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

I textrutan som finns under **[!UICONTROL Generate custom JWT]** Klistra in innehållet i den privata nyckeln som du tidigare genererade när du lade till Platform API i ditt tjänstkonto. Välj sedan **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

Sidan uppdateras för att visa den genererade JWT-filen tillsammans med ett exempel på ett cURL-kommando som gör att du kan generera en åtkomsttoken. I den här självstudiekursen väljer du **[!UICONTROL Copy]** nästa **[!UICONTROL Generated JWT]** om du vill kopiera token till Urklipp.

![](././images/api-authentication/copy-jwt.png)

## Generera en åtkomsttoken

När du har genererat en JWT-fil kan du använda den i ett API-anrop för att generera `{ACCESS_TOKEN}`. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda Platform API:er.

**Begäran**

Följande begäran genererar en ny `{ACCESS_TOKEN}` baserat på autentiseringsuppgifterna som anges i nyttolasten. Den här slutpunkten accepterar endast formulärdata som nyttolast och måste därför ges en `Content-Type` sidhuvud `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `{API_KEY}` | The `{API_KEY}` ([!UICONTROL Client ID]) som du har hämtat i en [föregående steg](#api-ims-secret). |
| `{SECRET}` | Klienthemligheten som du hämtade i en [föregående steg](#api-ims-secret). |
| `{JWT}` | Den JWT som du skapade i en [föregående steg](#jwt). |

>[!NOTE]
>
>Du kan använda samma API-nyckel, klienthemlighet och JWT för att generera en ny åtkomsttoken för varje session. Detta gör att du kan automatisera genereringen av åtkomsttoken i dina program.

**Svar**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `token_type` | Den typ av token som returneras. För åtkomsttoken är det här värdet alltid `bearer`. |
| `access_token` | Den genererade `{ACCESS_TOKEN}`. Detta värde, prefixat med ordet `Bearer`, krävs som `Authentication` header för alla API-anrop för plattformen. |
| `expires_in` | Antalet millisekunder som återstår tills åtkomsttoken upphör att gälla. När värdet når 0 måste en ny åtkomsttoken genereras för att du ska kunna fortsätta använda Platform API:er. |

## Testa autentiseringsuppgifter

När du har samlat in alla tre nödvändiga autentiseringsuppgifter kan du försöka göra följande API-anrop. Det här samtalet listar alla standarder [!DNL Experience Data Model] (XDM)-klasser som är tillgängliga för din organisation.

**Begäran**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Använd Postman för att autentisera och testa API-anrop

[Postman](https://www.postman.com/) är ett populärt verktyg som gör att utvecklare kan utforska och testa RESTful API:er. Detta [Medellång post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) I beskrivs hur du kan konfigurera Postman så att det automatiskt utför JWT-autentisering och använder det för att använda Platform API:er.

## Nästa steg

Genom att läsa det här dokumentet har du samlat in och testat dina autentiseringsuppgifter för plattforms-API:er. Du kan nu följa med i de exempel på API-anrop som finns i [dokumentation](../landing/documentation/overview.md).

Förutom de autentiseringsvärden du har samlat in i den här självstudiekursen kräver många plattforms-API:er även en giltig `{SANDBOX_NAME}` anges som rubrik. Se [översikt över sandlådor](../sandboxes/home.md) för mer information.