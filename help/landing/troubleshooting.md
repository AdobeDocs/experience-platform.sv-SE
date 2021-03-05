---
keywords: Experience Platform;home;populära topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform FAQ and Troubleshooting Guide
description: Hitta svar på vanliga frågor och en guide för felsökning av vanliga fel i Experience Platform.
landing-page-description: Hitta svar på vanliga frågor och en guide för felsökning av vanliga fel i Experience Platform.
topic: komma igång
type: Dokumentation
translation-type: tm+mt
source-git-commit: 83cc3ddbf067f413cb524a3a685d985d5853eafd
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 1%

---


# [!DNL Platform] Vanliga frågor och felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform samt en felsökningsguide på hög nivå för vanliga fel som kan uppstå i ett [!DNL Experience Platform] API. Felsökningsguider för enskilda [!DNL Platform]-tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## Vanliga frågor och svar {#faq}

Nedan följer en lista med svar på vanliga frågor om Adobe Experience Platform.

## Vad är [!DNL Experience Platform] API:er? {#what-are-experience-platform-apis}

[!DNL Experience Platform] erbjuder flera RESTful-API:er som använder HTTP-begäranden för att komma åt  [!DNL Platform] resurser. Dessa tjänst-API:er visar flera slutpunkter och gör att du kan utföra åtgärder för att lista (GET), söka (GET), redigera (PUT och/eller PATCH) och ta bort (DELETE) resurser. Mer information om specifika slutpunkter och åtgärder som är tillgängliga för respektive tjänst finns i [API Reference documentation](http://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

## Hur formaterar jag en API-begäran? {#how-do-i-format-an-api-request}

Format för begäranden varierar beroende på vilken [!DNL Platform]-API som används. Det bästa sättet att lära sig att strukturera API-anrop är att följa med exemplen i dokumentationen för den [!DNL Platform]-tjänst som du använder.

Mer information om hur du formaterar API-förfrågningar finns i guiden [hur du läser API-anrop](./api-guide.md#sample-api) för plattforms-API.

## Vad är min IMS-organisation? {#what-is-my-ims-organization}

En IMS-organisation är en Adobe-representation av en kund. Alla licensierade Adobe-lösningar är integrerade med den här kundorganisationen. När en IMS-organisation är berättigad till [!DNL Experience Platform] kan den tilldela utvecklare åtkomst. IMS-organisations-ID (`x-gw-ims-org-id`) representerar organisationen som ett API-anrop ska köras för, och krävs därför som huvud i alla API-begäranden. Detta ID finns via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en viss integrering för att hitta ID:t under **Klientautentiseringsuppgifter**. En steg-för-steg-genomgång av hur du autentiserar till [!DNL Platform] finns i [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering.

## Var hittar jag min API-nyckel? {#where-can-i-find-my-api-key}

En API-nyckel krävs som huvud i alla API-begäranden. Den finns på [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Gå till avsnittet **Översikt** på fliken **Integreringar** i konsolen för en viss integrering och du hittar nyckeln under **Klientautentiseringsuppgifter**. En stegvis genomgång av hur du autentiserar till [!DNL Platform] finns i [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering.

## Hur får jag en åtkomsttoken? {#how-do-i-get-an-access-token}

Åtkomsttoken krävs i auktoriseringshuvudet för alla API-anrop. De kan genereras med ett `curl`-kommando, förutsatt att du har tillgång till en integrering för en IMS-organisation. Åtkomsttoken är bara giltiga i 24 timmar. Därefter måste en ny token skapas för att du ska kunna fortsätta använda API:t. Mer information om hur du genererar åtkomsttoken finns i självstudiekursen [autentisering](https://www.adobe.com/go/platform-api-authentication-en).

## Hur använder jag frågeparametrar? {#how-do-i-user-query-parameters}

Vissa [!DNL Platform] API-slutpunkter accepterar frågeparametrar för att hitta specifik information och filtrera resultaten som returneras i svaret. Frågeparametrar läggs till i frågesökvägar med ett frågetecken (`?`), följt av en eller flera frågeparametrar med formatet `paramName=paramValue`. När du kombinerar flera parametrar i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda parametrar. I följande exempel visas hur en begäran som använder flera frågeparametrar återges i dokumentationen.

Exempel på vanliga frågeparametrar är:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Mer information om vilka frågeparametrar som är tillgängliga för en viss tjänst eller slutpunkt finns i den servicespecifika dokumentationen.

## Hur anger jag att ett JSON-fält ska uppdateras i en PATCH-begäran? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Många PATCH-åtgärder i [!DNL Platform] API:er använder [JSON-pekarsträngar](https://tools.ietf.org/html/rfc6901) för att ange att JSON-egenskaper ska uppdateras. Dessa inkluderas vanligtvis i begärandenyttolaster med formatet [JSON Patch](https://tools.ietf.org/html/rfc6902). I [API-handboken](api-fundamentals.md) finns detaljerad information om nödvändig syntax för dessa tekniker.

## Kan jag använda Postman för att ringa till API:er för [!DNL Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postmanis ](https://www.postman.com/) är ett användbart verktyg för att visualisera anrop till RESTful API:er. Guiden [Komma igång-start för plattforms-API](api-guide.md) innehåller en video och instruktioner för import av Postman-samlingar. Dessutom finns en lista med Postman-samlingar för varje tjänst.

## Vilka är systemkraven för [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Beroende på om du använder gränssnittet eller API:t gäller följande systemkrav:

**För UI-baserade åtgärder:**
- En modern standardwebbläsare. Den senaste versionen av [!DNL Chrome] rekommenderas, men aktuella och tidigare större versioner av [!DNL Firefox], [!DNL Internet Explorer] och Safari stöds också.
   - Varje gång en ny större version släpps har [!DNL Platform] stöd för den senaste versionen samtidigt som stöd för den tredje senaste versionen tas bort.
- Alla webbläsare måste ha cookies och JavaScript aktiverat.

**För API- och utvecklarinteraktioner:**
- En utvecklingsmiljö som ska utvecklas för integrering av REST, strömning och Webkrok.

## Fel och felsökning {#errors-and-troubleshooting}

Nedan följer en lista över fel som kan uppstå när du använder en [!DNL Experience Platform]-tjänst. Felsökningsguider för enskilda [!DNL Platform]-tjänster finns i [tjänstens felsökningskatalog](#service-troubleshooting-directory) nedan.

## API-statuskoder {#api-status-codes}

Följande statuskoder kan påträffas i alla [!DNL Experience Platform]-API:er. Det finns en mängd orsaker till detta, och därför är de förklaringar som ges i detta avsnitt av allmän karaktär. Mer information om specifika fel i enskilda [!DNL Platform]-tjänster finns i [servicefelsökningskatalogen](#service-troubleshooting-directory) nedan.

| Statuskod | Beskrivning | Möjliga orsaker |
--- | --- | ---
| 400 | Felaktig begäran | Begäran är felaktigt konstruerad, nyckelinformation saknas och/eller innehåller felaktig syntax. |
| 401 | Autentiseringen misslyckades | Begäran klarade inte en autentiseringskontroll. Åtkomsttoken kanske saknas eller är ogiltig. Mer information finns i avsnittet [OAuth-tokenfel](#oauth-token-is-missing) nedan. |
| 403 | Förbjuden | Resursen hittades, men du har inte rätt autentiseringsuppgifter för att visa den. |
| 404 | Hittades inte | Det gick inte att hitta den begärda resursen på servern. Resursen kan ha tagits bort eller så har den begärda sökvägen angetts felaktigt. |
| 500 | Internt serverfel | Det här är ett serverfel. Om du gör många samtidiga anrop kanske du når API-gränsen och behöver filtrera resultaten. (Se underhandboken för [!DNL Catalog Service] API-utvecklare om [filtrering av data](../catalog/api/filter-data.md) om du vill veta mer.) Vänta en stund innan du försöker utföra din begäran igen och kontakta administratören om problemet kvarstår. |

## Begär rubrikfel {#request-header-errors}

Alla API-anrop i [!DNL Platform] kräver specifika begäranderubriker. Om du vill se vilka huvuden som krävs för enskilda tjänster kan du läsa [API-referensdokumentationen](http://www.adobe.com/go/platform-api-reference-en). Om du vill hitta värden för de nödvändiga autentiseringshuvudena kan du läsa [Självstudiekursen om autentisering](https://www.adobe.com/go/platform-api-authentication-en). Om någon av dessa rubriker saknas eller är ogiltig när ett API-anrop görs kan följande fel uppstå.

### OAuth-token saknas {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Det här felmeddelandet visas när ett `Authorization`-huvud saknas i en API-begäran. Kontrollera att auktoriseringshuvudet ingår i en giltig åtkomsttoken innan du försöker igen.

### OAuth-token är inte giltig

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Det här felmeddelandet visas när den angivna åtkomsttoken i `Authorization`-huvudet inte är giltig. Kontrollera att token har angetts korrekt eller [generera en ny token](https://www.adobe.com/go/platform-api-authentication-en) i Adobe I/O Console.

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

Det här felmeddelandet visas när värdet för det angivna API-nyckelhuvudet (`x-api-key`) är ogiltigt. Kontrollera att du har angett nyckeln korrekt innan du försöker igen. Om du inte känner till din API-nyckel kan du hitta den i [Adobe I/O-konsolen](https://console.adobe.io): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en viss integrering för att hitta API-nyckeln under **Klientautentiseringsuppgifter**.


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

Det här felmeddelandet visas när integreringen av användaren eller Adobe I/O (identifieras av [åtkomsttoken](#how-do-i-get-an-access-token) i `Authorization`-huvudet) inte har rätt att göra anrop till [!DNL Experience Platform] API:er för IMS-organisationen som finns i `x-gw-ims-org-id`-huvudet. Kontrollera att du har angett rätt ID för IMS-organisationen i sidhuvudet innan du försöker igen. Om du inte känner till ditt organisations-ID kan du hitta det i [Adobe I/O Console](https://console.adobe.io): på fliken **Integrationer** navigerar du till avsnittet **Översikt** för en specifik integrering för att hitta ID:t under **Klientautentiseringsuppgifter**.

### Giltig innehållstyp har inte angetts

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Det här felmeddelandet visas när en POST-, PUT eller PATCH-begäran har ett ogiltigt eller saknar `Content-Type`-huvud. Kontrollera att rubriken är inkluderad i begäran och att dess värde är `application/json`.


## Tjänstens felsökningskatalog {#service-troubleshooting-directory}

Nedan följer en lista över felsökningsguider och API-referensdokumentation för [!DNL Experience Platform] API:er. Varje felsökningsguide ger svar på vanliga frågor och lösningar på problem som är specifika för enskilda [!DNL Platform]-tjänster. API-referensdokumenten innehåller en omfattande guide till alla tillgängliga slutpunkter för varje tjänst och visar exempel på begärandetexter, svar och felkoder som du kan få.

| Tjänst | API-referens | Felsökning |
| --- | --- | --- |
| Åtkomstkontroll | [API för åtkomstkontroll](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Felsökningsguide för åtkomstkontroll](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform datainmatning | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Felsökningsguide ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[för gruppinmatningFelsökningsguide för direktuppspelning](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] felsökningsguide](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform datastyrning | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] felsökningsguide](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] felsökningsguide](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentering | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Vanliga frågor och felsökningsguide](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] och  [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] felsökningsguide](../profile/troubleshooting.md) |
| Sandlådor | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Felsökningsguide för sandlådor](../sandboxes/troubleshooting-guide.md) |

