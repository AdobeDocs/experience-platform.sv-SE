---
title: Innehålls-API-slutpunkt
description: Lär dig hur du hämtar åtkomstdata med Privacy Services-API:t.
role: Developer
badgePrivateBeta: label="Privat beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c527771e051d39032642afae33945a45e5183a5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Innehållsslutpunkt

>[!IMPORTANT]
>
>The `/content` slutpunkten finns för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionen och dokumentationen kan komma att ändras.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

Få bättre säkerhet när du hämtar &#39;åtkomstinformation&#39; (den information som en privatperson kan begära åtkomst till). Hämtnings-URL:en som anges i svaret på en `/jobs/{JOB_ID}` GET-förfrågan pekar nu på en Adobe-tjänstslutpunkt. Du kan sedan göra en GET-förfrågan till `/jobs/:JOB_ID/content` för att returnera kunddata i JSON-format. Den här åtkomstmetoden implementerar flera lager av autentisering och åtkomstkontroll för att förbättra säkerheten.

Innan du använder den här handboken bör du läsa [komma igång-guide](./getting-started.md) om du vill ha information om de autentiseringshuvuden som visas i exemplet på API-anrop nedan.

>[!TIP]
>
>Om du inte känner till jobb-ID:t för den åtkomstinformation du behöver kan du ringa `/jobs`slutpunkt och använd ytterligare frågeparametrar för att filtrera resultatet. En fullständig lista över tillgängliga frågeparametrar finns i [slutpunktshandbok för sekretessjobb](./privacy-jobs.md).

## Hämta information om sekretessjobb

Om du vill hämta information om ett specifikt jobb, till exempel dess aktuella bearbetningsstatus, inkluderar du det jobbets `jobId` i sökvägen till en GET-begäran till `/jobs` slutpunkt.

**API-format**

```http
GET /jobs/{JOB_ID}
```

**Begäran**

Följande begäran hämtar information om jobbet vars `jobId` anges i sökvägen till begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar information om det angivna jobbet.

>[!NOTE]
>
>Sekretessjobb måste ha `complete` status som innehåller `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Egenskap | Beskrivning |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | En unik identifierare för sekretessjobbet. |
| `requestId` | En unik identifierare för den specifika begäran som gjorts till Privacy Servicen. |
| `userKey` | `userKey` är `key` värde som du angav när du skickade din sekretessförfrågan. The `key` värdet är din möjlighet att ge den registrerade en identifierare som passar dig. Det är vanligtvis en unik identifierare som ditt system har skapat för att spåra den registrerade. TIPS: Du kan lista alla aktiva sekretessjobb och jämföra dina `key` till varje jobb. |
| `action` | Den typ av åtgärd som begärdes. Godkända värden är `access` och `delete`. |
| `status` | Den aktuella statusen för sekretessjobbet. |
| `submittedBy` | E-postadressen till den person som skickade sekretessjobbet. |
| `createdDate` | Datum och tid då sekretessjobbet skapades. |
| `lastModifiedDate` | Datum och tid då sekretessjobbet senast ändrades. |
| `userIds` | En array som innehåller användaridentifierare och relaterad information. |
| `userIds.namespace` | Det namnutrymme som används för användaridentifieraren. |
| `userIds.value` | Det faktiska värdet för användaridentifieraren. |
| `userIds.type` | Typ av identifierare (till exempel `standard` eller `custom`). |
| `userIds.namespaceId` | En identifierare för det namnutrymme som används för att kategorisera och hantera användaridentiteter. |
| `userIds.isDeletedClientSide` | Ett booleskt värde som anger om identifieraren har tagits bort på klientsidan. |
| `productResponses` | En array som innehåller svar från olika produkter eller tjänster som rör sekretessjobbet. |
| `productResponses.product` | Namnet på den produkt eller tjänst som användes för att få information om den registrerade. |
| `productResponses.retryCount` | Antalet gånger som begäran har gjorts om. |
| `productResponses.processedDate` | Datum och tid då produktsvaret bearbetades. |
| `productResponses.productStatusResponse` | Ett objekt som innehåller status för produktsvaret. |
| `productResponses.productStatusResponse.status` | Status för produktsvaret. |
| `downloadURL` | Det här attributet tillhandahåller en slutpunkt som är tillgänglig att anropa i 60 dagar efter att jobbet har slutförts. Jobbets status måste vara `complete` och `action` måste vara `access`. I annat fall är det här fältet inte tillgängligt. |
| `regulation` | Det regelverk enligt vilket personuppgiftsinfordran behandlas, t.ex. `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`och så vidare. |

{style="table-layout:auto"}

## Hämta information om kundåtkomst {#retrieve-access-data}

Om du vill få den&quot;åtkomstinformation&quot; som skapas som svar på den fråga som den registrerade ställer, skickar du en GET till `/jobs/{JOB_ID}/content` slutpunkt. Svaret är en zip-fil (*.zip) som innehåller en mapp med undermappar för varje produkt som innehåller data om den registrerade.

>[!TIP]
>
>Du behöver ett specifikt jobb-ID för att kunna göra den här begäran. Om du behöver hämta det specifika jobb-ID:t måste du först göra en GET-förfrågan till `/jobs` slutpunkt och använd ytterligare frågeparametrar för att filtrera resultatet. Detaljerad information med de tillåtna frågeparametrarna finns i [slutpunktshandbok för sekretessjobb](./privacy-jobs.md).

**API-format**

```http
GET /jobs/{JOB_ID}/content
```

**Begäran**

Följande begäran returnerar &quot;åtkomstinformation&quot; för det jobb-ID som angavs i begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Svar**

Svaret är en zip-fil (*.zip). Informationen returneras vanligtvis i JSON-format, men det kan inte garanteras. Extraherade data kan returneras i vilket format som helst.

<!-- ## Constraints {#constraints}

During this private beta, the following constraints apply when using the `/content` endpoint:

- The new `/content` download URL is only available in STAGE environments. It is not yet available in PROD environments
- The `downloadUrl` should not be present in the JSON response unless the job has a `complete` status. Within the beta, the `downloadUrl` appears before a privacy job is complete.
- The `downloadUrl` is also currently provided for `delete` jobs (which should never have a download URL). -->
