---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autentisera och få tillgång till Experience Platform API:er
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

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

1. Gå till [Adobe I/O Console](https://console.adobe.io)
2. Klicka på **Skapa ett nytt konto**
3. Slutför registreringsprocessen


### Bli utvecklare och användare av Experience Platform för en organisation

Innan du skapar integreringar på Adobe I/O måste ditt konto ha utvecklarbehörighet för en produkt i en IMS-organisation. Detaljerad information om utvecklarkonton på Admin Console finns i [supportdokumentet](https://helpx.adobe.com/enterprise/using/manage-developers.html) för hantering av utvecklare.

**Få utvecklaråtkomst**

Kontakta en administratör för Admin Console i din organisation för att lägga till dig som utvecklare för en av organisationens produkter med hjälp av [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

Administratören måste tilldela dig som utvecklare minst en produktprofil för att kunna fortsätta.

![](images/authentication/add-developer.png)

När du har utsetts till utvecklare får du behörighet att skapa integreringar på [Adobe I/O](https://console.adobe.io/). Dessa integreringar är en pipeline från externa program och tjänster till Adobe API.

**Få användaråtkomst**

Administratören för Admin Console måste också lägga till dig i produkten som användare.

![](images/authentication/assign-users.png)

På samma sätt som när du lägger till en utvecklare måste administratören tilldela dig till minst en produktprofil för att kunna fortsätta.

![](images/authentication/assign-user-details.png)


## Engångsinställning

Följande steg behöver bara utföras en gång:

* Logga in på Adobe I/O Console
* Skapa integrering
* Kopiera ned åtkomstvärden

När du har dina integrerings- och åtkomstvärden kan du återanvända dem för autentisering i framtiden. Varje steg beskrivs närmare nedan.

### Logga in på Adobe I/O Console

Gå till [Adobe I/O Console](https://console.adobe.io/) och logga in med ditt Adobe ID.

När du är inloggad klickar du på fliken **Integrationer** högst upp på skärmen. En integrering är ett tjänstkonto som skapas för den valda IMS-organisationen. Du får bara ringa anrop till den IMS-organisation som integreringen skapas i.

>[!NOTE]
>Om ditt konto är kopplat till flera organisationer kan du enkelt växla mellan dem via den nedrullningsbara menyn längst upp till höger på skärmen.

### Skapa integrering

Starta processen genom att klicka på **Ny integrering** på sidan **Integreringar** . Processen innehåller tre steg:
* Välj typ av integrering
* Välj vilken Adobe-tjänst du vill integrera med
* Lägg till integreringsinformation, offentlig nyckel och produktprofil

![](images/authentication/integrations.png)

#### Välj typ av integrering

På nästa skärm visas en fråga om du vill få åtkomst till ett API eller få händelser i realtid. Välj **Åtkomst till ett API** och sedan **Fortsätt**.

![](images/authentication/create-new-integration.png)

#### Välj vilken Adobe-tjänst du vill integrera med

Om ditt konto är kopplat till flera IMS-organisationer kan du växla mellan dem med hjälp av den nedrullningsbara menyn längst upp till höger. Välj **Workshop** och **Experience Platform API** under **Adobe Experience Platform** för att få tillgång till API:erna.

![](images/authentication/integration-select-service.png)

Klicka på **Fortsätt** för att gå till nästa avsnitt.

#### Lägg till integreringsinformation, offentlig nyckel och produktprofil

På nästa skärm får du en uppmaning om att fylla i din integreringsinformation, ange ditt certifikat för offentlig nyckel och välja en produktprofil.

![](images/authentication/integration-details.png)

Ange först din integreringsinformation. Välj sedan en produktprofil. Produktprofiler ger detaljerad åtkomst till en grupp funktioner som tillhör tjänsten som du valde i tidigare steg.

För certifikatavsnittet måste du skapa ett certifikat:

**För MacOS- och Linux-plattformar:**

Öppna kommandoraden och kör följande kommando:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**För Windows-plattformar:**

1. Hämta en öppen klient för att generera offentliga certifikat (till exempel [OpenSL Windows-klient](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. Extrahera mappen och kopiera den till C:/libs/ plats.

1. Öppna kommandoradsfråga och kör följande kommandon:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Du får ett svar som liknar följande som uppmanar dig att ange viss information om dig själv:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

När informationen har angetts skapas två filer: `certificate_pub.crt` och `private.key`.

>[!NOTE]
>`certificate_pub.crt` upphör att gälla om 365 dagar. Du kan göra perioden längre genom att ändra värdet för `days` i `openssl` kommandot ovan, men att rotera inloggningsuppgifter regelbundet är en bra säkerhetsrutin.

Den `private.key` används för att generera vår JWT i det senare avsnittet.

Den `certificate_pub.crt` används för att skapa en API-nyckel. Gå tillbaka till Adobe I/O Console och klicka på **Välj en fil** för att överföra `certificate_pub.crt` filen.

Klicka på **Skapa integrering** för att slutföra processen.

### Kopiera ned åtkomstvärden

När du har skapat integreringen kan du visa information om den. Klicka på **Hämta klienthemlighet** så ser skärmen ut ungefär så här:

![](images/authentication/access-values.png)

Kopiera värdena för `{API KEY}`, `{IMS ORG}` som är organisations-ID, och `{CLIENT SECRET}` som de kommer att användas i nästa steg.

## Autentisering för varje session

Det sista steget är att skapa `{ACCESS_TOKEN}` som ska användas för att autentisera dina API-anrop. Åtkomsttoken måste inkluderas i auktoriseringshuvudet för alla API-anrop du gör till Adobe Experience Platform. Åtkomsttoken upphör att gälla efter 24 timmar. Därefter måste nya token genereras för att du ska kunna fortsätta använda API:erna.

### Skapa JWT

Gå till fliken **JWT** när du är på integreringssidan i Adobe I/O-konsolen:

![](images/authentication/generate-jwt.png)

På sidan uppmanas du att ange den `private.key` du skapade i föregående avsnitt. Öppna kommandoraden om du vill visa innehållet i din `private.key` fil:

```shell
cat private.key
```

Resultatet ser ut ungefär så här:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Kopiera hela utdata och klistra in dem i textfältet och klicka sedan på **Generera JWT**. Kopiera den genererade JWT-filen till nästa steg.

![](images/authentication/generated-jwt.png)

### Generera åtkomsttoken

Du kan generera en åtkomsttoken med ett cURL-kommando. Om du inte har installerat cURL kan du installera det med `npm install curl`. Du kan läsa mer om cURL [här](https://curl.haxx.se/)

När cURL har installerats måste du byta ut fälten i följande kommando mot ditt eget `{API_KEY}`, `{CLIENT_SECRET}`och `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

Om det lyckas ser resultatet ut ungefär så här:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Åtkomsttoken är värdet under `access_token` nyckeln. Åtkomsttoken `expires_in` 86399947 millisekunder (24 timmar). Efteråt måste du generera en ny åtkomsttoken genom att följa stegen ovan.

Nu kan du göra API-förfrågningar i Adobe Experience Platform!

### Testa åtkomstkod

Om du vill testa om din åtkomsttoken är giltig kan du försöka att göra följande API-anrop. Detta anrop listar alla klasser i `global` behållaren:

>[!NOTE]
>`{API_KEY}` och `{IMS_ORG}` hänvisa till värdena som du genererade ovan.

**Begäran**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Om ditt svar liknar det som visas nedan `access_token` är ditt giltigt och fungerar. (Det här svaret har trunkerats för utrymme.)

**Svar**

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