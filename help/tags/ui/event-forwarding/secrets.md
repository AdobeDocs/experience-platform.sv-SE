---
title: Konfigurera hemligheter i händelsevidarebefordran
description: Lär dig hur du konfigurerar hemligheter i användargränssnittet för att autentisera slutpunkter som används i egenskaper för vidarebefordran av händelser.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: a863d65c3e6e330254a58aa822383c0847b0e5f5
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 0%

---

# Konfigurera hemligheter i händelsevidarebefordran

Vid vidarebefordran av händelser är en hemlighet en resurs som representerar autentiseringsuppgifter för ett annat system, vilket möjliggör säkert datautbyte. Det går bara att skapa hemligheter i egenskaper för vidarebefordran av händelser.

Följande hemliga typer stöds för närvarande:

| Hemlig typ | Beskrivning |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Innehåller flera attribut som stöder [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) autentiseringsspecifikation för användning i [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) och [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). Systemet ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig med ett angivet intervall. |
| [!UICONTROL HTTP] | Innehåller två strängattribut för ett användarnamn respektive ett lösenord. |
| [!UICONTROL OAuth 2] | Innehåller flera attribut som stöder [tilldelningstyp för klientautentiseringsuppgifter](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) för [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) autentiseringsspecifikation. Systemet ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig med ett angivet intervall. |
| [!UICONTROL OAuth 2 JWT] | Innehåller flera attribut som stöder JSON Web Token-profil (JWT) för [OAuth 2.0-auktorisering](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) bidrag. Systemet ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig med ett angivet intervall. |
| [!UICONTROL Token] | En enda teckensträng som representerar ett autentiseringstokenvärde som är känt och begripligt för båda systemen. |

{style="table-layout:auto"}

Den här guiden ger en översikt på hög nivå över hur du konfigurerar hemligheter för en händelsevidarebefordring ([!UICONTROL Edge]) i användargränssnittet för Experience Platform eller användargränssnittet för datainsamling.

>[!NOTE]
>
>Detaljerad vägledning om hur du hanterar hemligheter i Reaktors-API:t, inklusive exempel-JSON för en hems struktur, finns i [API-guide för hemligheter](../../api/guides/secrets.md).

## Förutsättningar

I den här handboken förutsätts det att du redan känner till hur du hanterar resurser för taggar och vidarebefordran av händelser i användargränssnittet, inklusive hur du skapar ett dataelement och en regel för vidarebefordran av händelser. Se guiden [hantera resurser](../managing-resources/overview.md) om du behöver en introduktion.

Du bör också ha en fungerande förståelse för publiceringsflödet för taggar och vidarebefordran av händelser, inklusive hur du lägger till resurser i ett bibliotek och installerar ett bygge på webbplatsen för testning. Se [publicera översikt](../publishing/overview.md) för mer information.

## Skapa en hemlighet {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Hemligheter"
>abstract="För att en hemlighet ska kunna användas av händelsevidarebefordran måste den tilldelas en befintlig miljö. Om du inte har några miljöer skapade för egenskapen för vidarebefordring av händelser måste du konfigurera dem innan du fortsätter."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=sv-SE" text="Miljööversikt"

Om du vill skapa en hemlighet väljer du **[!UICONTROL Event Forwarding]** i den vänstra navigeringen öppnar du sedan den händelsevidarebefordringsegenskap som du vill lägga till hemligheten under. Nästa, välj **[!UICONTROL Secrets]** i den vänstra navigeringen, följt av **[!UICONTROL Create New Secret]**.

![Skapa ny hemlighet](../../images/ui/event-forwarding/secrets/create-new-secret.png)

På nästa skärm kan du konfigurera informationen om hemligheten. För att en hemlighet ska kunna användas av händelsevidarebefordran måste den tilldelas en befintlig miljö. Om du inte har skapat några miljöer för egenskapen för vidarebefordring av händelser läser du i handboken på [miljöer](../publishing/environments.md) om du vill ha mer information om hur du konfigurerar dem innan du fortsätter.

>[!NOTE]
>
>Om du fortfarande vill skapa och spara hemligheten innan du lägger till den i en miljö inaktiverar du **[!UICONTROL Attach Secret to Environments]** växla innan du fyller i resten av informationen. Observera att du måste tilldela den till en miljö senare om du vill använda hemligheten.
>
>![Inaktivera miljö](../../images/ui/event-forwarding/secrets/env-disabled.png)

