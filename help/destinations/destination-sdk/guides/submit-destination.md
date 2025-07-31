---
description: På den här sidan finns all information du behöver för att skicka in en produkterad destination för granskning när du har skrivit den med Destination SDK.
title: Skicka en produkterad destination för granskning
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# Skicka en produkterad destination för granskning

## Översikt {#overview}

>[!IMPORTANT]
>
>* Processen som beskrivs här krävs endast för partners som skickar producerade (offentliga) destinationer. Om du skapar ett privat mål för eget bruk behöver du inte producera och dela dessa material med Adobe.
>
>* Adobe standardsvarstid för granskning av målpubliceringsbegäranden är fem arbetsdagar.
>
>* Om Adobe-teamet frågar om du vill göra några uppdateringar av dina konfigurationer efter det att du skickat in ditt första bidrag, måste du skicka in en ny begäran om målpublicering när du har gjort uppdateringarna.
>
>* Om du behöver göra några uppdateringar av dina konfigurationer måste du skicka en ny begäran om målpublicering för att uppdateringarna ska återspeglas i konfigurationerna, även efter att destinationen är aktiv i Experience Platform-katalogen.
>
>* Tidslinjen för granskningen och nödvändiga artefakter är desamma för nya destinationer och befintliga destinationer som du uppdaterar.

Innan destinationen kan publiceras till [Experience Platform målkatalog](/help/destinations/catalog/overview.md) måste du förse Adobe med viss information om destinationen och testningen du utförde för att säkerställa att användarna får bästa möjliga upplevelse när de aktiverar data till din plattform.

På den här sidan visas all information du behöver ange när du skickar eller uppdaterar ett mål som du har skapat med Adobe Experience Platform Destination SDK. Om du vill skicka ett mål i Adobe Experience Platform skickar du ett e-postmeddelande till <aepdestsdk@adobe.com> som innehåller:

* En beskrivning av de användningsfall som målet löser. Detta är endast nödvändigt om du skickar in en ny målkonfiguration.
* En beskrivning av anledningen till att du skickat in destinationen. Detta är endast nödvändigt om du uppdaterar en befintlig målkonfiguration.
* Testa resultaten efter att du har använt API-slutpunkten för testmålet för att utföra ett HTTP-anrop till målet. Dela ett API-anrop till målslutpunkten med Adobe och det API-svar som tas emot från målslutpunkten.
* En skärminspelning som visar användarupplevelsen för någon som ansluter till destinationen och fortsätter genom aktiveringsstegen.
* Ytterligare krav för filbaserade mål:
   * Dela en begäran och ett svarsexempel efter att du har använt testnings-API:t för att [testa ditt filbaserade mål med exempelprofiler](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Bifoga en exempelfil som har genererats av ditt mål och exporterats till din lagringsplats.
   * Skicka in någon form av bevis på att du har importerat den exporterade filen från lagringsplatsen till systemet.
* Bevis på att du har skickat in en destinationspubliceringsbegäran för ditt mål med [målpublicerings-API:t](../publishing-api/create-publishing-request.md).
* En PR-dokumentation (pull-begäran) som följer instruktionerna som beskrivs i [självbetjäningsdokumentationsprocessen](../docs-framework/documentation-instructions.md).
* En bildfil som visas som en logotyp för målkortet i Experience Platform målkatalog.

Du hittar detaljerad information om varje objekt i avsnitten nedan:

## Använd fallbeskrivning {#use-case-description}

Ange en beskrivning av de användningsområden som din destination löser för Experience Platform-kunder. Dina beskrivningar kan likna användningsexempel från befintliga partners:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Skapa målgrupper från kundlistor, personer som har besökt din webbplats eller personer som redan har interagerat med ditt innehåll på Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-API:er är tillgängliga för annonsörer som vill ha en specifik målgruppsgrupp som är inkapslad med e-postadresser i Verizon Media (VMG) kan snabbt skapa en ny målgrupp och skicka den önskade målgruppsgruppen med hjälp av VMG:s API i nära realtid.

## Orsak till uppdatering {#reason-for-update}

>[!NOTE]
>
>Det här avsnittet behövs bara när du uppdaterar en befintlig konfiguration.

Ge en kort beskrivning av problemet som ditt bidrag löser för det befintliga målet. Ditt tävlingsbidrag kan till exempel uppdatera namnet, beskrivningen och logotypen för ditt mål när du går från betaversion till allmän tillgänglighet. Du kan också åtgärda ett fel som upptäckts i målkonfigurationen.

## Testresultat efter användning av testmåls-API {#testing-api-response}

Ange testresultat efter att du har använt [testmålets API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)-slutpunkt för att utföra ett HTTP-anrop till målet. Detta inkluderar:

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

## Ytterligare krav för filbaserade mål {#additional-file-based-destination-requirements}

För filbaserade mål måste du lägga in ytterligare bevis för att du har konfigurerat destinationen korrekt. Se till att du tar med objekten nedan:

### Testa API-svar {#testing-api-response-file-based}

Inkludera en begäran och ett svarsexempel efter att du har använt testnings-API:t för att [testa ditt filbaserade mål med exempelprofiler](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Bifoga exporterad fil {#attach-exported-file}

Bifoga en CSV-fil som exporterades till din lagringsplats av det mål som du konfigurerade i ditt [e-postmeddelande](#download-sample-email).

### Bevis på godkänt intag {#proof-of-successful-ingestion}

Slutligen måste du tillhandahålla någon form av bevis för att data har importerats till systemet efter att de exporterats till den angivna lagringsplatsen. Ange något av följande:

* Skärmbilder eller en kort skärmdumpsvideo där du tar filen manuellt från lagringsplatsen och importerar den till datorn.
* Skärmbilder eller en kort skärmdumpsvideo där användargränssnittet i systemet bekräftar att filnamnet som genererats av Experience Platform har importerats till systemet.
* Logga rader från ditt system som Adobe kan korrelera med filnamnet eller med data som genereras från Experience Platform.

## Bevis på att du har skickat in en begäran om målpublicering {#destination-publishing-request-proof}

När du har testat målet måste du använda [målpublicerings-API:t](../publishing-api/create-publishing-request.md) för att skicka målet till Adobe för granskning och publicering.

Ange ID:t för publiceringsbegäran för ditt mål. Mer information om hur du hämtar ID för publiceringsbegäran finns i [Hämta målpubliceringsbegäranden](../publishing-api/retrieve-publishing-request.md).

## Måldokumentation PR (pull-begäran) för producerade integreringar {#documentation-pr}

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [tillverkad integrering](../overview.md#productized-custom-integrations) måste du använda [självbetjäningsdokumentationsprocessen](../docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för ditt mål. Som en del av inlämningsprocessen anger du pull-begäran (PR) för destinationsdokumentationen.

## Logotyp för ditt mål {#logo}

Målkatalogen innehåller en logotyp för varje destinationskort. I e-postmeddelandet med ditt tävlingsbidrag inkluderar du en bild med logotypen för destinationen.

Bildkraven är:
* **Format**: `SVG`
* **Storlek**: mindre än 2 MB

## Ladda ned exempelmejl {#download-sample-email}

[Hämta](../assets/guides/sample-email-submit-destination.rtf) ett exempelmeddelande med all information som du behöver ange för Adobe.
