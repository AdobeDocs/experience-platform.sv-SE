---
title: Ta bort poster med hjälp av API:t för datahygien
description: Lär dig att programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform.
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Ta bort poster med hjälp av API:t för datahygien

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

Med Data Hygiene API kan du programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform.

Du kan komma åt API:t via samma rotsökväg som [Privacy Service API](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Komma igång

I det här avsnittet ges en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för datahygien.

### Samla in värden för obligatoriska rubriker

För att kunna anropa API:t för datahygien måste du först samla in dina autentiseringsuppgifter. Detta är samma autentiseringsuppgifter som används för att få åtkomst till Privacy Service API. Se [API-översikt](./overview.md#getting-started) för att generera värden för var och en av de rubriker som krävs för API:t för datahygien, så som visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

* `Content-Type: application/json`

### Läser exempel-API-anrop

Det här dokumentet innehåller ett exempel-API-anrop som visar hur du formaterar dina begäranden. Information om konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/api-guide.md#sample-api) i Komma igång-guiden för Experience Platform API:er.

## Skapa ett borttagningsjobb

Du kan skapa ett borttagningsjobb genom att göra en POST-begäran.

**API-format**

```http
POST /jobs
```

**Begäran**

Nyttolasten för begäran är strukturerad på ungefär samma sätt som en [delete-begäran i Privacy Service API](../../privacy-service/api/privacy-jobs.md#access-delete). Den innehåller en `users`-array vars objekt representerar de användare vars data ska tas bort.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `companyContexts` | En array som innehåller autentiseringsinformation för din organisation. Den måste innehålla ett enda objekt med följande egenskaper: <ul><li>`namespace`: Måste anges till `imsOrgID`.</li><li>`value`: Ditt organisations-ID. Det här är samma värde som anges i rubriken `x-gw-ims-org-id`.</li></ul> |
| `users` | En array som innehåller en samling med minst en användare vars information du vill ta bort. Varje användarobjekt innehåller följande information: <ul><li>`key`: En identifierare för en användare som används för att kvalificera separata jobb-ID:n i svarsdata. Det är bäst att välja en unik, lätt identifierbar sträng för det här värdet så att det kan refereras till eller slås upp senare.</li><li>`action`: En matris med en lista över önskade åtgärder som ska utföras på användarens data. Måste innehålla ett strängvärde: `delete`.</li><li>`userIDs`: En samling identiteter för användaren. Antalet identiteter som en enskild användare kan ha är begränsat till nio. Varje identitet innehåller följande egenskaper: <ul><li>`namespace`: [Identitetsnamnrymden](../../identity-service/features/namespaces.md) som är associerad med ID:t. Detta kan vara ett [standardnamnområde](../../privacy-service/api/appendix.md#standard-namespaces) som känns igen av Experience Platform, eller ett anpassat namnområde som definieras av din organisation. Den typ av namnutrymme som används måste återspeglas i egenskapen `type`.</li><li>`value`: Identitetsvärdet.</li><li>`type`: Måste anges till `standard` om du använder ett globalt identifierat namnutrymme, eller `custom` om du använder ett namnutrymme som definierats av din organisation.</li></ul></li></ul> |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar information om de skapade jobben.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
