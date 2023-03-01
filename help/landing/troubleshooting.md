---
keywords: Experience Platform;home;populära topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform FAQ and Troubleshooting Guide
description: Hitta svar på vanliga frågor och en användarhandbok om felsökning av vanliga fel i Experience Platform.
landing-page-description: Hitta svar på vanliga frågor och en användarhandbok om felsökning av vanliga fel i Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 3%

---

# [!DNL Platform] Vanliga frågor och felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform samt en guide på hög nivå om vanliga fel som kan uppstå i [!DNL Experience Platform] API. Felsökningsguider för enskilda användare [!DNL Platform] tjänster, se [tjänstfelsökningskatalog](#service-troubleshooting-directory) nedan.

## Vanliga frågor och svar {#faq}

Nedan följer en lista med svar på vanliga frågor om Adobe Experience Platform.

## Vad är [!DNL Experience Platform] API:er? {#what-are-experience-platform-apis}

[!DNL Experience Platform] erbjuder flera RESTful-API:er som använder HTTP-begäranden för åtkomst [!DNL Platform] resurser. Dessa tjänst-API:er visar flera slutpunkter och gör att du kan utföra åtgärder för att lista (GET), söka (GET), redigera (PUT och/eller PATCH) och ta bort (DELETE) resurser. Mer information om specifika slutpunkter och åtgärder som är tillgängliga för respektive tjänst finns i [API-referensdokumentation](https://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

## Hur formaterar jag en API-begäran? {#how-do-i-format-an-api-request}

Format varierar beroende på [!DNL Platform] API används. Det bästa sättet att lära sig att strukturera API-anrop är att följa med exemplen i dokumentationen för det aktuella [!DNL Platform] tjänster som du använder.

Mer information om hur du formaterar API-begäranden finns i guiden Komma igång-guide för plattforms-API [läsa exempel-API-anrop](./api-guide.md#sample-api) -avsnitt.

## Vad är min IMS-organisation? {#what-is-my-ims-organization}

En IMS-organisation är en Adobe-representation av en kund. Alla licensierade Adobe-lösningar är integrerade med den här kundorganisationen. När en IMS-organisation har rätt att [!DNL Experience Platform]kan den ge utvecklare åtkomst. IMS-organisations-ID (`x-gw-ims-org-id`) representerar organisationen som ett API-anrop ska köras för och därför krävs som huvud i alla API-begäranden. Detta ID finns via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): i **Integreringar** flik, navigera till **Översikt** för en viss integrering för att hitta ID:t under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur man autentiserar sig [!DNL Platform], se [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Var hittar jag min API-nyckel? {#where-can-i-find-my-api-key}

En API-nyckel krävs som huvud i alla API-begäranden. Den finns på [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). I konsolen på **Integreringar** flik, navigera till **Översikt** för en viss integrering och du hittar nyckeln under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur man autentiserar [!DNL Platform], se [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Hur får jag en åtkomsttoken? {#how-do-i-get-an-access-token}

Åtkomsttoken krävs i auktoriseringshuvudet för alla API-anrop. De kan genereras med en `curl` -kommando, förutsatt att du har tillgång till en integrering för en IMS-organisation. Åtkomsttoken är bara giltiga i 24 timmar. Därefter måste en ny token skapas för att du ska kunna fortsätta använda API:t. Mer information om hur du genererar åtkomsttoken finns i [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Hur använder jag frågeparametrar? {#how-do-i-user-query-parameters}

Några [!DNL Platform] API-slutpunkter accepterar frågeparametrar för att hitta specifik information och filtrera resultaten som returneras i svaret. Frågeparametrar läggs till i sökvägar med frågetecken (`?`), följt av en eller flera frågeparametrar med formatet `paramName=paramValue`. När du kombinerar flera parametrar i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda parametrar. I följande exempel visas hur en begäran som använder flera frågeparametrar återges i dokumentationen.

Exempel på vanliga frågeparametrar är:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Mer information om vilka frågeparametrar som är tillgängliga för en viss tjänst eller slutpunkt finns i den servicespecifika dokumentationen.

## Hur anger jag att ett JSON-fält ska uppdateras i en PATCH-begäran? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Många PATCH-åtgärder i [!DNL Platform] API:er använder [JSON-pekare](https://tools.ietf.org/html/rfc6901) strängar som anger JSON-egenskaper som ska uppdateras. Dessa inkluderas vanligtvis i begärandenyttolaster som använder [JSON Patch](https://tools.ietf.org/html/rfc6902) format. Se [Grundläggande API-guide](api-fundamentals.md) för detaljerad information om nödvändig syntax för dessa tekniker.

## Kan jag använda Postman för att ringa [!DNL Platform] API:er? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) är ett användbart verktyg för att visualisera anrop till RESTful API:er. The [Starthandbok för att komma igång med plattforms-API](api-guide.md) innehåller en video och instruktioner för hur du importerar Postman-samlingar. Dessutom finns en lista över Postman-samlingar för varje tjänst.

## Vilka är systemkraven för [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Beroende på om du använder gränssnittet eller API:t gäller följande systemkrav:

**För UI-baserade åtgärder:**
- En modern standardwebbläsare. Medan den senaste versionen av [!DNL Chrome] rekommenderas, aktuella och tidigare större versioner av [!DNL Firefox], [!DNL Internet Explorer]och Safari stöds också.
   - Varje gång en ny större version släpps, [!DNL Platform] har stöd för den senaste versionen medan stöd för den tredje senaste versionen har tagits bort.
- Alla webbläsare måste ha cookies och JavaScript aktiverat.

**För API- och utvecklarinteraktioner:**
- En utvecklingsmiljö som ska utvecklas för integrering av REST, strömning och Webkrok.

## Fel och felsökning {#errors-and-troubleshooting}

Nedan följer en lista över fel som du kan råka ut för när du använder [!DNL Experience Platform] service. Felsökningsguider för enskilda användare [!DNL Platform] tjänster, se [tjänstfelsökningskatalog](#service-troubleshooting-directory) nedan.

## API-statuskoder {#api-status-codes}

Följande statuskoder kan påträffas på alla [!DNL Experience Platform] API. Det finns en mängd orsaker till detta, och därför är de förklaringar som ges i detta avsnitt av allmän karaktär. Mer information om specifika fel i enskilda [!DNL Platform] tjänster, se [tjänstfelsökningskatalog](#service-troubleshooting-directory) nedan.

| Statuskod | Beskrivning | Möjliga orsaker |
|--- | --- | ---|
| 400 | Felaktig begäran | Begäran är felaktigt konstruerad, nyckelinformation saknas och/eller innehåller felaktig syntax. |
| 401 | Autentiseringen misslyckades | Begäran klarade inte en autentiseringskontroll. Åtkomsttoken kanske saknas eller är ogiltig. Se [OAuth-tokenfel](#oauth-token-is-missing) för mer information. |
| 403 | Förbjuden | Resursen hittades, men du har inte rätt autentiseringsuppgifter för att visa den. |
| 404 | Hittades inte | Det gick inte att hitta den begärda resursen på servern. Resursen kan ha tagits bort eller så har den begärda sökvägen angetts felaktigt. |
| 500 | Internt serverfel | Det här är ett serverfel. Om du gör många samtidiga anrop kanske du når API-gränsen och behöver filtrera resultaten. (Se [!DNL Catalog Service] Utvecklarhandbok för API på [filtrera data](../catalog/api/filter-data.md) om du vill veta mer.) Vänta en stund innan du försöker utföra din begäran igen och kontakta administratören om problemet kvarstår. |

## Fel i begärandehuvud {#request-header-errors}

Alla API-anrop [!DNL Platform] kräver särskilda begäranrubriker. Om du vill se vilka huvuden som krävs för enskilda tjänster kan du gå till [API-referensdokumentation](https://www.adobe.com/go/platform-api-reference-en). Information om hur du hittar värdena för de obligatoriska autentiseringshuvudena finns i [Självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). Om någon av dessa rubriker saknas eller är ogiltig när ett API-anrop görs kan följande fel uppstå.

### OAuth-token saknas {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Det här felmeddelandet visas när en `Authorization` huvud saknas i en API-begäran. Kontrollera att auktoriseringshuvudet ingår i en giltig åtkomsttoken innan du försöker igen.

### OAuth-token är inte giltig {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Det här felmeddelandet visas när den angivna åtkomsttoken finns i `Authorization` header is not valid. Kontrollera att token har angetts korrekt, eller [generera en ny token](https://www.adobe.com/go/platform-api-authentication-en) i Adobe I/O Console.

### API-nyckel krävs {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Det här felmeddelandet visas när ett API-nyckelhuvud (`x-api-key`) saknas i en API-begäran. Kontrollera att rubriken är inkluderad med en giltig API-nyckel innan du försöker igen.

### API-nyckeln är ogiltig {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Det här felmeddelandet visas när värdet för den angivna API-nyckelrubriken (`x-api-key`) är ogiltigt. Kontrollera att du har angett nyckeln korrekt innan du försöker igen. Om du inte känner till din API-nyckel kan du hitta den i [Adobe I/O Console](https://console.adobe.io): i **Integreringar** flik, navigera till **Översikt** för en specifik integrering för att hitta API-nyckeln under **Klientautentiseringsuppgifter**.

### Rubrik saknas {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Det här felmeddelandet visas när en IMS-organisationshuvud (`x-gw-ims-org-id`) saknas i en API-begäran. Kontrollera att rubriken är inkluderad i ID:t för IMS-organisationen innan du försöker igen.

### Profilen är inte giltig {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Det här felmeddelandet visas när integreringen mellan användare och Adobe I/O (identifieras av [åtkomsttoken](#how-do-i-get-an-access-token) i `Authorization` header) inte har rätt att ringa [!DNL Experience Platform] API:er för IMS-organisationen som finns i `x-gw-ims-org-id` header. Kontrollera att du har angett rätt ID för IMS-organisationen i sidhuvudet innan du försöker igen. Om du inte känner till ditt organisations-ID kan du hitta det i [Adobe I/O Console](https://console.adobe.io): i **Integreringar** flik, navigera till **Översikt** för en specifik integrering för att hitta ID:t under **Klientautentiseringsuppgifter**.

### Fel vid uppdatering av tagg {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Du kan få ett taggfel om en ändring har gjorts för en käll- eller målenhet, t.ex. flöde, anslutning, källkoppling eller målanslutning av en annan API-anropare. På grund av versionsmatchningsfelet tillämpas inte den ändring du försöker göra på den senaste versionen av entiteten.

För att lösa detta måste du hämta entiteten igen, se till att dina ändringar är kompatibla med den nya versionen av entiteten och sedan placera den nya taggen i `If-Match` och anropa slutligen API.

### Giltig innehållstyp har inte angetts {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Det här felmeddelandet visas när en POST-, PUT eller PATCH-begäran saknar eller är ogiltig `Content-Type` header. Kontrollera att rubriken är inkluderad i begäran och att dess värde är `application/json`.

### Användarregion saknas {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Det här felmeddelandet visas i något av följande två fall:
- Om IMS-organisationshuvudet är felaktigt eller har fel format (`x-gw-ims-org-id`) skickas i en API-begäran. Kontrollera att rätt ID för IMS-organisationen finns med innan du försöker igen.
- När ditt konto (som representeras av de angivna autentiseringsuppgifterna) inte är associerat med en produktprofil för Experience Platform. Följ stegen på [generera autentiseringsuppgifter](./api-authentication.md#authentication-for-each-session) i självstudiekursen för autentisering av plattforms-API för att lägga till plattform i ditt konto och uppdatera dina autentiseringsuppgifter i enlighet med detta.

## Felsökningskatalog för tjänst {#service-troubleshooting-directory}

Här följer en lista med felsökningsguider och API-referensdokumentation för [!DNL Experience Platform] API:er. Varje felsökningsguide ger svar på vanliga frågor och lösningar på problem som är specifika för enskilda användare [!DNL Platform] tjänster. API-referensdokumenten innehåller en omfattande guide till alla tillgängliga slutpunkter för varje tjänst och visar exempel på begärandetexter, svar och felkoder som du kan få.

| Tjänst | API-referens | Felsökning |
| --- | --- | --- |
| Åtkomstkontroll | [API för åtkomstkontroll](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Felsökningsguide för åtkomstkontroll](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform datainmatning | [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) | [Felsökningsguide för batchimport](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Felsökningsguide för direktuppspelning](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] felsökningsguide](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform datastyrning | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] felsökningsguide](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] felsökningsguide](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentering | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Vanliga frågor och felsökningsguide](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] och [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] felsökningsguide](../profile/troubleshooting.md) |
| Sandlådor | [Sandbox-API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Felsökningsguide för sandlådor](../sandboxes/troubleshooting-guide.md) |
