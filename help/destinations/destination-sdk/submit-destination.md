---
description: På den här sidan finns all information du behöver för att kunna granska en produkterad målplats som skapats med Destination SDK.
title: Skicka för granskning av ett produkterat mål som skapats i Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: e68ae7d1cb87d078d9fce5a5df501cc6ce944403
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Skicka för granskning av ett produkterat mål som skapats i Destination SDK

## Översikt {#overview}

>[!IMPORTANT]
>
>* Processen som beskrivs här krävs endast för partners som skickar producerade (offentliga) destinationer. Om du skapar ett privat mål för eget bruk behöver du inte producera och dela dessa material med Adobe.
>
>* Adobe standardsvarstid för att granska begäranden om publicering är fem arbetsdagar.
>
>* Om Adobe-teamet frågar om du vill göra några uppdateringar av dina konfigurationer efter ditt ursprungliga inskick, måste du skicka in en ny begäran om målpublicering när du har gjort uppdateringarna.
>
>* Även efter att målet finns i Experience Platform-katalogen måste du, om du behöver göra några uppdateringar av dina konfigurationer, skicka en ny begäran om målpublicering för att uppdateringarna ska återspeglas i konfigurationerna.


Innan destinationen kan publiceras på [Experience Platform destinationskatalog](/help/destinations/catalog/overview.md)måste du ge Adobe viss information om destinationen och testningen du utförde för att säkerställa att användarna får bästa möjliga upplevelse när de aktiverar data till din plattform.

På den här sidan visas all information du behöver ange när du skickar eller uppdaterar ett mål som du har skapat med Adobe Experience Platform Destination SDK. Om du vill skicka ett mål i Adobe Experience Platform skickar du ett e-postmeddelande till <aepdestsdk@adobe.com> som innehåller

* En beskrivning av de användningsfall som målet löser. Detta är inte nödvändigt om du uppdaterar en befintlig målkonfiguration.
* Testa resultaten efter att du har använt API-slutpunkten för testmålet för att utföra ett HTTP-anrop till målet. Dela med Adobe:
   * Ett API-anrop har gjorts till målslutpunkten.
   * API-svaret som togs emot från målslutpunkten.
* Bevis på att du har skickat in en begäran om målpublicering för destinationen med [målpublicerings-API](./destination-publish-api.md).
* A documentation PR (pull request), following the instructions descriin the [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md).
* En bildfil som visas som logotyp för målkortet i Experience Platform-katalogen.

Du hittar detaljerad information om varje objekt i avsnitten nedan:

## Använd fallbeskrivning

Ange en beskrivning av de användningsfall som din destination löser för Experience Platform-kunder. Dina beskrivningar kan likna användningsexempel från befintliga partners:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-API:er är tillgängliga för annonsörer som vill rikta sig till en viss målgruppsgrupp som är avstämd från e-postadresser i Verizon Media (VMG) kan snabbt skapa ett nytt segment och skicka den önskade målgruppsgruppen med hjälp av VMG:s API i nära realtid.

## Testresultat efter användning av testmåls-API

Tillhandahåll testresultat efter användning av [API för testmål](./test-destination.md) slutpunkt för att utföra ett HTTP-anrop till målet. Det inkluderar:

* Den fullständiga API-begäran (huvuden och brödtext) som görs till målslutpunkten med hjälp av testnings-API:t.
* API-svaret som togs emot från målslutpunkten.

Din begäran och ditt svar kan till exempel se ut som i exemplen nedan:

**Begäran**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Svar**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## Bevis på att du har skickat in en begäran om målpublicering

När du har testat destinationen måste du använda [målpublicerings-API](./destination-publish-api.md) skicka in destinationen till Adobe för granskning och publicering.

Ange ID:t för publiceringsbegäran för ditt mål. Mer information om hur du hämtar ID för publiceringsbegäran finns i [Lista målpubliceringsbegäranden](./destination-publish-api.md#retrieve-list).

## Måldokumentation PR (pull-begäran) för producerade integreringar

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktionsintegrering](./overview.md#productized-custom-integrations), använder du [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen. Som en del av inlämningsprocessen anger du pull-begäran (PR) för destinationsdokumentationen.

## Logotyp för ditt mål {#logo}

Målkatalogen innehåller en logotyp för varje destinationskort. I e-postmeddelandet med ditt tävlingsbidrag inkluderar du en bild med logotypen för destinationen.

Bildkraven är:
* **Format**: `SVG`
* **Storlek**: mindre än 2 MB

## Ladda ned exempelmejl

[Hämta](./assets/sample-email-submit-destination.rtf) ett exempelmejl med all information du behöver ge Adobe.