Under **[!UICONTROL Target Environment]** använder du listrutan för att välja den miljö som du vill tilldela hemligheten till. Under **[!UICONTROL Secret Name]**, anger ett namn för hemligheten i miljösammanhang. Det här namnet måste vara unikt för alla hemligheter under händelsevidarebefordringsegenskapen.

![Miljö och namn](../../images/ui/event-forwarding/secrets/env-and-name.png)

En hemlighet kan bara tilldelas till en miljö i taget, men du kan tilldela samma autentiseringsuppgifter till flera hemligheter i olika miljöer om du vill. Välj **[!UICONTROL Add Environment]** om du vill lägga till ytterligare en rad i listan.

![Lägg till miljö](../../images/ui/event-forwarding/secrets/add-env.png)

För varje miljö som du lägger till måste du ange ett annat unikt namn för den associerade hemligheten. Om du tar bort alla tillgängliga miljöer kan du **[!UICONTROL Add Environment]** knappen kommer inte att vara tillgänglig.

![Lägg till miljö ej tillgänglig](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Här skiljer sig stegen för att skapa hemligheten åt beroende på vilken typ av hemlighet du skapar. Se underavsnitten nedan för mer information:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)

### [!UICONTROL Token] {#token}

Om du vill skapa en tokenhemlighet väljer du **[!UICONTROL Token]** från **[!UICONTROL Type]** listruta. I **[!UICONTROL Token]** anger du den autentiseringssträng som identifieras av det system du autentiserar till. Välj **[!UICONTROL Create Secret]** för att spara hemligheten.

