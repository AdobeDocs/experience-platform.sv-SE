---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Behandling av sekretessförfrågningar i Data Lake

Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i Data Lake.

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande Experience Platform-tjänster innan du läser den här handboken:

* [Integritetstjänst](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av personliga data mellan Adobe Experience Cloud-program.
* [Katalogtjänst](home.md): Registersystemet för dataplats och datalinje inom Experience Platform. Tillhandahåller ett API som kan användas för att uppdatera datauppsättningsmetadata.
* [Experience Data Model (XDM) System](../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.

## Lägga till sekretessetiketter i datauppsättningar {#privacy-labels}

För att en datauppsättning ska kunna bearbetas i en sekretessbegäran för Data Lake måste datauppsättningen få sekretessetiketter. Sekretessetiketter anger vilka fält i en datamängds associerade schema som gäller för de namnutrymmen som du förväntar ska skickas i sekretessförfrågningar.

I det här avsnittet visas hur du lägger till sekretessetiketter i en datauppsättning för användning i Data Lake-sekretessbegäranden. Ta till att börja med följande datauppsättning:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

Egenskapen `schemaMetadata` för datauppsättningen innehåller en `gdpr` array som för närvarande är tom. Om du vill lägga till sekretessetiketter i datauppsättningen måste den här matrisen uppdateras med en PATCH-begäran till API:t för [katalogtjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

>[!NOTE] Även om arrayen heter `gdpr`kan du lägga till etiketter för att tillåta sekretessjobbbegäranden för både GDPR- och CCPA-regler.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Värdet `id` för datauppsättningen som ska uppdateras. |

**Begäran**

I det här exemplet innehåller en datauppsättning en e-postadress i `personalEmail.address` fältet. För att det här fältet ska fungera som en identifierare för Data Lake-sekretessbegäranden måste en etikett som använder ett oregistrerat namnutrymme läggas till i dess `gdpr` array.

Följande begäran lägger till en sekretessetikett som tilldelar namnutrymmet &quot;email_label&quot; till `personalEmail.address` fältet.

>[!IMPORTANT] När du kör en PATCH-åtgärd på en datamängds `schemaMetadata` egenskap måste du kopiera alla befintliga underegenskaper inom nyttolasten för begäran. Om befintliga värden utesluts från nyttolasten tas de bort från datauppsättningen.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `namespace` | En array med en lista över de namnutrymmen som ska associeras med det fält som anges i `path`. Namnutrymmen används för att identifiera sekretessrelaterade fält när du [skickar åtkomstbegäranden eller borttagningsbegäranden](#submit) i sekretesstjänstens API. |
| `path` | Sökvägen till fältet i datasetens associerade schema som gäller för `namespace`. Helst ska sekretessetiketter endast användas för&quot;lövfält&quot; (fält utan underfält). |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med ID:t för datauppsättningen i nyttolasten. Om du använder ID:t för att söka efter datauppsättningen igen visas att sekretessetiketterna har lagts till.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Märka kapslade mappningsfält

Det är viktigt att komma ihåg att det finns två typer av kapslade mappningsfält som inte har stöd för sekretessetiketter:

* Ett mappningsfält i ett matristypsfält
* Ett mappningsfält i ett annat mappningsfält

Bearbetning av sekretessjobb för något av de två exemplen ovan kommer så småningom att misslyckas. Därför rekommenderar vi att du undviker att använda kapslade mappningsfält för att lagra privata kunddata. Relevanta konsument-ID:n ska lagras som en icke-mappad datatyp i `identityMap` fältet (i sig ett mappningsfält) för postbaserade datauppsättningar, eller i `endUserID` fältet för tidsseriebaserade datauppsättningar.

## Skicka begäranden {#submit}

>[!NOTE] I det här avsnittet beskrivs hur du formaterar sekretessförfrågningar för Data Lake. Vi rekommenderar att du läser igenom [sekretesstjänstens API](../privacy-service/api/getting-started.md) eller [sekretesstjänstens](../privacy-service/ui/overview.md) användargränssnittsdokumentation för att få information om hur du skickar ett sekretessjobb, inklusive hur du formaterar inskickade användaridentitetsdata i begärande nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för Data Lake med API:t för sekretesstjänsten eller användargränssnittet.

### Använda API

När du skapar jobbförfrågningar i API:t måste alla `userIDs` som anges använda ett specifikt `namespace` och `type` beroende på vilket datalager de gäller för. ID:n för Data Lake måste använda&quot;unregistered&quot; för sitt `type` värde och ett `namespace` värde som matchar en av de [sekretessetiketter](#privacy-labels) som har lagts till i tillämpliga datauppsättningar.

Dessutom måste arrayen för den begärda nyttolasten innehålla produktvärdena för de olika datalager som begäran görs till. `include` När du gör förfrågningar till Data Lake måste arrayen innehålla värdet &quot;aepDataLake&quot;.

Följande begäran skapar ett nytt sekretessjobb för Data Lake med det oregistrerade namnutrymmet&quot;email_label&quot;. Den innehåller också produktvärdet för Data Lake i `include` arrayen:

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
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### Använda gränssnittet

När du skapar jobbförfrågningar i användargränssnittet måste du välja **AEP Data Lake** och/eller **Profile** under _Products_ för att kunna bearbeta jobb för data som lagras i Data Lake respektive Real-time Customer Profile.

<img src="images/privacy/product-value.png" width="450"><br>

## Ta bort bearbetning av begäran

När Experience Platform tar emot en begäran om borttagning från Integritetstjänst skickar Platform en bekräftelse till Integritetstjänst om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från datasjön inom sju dagar. Under denna sjudagarsperiod tas data bort på skärmen och är därför inte tillgängliga för någon plattformstjänst.

I framtida versioner kommer Platform att skicka en bekräftelse till sekretesstjänsten när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till i de viktiga koncept som ingår i bearbetning av sekretessförfrågningar för Data Lake. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

I dokumentet om behandling av [sekretessförfrågningar för kundprofil](../profile/privacy.md) i realtid finns information om hur du hanterar sekretessförfrågningar för profilbutiken.