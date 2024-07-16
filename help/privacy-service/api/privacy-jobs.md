---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Sekretessjobb API-slutpunkt
description: Lär dig hur du hanterar sekretessjobb för Experience Cloud-program med Privacy Service-API:t.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: e8e8a9267ddcf7ee9d1d199da8d157ed5f36d344
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 0%

---

# Slutpunkt för sekretessjobb

Det här dokumentet beskriver hur du arbetar med sekretessjobb med API-anrop. Det omfattar särskilt användningen av slutpunkten `/job` i API:t [!DNL Privacy Service]. Innan du läser den här guiden bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna anropa API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

>[!NOTE]
>
>Om du försöker hantera begäranden om samtycke eller avanmälan från kunder, se [slutpunktshandboken för samtycke](./consent.md).

## Visa alla jobb {#list}

Du kan visa en lista över alla tillgängliga sekretessjobb inom din organisation genom att göra en GET-förfrågan till slutpunkten `/jobs`.

**API-format**

Det här frågeformatet använder en `regulation`-frågeparameter på `/jobs`-slutpunkten, och börjar därför med ett frågetecken (`?`) enligt nedan. När resurser listas returneras upp till 1 000 jobb och Privacy Servicen numreras. Använd andra frågeparametrar (`page`, `size` och datumfilter) för att filtrera svaret. Du kan separera flera parametrar med et-tecken (`&`).