![Tokenhemlighet](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Om du vill skapa en HTTP-hemlighet väljer du **[!UICONTROL Simple HTTP]** från **[!UICONTROL Type]** listruta. I fälten som visas nedan anger du ett användarnamn och lösenord för inloggningsuppgifterna innan du väljer **[!UICONTROL Create Secret]** för att spara hemligheten.

>[!NOTE]
>
>När inloggningsuppgifterna sparas kodas de med [&quot;Grundläggande&quot; HTTP-autentiseringsschema](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP-hemlighet](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Om du vill skapa en OAuth 2-hemlighet väljer du **[!UICONTROL OAuth 2]** från **[!UICONTROL Type]** listruta. I fälten som visas nedan anger du [[!UICONTROL Client ID] och [!UICONTROL Client Secret]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)och [[!UICONTROL Token URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) för din OAuth-integrering. The [!UICONTROL Token URL] i användargränssnittet är en sammanfogning mellan auktoriseringsservervärden och tokensökvägen.

![OAuth 2-hemlighet](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Under **[!UICONTROL Credential Options]** kan du ange andra alternativ för autentiseringsuppgifter, till exempel `scope` och `audience` i form av nyckelvärdepar. Om du vill lägga till fler nyckelvärdepar väljer du **[!UICONTROL Add another]**.

![Alternativ för autentiseringsuppgifter](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Slutligen kan du konfigurera **[!UICONTROL Refresh Offset]** värdet för hemligheten. Detta anger antalet sekunder innan token upphör att gälla som systemet utför en automatisk uppdatering. Motsvarande tid i timmar och minuter visas till höger om fältet och uppdateras automatiskt när du skriver.

![Uppdatera förskjutning](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Om uppdateringsförskjutningen till exempel är inställd på standardvärdet `14400` (fyra timmar) och åtkomsttoken har en `expires_in` värde för `86400` (24 timmar) uppdateras hemligheten automatiskt om 20 timmar.

>[!IMPORTANT]
>
>En OAuth-hemlighet kräver minst fyra timmar mellan uppdateringarna och måste också vara giltig i minst åtta timmar. Den här begränsningen ger dig minst fyra timmar att ingripa om det uppstår problem med den genererade token.
>
>Om förskjutningen till exempel är inställd på `28800` (åtta timmar) och åtkomsttoken har en `expires_in` av `36000` (tio timmar), skulle bytet misslyckas på grund av att den resulterande skillnaden är mindre än fyra timmar.

När du är klar väljer du **[!UICONTROL Create Secret]** för att spara hemligheten.

![Spara OAuth 2-förskjutning](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

Om du vill skapa en OAuth 2 JWT-hemlighet väljer du **[!UICONTROL OAuth 2 JWT]** från **[!UICONTROL Type]** listruta.

![The [!UICONTROL Create Secret] med OAuth 2 JWT-hemlighet markerad i [!UICONTROL Type] listruta.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>De enda [!UICONTROL Algorithm] som för närvarande stöds för signering av JWT är RS256.

I fälten som visas nedan anger du [!UICONTROL Issuer], [!UICONTROL Subject], [!UICONTROL Audience], [!UICONTROL Custom Claims], [!UICONTROL TTL]väljer du [!UICONTROL Algorithm] i listrutan. Ange sedan [!UICONTROL Private Key Id]och [[!UICONTROL Token URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) för din OAuth-integrering. The [!UICONTROL Token URL] fältet är inte ett obligatoriskt fält. Om ett värde anges byts JWT ut mot en åtkomsttoken. Hemligheten kommer att uppdateras enligt `expires_in` attribut från svaret och [!UICONTROL Refresh Offset] värde. Om inget värde anges är den hemlighet som skickas till kanten JWT. Den gemensamma arbetsgruppen kommer att uppdateras i enlighet med [!UICONTROL TTL] och [!UICONTROL Refresh Offset] värden.

![The [!UICONTROL Create Secret] med ett urval av inmatningsfält markerat.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

Under **[!UICONTROL Credential Options]** kan du ange andra alternativ för autentiseringsuppgifter, till exempel `jwt_param` i form av nyckelvärdepar. Om du vill lägga till fler nyckelvärdepar väljer du **[!UICONTROL Add another]**.

![The [!UICONTROL Create Secret] tabbmarkera [!UICONTROL Credential Options] fält.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Slutligen kan du konfigurera **[!UICONTROL Refresh Offset]** värdet för hemligheten. Detta anger antalet sekunder innan token upphör att gälla som systemet utför en automatisk uppdatering. Motsvarande tid i timmar och minuter visas till höger om fältet och uppdateras automatiskt när du skriver.

![The [!UICONTROL Create Secret] tabbmarkera [!UICONTROL Refresh Offset] fält.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Om uppdateringsförskjutningen till exempel är inställd på standardvärdet `1800` (30 minuter) och åtkomsttoken har en `expires_in` värde för `3600` (en timme) uppdateras hemligheten automatiskt om en timme.

>[!IMPORTANT]
>
>En OAuth 2 JWT-hemlighet kräver minst 30 minuter mellan uppdateringarna och måste också vara giltig i minst en timme. Den här begränsningen ger dig minst 30 minuter att ingripa om det uppstår problem med den genererade token.
>
>Om förskjutningen till exempel är inställd på `1800` (30 minuter) och åtkomsttoken har en `expires_in` av `2700` (45 minuter), skulle bytet misslyckas på grund av att den resulterande skillnaden är mindre än 30 minuter.

När du är klar väljer du **[!UICONTROL Create Secret]** för att spara hemligheten.

![The [!UICONTROL Create Secret] tabbmarkering [!UICONTROL Create Secret]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Om du vill skapa en hemlighet i Google OAuth 2 väljer du **[!UICONTROL Google OAuth 2]** från **[!UICONTROL Type]** listruta. Under **[!UICONTROL Scopes]** markerar du de Google-API:er som du vill använda den här hemligheten för att ge åtkomst till. Följande produkter stöds för närvarande:

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

När du är klar väljer du **[!UICONTROL Create Secret]**.

![Google OAuth 2 - hemlighet](../../images/ui/event-forwarding/secrets/google-oauth.png)

En pover som informerar dig om att hemligheten måste auktoriseras manuellt via Google visas. Välj **[!UICONTROL Create & Authorize]** för att fortsätta.

![Google auktoriseringsleverantör](../../images/ui/event-forwarding/secrets/google-authorization.png)

En dialogruta visas där du kan ange autentiseringsuppgifter för ditt Google-konto. Följ instruktionerna för att ge händelsevidarebefordringsåtkomst till dina data i det valda omfånget. När auktoriseringsprocessen är klar skapas hemligheten.

>[!IMPORTANT]
>
>Om din organisation har en återautentiseringsprincip för Google Cloud-program kommer de hemligheter som skapas inte att uppdateras korrekt efter att autentiseringen har upphört att gälla (mellan 1 och 24 timmar beroende på principkonfigurationen).
>
>Du löser det här problemet genom att logga in på Google Admin Console och gå till **[!DNL App access control]** så att du kan markera appen för händelsevidarebefordran (Adobe Real-Time CDP Event Forwarding) som [!DNL Trusted]. Läs Google-dokumentationen på [ange sessionslängder för Google Cloud-tjänster](https://support.google.com/a/answer/9368756) för mer information.

## Redigera en hemlighet

När du har skapat hemligheter för en egenskap hittar du dem i **[!UICONTROL Secrets]** arbetsyta. Om du vill redigera informationen om en befintlig hemlighet markerar du namnet i listan.

![Välj hemlighet att redigera](../../images/ui/event-forwarding/secrets/edit-secret.png)

På nästa skärm kan du ändra namn och autentiseringsuppgifter för hemligheten.

![Redigera hemlighet](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Om hemligheten är kopplad till en befintlig miljö kan du inte tilldela om hemligheten till en annan miljö. Om du vill använda samma inloggningsuppgifter i en annan miljö måste du [skapa en ny hemlighet](#create) i stället. Det enda sättet att tilldela om miljön från den här skärmen är om du aldrig har tilldelat hemligheten till en miljö i förväg eller om du har tagit bort den miljö som hemligheten var kopplad till.

### Försök igen med ett hemligt utbyte

Du kan försöka göra om eller uppdatera ett hemligt utbyte från redigeringsskärmen. Den här processen varierar beroende på vilken typ av hemlighet som redigeras:

| Hemlig typ | Försök igen |
| --- | --- |
| [!UICONTROL Token] | Välj **[!UICONTROL Exchange Secret]** för att försöka göra om det hemliga utbytet. Den här kontrollen är bara tillgänglig när det finns en miljö kopplad till hemligheten. |
| [!UICONTROL HTTP] | Om ingen miljö är kopplad till hemligheten väljer du **[!UICONTROL Exchange Secret]** för att växla autentiseringsuppgifter till base64. Om en miljö är bifogad markerar du **[!UICONTROL Exchange and Deploy Secret]** att utbyta till base64 och driftsätta hemligheten. |
| [!UICONTROL OAuth 2] | Välj **[!UICONTROL Generate Token]** för att växla autentiseringsuppgifter och returnera en åtkomsttoken från autentiseringsprovidern. |

## Ta bort en hemlighet

Ta bort en befintlig hemlighet i  **[!UICONTROL Secrets]** på arbetsytan markerar du kryssrutan bredvid dess namn innan du markerar **[!UICONTROL Delete]**.

![Ta bort hemlighet](../../images/ui/event-forwarding/secrets/delete.png)

## Använda hemligheter i händelsevidarebefordran

Om du vill använda en hemlighet vid vidarebefordran av händelser måste du först skapa en [dataelement](../managing-resources/data-elements.md) som refererar till hemligheten. När du har sparat dataelementet kan du inkludera det i händelsevidarebefordran [regler](../managing-resources/rules.md) och lägga till dessa regler i [bibliotek](../publishing/libraries.md), som i sin tur kan driftsättas på Adobe servrar som [bygga](../publishing/builds.md).

När du skapar dataelementet väljer du **[!UICONTROL Core]** tillägg, välj **[!UICONTROL Secret]** för elementtypen data. Den högra panelen uppdateras och innehåller listrutekontroller för att tilldela dataelementet upp till tre hemligheter: en för [!UICONTROL Development], [!UICONTROL Staging]och [!UICONTROL Production] respektive.

![Dataelement](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Det är bara hemligheter kopplade till utvecklings-, staging- och produktionsmiljöerna som visas för respektive listruta.

Genom att tilldela flera hemligheter till ett dataelement och inkludera det i en regel, kan du få dataelementets värde att ändras beroende på var innehållsbiblioteket finns i [publiceringsflöde](../publishing/publishing-flow.md).

![Dataelement med flera hemligheter](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>När du skapar dataelementet måste du tilldela en utvecklingsmiljö. Hemligheter för staging- och produktionsmiljöer behövs inte, men byggen som försöker gå över till dessa miljöer kommer att misslyckas om deras dataelement av hemlig typ inte har någon hemlighet vald för den aktuella miljön.

## Nästa steg

I den här guiden beskrivs hur du hanterar hemligheter i användargränssnittet. Mer information om hur du interagerar med hemligheter med Reaktors API finns i [Slutpunktshandbok för hemligheter](../../api/endpoints/secrets.md).
