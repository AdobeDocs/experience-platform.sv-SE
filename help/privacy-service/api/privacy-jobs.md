---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Jobb
topic: developer guide
translation-type: tm+mt
source-git-commit: 5d06932cbfe8a04589d33590c363412c054fc9fd
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---


# Sekretessjobb

Det här dokumentet beskriver hur du arbetar med sekretessjobb med API-anrop. Det omfattar särskilt användningen av `/job` slutpunkten i [!DNL Privacy Service] API:t. Innan du läser den här handboken bör du läsa avsnittet [](./getting-started.md#getting-started) Komma igång för att få viktig information som du behöver känna till för att kunna anropa API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

>[!NOTE]
>
>Om du försöker hantera begäranden om samtycke eller avanmälan från kunder, se [slutpunktshandboken](./consent.md)för godkännande.

## Visa alla jobb {#list}

Du kan visa en lista över alla tillgängliga sekretessjobb inom din organisation genom att göra en GET-förfrågan till `/jobs` slutpunkten.

**API-format**

Det här frågeformatet använder en `regulation` frågeparameter på `/jobs` slutpunkten, och börjar därför med ett frågetecken (`?`) enligt nedan. Svaret sidnumreras så att du kan använda andra frågeparametrar (`page` och `size`) för att filtrera svaret. Du kan separera flera parametrar med et-tecken (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{REGULATION}` | Regeltypen som ska sökas efter. Godkända värden är `gdpr`, `ccpa`, `lgpd_bra`och `pdpa_tha`. |
| `{PAGE}` | Sidan med data som ska visas med nollbaserad numrering. Standardvärdet är `0`. |
| `{SIZE}` | Antalet resultat som ska visas på varje sida. Standardvärdet är `1` och maxvärdet är `100`. Om det maximala värdet överskrids returneras ett 400-kodfel. |

**Begäran**

Följande begäran hämtar en numrerad lista över alla jobb inom en IMS-organisation, med början från den tredje sidan med sidstorleken 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Ett lyckat svar returnerar en lista med jobb, där varje jobb innehåller information om t.ex. dess `jobId`. I det här exemplet innehåller svaret en lista med 50 jobb, med början på den tredje resultatsidan.

### Åtkomst till efterföljande sidor

Om du vill hämta nästa resultatuppsättning i ett sidnumrerat svar måste du göra ett annat API-anrop till samma slutpunkt samtidigt som du ökar `page` frågeparametern med 1.

## Skapa ett sekretessjobb {#create-job}

Innan du skapar en ny jobbbegäran måste du först samla in identifieringsinformation om de registrerade vars uppgifter du vill få tillgång till, ta bort eller avanmäla dig från försäljning. När du har de data som krävs måste de anges i nyttolasten för en POST-förfrågan till `/jobs` slutpunkten.

>[!NOTE]
>
>Kompatibla Adobe Experience Cloud-program använder olika värden för att identifiera registrerade. Mer information om vilka identifierare som krävs för dina program finns i guiden om program [för](../experience-cloud-apps.md) Privacy Service och Experience Cloud. Mer allmän vägledning om hur du avgör vilka ID:n du ska skicka till [!DNL Privacy Service]finns i dokumentet om [identitetsdata i sekretessförfrågningar](../identity-data.md).

API:t [!DNL Privacy Service] stöder två typer av jobbförfrågningar för personuppgifter:

* [Åtkomst och/eller borttagning](#access-delete): Få åtkomst till (läsa) eller ta bort personuppgifter.
* [Avanmäl dig](#opt-out): Märk personuppgifter som att de inte ska säljas.

>[!IMPORTANT]
>
>Åtkomst- och borttagningsbegäranden kan kombineras som ett enda API-anrop, men avanmälningsbegäranden måste göras separat.

### Skapa ett åtkomst-/borttagningsjobb {#access-delete}

I det här avsnittet visas hur du gör en begäran om åtkomst/borttagning av jobb med API:t.

**API-format**

```http
POST /jobs
```

**Begäran**

Följande begäran skapar en ny jobbbegäran, konfigurerad med attributen som anges i nyttolasten enligt beskrivningen nedan.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `companyContexts` **(Obligatoriskt)** | En array som innehåller autentiseringsinformation för din organisation. Varje identifierare i listan innehåller följande attribut: <ul><li>`namespace`: Namnutrymmet för en identifierare.</li><li>`value`: Identifierarens värde.</li></ul>Det **krävs** att en av identifierarna använder `imsOrgId` den som `namespace`, med `value` det unika ID:t för IMS-organisationen. <br/><br/>Ytterligare identifierare kan vara produktspecifika företagskvalificerare (till exempel `Campaign`) som identifierar en integrering med ett Adobe-program som tillhör din organisation. Möjliga värden är kontonamn, klientkoder, klient-ID:n eller andra programidentifierare. |
| `users` **(Obligatoriskt)** | En array som innehåller en samling med minst en användare vars information du vill komma åt eller ta bort. Högst 1 000 användar-ID kan anges i en enda begäran. Varje användarobjekt innehåller följande information: <ul><li>`key`: En identifierare för en användare som används för att kvalificera separata jobb-ID:n i svarsdata. Det är bäst att välja en unik, lätt identifierbar sträng för det här värdet så att det är enkelt att referera till eller söka efter den senare.</li><li>`action`: En array som visar vilka åtgärder som önskas för användarens data. Beroende på vilka åtgärder du vill utföra måste den här arrayen innehålla `access`, `delete`eller båda.</li><li>`userIDs`: En samling identiteter för användaren. Antalet identiteter som en enskild användare kan ha är begränsat till nio. Varje identitet består av en `namespace`, en `value`och en namnutrymmeskvalificerare (`type`). Mer information om de här obligatoriska egenskaperna finns i [bilagan](appendix.md) .</li></ul> En mer detaljerad förklaring av `users` och `userIDs`information finns i [felsökningsguiden](../troubleshooting-guide.md#user-ids). |
| `include` **(Obligatoriskt)** | En uppsättning Adobe-produkter som ska ingå i bearbetningen. Om det här värdet saknas eller är tomt på annat sätt, kommer begäran att avvisas. Inkludera endast produkter som din organisation är integrerad med. Mer information finns i avsnittet om [godkända produktvärden](appendix.md) i bilagan. |
| `expandIDs` | En valfri egenskap som, när den anges till `true`, representerar en optimering för bearbetning av ID:n i programmen (stöds för närvarande bara av [!DNL Analytics]). Om det utelämnas blir det här värdet som standard `false`. |
| `priority` | En valfri egenskap som används av Adobe Analytics och som anger prioriteten för bearbetning av begäranden. Godkända värden är `normal` och `low`. Om `priority` utelämnas används standardbeteendet `normal`. |
| `analyticsDeleteMethod` | En valfri egenskap som anger hur Adobe Analytics ska hantera personuppgifter. Två möjliga värden accepteras för det här attributet: <ul><li>`anonymize`: Alla data som refereras av den angivna samlingen med användar-ID görs anonyma. Om `analyticsDeleteMethod` utelämnas är detta standardbeteendet.</li><li>`purge`: Alla data tas bort helt.</li></ul> |
| `regulation` **(Obligatoriskt)** | Förordningen om begäran. Måste vara ett av följande fyra värden: <ul><li>`gdpr`</li><li>`ccpa`</li><li>`lgpd_bra`</li><li>`pdpa_tha`</li></ul> |

**Svar**

Ett lyckat svar returnerar information om de nya jobben.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `jobId` | Ett skrivskyddat, unikt systemgenererat ID för ett jobb. Det här värdet används i nästa steg när du söker efter ett specifikt jobb. |

När du har skickat jobbförfrågan kan du fortsätta till nästa steg för att [kontrollera jobbets status](#check-status).

## Kontrollera status för ett jobb {#check-status}

Du kan hämta information om ett visst jobb, till exempel dess aktuella bearbetningsstatus, genom att ta med det jobbet `jobId` i sökvägen för en GET-förfrågan till `/jobs` slutpunkten.

>[!IMPORTANT]
>
>Data för tidigare skapade jobb är endast tillgängliga för hämtning inom 30 dagar efter jobbets slutförandedatum.

**API-format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{JOB_ID}` | ID:t för det jobb som du vill söka efter. Detta ID returneras under `jobId` i lyckade API-svar för [att skapa ett jobb](#create-job) och [visa alla jobb](#list). |

**Begäran**

Följande begäran hämtar information om jobbet vars sökväg `jobId` anges i begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Ett lyckat svar returnerar information om det angivna jobbet.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `productStatusResponse` | Varje objekt i `productResponses` arrayen innehåller information om jobbets aktuella status i förhållande till ett specifikt [!DNL Experience Cloud] program. |
| `productStatusResponse.status` | Jobbets aktuella statuskategori. I tabellen nedan finns en lista över [tillgängliga statuskategorier](#status-categories) och deras motsvarande betydelse. |
| `productStatusResponse.message` | Jobbets specifika status, som motsvarar statuskategorin. |
| `productStatusResponse.responseMsgCode` | En standardkod för produktsvarsmeddelanden som tas emot av [!DNL Privacy Service]. Information om meddelandet finns under `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | En mer detaljerad förklaring av jobbets status. Meddelanden för liknande status kan variera mellan olika produkter. |
| `productStatusResponse.results` | För vissa statusvärden kan vissa produkter returnera ett `results` objekt som ger ytterligare information som inte täcks av `responseMsgDetail`. |
| `downloadURL` | Om jobbets status är `complete`ger det här attributet en URL för att hämta jobbresultaten som en ZIP-fil. Den här filen kan laddas ned i 60 dagar efter att jobbet har slutförts. |

### Jobbstatuskategorier {#status-categories}

I följande tabell visas olika möjliga jobbstatuskategorier och deras motsvarande betydelse:

| Statuskategori | Betydelse |
| -------------- | -------- |
| `complete` | Jobbet är klart och (om det behövs) filer överförs från alla program. |
| `processing` | Ansökningarna har bekräftat jobbet och bearbetar för närvarande. |
| `submitted` | Jobbet skickas till alla tillämpliga program. |
| `error` | Något misslyckades vid bearbetningen av jobbet - mer specifik information kan hämtas genom att information om enskilda jobb hämtas. |

>[!NOTE]
>
>Ett skickat jobb kan vara i ett `processing` tillstånd om det har ett beroende underordnat jobb som fortfarande bearbetas.

## Nästa steg

Nu vet du hur man skapar och övervakar sekretessjobb med [!DNL Privacy Service] API. Mer information om hur du utför samma uppgifter med användargränssnittet finns i [Privacy Servicens användargränssnitt - översikt](../ui/overview.md).
