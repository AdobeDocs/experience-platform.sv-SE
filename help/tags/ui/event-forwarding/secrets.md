---
title: Konfigurera hemligheter i händelsevidarebefordran
description: Lär dig hur du konfigurerar hemligheter i användargränssnittet för datainsamling för att autentisera slutpunkter som används i egenskaper för vidarebefordran av händelser.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 737354ca3b286f6c39cb71bc09aa4d6141c4d9a4
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 0%

---

# Konfigurera hemligheter i händelsevidarebefordran

Vid vidarebefordran av händelser är en hemlighet en resurs som representerar autentiseringsuppgifter för ett annat system, vilket möjliggör säkert datautbyte. Det går bara att skapa hemligheter i egenskaper för vidarebefordran av händelser.

Det finns för närvarande tre hemliga typer som stöds:

| Hemlig typ | Beskrivning |
| --- | --- |
| [!UICONTROL Token] | En enda teckensträng som representerar ett autentiseringstokenvärde som är känt och begripligt för båda systemen. |
| [!UICONTROL HTTP] | Innehåller två strängattribut för ett användarnamn respektive ett lösenord. |
| [!UICONTROL OAuth2] | Innehåller flera attribut som stöder [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) autentiseringsspecifikation. Systemet ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig med ett angivet intervall. För närvarande bara [Klientautentiseringsuppgifter](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) version av OAuth2 stöds. |

{style=&quot;table-layout:auto&quot;}

Den här guiden ger en översikt på hög nivå över hur du konfigurerar hemligheter för en händelsevidarebefordring ([!UICONTROL Edge]) i användargränssnittet för datainsamling.

>[!NOTE]
>
>Detaljerad vägledning om hur du hanterar hemligheter i Reaktors-API:t, inklusive exempel-JSON för en hems struktur, finns i [API-guide för hemligheter](../../api/guides/secrets.md).

## Förutsättningar

I den här handboken förutsätts det att du redan känner till hur du hanterar resurser för taggar och vidarebefordran av händelser i användargränssnittet för datainsamling, inklusive hur du skapar ett dataelement och en regel för vidarebefordran av händelser. Se guiden [hantera resurser](../managing-resources/overview.md) om du behöver en introduktion.

Du bör också ha en fungerande förståelse för publiceringsflödet för taggar och vidarebefordran av händelser, inklusive hur du lägger till resurser i ett bibliotek och installerar ett bygge på webbplatsen för testning. Se [publicera översikt](../publishing/overview.md) för mer information.

## Skapa en hemlighet {#create}

Om du vill skapa en hemlighet loggar du in på användargränssnittet för datainsamlingen och öppnar den händelsevidarebefordringsegenskap som du vill lägga till hemligheten under. Nästa, välj **[!UICONTROL Secrets]** i den vänstra navigeringen, följt av **[!UICONTROL Create New Secret]**.

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
* [[!UICONTROL OAuth2]](#oauth2)

### [!UICONTROL Token] {#token}

Om du vill skapa en tokenhemlighet väljer du **[!UICONTROL Token]** från **[!UICONTROL Type]** listruta. I **[!UICONTROL Token]** anger du den autentiseringssträng som identifieras av det system du autentiserar till. Välj **[!UICONTROL Create Secret]** för att spara hemligheten.

![Tokenhemlighet](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Om du vill skapa en HTTP-hemlighet väljer du **[!UICONTROL Simple HTTP]** från **[!UICONTROL Type]** listruta. I fälten som visas nedan anger du ett användarnamn och lösenord för inloggningsuppgifterna innan du väljer **[!UICONTROL Create Secret]** för att spara hemligheten.

>[!NOTE]
>
>När inloggningsuppgifterna sparas kodas de med [&quot;Grundläggande&quot; HTTP-autentiseringsschema](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP-hemlighet](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth2] {#oauth2}

Om du vill skapa en OAuth2-hemlighet väljer du **[!UICONTROL OAuth2]** från **[!UICONTROL Type]** listruta. I fälten som visas nedan anger du [[!UICONTROL Client ID] och [!UICONTROL Client Secret]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)och [Autentiserings-URL](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) för din OAuth-integrering. The [!UICONTROL Authorization URL] i användargränssnittet för datainsamling är en sammanfogning mellan auktoriseringsservervärden och tokensökvägen.

![OAuth2-hemlighet](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

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

![Spara OAuth2-förskjutning](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

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
| [!UICONTROL OAuth2] | Välj **[!UICONTROL Generate Token]** för att växla autentiseringsuppgifter och returnera en åtkomsttoken från autentiseringsprovidern. |

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

I den här guiden beskrivs hur du hanterar hemligheter i användargränssnittet för datainsamling. Mer information om hur du interagerar med hemligheter med Reaktors API finns i [Slutpunktshandbok för hemligheter](../../api/endpoints/secrets.md).
