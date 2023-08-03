---
solution: Experience Platform
title: Autentisera och få åtkomst till Experience Platform API:er
type: Tutorial
description: Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f598c6dabe9296044055d8e961cf5177a655f5fa
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 1%

---


# Autentisera och få åtkomst till Experience Platform-API:er

Det här dokumentet innehåller en stegvis självstudiekurs för att få tillgång till ett Adobe Experience Platform-utvecklarkonto för att ringa anrop till Experience Platform API:er. I slutet av den här självstudiekursen kommer du att ha genererat eller samlat in följande autentiseringsuppgifter som krävs som huvuden i alla API-anrop för plattformen:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>Förutom de tre autentiseringsuppgifterna ovan kräver många plattforms-API:er även en giltig `{SANDBOX_NAME}` anges som rubrik. Se [översikt över sandlådor](../sandboxes/home.md) för mer information om sandlådor och [slutpunkt för sandlådehantering](/help/sandboxes/api/sandboxes.md#list) dokumentation som innehåller information om hur du listar de sandlådor som är tillgängliga för din organisation.

För att skydda program och användare måste alla förfrågningar till Experience Platform API:er autentiseras och auktoriseras med standarder som OAuth.

I den här självstudiekursen beskrivs hur du samlar in nödvändiga inloggningsuppgifter för att autentisera API-anrop för plattformar, enligt vad som beskrivs i nedanstående flödesschema. Du kan samla de flesta nödvändiga autentiseringsuppgifter i den första engångsinställningen. Åtkomsttoken måste dock uppdateras var 24:e timme.

![](./images/api-authentication/authentication-flowchart.png)

## Förutsättningar {#prerequisites}

För att kunna anropa Experience Platform API:er måste du ha följande:

* En organisation med tillgång till Adobe Experience Platform.
* En Admin Console-administratör som kan lägga till dig som utvecklare och som användare för en produktprofil.
* En Experience Platform-systemadministratör som kan ge dig nödvändiga attributbaserade åtkomstkontroller för att kunna utföra läs- och skrivåtgärder på olika delar av Experience Platform via API:er.

Du måste också ha en Adobe ID för att slutföra kursen. Om du inte har någon Adobe ID kan du skapa en med följande steg:

1. Gå till [Adobe Developer Console](https://console.adobe.io).
2. Välj **[!UICONTROL Create a new account]**.
3. Slutför registreringsprocessen.

## Få utvecklare och användare åtkomst till Experience Platform {#gain-developer-user-access}

Innan du skapar integreringar på Adobe Developer Console måste ditt konto ha utvecklar- och användarbehörigheter för en produktprofil för Experience Platform i Adobe Admin Console.

### Få utvecklaråtkomst {#gain-developer-access}

Kontakta en [!DNL Admin Console] administratör i din organisation för att lägga till dig som utvecklare i en Experience Platform-produktprofil med hjälp av [[!DNL Admin Console]](https://adminconsole.adobe.com/). Se [!DNL Admin Console] dokumentation för specifika instruktioner om hur man [hantera utvecklaråtkomst för produktprofiler](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

När du har utsetts till utvecklare kan du börja skapa integreringar i [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Dessa integreringar är en pipeline från externa program och tjänster till Adobe-API:er.

### Få användaråtkomst {#gain-user-access}

Dina [!DNL Admin Console] måste administratören också lägga till dig som användare i samma produktprofil. Med användaråtkomst kan du i gränssnittet se resultatet av de API-åtgärder du utför.

Se guiden på [hantera användargrupper i [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) för mer information.

## Generera en API-nyckel (klient-ID) och ett företags-ID {#generate-credentials}

>[!NOTE]
>
>Om du följer det här dokumentet från [API-guide för Privacy Service](../privacy-service/api/getting-started.md)kan du nu gå tillbaka till den guiden för att generera unika autentiseringsuppgifter för [!DNL Privacy Service].

När du har fått utvecklare och användare åtkomst till Platform via [!DNL Admin Console]är nästa steg att skapa `{ORG_ID}` och `{API_KEY}` autentiseringsuppgifter i Adobe Developer Console. Dessa autentiseringsuppgifter behöver bara genereras en gång och kan återanvändas i framtida API-anrop för plattformen.

### Lägga till Experience Platform i ett projekt {#add-platform-to-project}

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan instruktionerna i självstudiekursen på [skapa ett tomt projekt](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) i dokumentationen för Adobe Developer Console.

När du har skapat ett nytt projekt väljer du **[!UICONTROL Add API]** på **[!UICONTROL Project Overview]** skärm.

>[!TIP]
>
>Om du har etablerat dig för flera organisationer använder du organisationsväljaren i det övre högra hörnet av gränssnittet för att kontrollera att du är i den organisation du behöver.

![Developer Console-skärmen med alternativet Lägg till API markerat.](./images/api-authentication/add-api.png)

The **[!UICONTROL Add an API]** visas. Markera produktikonen för Adobe Experience Platform och välj sedan **[!UICONTROL Experience Platform API]** före markering **[!UICONTROL Next]**.

![Välj Experience Platform API.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>Välj **[!UICONTROL View docs]** alternativ för att navigera i ett separat webbläsarfönster till det fullständiga [Referenshandbok för Experience Platform API](https://developer.adobe.com/experience-platform-apis/).

### Välj autentiseringstypen OAuth Server-till-server {#select-oauth-server-to-server}

Välj sedan autentiseringstypen för att generera åtkomsttoken och få åtkomst till Experience Platform-API:t.

>[!IMPORTANT]
>
>Välj **[!UICONTROL OAuth Server-to-Server]** eftersom det här är den enda metod som stöds för att gå framåt. The **[!UICONTROL Service Account (JWT)]** -metoden är inaktuell. Även om integreringar med JWT-autentiseringsmetoden fortsätter att fungera fram till 1 januari 2025 rekommenderar Adobe starkt att du migrerar befintliga integreringar till den nya OAuth Server-till-Server-metoden före detta datum. Hämta mer information i avsnittet [!BADGE Föråldrat]{type=negative}[Generera en JSON-webbtoken (JWT)](#jwt).

![Välj Experience Platform API.](./images/api-authentication/oauth-authentication-method.png)

### Välj produktprofiler för integreringen {#select-product-profiles}

I **[!UICONTROL Configure API]** skärm, välja **[!UICONTROL AEP-Default-All-Users]**.

<!--
Your integration's service account will gain access to granular features through the product profiles selected here.

-->

>[!IMPORTANT]
>
För att få tillgång till vissa funktioner i Platform behöver du också en systemadministratör som ger dig de nödvändiga attributbaserade behörigheterna för åtkomstkontroll. Läs mer i avsnittet [Skaffa nödvändiga attributbaserade behörigheter för åtkomstkontroll](#get-abac-permissions).

![Välj produktprofiler för din integrering.](./images/api-authentication/select-product-profiles.png)

Välj **[!UICONTROL Save configured API]** när du är redo.

En genomgång av de steg som beskrivs ovan för att konfigurera en integrering med API:t för Experience Platform finns också i videosjälvstudien nedan:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### Samla in inloggningsuppgifter {#gather-credentials}

När API:t har lagts till i projektet **[!UICONTROL Experience Platform API]** På projektsidan visas följande autentiseringsuppgifter som krävs för alla anrop till API:er för Experience Platform:

![Integreringsinformation när du har lagt till ett API i Developer Console.](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## Generera en åtkomsttoken {#generate-access-token}

Nästa steg är att skapa en `{ACCESS_TOKEN}` autentiseringsuppgifter för användning i API-anrop för plattformar. Till skillnad från värdena för `{API_KEY}` och `{ORG_ID}`måste en ny token genereras var 24:e timme för att du ska kunna fortsätta använda Platform API:er. Välj **[!UICONTROL Generate access token]**, vilket visas nedan.

![Visa hur du genererar åtkomsttoken](././images/api-authentication/generate-access-token.gif)

>[!TIP]
>
Du kan också använda en Postman-miljö och en samling för att generera åtkomsttoken. Läs mer om [använda Postman för att autentisera och testa API-anrop](#use-postman).

## [!BADGE Föråldrat]{type=negative} Generera en JSON-webbtoken (JWT) {#jwt}

>[!WARNING]
>
JWT-metoden för att generera åtkomsttoken har tagits bort. Alla nya integreringar måste skapas med [OAuth Server-till-Server-autentiseringsmetod](#select-oauth-server-to-server). Adobe rekommenderar också att du migrerar dina befintliga integreringar till OAuth-metoden. Läs följande viktiga dokumentation:
> 
* [Migreringsguide för program från JWT till OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
* [Implementeringsguide för nya och gamla program med OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
* [Fördelar med att använda inloggningsmetoden OAuth Server-till-Server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ Visa inaktuell information

Nästa steg är att generera en JSON Web Token (JWT) baserat på dina kontouppgifter. Detta värde används för att generera `{ACCESS_TOKEN}` autentiseringsuppgifter för användning i API-anrop för plattformen, som måste genereras om var 24:e timme.

>[!IMPORTANT]
>
I den här självstudiekursen beskrivs hur du skapar en JWT-fil i Developer Console i stegen nedan. Denna genereringsmetod bör dock endast användas för testning och utvärdering.
>
För normal användning måste JWT genereras automatiskt. Mer information om programmässig generering av JWT finns i [autentiseringsguide för tjänstkonto](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) på Adobe Developer.

Välj **[!UICONTROL Service Account (JWT)]** i den vänstra navigeringen väljer du **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

I textrutan som finns under **[!UICONTROL Generate custom JWT]** Klistra in innehållet i den privata nyckeln som du tidigare genererade när du lade till Platform API i ditt tjänstkonto. Välj sedan **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

Sidan uppdateras för att visa den genererade JWT-filen tillsammans med ett exempel på ett cURL-kommando som gör att du kan generera en åtkomsttoken. I den här självstudiekursen väljer du **[!UICONTROL Copy]** nästa **[!UICONTROL Generated JWT]** om du vill kopiera token till Urklipp.

![](././images/api-authentication/copy-jwt.png)

**Generera en åtkomsttoken**

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
| `{API_KEY}` | The `{API_KEY}` ([!UICONTROL Client ID]) som du hämtade i en [föregående steg](#api-ims-secret). |
| `{SECRET}` | Klienthemligheten som du hämtade i en [föregående steg](#api-ims-secret). |
| `{JWT}` | Den JWT som du skapade i en [föregående steg](#jwt). |

>[!NOTE]
>
Du kan använda samma API-nyckel, klienthemlighet och JWT för att generera en ny åtkomsttoken för varje session. Detta gör att du kan automatisera genereringen av åtkomsttoken i dina program.

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

+++

## Testa autentiseringsuppgifter {#test-credentials}

När du har samlat in alla tre nödvändiga autentiseringsuppgifter - åtkomsttoken, API-nyckel och organisations-ID - kan du försöka göra följande API-anrop. Det här samtalet listar alla standarder [!DNL Experience Data Model] (XDM)-klasser som är tillgängliga för din organisation. Importera och köra samtalet i [Postman](#use-postman).

>[!BEGINSHADEBOX]

**Begäran**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
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

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
Samtalet ovan räcker för att testa dina inloggningsuppgifter, men tänk på att du inte kommer att kunna komma åt eller ändra flera resurser utan rätt attributbaserad åtkomstkontrollbehörighet. Läs mer i **Skaffa nödvändiga attributbaserade behörigheter för åtkomstkontroll** nedan.

## Skaffa nödvändiga attributbaserade behörigheter för åtkomstkontroll {#get-abac-permissions}

Om du vill få åtkomst till eller ändra flera resurser i Experience Platform måste du ha rätt åtkomstkontrollbehörighet. Systemadministratörer kan ge dig [behörigheter du behöver](/help/access-control/ui/permissions.md). Hämta mer information om [hantera API-autentiseringsuppgifter för en roll](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

Detaljerad information om hur en systemadministratör kan ge de behörigheter som krävs för att få åtkomst till plattformsresurser via API finns också i videosjälvstudien nedan:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## Använd Postman för att autentisera och testa API-anrop {#use-postman}

[Postman](https://www.postman.com/) är ett populärt verktyg som gör att utvecklare kan utforska och testa RESTful API:er. Du kan använda Experience Platform Postman-samlingar och miljöer för att snabba upp arbetet med Experience Platform API:er. Läs mer om [med Postman i Experience Platform](/help/landing/postman.md) och komma igång med samlingar och miljöer.

Detaljerad information om hur du använder Postman med Experience Platform i samlingar och miljöer finns också i videosjälvstudierna nedan:

**Hämta och importera en Postman-miljö som kan användas med Experience Platform API:er**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**Använd en Postman-samling för att generera åtkomsttoken**

Ladda ned [Identity Management Service Postman Collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) och se videon nedan för att lära dig hur du skapar åtkomsttoken.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**Ladda ned Experience Platform API Postman-samlingar och interagera med API:erna**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Platform APIs.
-->

## Systemadministratörer: Bevilja utvecklare och API-åtkomstkontroll med Experience Platform behörigheter {#grant-developer-and-api-access-control}

>[!NOTE]
>
Det är bara systemadministratörer som kan visa och hantera API-autentiseringsuppgifter i behörigheter.

Innan du skapar integreringar på Adobe Developer Console måste ditt konto ha utvecklar- och användarbehörigheter för en produktprofil för Experience Platform i Adobe Admin Console.

### Lägg till utvecklare i produktprofilen {#add-developers-to-product-profile}

Gå till [[!DNL Admin Console]](https://adminconsole.adobe.com/) och logga in med din Adobe ID.

Välj **[!UICONTROL Products]** väljer **[!UICONTROL Adobe Experience Platform]** i produktlistan.

![Produktlista på Admin Console](././images/api-authentication/products.png)

På fliken **[!UICONTROL Product Profiles]** väljer du **[!UICONTROL AEP-Default-All-Users]**. Du kan också använda sökfältet för att söka efter produktprofilen genom att ange namnet.

![Sök efter produktprofilen](././images/api-authentication/select-product-profile.png)

Välj **[!UICONTROL Developers]** tabbtangenten och sedan välja **[!UICONTROL Add Developer]**.

![Lägg till utvecklare från fliken Utvecklare](././images/api-authentication/add-developer1.png)

Ange utvecklarens **[!UICONTROL Email or username]**. Ett giltigt [!UICONTROL Email or username] visar utvecklarinformationen. Välj **[!UICONTROL Save]**.

![Lägg till utvecklare via e-post eller användarnamn](././images/api-authentication/add-developer-email.png)

Utvecklaren har lagts till och visas på [!UICONTROL Developers] -fliken.

![Utvecklare som listas på fliken Utvecklare](././images/api-authentication/developer-added.png)

<!--

Commenting out this part since it duplicates information from the section Add Experience Platform to a project

### Set up an API

A developer can add and configure an API within a project in the Adobe Developer Console.

Select your project, then select **[!UICONTROL Add API]**.

![Add API to a project](././images/api-authentication/add-api-project.png)

In the **[!UICONTROL Add an API]** dialog box select **[!UICONTROL Adobe Experience Platform]**, then select **[!UICONTROL Experience Platform API]**.

![Add an API in Experience Platform](././images/api-authentication/add-api-platform.png)

In the **[!UICONTROL Configure API]** screen, select **[!UICONTROL AEP-Default-All-Users]**.

-->

### Tilldela API till en roll

En systemadministratör kan tilldela API:er till roller i användargränssnittet i Experience Platform.

Välj **[!UICONTROL Permissions]** och den roll du vill lägga till API:t i. Välj **[!UICONTROL API credentials]** tabbtangenten och sedan välja **[!UICONTROL Add API credentials]**.

![Fliken API-autentiseringsuppgifter i den valda rollen](././images/api-authentication/api-credentials.png)

Välj det API som du vill lägga till i rollen och välj sedan **[!UICONTROL Save]**.

![Lista över tillgängliga API:er för val](././images/api-authentication/select-api.png)

Du kommer tillbaka till [!UICONTROL API credentials] -fliken, där det nya API:t visas.

![Fliken API-autentiseringsuppgifter med nyligen tillagt API](././images/api-authentication/api-credentials-with-added-api.png)

## Ytterligare resurser {#additional-resources}

Se de ytterligare resurserna nedan för att få hjälp med att komma igång med Experience Platform API:er

* [Autentisera och få åtkomst till Experience Platform API:er](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html) videosjälvstudiekurser
* [Identity Management Service Postman Collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) för generering av åtkomsttoken
* [Experience Platform API Postman Collections](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet har du samlat in och testat dina autentiseringsuppgifter för plattforms-API:er. Du kan nu följa med i de exempel på API-anrop som finns i [dokumentation](../landing/documentation/overview.md).

Förutom de autentiseringsvärden du har samlat in i den här självstudiekursen kräver många plattforms-API:er även en giltig `{SANDBOX_NAME}` anges som rubrik. Se [översikten över sandlådor](../sandboxes/home.md) för mer information.