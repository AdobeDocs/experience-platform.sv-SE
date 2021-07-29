---
title: Komma igång med Reactor API
description: Lär dig hur du kommer igång med Reaktors-API, inklusive steg för att generera nödvändiga inloggningsuppgifter.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 0%

---

# Komma igång med Reactor API

För att kunna använda [Reaktors-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml) måste varje begäran innehålla följande autentiseringsrubriker:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

I den här guiden beskrivs hur du använder utvecklarkonsolen i Adobe för att samla in värdena för vart och ett av dessa rubriker så att du kan börja anropa Reaktors API.

## Få utvecklare tillgång till Adobe Experience Platform

Innan du kan generera autentiseringsvärden för Reactor API måste du ha utvecklaråtkomst till Experience Platform. Följ de inledande stegen i [självstudiekursen för autentisering av Experience Platform](http://www.adobe.com/go/platform-api-authentication-en) för att få utvecklaråtkomst. När du kommit till steget&quot;Generera inloggningsuppgifter i Adobe Developer Console&quot; går du tillbaka till den här självstudiekursen för att generera de inloggningsuppgifter som är specifika för Reactor API.

## Generera autentiseringsuppgifter för åtkomst

Med Adobe Developer Console måste du generera följande tre autentiseringsuppgifter:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

IMS-organisationens ID (`{IMS_ORG}`) och API-nyckel (`{API_KEY}`) kan återanvändas i framtida API-anrop efter att de har skapats initialt. Åtkomsttoken (`{ACCESS_TOKEN}`) är tillfällig och måste genereras om var 24:e timme.

Stegen för att generera dessa värden beskrivs närmare nedan.

### Engångskonfiguration

Gå till [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) och logga in med din Adobe ID. Följ sedan stegen som beskrivs i självstudiekursen om att [skapa ett tomt projekt](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) i dokumentationen för Developer Console.

När du har skapat ett projekt väljer du **Lägg till API** på skärmen **Projektöversikt**.

![](../images/api/getting-started/add-api-button.png)

Skärmen **Lägg till ett API** visas. Välj **Experience Platform Reactor API** i listan över tillgängliga API:er innan du väljer **Next**.

![](../images/api/getting-started/add-launch-api.png)

På nästa skärm uppmanas du att skapa en JWT-autentiseringsuppgift (JSON Web Token) som antingen genererar ett nytt nyckelpar eller överför din egen offentliga nyckel. I den här självstudiekursen väljer du alternativet **Generera ett nyckelpar** och sedan **Generera nyckelpar** i det nedre högra hörnet.

![](../images/api/getting-started/create-jwt.png)

Nästa skärm bekräftar att nyckelparet har genererats och en komprimerad mapp som innehåller ett offentligt certifikat och en privat nyckel hämtas automatiskt till datorn. Den här privata nyckeln krävs i ett senare steg för att generera en åtkomsttoken.

Välj **Nästa** om du vill fortsätta.

![](../images/api/getting-started/keypair-generated.png)

På nästa skärm får du en uppmaning om att välja en eller flera produktprofiler som ska associeras med API-integreringen.

>[!NOTE]
>
>Produktprofiler hanteras av er organisation via Adobe Admin Console och innehåller specifika behörighetsgrupper för detaljfunktioner. Produktprofiler och deras behörigheter kan bara hanteras av användare med administratörsbehörighet inom organisationen. Om du är osäker på vilka produktprofiler du ska välja för API kontaktar du administratören.

Välj önskade produktprofiler i listan och välj sedan **Spara konfigurerad API** för att slutföra API-registreringen.

![](../images/api/getting-started/select-product-profile.png)

När API:t har lagts till i projektet visas projektsidan igen på Experience Platform Reactor API-sidan. Här rullar du ned till avsnittet **Tjänstkonto (JWT)**, som innehåller följande autentiseringsuppgifter som krävs för alla anrop till Reactor API:

* **KLIENT-ID**: Klient-ID är det obligatoriska  `{API_KEY}` som måste anges i  `x-api-key` rubriken.
* **ORGANISATIONS-ID**: Organisations-ID är det  `{IMS_ORG}` värde som måste användas i  `x-gw-ims-org-id` rubriken.

![](../images/api/getting-started/access-creds.png)

### Autentisering för varje session

Nu när du har dina `{API_KEY}`- och `{IMS_ORG}`-värden genererar det sista steget ett `{ACCESS_TOKEN}`-värde.

>[!NOTE]
>
>Dessa token upphör att gälla efter 24 timmar. Om du använder den här integreringen för ett program är det en bra idé att hämta din innehavartoken programmatiskt inifrån programmet.

Det finns två alternativ för att generera åtkomsttoken, beroende på hur du använder dem:

* [Generera tokens manuellt](#manual)
* [Generera tokens programmatiskt](#program)

#### Generera åtkomsttoken manuellt {#manual}

Öppna den privata nyckeln som du hämtade tidigare i en textredigerare eller webbläsare och kopiera innehållet. Gå sedan tillbaka till Developer Console och klistra in den privata nyckeln i avsnittet **Generera åtkomsttoken** på API-sidan för reaktorn för ditt projekt innan du väljer **Generera token**.

![](../images/api/getting-started/paste-private-key.png)

En ny åtkomsttoken genereras och en knapp för att kopiera token till Urklipp tillhandahålls. Det här värdet används för det obligatoriska `Authorization`-huvudet och måste anges i formatet `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### Generera åtkomsttoken programmatiskt {#program}

Om du använder integreringen för ett program kan du programmässigt generera åtkomsttoken via API-begäranden. För att uppnå detta måste du få följande värden:

* Klient-ID (`{API_KEY}`)
* Klienthemlighet (`{SECRET}`)
* En JSON-webbtoken (`{JWT}`)

Ditt klient-ID och din hemlighet kan hämtas från huvudsidan för ditt projekt, vilket visas i [föregående steg](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

Om du vill hämta JWT-autentiseringsuppgifter går du till **JWT (Service Account)** till vänster och väljer sedan fliken **Generera JWT**. På den här sidan, under **Generera anpassad JWT**, klistrar du in innehållet i din privata nyckel i den angivna textrutan och väljer sedan **Generera token**.

![](../images/api/getting-started/generate-jwt.png)

Den genererade JWT-filen visas nedan när bearbetningen är klar, tillsammans med ett exempel på ett cURL-kommando som du kan använda för att testa variabeln om du vill. Använd knappen **Kopiera** för att kopiera token till Urklipp.

![](../images/api/getting-started/jwt-generated.png)

När du har samlat in dina inloggningsuppgifter kan du integrera API-anropet nedan i ditt program för att programmatiskt generera åtkomsttoken.

**Begäran**

Begäran måste skicka en `multipart/form-data`-nyttolast, med dina autentiseringsuppgifter som visas nedan:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Svar**

Ett lyckat svar returnerar en ny åtkomsttoken samt antalet sekunder som återstår tills det upphör att gälla.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Egenskap | Beskrivning |
| :-- | :-- |
| `access_token` | Det nyligen genererade åtkomsttokenvärdet. Det här värdet används för det obligatoriska `Authorization`-huvudet och måste anges i formatet `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | Återstående tid tills token upphör att gälla, i millisekunder. När en token upphör att gälla måste en ny genereras. |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

Om du följer stegen i den här självstudiekursen bör du ha ett giltigt värde för `{IMS_ORG}`, `{API_KEY}` och `{ACCESS_TOKEN}`. Du kan nu testa dessa värden genom att använda dem i en enkel cURL-begäran till Reactor API.

Börja med att försöka göra ett API-anrop till [listan över alla företag](./endpoints/companies.md#list).

>[!NOTE]
>
>Du kanske inte har några företag i din organisation, och då är svaret HTTP-status 404 (Hittades inte). Så länge du inte får ett 403-fel (Ej tillåtet) är dina inloggningsuppgifter giltiga och fungerar.

När du har bekräftat att dina inloggningsuppgifter fungerar kan du fortsätta att utforska den andra API-referensdokumentationen och lära dig API:ts många funktioner.

## Ytterligare resurser

JWT Libraries och SDK: [https://jwt.io/](https://jwt.io/)

API-utveckling för Postman: [https://www.postman.com/](https://www.postman.com/)