>[!TIP]
>
>Använd ytterligare frågeparametrar om du vill filtrera resultaten ytterligare för specifika frågor. Du kan till exempel identifiera hur många sekretessjobb som har skickats under en viss tidsperiod och vilken status de har med frågeparametrarna `status`, `fromDate` och `toDate`.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{REGULATION}` | Regeltypen som ska sökas efter. Godkända värden är: <ul><li>`apa_aus`</li><li>`cpa_usa`</li><li>`cpra_usa`</li><li>`ctdpa_usa`</li><li>`gdpr` - Obs! Detta används också för begäranden som rör **ccpa** -regler.</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`mhmda_usa`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>Se översikten över [regler som stöds](../regulations/overview.md) för mer information om sekretessreglerna som ovanstående värden representerar. |
| `{PAGE}` | Sidan med data som ska visas med nollbaserad numrering. Standardvärdet är `0`. |
| `{SIZE}` | Antalet resultat som ska visas på varje sida. Standardvärdet är `100` och maxvärdet är `1000`. Om det maximala värdet överskrids returneras ett 400-kodfel. |
| `{status}` | Standardbeteendet är att inkludera alla statusvärden. Om du anger en statustyp returnerar begäran endast sekretessjobb som matchar den statustypen. Godkända värden är: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Den här parametern begränsar resultaten till de som bearbetas före ett angivet datum. Från och med datumet för begäran kan systemet leta upp 45 dagar. Intervallet får dock inte vara längre än 30 dagar.<br>Formatet ÅÅÅ-MM-DD godkänns. Datumet du anger tolkas som avslutsdatumet uttryckt i GMT (Greenwich Mean Time).<br>Om du inte anger den här parametern (och en motsvarande `fromDate`) returnerar standardbeteendet jobb som är tillbaka de senaste sju dagarna. Om du använder `toDate` måste du också använda frågeparametern `fromDate`. Om du inte använder båda returnerar anropet ett 400-fel. |
| `{fromDate}` | Den här parametern begränsar resultaten till de som bearbetas efter ett angivet datum. Från och med datumet för begäran kan systemet leta upp 45 dagar. Intervallet får dock inte vara längre än 30 dagar.<br>Formatet ÅÅÅ-MM-DD godkänns. Datumet som du anger tolkas som begärans ursprungsdatum uttryckt i GMT (Greenwich Mean Time).<br>Om du inte anger den här parametern (och en motsvarande `toDate`) returnerar standardbeteendet jobb som är tillbaka de senaste sju dagarna. Om du använder `fromDate` måste du också använda frågeparametern `toDate`. Om du inte använder båda returnerar anropet ett 400-fel. |
| `{filterDate}` | Den här parametern begränsar resultaten till de som bearbetas ett visst datum. Formatet YYY-MM-DD godkänns. Systemet kan titta tillbaka under de senaste 45 dagarna. |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li> 
 -->

**Begäran**

Följande begäran hämtar en sidnumrerad lista över alla jobb i en organisation, med början från den tredje sidan med sidstorleken 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar en lista med jobb, där varje jobb innehåller information som `jobId`. I det här exemplet innehåller svaret en lista med 50 jobb, med början på den tredje resultatsidan.

### Åtkomst till efterföljande sidor

Om du vill hämta nästa resultatuppsättning i ett sidnumrerat svar måste du göra ett annat API-anrop till samma slutpunkt samtidigt som frågeparametern `page` ökas med 1.

## Skapa ett sekretessjobb {#create-job}

>[!IMPORTANT]
>
>Privacy Service är endast avsedd för den registrerade och för förfrågningar om konsumenträttigheter. All annan användning av Privacy Service för datarensning eller underhåll stöds inte eller tillåts inte. Adobe har en rättslig skyldighet att uppfylla dem i tid. Därför är lasttestning inte tillåtet på Privacy Service eftersom det är en produktionsmiljö och skapar en onödig eftersläpning av giltiga sekretessbegäranden.
>
>Det finns nu en hög överföringsgräns per dag för att förhindra missbruk av tjänsten. Användare som råkar missbruka systemet kommer att ha åtkomst till tjänsten inaktiverad. Därefter kommer ett möte att hållas med dem för att diskutera deras åtgärder och hur Privacy Servicen kan användas.

Innan du skapar en ny jobbbegäran måste du först samla in identifieringsinformation om de registrerade vars uppgifter du vill få tillgång till, ta bort eller avanmäla dig från försäljning. När du har de data som krävs måste de anges i nyttolasten för en POST-förfrågan till slutpunkten `/jobs`.

>[!NOTE]
>
>Kompatibla Adobe Experience Cloud-program använder olika värden för att identifiera registrerade. Mer information om vilka identifierare som krävs för dina program finns i guiden för [Privacy Service och Experience Cloud ](../experience-cloud-apps.md). Mer allmän vägledning om hur du avgör vilka ID:n som ska skickas till [!DNL Privacy Service] finns i dokumentet om [identitetsdata i sekretessförfrågningar](../identity-data.md).

API:t [!DNL Privacy Service] har stöd för två typer av jobbförfrågningar för personliga data:

* [Åtkomst och/eller borttagning](#access-delete): Åtkomst (läs) eller radering av personuppgifter.
* [Avanmäl dig från försäljningen](#opt-out): Markera personliga data som inte ska säljas.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `companyContexts` **(Obligatoriskt)** | En array som innehåller autentiseringsinformation för din organisation. Varje identifierare i listan innehåller följande attribut: <ul><li>`namespace`: Namnområdet för en identifierare.</li><li>`value`: Identifierarens värde.</li></ul>Det är **obligatoriskt** som en av identifierarna använder `imsOrgId` som `namespace`, med dess `value` som innehåller det unika ID:t för din organisation. <br/><br/>Ytterligare identifierare kan vara produktspecifika företagskvalificerare (till exempel `Campaign`), som identifierar en integrering med ett Adobe-program som tillhör din organisation. Möjliga värden är kontonamn, klientkoder, klient-ID eller andra programidentifierare. |
| `users` **(Obligatoriskt)** | En array som innehåller en samling med minst en användare vars information du vill komma åt eller ta bort. Högst 1 000 användare kan anges i en enda begäran. Varje användarobjekt innehåller följande information: <ul><li>`key`: En identifierare för en användare som används för att kvalificera separata jobb-ID:n i svarsdata. Det är bäst att välja en unik, lätt identifierbar sträng för det här värdet så att det är enkelt att referera till eller söka efter den senare.</li><li>`action`: En matris med en lista över önskade åtgärder som ska utföras på användarens data. Beroende på vilka åtgärder du vill utföra måste den här arrayen innehålla `access`, `delete` eller båda.</li><li>`userIDs`: En samling identiteter för användaren. Antalet identiteter som en enskild användare kan ha är begränsat till nio. Varje identitet består av en `namespace`, en `value` och en namnutrymmeskvalificerare (`type`). Mer information om de här obligatoriska egenskaperna finns i [bilagan](appendix.md).</li></ul> En mer detaljerad förklaring av `users` och `userIDs` finns i [felsökningsguiden](../troubleshooting-guide.md#user-ids). |
| `include` **(Obligatoriskt)** | En uppsättning Adobe-produkter som ska ingå i bearbetningen. Om det här värdet saknas eller är tomt på annat sätt, kommer begäran att avvisas. Inkludera endast produkter som din organisation är integrerad med. Mer information finns i avsnittet [Godkända produktvärden](appendix.md) i bilagan. |
| `expandIDs` | En valfri egenskap som, när den anges till `true`, representerar en optimering för bearbetning av ID:n i programmen (stöds för närvarande bara av [!DNL Analytics]). Om det utelämnas blir det här värdet som standard `false`. |
| `priority` | En valfri egenskap som används av Adobe Analytics och som anger prioriteten för bearbetning av begäranden. Godkända värden är `normal` och `low`. Om `priority` utelämnas är standardbeteendet `normal`. |
| `mergePolicyId` | När du gör sekretessförfrågningar för kundprofilen i realtid (`profileService`) kan du välja att ange ID:t för den specifika [sammanfogningsprincipen](../../profile/merge-policies/overview.md) som du vill använda för sammanfogning av ID. Genom att ange en kopplingsprofil kan sekretessförfrågningar inkludera målgruppsinformation när data returneras till en kund. Endast en sammanfogningsprincip kan anges per begäran. Om det inte finns någon sammanfogningspolicy inkluderas inte segmenteringsinformation i svaret. |
| `regulation` **(Obligatoriskt)** | Reglerna för sekretessarbetet. Följande värden accepteras: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Se översikten över [regler som stöds](../regulations/overview.md) för mer information om sekretessreglerna som ovanstående värden representerar. |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

När du har skickat jobbförfrågan kan du fortsätta till nästa steg i [kontrollera jobbets status](#check-status).

## Kontrollera status för ett jobb {#check-status}

Du kan hämta information om ett specifikt jobb, till exempel dess aktuella bearbetningsstatus, genom att ta med det jobbets `jobId` i sökvägen för en GET-förfrågan till slutpunkten `/jobs`.

>[!IMPORTANT]
>
>Data för tidigare skapade jobb är endast tillgängliga för hämtning inom 30 dagar efter jobbets slutförandedatum.

**API-format**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{JOB_ID}` | ID:t för det jobb som du vill söka efter. Detta ID returneras under `jobId` i lyckade API-svar för [att skapa ett jobb](#create-job) och [att lista alla jobb](#list). |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar information om jobbet vars `jobId` anges i sökvägen till begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `productStatusResponse` | Varje objekt i arrayen `productResponses` innehåller information om jobbets aktuella status i förhållande till ett specifikt [!DNL Experience Cloud]-program. |
| `productStatusResponse.status` | Jobbets aktuella statuskategori. I tabellen nedan finns en lista över [tillgängliga statuskategorier](#status-categories) och deras motsvarande betydelse. |
| `productStatusResponse.message` | Jobbets specifika status, som motsvarar statuskategorin. |
| `productStatusResponse.responseMsgCode` | En standardkod för produktsvarsmeddelanden som tagits emot av [!DNL Privacy Service]. Information om meddelandet finns under `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | En mer detaljerad förklaring av jobbets status. Meddelanden för liknande status kan variera mellan olika produkter. |
| `productStatusResponse.results` | För vissa statusvärden kan vissa produkter returnera ett `results`-objekt som ger ytterligare information som inte täcks av `responseMsgDetail`. |
| `downloadURL` | Om jobbstatusen är `complete` tillhandahåller det här attributet en URL för att hämta jobbresultaten som en ZIP-fil. Den här filen kan laddas ned i 60 dagar efter att jobbet har slutförts. |

{style="table-layout:auto"}

### Jobbstatuskategorier {#status-categories}

I följande tabell visas olika möjliga jobbstatuskategorier och deras motsvarande betydelse:

| Statuskategori | Betydelse |
| -------------- | -------- |
| `complete` | Jobbet är klart och (om det behövs) filer överförs från alla program. |
| `processing` | Ansökningarna har bekräftat jobbet och bearbetar för närvarande. |
| `submitted` | Jobbet skickas till alla tillämpliga program. |
| `error` | Något misslyckades vid bearbetningen av jobbet - mer specifik information kan hämtas genom att information om enskilda jobb hämtas. |

{style="table-layout:auto"}

>[!NOTE]
>
>Ett skickat jobb kan förbli i tillståndet `processing` om det har ett beroende underordnat jobb som fortfarande bearbetas.

## Nästa steg

Du kan nu skapa och övervaka sekretessjobb med API:t [!DNL Privacy Service]. Mer information om hur du utför samma uppgifter med användargränssnittet finns i [Privacy Servicens användargränssnittsöversikt](../ui/overview.md).
