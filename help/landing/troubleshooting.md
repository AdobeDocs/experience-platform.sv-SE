---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vanliga frågor om Adobe Experience Platform och felsökningsguide
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 1%

---


# [!DNL Platform] Vanliga frågor och felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform samt en felsökningsguide på hög nivå för vanliga fel som kan uppstå i alla [!DNL Experience Platform] API:er. Felsökningsguider för enskilda [!DNL Platform] tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## Vanliga frågor {#faq}

Här följer en lista med svar på vanliga frågor om Adobe Experience Platform.

## Vad är [!DNL Experience Platform] API:er? {#what-are-experience-platform-apis}

[!DNL Experience Platform] erbjuder flera RESTful-API:er som använder HTTP-begäranden för att komma åt [!DNL Platform] resurser. Dessa tjänst-API:er visar var och en flera slutpunkter och gör att du kan utföra åtgärder för att lista (GET), söka (GET), redigera (PUT och/eller PATCH) och ta bort (DELETE) resurser. Mer information om specifika slutpunkter och åtgärder som är tillgängliga för respektive tjänst finns i [API-referensdokumentationen](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) för Adobe I/O.

## Hur formaterar jag en API-begäran? {#how-do-i-format-an-api-request}

Format för förfrågningar varierar beroende på vilket API som [!DNL Platform] används. Det bästa sättet att lära sig att strukturera API-anrop är att följa med exemplen i dokumentationen för den aktuella [!DNL Platform] tjänsten.

### Läser exempel-API-anrop

I dokumentationen för [!DNL Experience Platform] visas exempel-API-anrop på två olika sätt. Först presenteras anropet i dess **API-format**, en mallrepresentation som endast visar operationen (GET, POST, PUT, PATCH, DELETE) och slutpunkten som används (till exempel `/global/classes`). Vissa mallar visar också var det finns variabler för att illustrera hur ett anrop ska formuleras, till exempel `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Anropen visas sedan som cURL-kommandon i en **begäran**, som innehåller nödvändiga rubriker och fullständig &quot;bassökväg&quot; som behövs för att interagera med API:t. Basbanan ska vara förpended för alla slutpunkter. Den tidigare nämnda `/global/classes` slutpunkten blir till exempel `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Du kommer att se API-formatet/begäranmönstret i hela dokumentationen och förväntas använda den fullständiga sökvägen som visas i exempelbegäran när du anropar Platform API:er.

### Exempel på API-begäran

Följande är ett exempel på en API-begäran som visar vilket format du kommer att stöta på i dokumentationen.

**API-format**

