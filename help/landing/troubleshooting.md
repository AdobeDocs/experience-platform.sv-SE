---
keywords: Experience Platform;home;populära topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform FAQ and Troubleshooting Guide
description: Hitta svar på vanliga frågor och en användarhandbok om felsökning av vanliga fel i Adobe Experience Platform.
landing-page-description: Hitta svar på vanliga frågor och en användarhandbok om felsökning av vanliga fel i Adobe Experience Platform.
short-description: Hitta svar på vanliga frågor och en användarhandbok om felsökning av vanliga fel i Experience Platform.
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 3%

---

# [!DNL Experience Platform] Vanliga frågor och felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform samt en felsökningsguide på hög nivå för vanliga fel som kan uppstå i ett [!DNL Experience Platform]-API. Felsökningsguider för enskilda [!DNL Experience Platform]-tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## Vanliga frågor och svar {#faq}

Nedan följer en lista med svar på vanliga frågor om Adobe Experience Platform.

## Vad är [!DNL Experience Platform] API:er? {#what-are-experience-platform-apis}

[!DNL Experience Platform] erbjuder flera RESTful API:er som använder HTTP-begäranden för att komma åt [!DNL Experience Platform]-resurser. Dessa tjänst-API:er visar flera slutpunkter och gör att du kan utföra åtgärder för att lista (GET), söka (GET), redigera (PUT och/eller PATCH) och ta bort (DELETE) resurser. Mer information om specifika slutpunkter och åtgärder som är tillgängliga för respektive tjänst finns i [API-referensdokumentationen](https://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

## Hur formaterar jag en API-begäran? {#how-do-i-format-an-api-request}

Format för begäranden varierar beroende på vilket [!DNL Experience Platform]-API som används. Det bästa sättet att lära sig hur du strukturerar dina API-anrop är att följa med exemplen i dokumentationen för den [!DNL Experience Platform]-tjänst som du använder.

Mer information om hur du formaterar API-begäranden finns i Experience Platform API-guiden [läsa exempel på API-anrop](./api-guide.md#sample-api).

## Vad är min organisation? {#what-is-my-ims-organization}

En organisation är en Adobe-representation av en kund. Alla licensierade Adobe-lösningar är integrerade med denna kundorganisation. När en organisation är berättigad till [!DNL Experience Platform] kan den tilldela utvecklare åtkomst. Organisations-ID:t (`x-gw-ims-org-id`) representerar organisationen som ett API-anrop ska köras för och krävs därför som huvud i alla API-begäranden. Det här ID:t finns på [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): Gå till **Översikt** på fliken **Integrationer** för att hitta ID:t under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur du autentiserar dig för [!DNL Experience Platform] finns i [självstudiekursen för autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Var hittar jag min API-nyckel? {#where-can-i-find-my-api-key}

En API-nyckel krävs som huvud i alla API-begäranden. Den kan hittas via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Gå till avsnittet **Översikt** på fliken **Integrationer** i konsolen för en viss integrering och du hittar nyckeln under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur du autentiserar till [!DNL Experience Platform] finns i [självstudiekursen för autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Hur får jag en åtkomsttoken? {#how-do-i-get-an-access-token}

Åtkomsttoken krävs i auktoriseringsrubriken för alla API-anrop. De kan genereras med ett CURL-kommando, förutsatt att du har tillgång till en integrering för en organisation. Åtkomsttoken är bara giltiga i 24 timmar. Därefter måste en ny token skapas för att du ska kunna fortsätta använda API:t. Mer information om hur du genererar åtkomsttoken finns i självstudiekursen [Autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Hur använder jag frågeparametrar? {#how-do-i-user-query-parameters}

Vissa [!DNL Experience Platform] API-slutpunkter accepterar frågeparametrar för att hitta specifik information och filtrera resultaten som returneras i svaret. Frågeparametrar har lagts till för att begära sökvägar med ett frågetecken (`?`), följt av en eller flera frågeparametrar med formatet `paramName=paramValue`. När du kombinerar flera parametrar i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda parametrar. I följande exempel visas hur en begäran som använder flera frågeparametrar återges i dokumentationen.

Exempel på vanliga frågeparametrar är:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Mer information om vilka frågeparametrar som är tillgängliga för en viss tjänst eller slutpunkt finns i den servicespecifika dokumentationen.

## Hur anger jag att ett JSON-fält ska uppdateras i en begäran från PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Många PATCH-åtgärder i [!DNL Experience Platform] API:er använder [&#x200B; JSON-pekarsträngar &#x200B;](https://tools.ietf.org/html/rfc6901) för att ange att JSON-egenskaper ska uppdateras. Dessa inkluderas vanligtvis i begärandenyttolaster med formatet [JSON Patch](https://tools.ietf.org/html/rfc6902). I guiden [Grundläggande API &#x200B;](api-fundamentals.md) finns detaljerad information om nödvändig syntax för dessa tekniker.

## Kan jag använda Postman för att ringa anrop till [!DNL Experience Platform] API:er? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) är ett användbart verktyg för att visualisera anrop till RESTful API:er. Guiden [Komma igång-start för Experience Platform API](api-guide.md) innehåller en video och instruktioner för hur du importerar Postman-samlingar. Dessutom finns en lista över Postman-samlingar för varje tjänst.

## Vilka är systemkraven för [!DNL Experience Platform]? {#what-are-the-system-requirements-for-platform}

Beroende på om du använder gränssnittet eller API:t gäller följande systemkrav:

**För gränssnittsbaserade åtgärder:**
- En modern standardwebbläsare. Även om den senaste versionen av [!DNL Chrome] rekommenderas stöds även aktuella och tidigare större versioner av [!DNL Firefox], [!DNL Internet Explorer] och Safari.
   - Varje gång en ny större version släpps har [!DNL Experience Platform] stöd för den senaste versionen, medan stöd för den tredje senaste versionen tas bort.
- Alla webbläsare måste ha cookies och JavaScript aktiverat.

**För API- och utvecklarinteraktioner:**
- En utvecklingsmiljö som ska utvecklas för integrering av REST, strömning och Webkrok.

## Fel och felsökning {#errors-and-troubleshooting}

Nedan följer en lista över fel som kan uppstå när du använder någon [!DNL Experience Platform]-tjänst. Felsökningsguider för enskilda [!DNL Experience Platform]-tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## API-statuskoder {#api-status-codes}

Följande statuskoder kan påträffas i alla [!DNL Experience Platform]-API:er. Det finns en mängd orsaker till detta, och därför är de förklaringar som ges i detta avsnitt av allmän karaktär. Mer information om specifika fel i enskilda [!DNL Experience Platform]-tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

| Statuskod | Beskrivning | Möjliga orsaker |
|--- | --- | ---|
| 400 | Felaktig begäran | Begäran var felaktigt konstruerad, saknade nyckelinformation och/eller innehöll felaktig syntax. |
| 401 | Autentiseringen misslyckades | Begäran klarade inte en autentiseringskontroll. Åtkomsttoken kanske saknas eller är ogiltig. Mer information finns i avsnittet [OAuth-tokenfel](#oauth-token-is-missing) nedan. |
| 403 | Förbjuden | Resursen hittades, men du har inte rätt autentiseringsuppgifter för att visa den. <br> En trolig orsak till det här felet är att du kanske inte har de [åtkomstkontrollsbehörigheter](/help/access-control/home.md) som krävs för att komma åt eller redigera resursen. Läs om hur du [får de nödvändiga attributbaserade åtkomstkontrollsbehörigheterna](/help/landing/api-authentication.md#get-abac-permissions) för att använda Experience Platform API:er. </p> |
| 404 | Hittades inte | Det gick inte att hitta den begärda resursen på servern. Resursen kan ha tagits bort eller så har den begärda sökvägen angetts felaktigt. |
| 500 | Internt serverfel | Det här är ett serverfel. Om du gör många samtidiga anrop kanske du når API-gränsen och behöver filtrera resultaten. (Läs underhandboken för [!DNL Catalog Service] API-utvecklare om [filtrering av data](../catalog/api/filter-data.md) om du vill veta mer.) Vänta en stund innan du försöker utföra din begäran igen och kontakta administratören om problemet kvarstår. |

## Fel i begärandehuvud {#request-header-errors}

Alla API-anrop i [!DNL Experience Platform] kräver specifika begäranderubriker. Om du vill se vilka huvuden som krävs för enskilda tjänster kan du läsa [API-referensdokumentationen](https://www.adobe.com/go/platform-api-reference-en). Information om hur du hittar värden för de autentiseringshuvuden som krävs finns i [Autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). Om någon av dessa rubriker saknas eller är ogiltig när ett API-anrop görs kan följande fel uppstå.

### OAuth-token saknas {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Det här felmeddelandet visas när ett `Authorization`-huvud saknas i en API-begäran. Kontrollera att auktoriseringshuvudet ingår i en giltig åtkomsttoken innan du försöker igen.

### OAuth-token är inte giltig {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Det här felmeddelandet visas när den angivna åtkomsttoken i huvudet `Authorization` inte är giltig. Kontrollera att token har angetts korrekt eller [generera en ny token](https://www.adobe.com/go/platform-api-authentication-en) i Adobe I/O Console.

### API-nyckel krävs {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Det här felmeddelandet visas när en API-nyckelrubrik (`x-api-key`) saknas i en API-begäran. Kontrollera att rubriken är inkluderad med en giltig API-nyckel innan du försöker igen.

### API-nyckeln är ogiltig {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Det här felmeddelandet visas när värdet för det angivna API-nyckelhuvudet (`x-api-key`) är ogiltigt. Kontrollera att du har angett nyckeln korrekt innan du försöker igen. Om du inte känner till din API-nyckel kan du hitta den i [Adobe I/O Console](https://console.adobe.io): navigera till avsnittet **Översikt** på fliken **Integreringar** för att hitta API-nyckeln under **Klientautentiseringsuppgifter**.

### Rubrik saknas {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Det här felmeddelandet visas när ett organisationshuvud (`x-gw-ims-org-id`) saknas i en API-begäran. Se till att rubriken är inkluderad i din organisations ID innan du försöker igen.

### Profilen är ogiltig {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Det här felmeddelandet visas när användaren eller Adobe I/O-integreringen (identifieras av [åtkomsttoken](#how-do-i-get-an-access-token) i `Authorization` -huvudet) inte har rätt att göra anrop till [!DNL Experience Platform] API:er för organisationen som anges i `x-gw-ims-org-id` -huvudet. Kontrollera att du har angett rätt ID för din organisation i huvudet innan du försöker igen. Om du inte känner till ditt organisations-ID hittar du det i [Adobe I/O Console](https://console.adobe.io): navigera till avsnittet **Översikt** på fliken **Integreringar** för att hitta ett ID under **Klientautentiseringsuppgifter**.

### Fel vid uppdatering av tagg {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Du kan få ett taggfel om en ändring har gjorts för en käll- eller målenhet, t.ex. flöde, anslutning, källkoppling eller målanslutning av en annan API-anropare. På grund av versionsmatchningsfelet tillämpas inte den ändring du försöker göra på den senaste versionen av entiteten.

För att lösa detta måste du hämta entiteten igen, se till att dina ändringar är kompatibla med den nya versionen av entiteten, sedan placera den nya taggen i rubriken `If-Match` och slutligen göra API-anropet.

### Giltig innehållstyp har inte angetts {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Det här felmeddelandet visas när en POST-, PUT- eller PATCH-begäran har ett ogiltigt eller saknat `Content-Type`-huvud. Kontrollera att rubriken ingår i begäran och att dess värde är `application/json`.

### Användarregion saknas {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Det här felmeddelandet visas i något av följande två fall:
- När ett felaktigt eller felaktigt ID-huvud (`x-gw-ims-org-id`) skickas i en API-begäran. Kontrollera att rätt ID för din organisation finns med innan du försöker igen.
- När ditt konto (som representeras av de angivna autentiseringsuppgifterna) inte är associerat med en produktprofil för Experience Platform. Följ stegen för att [generera autentiseringsuppgifter](./api-authentication.md#authentication-for-each-session) i självstudiekursen för Experience Platform API-autentisering för att lägga till Experience Platform i ditt konto och uppdatera autentiseringsuppgifterna i enlighet med detta.

## Felsökningskatalog för tjänst {#service-troubleshooting-directory}

Nedan följer en lista över felsökningsguider och API-referensdokumentation för [!DNL Experience Platform] API:er. Varje felsökningsguide ger svar på vanliga frågor och lösningar på problem som är specifika för enskilda [!DNL Experience Platform]-tjänster. API-referensdokumenten innehåller en omfattande guide till alla tillgängliga slutpunkter för varje tjänst och visar exempel på begärandetexter, svar och felkoder som du kan få.

| Tjänst | API-referens | Felsökning |
| --- | --- | --- |
| Åtkomstkontroll | [API för åtkomstkontroll](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Felsökningsguide för åtkomstkontroll](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform datainmatning | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Felsökningsguide för gruppinmatning](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform datainmatning | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Felsökningsguide för direktuppspelning av frågor](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | [[!DNL Data Science Workspace] felsökningsguide](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform datastyrning | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] felsökningsguide](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] felsökningsguide](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentering | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Vanliga frågor och felsökningsguide](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] och [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] felsökningsguide](../profile/troubleshooting.md) |
| Sandlådor | [Sandbox-API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Felsökningsguide för sandlådor](../sandboxes/troubleshooting-guide.md) |