API-formatet visar åtgärden (GET) och slutpunkten som används. Variabler indikeras med klammerparenteser (i det här fallet `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Begäran**

I den här exempelbegäran får variablerna från API-formatet faktiska värden i sökvägen för begäran. Alla obligatoriska rubriker visas också, som exempel på rubrikvärden eller variabler där känslig information (t.ex. säkerhetstoken och åtkomst-ID) ska inkluderas.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret visar vad du förväntar dig efter ett lyckat anrop till API:t, baserat på den begäran som skickades. Ibland kortas svaret av för blanksteg, vilket innebär att du kan se mer information eller mer information än den som visas i exemplet.

```json
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
    ],
    "_links": {}
}
```

Mer information om specifika slutpunkter i Platform API:er, inklusive obligatoriska rubriker och förfrågningsbrödtext, finns i [API-referensdokumentationen](https://www.adobe.io/apis/experienceplatform/home/api-reference.html).

## Vad är min IMS-organisation? {#what-is-my-ims-organization}

En IMS-organisation är en Adobe-representation av en kund. Alla licensierade Adobe-lösningar är integrerade med denna kundorganisation. När en IMS-organisation har rätt till [!DNL Experience Platform]kan den tilldela utvecklare åtkomst. IMS-organisationsnumret (`x-gw-ims-org-id`) representerar organisationen som ett API-anrop ska köras för och därför krävs som huvud i alla API-begäranden. Detta ID finns på [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en viss integrering för att hitta ID:t under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur du autentiserar dig [!DNL Platform]finns i [självstudiekursen](../tutorials/authentication.md)för autentisering.

## Var hittar jag min API-nyckel? {#where-can-i-find-my-api-key}

En API-nyckel krävs som huvud i alla API-begäranden. Du hittar den på [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). På fliken **Integrationer** i konsolen går du till **Översikt** för en viss integrering och du hittar nyckeln under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur du autentiserar dig [!DNL Platform]finns i [självstudiekursen](../tutorials/authentication.md)för autentisering.

## Hur får jag en åtkomsttoken? {#how-do-i-get-an-access-token}

Åtkomsttoken krävs i auktoriseringshuvudet för alla API-anrop. De kan genereras med ett `curl` kommando, förutsatt att du har tillgång till en integrering för en IMS-organisation. Åtkomsttoken är bara giltiga i 24 timmar. Därefter måste en ny token skapas för att du ska kunna fortsätta använda API:t. Mer information om hur du genererar åtkomsttoken finns i [självstudiekursen](../tutorials/authentication.md)för autentisering.

## Hur använder jag frågeparametrar? {#how-do-i-user-query-parameters}

Vissa API- [!DNL Platform] slutpunkter accepterar frågeparametrar för att hitta specifik information och filtrera resultaten som returneras i svaret. Frågeparametrar läggs till för att begära sökvägar med ett frågetecken (`?`), följt av en eller flera frågeparametrar med formatet `paramName=paramValue`. När du kombinerar flera parametrar i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda parametrar. I följande exempel visas hur en begäran som använder flera frågeparametrar återges i dokumentationen.

Exempel på vanliga frågeparametrar är:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Mer information om vilka frågeparametrar som är tillgängliga för en viss tjänst eller slutpunkt finns i den servicespecifika dokumentationen.

## Hur anger jag att ett JSON-fält ska uppdateras i en PATCH-begäran? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Många PATCH-åtgärder i API: [!DNL Platform] er använder [JSON-pekarsträngar](https://tools.ietf.org/html/rfc6901) för att ange att JSON-egenskaper ska uppdateras. Dessa inkluderas vanligtvis i begärandenyttolaster i [JSON-korrigeringsformat](https://tools.ietf.org/html/rfc6902) . I [API-handboken](api-fundamentals.md) finns detaljerad information om syntaxen som krävs för dessa tekniker.

## Kan jag använda Postman för att ringa till API: [!DNL Platform] er? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) är ett användbart verktyg för att visualisera anrop till RESTful API:er. I det här [mediapostmeddelandet](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beskrivs hur du kan konfigurera Postman så att autentisering utförs automatiskt och använda det för att använda [!DNL Experience Platform] API:er.

## Vilka är systemkraven för [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Beroende på om du använder gränssnittet eller API:t gäller följande systemkrav:

**För UI-baserade åtgärder:**
- En modern standardwebbläsare. Den senaste versionen av [!DNL Chrome] rekommenderas, men både aktuella och tidigare större versioner av [!DNL Firefox], [!DNL Internet Explorer]och Safari stöds också.
   - Varje gång en ny större version släpps får [!DNL Platform] stöd för den senaste versionen samtidigt som stödet för den tredje senaste versionen tas bort.
- Alla webbläsare måste ha cookies och JavaScript aktiverat.

**För API- och utvecklarinteraktioner:**
- En utvecklingsmiljö som ska utvecklas för integrering av REST, strömning och Webkrok.

## Fel och felsökning {#errors-and-troubleshooting}

Nedan följer en lista över fel som kan uppstå när du använder någon [!DNL Experience Platform] tjänst. Felsökningsguider för enskilda [!DNL Platform] tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## API-statuskoder {#api-status-codes}

Följande statuskoder kan påträffas i alla [!DNL Experience Platform] API:er. Det finns en mängd orsaker till detta, och därför är de förklaringar som ges i detta avsnitt av allmän karaktär. Mer information om specifika fel i enskilda [!DNL Platform] tjänster finns i [felsökningskatalogen](#service-troubleshooting-directory) nedan.

| Statuskod | Beskrivning | Möjliga orsaker |
--- | --- | ---
| 400 | Felaktig begäran | Begäran är felaktigt konstruerad, saknar nyckelinformation och/eller innehåller felaktig syntax. |
| 401 | Autentiseringen misslyckades | Begäran klarade inte en autentiseringskontroll. Åtkomsttoken kanske saknas eller är ogiltig. Mer information finns i avsnittet [OAuth-tokenfel](#oauth-token-is-missing) nedan. |
| 403 | Förbjuden | Resursen hittades, men du har inte rätt autentiseringsuppgifter för att visa den. |
| 404 | Hittades inte | Det gick inte att hitta den begärda resursen på servern. Resursen kan ha tagits bort eller så har den begärda sökvägen angetts felaktigt. |
| 500 | Internt serverfel | Det här är ett serverfel. Om du gör många samtidiga anrop kanske du når API-gränsen och behöver filtrera resultaten. (Läs mer i underhandboken för [!DNL Catalog Service] API-utvecklare om [filtrering av data](../catalog/api/filter-data.md) .) Vänta en stund innan du försöker utföra din begäran igen och kontakta administratören om problemet kvarstår. |

## Fel i begärandehuvud {#request-header-errors}

Alla API-anrop i [!DNL Platform] kräver specifika begäranderubriker. Om du vill se vilka huvuden som krävs för enskilda tjänster kan du läsa [API-referensdokumentationen](https://www.adobe.io/apis/experienceplatform/home/api-reference.html). Om du vill hitta värden för de obligatoriska autentiseringshuvuden kan du läsa [Autentisering](../tutorials/authentication.md). Om någon av dessa rubriker saknas eller är ogiltig när ett API-anrop görs kan följande fel uppstå.

### OAuth-token saknas {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Det här felmeddelandet visas när ett `Authorization` huvud saknas i en API-begäran. Kontrollera att auktoriseringshuvudet ingår i en giltig åtkomsttoken innan du försöker igen.

### OAuth-token är inte giltig

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Det här felmeddelandet visas när den angivna åtkomsttoken i huvudet inte är giltig `Authorization` . Kontrollera att token har angetts korrekt eller [generera en ny token](../tutorials/authentication.md) i Adobe I/O Console.

### API-nyckel krävs

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Det här felmeddelandet visas när en API-nyckelrubrik (`x-api-key`) saknas i en API-begäran. Kontrollera att rubriken är inkluderad med en giltig API-nyckel innan du försöker igen.

### API-nyckeln är ogiltig

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Det här felmeddelandet visas när värdet för det angivna API-nyckelhuvudet (`x-api-key`) är ogiltigt. Kontrollera att du har angett nyckeln korrekt innan du försöker igen. Om du inte känner till din API-nyckel kan du hitta den i [Adobe I/O Console](https://console.adobe.io): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en viss integrering för att hitta API-nyckeln under **Klientautentiseringsuppgifter**.


### Rubrik saknas

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Det här felmeddelandet visas när en IMS-organisationshuvud (`x-gw-ims-org-id`) saknas i en API-begäran. Kontrollera att rubriken är inkluderad i ID:t för IMS-organisationen innan du försöker igen.

### Profilen är inte giltig

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Det här felmeddelandet visas när användaren eller Adobe I/O-integreringen (som identifieras av [åtkomsttoken](#how-do-i-get-an-access-token) i `Authorization` huvudet) inte har rätt att anropa API: [!DNL Experience Platform] er för IMS-organisationen som anges i `x-gw-ims-org-id` rubriken. Kontrollera att du har angett rätt ID för IMS-organisationen i sidhuvudet innan du försöker igen. Om du inte känner till ditt organisations-ID kan du hitta det i [Adobe I/O Console](https://console.adobe.io): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en specifik integrering för att hitta ID:t under **Klientautentiseringsuppgifter**.

### Giltig innehållstyp har inte angetts

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Det här felmeddelandet visas när en POST-, PUT- eller PATCH-begäran har ett ogiltigt eller saknar `Content-Type` huvud. Kontrollera att rubriken är inkluderad i begäran och att dess värde är `application/json`.


## Felsökningskatalog för tjänst {#service-troubleshooting-directory}

Här följer en lista med felsökningsguider och API-referensdokumentation för API: [!DNL Experience Platform] er. Varje felsökningsguide ger svar på vanliga frågor och lösningar på problem som är specifika för enskilda [!DNL Platform] tjänster. API-referensdokumenten innehåller en omfattande guide till alla tillgängliga slutpunkter för varje tjänst och visar exempel på begärandetexter, svar och felkoder som du kan få.

| Tjänst | API-referens | Felsökning |
--- | --- | ---
| Åtkomstkontroll | [API för åtkomstkontroll](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Felsökningsguide för åtkomstkontroll](../access-control/troubleshooting-guide.md) |
| Katalog | [Katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Dataintag (batch) | [API för datainmatning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Felsökningsguide för batchimport](../ingestion/batch-ingestion/troubleshooting.md) |
| Dataintag (direktuppspelning) | [API för datainmatning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Felsökningsguide för direktuppspelning](../ingestion/streaming-ingestion/troubleshooting.md) |
| Datavetenskapens arbetsyta | [API för Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Felsökningsguide för Data Science Workspace](../data-science-workspace/troubleshooting-guide.md) |
| Dataanvändningsetiketter och -verkställighet (DULE) | [API för DULE-principtjänst](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Experience Data Model (XDM) | [API för schemaregister](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [Vanliga frågor om XDM-system och felsökningsguide](../xdm/troubleshooting-guide.md) |
| Identitetstjänst | [Identitetstjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Felsökningsguide för identitetstjänst](../identity-service/troubleshooting-guide.md) |
| Frågetjänst | [API för frågetjänst](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Felsökningsguide för frågetjänst](../query-service/troubleshooting-guide.md) |
| Kundprofil i realtid | [Kundprofil-API i realtid](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| Sandlådor | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Felsökningsguide för sandlådor](../sandboxes/troubleshooting-guide.md) |
| Segmentering | [Segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |