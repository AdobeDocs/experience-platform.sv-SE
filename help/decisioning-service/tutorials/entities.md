---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Hantera beslutstjänstentiteter med API:er
topic: tutorial
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '7207'
ht-degree: 0%

---


# Hantera beslutsobjekt och regler med API:er

I det här dokumentet finns en självstudiekurs om hur du arbetar med affärsenheterna i [!DNL Decisioning Service] Adobe Experience Platform API:er.

Självstudiekursen består av två delar:

- Allmänna databas-API:er för att hantera affärsobjekt introduceras i [första delen](#managing-repository-entities-using-apis). Dessa API:er är generiska i den mening att de ger funktioner för att skapa, läsa, uppdatera, ta bort och söka efter **alla** typer av affärsobjekt. Den allmänna API-modellen beskrivs och relationen till HAL (Hypertext Application Language) förklaras.

- Genom att tillämpa kunskaperna om databas-API:erna fokuserar den [andra delen](#creating-and-managing-offer-decisioning-entities-using-apis) på de affärsenheter som hanteras via API:erna för databasen. När samma API:er används är den enda skillnaden mellan att hantera två olika enheter, till exempel en aktivitet, och en affärsregel är nyttolasten för begäran och svar, plus nödvändiga huvudvärden som anger vilken typ av objekt som hanteras.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL Experience Platform] tjänsterna och API-konventionerna. Databasen är en tjänst som används av flera andra [!DNL Platform] [!DNL Platform] tjänster för att lagra affärsobjekt och olika typer av metadata. Det är ett säkert och flexibelt sätt att hantera och fråga efter dessa objekt för användning av flera runtime-tjänster. Det [!DNL Decisioning Service] är en sådan. Innan du börjar med den här självstudiekursen bör du läsa i dokumentationen om följande:

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
- [!DNL Decisioning Service](./../home.md): Beskriver de begrepp och komponenter som används för Experience Decision i allmänhet och offertbeslut i synnerhet. Illustrerar de strategier som används för att välja det bästa alternativet att presentera under en kunds upplevelse.
- [!DNL Profile Query Language (PQL)](../../segmentation/pql/overview.md): PQL är ett kraftfullt språk för att skriva uttryck över XDM-instanser. PQL används för att definiera beslutsregler.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API: [!DNL Platform] erna.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Konventioner för databas-API

[!DNL Decisioning Service] styrs av ett antal affärsobjekt som är relaterade till varandra. Alla affärsobjekt lagras i [!DNL Platform’s] Business Object Repository. En viktig funktion i den här databasen är att API:erna är ortogonala till typen av affärsobjekt. I stället för att använda API:t POST, GET, PUT, PATCH eller DELETE som anger resurstypen i dess API-slutpunkt, finns det bara 6 generiska slutpunkter, men de accepterar eller returnerar en parameter som anger objekttypen när det behöver det. Schemat måste registreras med databasen, men utöver det kan databasen användas för en öppen uppsättning objekttyper.

Förutom rubrikerna ovan har API:erna för att skapa, läsa, uppdatera, ta bort och fråga databasobjekt följande konventioner:

- Slutpunktssökvägarna för alla databas-API:er börjar med `https://platform.adobe.io/data/core/xcore/`.

API-nyttolastformat förhandlas med en `Accept` eller `Content-Type` en rubrik. Meddelandeformat i `Accept` - eller `Content-Type` -huvudet anges med ett värde `application/vnd.adobe.platform.xcore.{FORMAT}+json` där {FORMAT} är beroende av den specifika databasens API-begäran eller svarsmeddelande, enligt följande tabell.

| FORMAT-variant | Beskrivning av begäran eller svar |
| --- | --- |
| halföljt<br>av en parameter `schema={schemaId}` | Meddelandet innehåller en instans som beskrivs av ett JSON-schema som anges av formatparameterschemat. Instansen kapslas i en JSON-egenskap `_instance`. De andra egenskaperna på den översta nivån i svarsnyttolasten anger databasinformation som är tillgänglig för alla resurser.  Meddelanden som överensstämmer med HAL-formatet har en `_links` egenskap som innehåller referenser i HAL-format. |
| `patch.hal` | Meddelandet innehåller en JSON PATCH-nyttolast med antagandet att instansen som ska korrigeras är HAL-kompatibel. Det innebär att det inte bara är instansens egna instansegenskaper som kan korrigeras, utan även instansens HAL-länkar. Observera att det finns begränsningar för vilka egenskaper klienten kan uppdatera. |
| `home.hal` | Meddelandet innehåller en JSON-formaterad representation av en dokumentresurs hemma för databasen. |
| xdm.receipt | Meddelandet innehåller ett JSON-formaterat svar för en skapad, uppdaterad (fullständig och korrigerad) eller borttagningsåtgärd. Kvittenser innehåller kontrolldata som anger ändringen av instansen i form av en ETag. |

Användningen av varje **formatvariant** beror på det specifika API:t:

| API | Content-Type header | Acceptera rubrik |
| --- | --- | --- |
| Skapa behållare <br/>för instansskapande | `hal`<br/>med schemaparameter | `xdm.receipt` |
| Uppdatera<br/>InstanceUpdate-behållare | `hal`<br/>med schemaparameter | `xdm.receipt` |
| Korrigeringsinstans | `patch.hal` | `xdm.receipt` |
| Ta bort<br/>behållare för instanceDelete | Ej tillämpligt | `xdm.receipt` |
| Läsa<br/>InstanceRead-behållare | Ej tillämpligt | `hal` med `schema` parameter |
| List<br/>instancesList containers | Ej tillämpligt | `hal` med särskild `schema` parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Sökinstanser | Ej tillämpligt | hal med särskild `schema` parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Läs repo-rot | Ej tillämpligt | `home.hal` |

För behållarens API:er för att skapa, uppdatera och läsa har formatparameterschemat värdet `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` är den första sökvägsparametern för instans-API:erna. Alla affärsenheter finns i vad som kallas behållare. En behållare är en isoleringsmekanism för att hålla olika bekymmer isär. Det första sökvägselementet för databasinstansens API:er efter den allmänna slutpunkten är `containerId`. Identifieraren hämtas från listan med behållare som är tillgängliga för anroparen. Exempel: API:t för att skapa en instans i en behållare är `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

Listan över tillgängliga behållare hämtas genom att databasens rotslutpunkt &quot;/&quot; anropas med en HTTP GET-begäran med standardrubrikerna.

## Hantera åtkomst till behållare

En administratör kan gruppera liknande principer, resurser och åtkomstbehörigheter i profiler. Detta minskar den administrativa bördan och stöds av användargränssnittet [för](https://adminconsole.adobe.com)Adobe i Admin Console. Du måste vara produktadministratör för Adobe Experience Platform i din organisation för att kunna skapa profiler och tilldela användare till dem.

Det räcker med att skapa produktprofiler som matchar vissa behörigheter i ett enda steg och sedan lägga till användare i dessa profiler. Profiler fungerar som grupper som har beviljats behörigheter och alla verkliga användare eller tekniska användare i gruppen ärver dessa behörigheter.

### Visa behållare som är tillgängliga för användare och integreringar

När administratören har beviljat åtkomst till behållare för vanliga användare eller integreringar visas dessa behållare i databasens så kallade&quot;Hem&quot;-lista. Listan kan vara annorlunda för olika användare eller integreringar eftersom den är en delmängd av alla behållare som är tillgängliga för anroparen. Listan med behållare kan filtreras efter deras koppling till produktkontexter. Filterparametern anropas `product` och kan upprepas. Om fler än ett produktkontextfilter anges returneras kombinationen av de behållare som har associationer med någon av de angivna produktkontexterna. Observera att en enstaka behållare kan kopplas till flera produktkontexter.

Kontexten för [!DNL Platform][!DNL Decisioning Service] behållarna är för närvarande `dma_offers`.

>[!NOTE]
>
>Kontexten för [!DNL Platform Decisioning Containers] är snart på väg att ändras till `acp`. Filtrering är valfritt, men bara filter `dma_offers` kräver redigering vid en framtida release. För att förbereda den här ändringen ska klienterna inte använda några filter eller använda båda produktkontexterna som filter.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Svar**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Observera vad som `instanceId` visas i resultatalternativen. Den används som `containerId` parameter i API:erna för att läsa och ändra vanliga affärsobjekt.

Listan har redan filtrerats för användarna efter deras åtkomstbehörigheter, men kan filtreras ytterligare av en egenskapsfråga.

## Allmänna API:er för att hantera entiteter

### Skapa instanser

API:t för att skapa en ny instans i databasen tar en sökvägsparameter och identifierar typen av instans i `containerId` `Content-Type` huvudet med schemaparametern.

Instansegenskaperna anges i nyttolasten som omsluts av `_instance` egenskapen. Instansegenskaperna måste vara giltiga mot JSON-schemat med den angivna schema-ID:t.

HAL- `_links` egenskapen måste finnas men kan vara tom. Det betyder att inga anpassade länkar har definierats för den här instansen.

**Begäran**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Svar**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

Svaret innehåller instanceId för objektet som precis skapades. Detta instanceId kan inte ändras, tilldelas alltid av databasen och är globalt unikt. Värdet fungerar som en fysisk identifierare.

Dessutom returneras en URI (Universal resource identifier) i `@id` egenskapen för svarsnyttolasten om schemat har en sådan egenskap. Varje instans ska ha en egenskap som fungerar som URI och instansens primärnyckel. Den här identifieraren används av andra instanser för att skapa relationer med den nya instansen, även mellan olika typer. I den aktuella versionen genereras URI:erna av databasen och finns i `@id` egenskapen. Framtida versioner kan koppla av den här regeln och låta klienterna hantera sina egna URI-värden och namnge egenskapen som innehåller den.

Observera att dessa URI:er inte är URL:er och inte tillhandahåller ett sätt att hämta resursen direkt. För att ange den aspekten har URI:n ett URI-schema som inte anger ett hämtningsprotokoll. URI:erna kan dock användas för att söka efter instansen med en fråga.

REST-svaret kommer att ha ett Location-huvud som innehåller en URL-komponent som kan användas för att hämta instansen som precis skapades. Den här komponenten är en relativ URI-referens och måste tillämpas på databasens bas-URI. Bas-URI returneras i `Content-Base` rubriken.

Egenskapen anger `repo:etag` instansens revision. Det här värdet kan användas i uppdateringsåtgärder för att framtvinga konsekvens. HTTP-huvudet `If-Match` kan användas för att lägga till ett villkor i ett API-anrop för PUT eller PATCH som säkerställer att det inte fanns några andra ändringar i instansen som skulle kunna skrivas över av misstag. Värdet `repo:etag` returneras med varje anrop om att skapa, läsa, uppdatera, ta bort och fråga. Värdet används som värde i ` If-Match` huvudet, enligt [RFC7232, avsnitt 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

De återstående egenskaperna anger vilket konto och vilken API-nyckel som användes för att skapa och senast ändra instansen. Eftersom instansen skapades av det här anropet är de respektive värdena för begäran.

### Söka efter en instans med ID

Med hjälp av URL:en i Location-huvudet som returneras med Create-anropet kan ett program söka efter en instans.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Även om det `instanceId` anges som en sökvägsparameter bör program, när det är möjligt, inte konstruera själva sökvägen utan i stället följa länkar till förekomster i list- och sökåtgärder. Se avsnitt ‎ 6.4.4 och ‎ 6.4.6 för mer information.

**Svar**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Instansens JSON-egenskaper kapslas i `_instance` egenskapen och de andra rotnivåegenskaperna innehåller metadata om instansen.

Resursen innehåller även en array med JSON-schema-ID:n. Den här arrayen anger de JSON-scheman som den här instansen valideras mot.

Varje instans innehåller en HAL-länk av relationstypen self som motsvarar den IANA-registrerade självrelationen (enligt definition i [RFC5988]).

**Testa om det finns nyare versioner av en instans**

Det aktuella `eTag` värdet för instansen returneras med svaret, vilket gör att klienter kan utfärda villkorliga åtgärder mot instansen, antingen för att undvika att hämta samma resurstillstånd igen eller för att undvika att skriva över en senare revisions värden utan att klientens vetskap.

Med API:t för sökning kan en klient ange en `If-None-Match` rubrikparameter. Se definitionen av den här standard-HTTP-parametern [RFC2616]. Värdet för enhetstaggen som en klient anger är det värde som den fick med det senaste svaret, antingen från ett API-anrop för uppdatering, läsning, lista eller sökning. Observera att `etag` värdet ska vara ogenomskinligt för klienten och måste anges som en sträng omgivet av citattecken.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

Databas-API:t svarar med statusen 304 Inte ändrad när instansens senaste version är den som har taggen angiven.

### Visa instanser för ett schema - sortering och sidindelning

Klienter kan inte hålla reda på de instanser som de skapar och därmed komma åt dem med sitt fysiska instanceId. Undantaget blir att använda API:t för läsinstans. Klienterna vet inte heller vilka instanser andra klienter har skapat.

Ett vanligare åtkomstmönster är att bläddra igenom alla förekomster.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Svar**

Svaret beror på det `{schemaId}` angivna värdet. För&quot;/ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73&quot; liknar svaret följande:<span></span>

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>Resultatet innehåller instanser för det angivna schemat eller den första sidan i listan. Observera att instanser kan vara kompatibla med mer än ett schema och därför kan visas i mer än en lista.

Sidresurserna är övergående och skrivskyddade; de kan inte uppdateras eller tas bort. Sidindelningsmodellen ger slumpmässig åtkomst till delmängder av stora listor över en längre tidsperiod utan att något klienttillstånd upprätthålls.

Om du vill få åtkomst till en instanslista per sida på det här sättet måste det vara möjligt att definiera en stabil sortering över posterna som räknas upp i instanslistan. Observera att&quot;stabil&quot; inte innebär att instanser visas på en förbestämd sida. När en sidordning skapas genom att instanser sorteras enligt egenskapen P och en klient uppdaterar egenskapen P, kan en annan klient komma åt den här instansen igen på en annan sida medan användaren bläddrar igenom listan. Med andra ord prioriterar modellen att returnera mer aktuella resultat.

När sorteringsordningen baseras på en icke-modifierbar egenskap garanterar en&quot;stabil&quot; sorteringsordning att alla förekomster som fanns i början av växlingsåtgärden kommer att nås (om de inte togs bort när sidan nåddes). När den här sorteringsordningen finns på en egenskap som ökar monotont, kommer även instanser som skapas efter att växlingsåtgärden har startats att nås.

En klient kan ge tips om den sidstorlek som kunden vill ha, men det är helt och hållet upp till databasen att tillhandahålla fler eller färre instanser av den sida som returneras. För att garantera en stabil ordning måste tjänsten lägga till eller ta bort objekt från sidan så att värdet för sorteringsegenskapen skiljer sig åt över sidgränserna. På så sätt kommer nästa sida inte att innehålla några objekt från den sista sidan igen eller i ett värsta fall kommer de att fastna med samma objekt på varje sida.

Sidindelning styrs av följande parametrar:

- **`orderBy`**: Innehåller en kommaavgränsad, ordnad lista med egenskaper som instanslistan sorteras efter. Den första egenskapen används för primär sortering, den andra egenskapen för att lösa bindningar i primär sortering och så vidare. När en egenskap som har ett unikt värde per instans anges, går det inte att använda linjer och en sidbrytning kan inträffa efter varje objekt. Namnet på en egenskap kan föregås av ett `+` för att ange stigande ordning eller `-` för att ange fallande ordning för den egenskapen. Om egenskapsnamnet inte är prefix sorteras resultatet i stigande ordning. Om `orderBy` inte anges i begäran kommer databasen att använda egenskapen physical instanceId i stället.
- **`start`**: Klienter använder startparametern för att definiera sidan som de vill hämta. Startparametern bestämmer början på den önskade sidan. Svaret innehåller instanser som börjar med de som har ett `orderBy` egenskapsvärde som är strikt större än (för stigande) eller strikt mindre än (för fallande) det angivna värdet. När frågeparametern inte har angetts blir standardvärdet ett instanceId-värde som sorterar före den första möjliga förekomstidentifieraren, och därför utelämnas det här värdet från den första sidan.
- **`limit`**: anger ett positivt heltal som ett tips om det maximala antalet objekt som ska returneras för en viss begäran. Den faktiska svarsstorleken kan vara mindre eller större, vilket begränsas av behovet av att kunna erbjuda tillförlitlig användning av startparametern

### Filtreringslistor

Det går att filtrera listresultaten och de utförs oberoende av sidindelningsmekanismen. Filtren hoppar över förekomster i listordningen eller ber uttryckligen bara om de förekomster som uppfyller ett visst villkor ska tas med. En klient kan begära att egenskapsuttryck ska användas som ett filter eller ange en lista med URI:er som ska användas som värden för primärnyckeln för instanserna.

- **`property`**: Innehåller en egenskapsnamnsökväg följt av en jämförelseoperator följt av ett värde. <br/>
Listan med returnerade instanser innehåller de för vilka uttrycket utvärderas till true. Anta till exempel att instansen har en nyttolast-egenskap 
`status` och de möjliga värdena är `draft`, `approved`och `archived` sedan `deleted` `property=_instance.status==approved` returnerar frågeparametern bara instanser för vilka statusen har godkänts. <br/>
<br/>
Egenskapen som ska jämföras med det angivna värdet identifieras som en sökväg. De enskilda bankomponenterna avgränsas med ".", som: `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

För egenskaper som har strängvärden, numeriska värden eller datum/tid-värden är följande tillåtna operatorer: `==`, `!=`, `<`, `<=`och `>``>=`. Dessutom `~` kan en operator användas för egenskaper med ett strängvärde. Operatorn `~` matchar den angivna egenskapen enligt ett reguljärt uttryck. Egenskapens strängvärde måste matcha **hela** uttrycket för entiteterna som ska inkluderas i filtrerade resultat. Om du till exempel söker efter strängen `cars` var som helst inuti egenskapsvärdet måste det reguljära uttrycket vara `.*cars.*`. Utan inledande eller avslutande `.*`skulle bara enheter som har ett egenskapsvärde som börjar eller slutar med `cars`. Jämförelsen av tecken för operatorn är inte skiftlägeskänslig för `~` operatorn. För alla andra operatorer är jämförelsen skiftlägeskänslig.<br/><br/>
Det är inte bara egenskaper för instansnyttolast som kan användas i filteruttryck. Omslagsegenskaperna jämförs på samma sätt, t.ex. `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Frågeparametern kan upprepas så att flera filtervillkor används, t.ex. för att returnera alla instanser som senast ändrades efter ett visst datum och före ett visst datum. `property` Värdena i dessa uttryck måste vara URL-kodade. Om inget uttryck anges och egenskapens namn visas bara de objekt som är kvalificerade är de som har en egenskap med det angivna namnet.<br/>
<br/>

- **`id`**: Ibland måste en lista filtreras efter instansens URI. Frågeparametern kan användas för att filtrera ut en instans, men för att hämta mer än en instans kan en lista över URI:er ges till begäran. `property` Parametern `id` upprepas och varje förekomst anger ett URI-värde. URI- `id={URI_1}&id={URI_2},…` värdena måste vara URL-kodade.

Växlingsresultatet returneras som en speciell MIME-typ `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Svar**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

Svaret innehåller en lista med resultatobjekt i JSON-egenskapsresultaten intill två egenskaper som anger antalet resultat på den här sidan och det totala antalet objekt i den filtrerade listan som börjar med sidan som precis returnerats.

### Fullständig textsökning och strukturerade frågor

I de fall där klienterna vill skapa mer komplexa filtervillkor och söka efter instanser med hjälp av termer i strängegenskaper erbjuder databasen ett mer kraftfullt söknings-API.

**Begäran**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Förutom sidindelning och filtreringsparametrarna från list-API:erna tillåter detta API att klienter lägger till full text och booleska frågeparametrar.

Fulltextsökning styrs av följande parametrar:

- **`q`**: Innehåller en blankstegsavgränsad osorterad lista med termer som normaliseras innan de matchas mot strängegenskaper för förekomsterna. Strängegenskaper analyseras efter termer och dessa termer normaliseras också. Sökfrågan försöker matcha en eller flera av de termer som anges i `q` parametern. Tecknen +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,]^, &quot;, ~, *, ?, :, / har en speciell innebörd för att bestämma ordgränserna i frågesträngen och bör föregås av ett omvänt snedstreck i en token som ska matcha tecknet. Frågesträngen kan omges av citattecken för exakt strängmatchning och för att undvika specialtecken.
- **`field`**: Om söktermerna bara ska matchas mot en delmängd av egenskaperna kan fältparametern ange sökvägen till den egenskapen. Parametern kan upprepas för att ange mer än en egenskap som ska matchas mot.
- **`qop`**: Innehåller en kontrollparameter som används för att ändra sökningens matchande beteende. När parametern är inställd på och sedan måste alla söktermer matcha och när parametern är frånvarande eller dess värde är inställt på, kan alla termer räkna för en matchning.

### Uppdatera och korrigera instanser

Om du vill uppdatera en instans kan klienten antingen skriva över hela egenskapslistan samtidigt eller använda en JSON PATCH-begäran för att ändra enskilda egenskapsvärden, inklusive listor.

I båda fallen anger URL:en för begäran sökvägen till den fysiska instansen och i båda fallen är svaret en JSON-kvittonyttolast som den som returneras från [skapandeåtgärden](#create-instances). En klient bör helst använda det huvud eller den HAL-länk som den fått från ett tidigare API-anrop för det här objektet som den fullständiga URL-sökvägen för det här API:t. `Location` Om detta inte är möjligt kan klienten skapa URL:en från `containerId` och `instanceId`.

**Begäran** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Begäran** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

PATCH-begäran tillämpar instruktionerna och validerar sedan den resulterande entiteten mot schemat och samma entitet och referensintegritetsregler som PUT-begäran.

**Styra redigeringar av egenskapsvärden**

Du kan förhindra att egenskaper anges när du skapar och/eller uppdaterar med följande anteckningar:

- **`"meta:usereditable"`**: Boolesk - När en begäran kommer från en användaragent som identifierar anroparen med en användar- eller teknisk kontoåtkomsttoken, ska egenskaper som är kommenterade med `"meta:usereditable": false` inte finnas i nyttolasten. Om de är det får de inte ha ett annat värde än det som är inställt. Om värdena skiljer sig, avvisas uppdaterings- eller korrigeringsbegäran med statusen 422 Unbehandlable Entity.
- **`"meta:immutable"`**: Boolean - Egenskaper som är kommenterade med `"meta:immutable": true` kan inte ändras när de har angetts. Detta gäller förfrågningar från en slutanvändare, integrering av ett tekniskt konto eller en specialtjänst.

**Test för samtidig uppdatering**

Det finns villkor där flera klienter försöker uppdatera en instans samtidigt. Databasen körs på en grupp datornoder utan central transaktionshantering. För att undvika att en klient skriver en instans som skrivs samtidigt av en annan, kan klienterna använda en villkorlig uppdatering eller korrigeringsbegäran. Genom att ange `etag` strängen i huvudet ser du till `If-Match` att endast den första begäran lyckas och att efterföljande begäranden från andra klienter som använder samma `etag` värde misslyckas. Värdet ändras `etag` för varje ändring av instansen. Klienterna måste hämta instansen för att få det senaste `etag` värdet och sedan kan bara en av många klienter som försöker uppdatera det värdet. Andra klienter kommer att refuseras med meddelandet 409 Conflict.

### Tar bort instanser

Instanser kan tas bort med ett DELETE-anrop. En klient bör helst använda det huvud eller den HAL-länk som den fått från ett tidigare API-anrop för detta som den fullständiga URL-sökvägen. `Location` Om detta inte är möjligt kan klienten skapa URL:en från `containerId` och den fysiska `instanceId`.

**Begäran**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Svar**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

När databasen tar emot en borttagningsbegäran söker den efter andra instanser av ett schema och refererar fortfarande till den instans som ska tas bort. I ett distribuerat system med hög tillgänglighet går det inte att kontrollera referensintegriteten direkt. När sekundärnyckelrelationer har definierats utförs kontroller asynkront. Detta resulterar i ett något fördröjt svar på resultatet av borttagningsbegäran. När dessa kontroller utförs innehåller det omedelbara svaret statusen 202 Godkänd och en länk för att kontrollera resultatet av borttagningsåtgärden i `Location` huvudet. En kund bör sedan kontrollera länken för att se resultatet.

Om en instans som refererar till den instans som tas bort hittas, avvisas borttagningsåtgärden. Om inga andra referenser för främmande nycklar identifieras slutförs borttagningen. Om resultatet ännu inte avgörs kommer svaret att ange att ytterligare 202 svar med samma `Location` huvud kommer att godkännas och kunden kommer att uppmanas att fortsätta att kontrollera. När resultatet är fastställt kommer svaret att ange att med statusen 200 OK och svarets nyttolast kommer att innehålla resultatet av den ursprungliga raderingsbegäran. Observera att svaret från 2000 OK bara innebär att resultatet är känt och att svarstexten innehåller bekräftelsen eller avslaget på raderingsbegäran.

## Skapa erbjudanden och deras underkomponenter

De API:er som beskrivs i föregående avsnitt gäller enhetligt alla typer av affärsobjekt. Den enda skillnaden mellan, till exempel att skapa ett erbjudande och en aktivitet, är den rubrik som anger JSON-schemat som JSON-nyttolasten för den begäran som uppfyller schemat. `content-type` Följande avsnitt behöver därför bara fokusera på dessa scheman och relationerna mellan dem.

När du använder API:erna med innehållstypen `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`bäddas instansens egna egenskaper in i den `_instance` egenskap som det finns en `_links` egenskap bredvid. Det här är det allmänna format som alla instanser representeras i:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Av utrymmesskäl illustreras endast förekomstegenskaperna i alla JSON-kodfragment, och endast när det krävs visas avsnittet kuvertegenskaper och _links.

### Allmänna egenskaper för erbjudanden

Erbjudandena är en typ av beslutsalternativ och erbjudandenas JSON-schema ärver de standardalternativ som varje alternativinstans har.

- **`@id`** - En unik identifierare för varje alternativ som är primärnyckel och som används för att referera till alternativet från andra objekt. Den här egenskapen tilldelas när instansen skapas, är oföränderlig och kan inte redigeras.
- **`xdm:name`** - Alla alternativ har ett namn som används för sök- och visningsändamål. Namnet är inte oföränderligt och kan inte användas för att unikt identifiera instansen. Namnet kan väljas fritt men ska vara unikt för alla instanser av erbjudandet.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern måste vara `schemaId` eller `https://ns.adobe.com/experience/offer-management/personalized-offer` `https://ns.adobe.com/experience/offer-management/fallback-offer` om erbjudandet är ett reserverbjudande.

Varje offer-instans kan ha en valfri uppsättning egenskaper som bara är karakteristiska för den instansen. Olika erbjudanden kan ha olika nycklar för dessa egenskaper, men värdena måste vara strängar. Dessa egenskaper kan användas i beslut och segmenteringsregler. De är också tillgängliga för att sammanställa den beslutna upplevelsen för att ytterligare anpassa meddelandena.

### Erbjud livscykel

Det finns ett enkelt flöde för övergång mellan lägen som alla alternativ följer. De börjar i ett utkast och när de är klara kommer deras tillstånd att godkännas. När slutdatumet har passerat kan de flyttas till arkiverat läge. I det läget kan de tas bort eller återanvändas genom att de flyttas till redigeringsläget igen.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Den här egenskapen används för instansens livscykelhantering. Värdet representerar ett arbetsflödestillstånd som används för att indikera om erbjudandet fortfarande är under uppbyggnad (värde = utkast), kan vanligtvis övervägas av körningsmiljön (värde = godkänt) eller om det inte längre ska användas (värde = arkiverat).

En enkel PATCH-åtgärd i instansen används vanligtvis för att ändra en `xdm:status` egenskap:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern måste vara `schemaId` eller `https://ns.adobe.com/experience/offer-management/personalized-offer` `https://ns.adobe.com/experience/offer-management/fallback-offer` om erbjudandet är ett reserverbjudande.

### Representationer och placeringar

Erbjudandena är beslutsalternativ med innehållsrepresentationer. När ett beslut fattas väljs alternativet och dess identifierare används för att hämta innehålls- eller innehållsreferenserna för den placering som behöver anges. Ett erbjudande kan ha mer än en representation men var och en av dem måste ha olika placeringsreferenser. Detta säkerställer att representationen kan bestämmas entydigt med en viss placering.
Under beslutsåtgärden bestäms placeringen tillsammans med aktivitetsobjektet. Erbjudanden som inte har någon representation med den placeringen som referens tas automatiskt bort från listan med alternativ.

Innan representationer kan läggas till i ett erbjudande måste det finnas placeringsinstanser. Dessa instanser skapas med schema-ID`https://ns.adobe.com/experience/offer-management/offer-placement`.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern måste vara `schemaId` eller `https://ns.adobe.com/experience/offer-management/personalized-offer` `https://ns.adobe.com/experience/offer-management/fallback-offer` om erbjudandet är ett reserverbjudande.

En **Placement** -instans kan ha följande egenskaper:

- **`xdm:name`** - Innehåller ett tilldelat namn för placeringen som refererar till den i mänskliga interaktioner och användargränssnitt.
- **`xdm:description`** - Används för att förmedla mänskliga, läsbara avsikter om hur innehållet i den här placeringen används i den övergripande meddelandeleveransen. När leveranskanaler definierar nya placeringar kan de lägga till ytterligare information i den här egenskapen så att den som skapar innehållet kan skapa eller välja innehållet. Dessa instruktioner tolkas inte formellt eller verkställs inte. Den här egendomen fungerar bara som en plats för att förmedla avsikterna.
- **`xdm:channel`** - En kanals URI. Kanalen anger var det dynamiska innehållet ska levereras. Kanalbegränsningen används för att förmedla inte bara var erbjudandet kommer att användas, utan även för att avgöra vilken innehållsredigerare eller validerare som används för upplevelsen.
- **`xdm:componentType`** - En modellidentifierare, dvs. URI, för innehållet som kan visas på den plats som beskrivs av den här placeringen. Komponenttyperna är: bildlänk, html eller oformaterad text. Varje komponenttyp kan innehålla en viss uppsättning egenskaper (en modell) som innehållsobjektet kan ha. Listan över komponenttyper kan utökas. Det finns tre fördefinierade komponenttypsvärden:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, En begränsning för medietyperna för de komponenter som förväntas i den här placeringen. Det kan finnas mer än en medietyp för en komponenttyp, till exempel olika bildformat.

**Representationsobjekt** i ett erbjudande har en objektstruktur i arrayegenskapen `xdm:representations`. Varje objekt kan ha följande egenskaper:

- **`xdm:placement`** - Den här egenskapen innehåller referensen till placeringsförekomsten. Värdet kontrolleras när representationen läggs till i erbjudandet. Det måste finnas en placeringsinstans med denna URI och den får inte markeras som borttagen. Dessutom utförs en kontroll för att säkerställa att en offertinstans inte har två representationer med samma värde för placeringsreferensen.
- **`xdm:components`** - Innehållskomponenterna är de fragment som är kopplade till en viss anbudsrepresentation. Dessa fragment används senare för att skapa slutanvändarupplevelsen. Observera att beslutstjänsten i sig inte utgör den fullständiga användarupplevelsen. Följande egenskaper är en del av varje komponents modell.
   - **`@type`** - den här egenskapen identifierar komponenttypen. Ett annat namn för det här konceptet är innehållsfragmentmodellen. Komponentens värde är helt enkelt en URI för en modell som definieras av programmet eller tjänsten som sammanställer slutanvändarens upplevelse. `@type`
   - **`repo:id`** - den här egenskapen innehåller en globalt unik, oföränderlig identifierare för komponentens huvudresurs i databasen där resursen lagras.
   - **`repo:name`** - Den här egenskapen innehåller ett läsbart namn för resursen i databasen. Det här namnet är användardefinierat och garanterat inte unikt.
   - **`repo:resolveURL`** - den här egenskapen innehåller en unik resurslokaliserare som kan läsa resursen i en innehållsdatabas. Detta gör det enklare att hämta resursen utan att kunden förstår vilka API:er som ska anropas. URL:en returnerar byte för resursens primära resurs.
   - **`dc:format`** - denna egendom kommer från Dublin Core Metadata Initiative. Format kan användas för att fastställa programvara, maskinvara eller annan utrustning som behövs för att visa eller använda resursen. Rekommenderad bästa metod är att välja ett värde från en kontrollerad vokabulär (till exempel en lista över Internetmedietyper som definierar datormediaformat).
   - **`dc:language`** - Den här egenskapen innehåller resursens språk. Språk anges i språkkoden enligt definitionen i IETF RFC 3066.

Det finns tre fördefinierade komponenttyper som uttrycks i `@type` egenskapen:

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

Beroende på värdet för `@type` egenskapen `xdm:components` kommer att innehålla ytterligare egenskaper:

- **`xdm:linkURL`** - Visas när komponenten är en bildlänk. Den här egenskapen innehåller länken som är kopplad till bilden och som `user-agent` användaren kommer att navigera till när slutanvändaren interagerar med innehållet i erbjudandet.
- **`xdm:copyline`** - Används när komponenten är en text. Förutom att referera till en textresurs, t.ex. för text i lång form Erbjudanden som kan ha formatering i den, kan en kort textsträng lagras direkt i egenskapen xdm:compyline.

Ytterligare egenskaper kan användas av klienter för att ange och utvärdera kontexthanteringsanvisningar. Till exempel lägger klienten Offer UI Library till följande valfria egenskaper som gör det enklare att hantera visningen:

- I varje objekt i `xdm:components` arrayen lägger klienten för användargränssnittet för erbjudandebiblioteket till följande egenskaper. Dessa egenskaper bör inte tas bort eller ändras utan att förstå hur gränssnittet påverkas:
   - **`offerui:previewThumbnail`** - Det här är en valfri egenskap som gränssnittet för erbjudandebiblioteket använder för att visa en återgivning av resursen. Den här återgivningen är inte densamma som själva resursen. Innehållet kan till exempel vara HTML och återgivningen är en bitmappsbild som bara visar en uppskattning av den. Den här (lägre kvalitet) återgivningen visas i erbjudandets representationsblock.

Ett exempel på PATCH-åtgärd för en offertinstans visar hur du hanterar representationerna:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern måste vara `schemaId` eller `https://ns.adobe.com/experience/offer-management/personalized-offer` `https://ns.adobe.com/experience/offer-management/fallback-offer` om erbjudandet är ett reserverbjudande.

Åtgärden PATCH kan misslyckas om det inte finns någon egenskap `xdm:representations` ännu. I så fall kan åtgärden lägg till ovan föregås av en annan tilläggsåtgärd som skapar `xdm:representations` arrayen eller så anger åtgärden lägg till arrayen direkt.
Scheman och egenskaperna som beskrivs används för alla erbjudandetyper, personaliseringserbjudanden och reserverbjudanden. Följande två avsnitt om begränsningar och beslutsregler beskriver olika aspekter av personaliseringserbjudanden.

## Ange begränsningar för erbjudanden

### Kalenderbegränsningar

Beslutsalternativen kan i allmänhet vara ett start- och slutdatum och en sluttid som fungerar som en kalenderbegränsning. Egenskaperna är inbäddade i egenskapen `xdm:selectionConstraint`:

- **`xdm:startDate`** - Den här egenskapen anger startdatum och -tid. Värdet är en sträng som är formaterad enligt RFC 339-regler, d.v.s. följande tidsstämpel: &quot;2019-06-13T11:21:23.356Z&quot;.
Beslutsalternativ som inte har nått sitt startdatum och sin starttid anses ännu inte berättigade i beslutet.
- **`xdm:endDate`** - Den här egenskapen anger slutdatum och sluttid. Värdet är en sträng som är formaterad enligt RFC 339-regler, d.v.s. följande tidsstämpel: &quot;2019-07-13T11:00:00.000Z&quot;Beslutsalternativ som har passerat slutdatum och sluttid anses inte längre vara berättigade i beslutsprocessen.

Du kan ändra en kalenderbegränsning med följande PATCH-anrop:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/personalized-offer`. Reserverbjudanden har inga begränsningar.

### Begränsningar

En begränsning är en komponent i ett beslutsalternativ som definierar parametrarna för begränsning. Funktionen för begränsning av hur många gånger ett alternativ kan föreslås, både för en enskild profil och för alla profiler. Egenskaperna innehåller ett heltalsvärde som måste vara större än eller lika med 1. Egenskaperna är kapslade i en egenskap `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Ett globalt tak är en begränsning av hur många gånger ett erbjudande kan föreslås totalt.
- **`xdm:profileCap`** - Ett profillistecken är en begränsning av hur många gånger ett erbjudande kan föreslås till en viss profil.

Du kan ställa in eller ändra begränsningen för ett personaliseringserbjudande med följande PATCH-anrop:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/personalized-offer`. Reserverbjudanden har inga begränsningar.

Om du vill ta bort capping-värdena ersätts åtgärden &quot;add&quot; med åtgärden &quot;remove&quot;. Observera att capping-värdena finns var för sig och kan ställas in eller tas bort individuellt.

### Behörighetsbegränsningar

Erbjudandena kan väljas på villkor i beslutsprocessen. När ett personaliseringserbjudande har en referens till en berättiganderegel måste villkoret för regeln utvärderas som sant för att erbjudandeobjektet ska beaktas för en viss profil. Behörighetsreglerna skapas och hanteras oberoende av beslutsalternativen och samma regel kan refereras från flera personaliseringserbjudanden.

Referensen till regeln är inbäddad i egenskapen `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Den här egenskapen innehåller en referens till en berättiganderegel. Värdet är värdet `@id` för en instans av schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

Du kan även lägga till och ta bort en regel med en PATCH-åtgärd:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/personalized-offer`. Reserverbjudanden har inga begränsningar.

Observera att berättiganderegeln är inbäddad i `xdm:selectionConstraint` egenskapen tillsammans med kalenderbegränsningarna. PATCH-åtgärder bör inte försöka ta bort hela `SelectionConstraint` egenskapen.

## Ange prioriteten för ett erbjudande

Vilka beslutsalternativ som är kvalificerade rangordnas för att avgöra vilket som är det bästa alternativet för den angivna profilen. För att stödja rankningen och tillhandahålla en standard om rankningen inte kan bestämmas av en annan mekanism kan en basprioritet anges för varje personaliseringserbjudande.
Basprioriteten är inbäddad i egenskapen `xdm:rank`:

- **`xdm:priority`** - Den här egenskapen representerar den standardordning i vilken ett erbjudande väljs över ett annat om det inte finns någon känd profilspecifik rangordningsordning. Om två eller flera personaliseringserbjudanden fortfarande är knutna till varandra efter en jämförelse av prioritetsvärdet väljs de slumpmässigt och används i erbjudandeförslaget. Värdet för den här egenskapen måste vara ett heltal som är större än eller lika med 0.

Du kan justera basprioriteten med följande PATCH-anrop:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/personalized-offer`. Reserverbjudanden har inga rankningsegenskaper.

## Beslutsregler för hantering

Behörighetsreglerna innehåller de villkor som utvärderas för att avgöra om ett visst beslutsalternativ är valbart för en viss profil. Att bifoga en regel till ett eller flera beslutsalternativ definierar implicit att för det här alternativet måste regeln utvärderas till true för att alternativet ska kunna övervägas för den här användaren. Regeln kan innehålla tester av profilattribut, kan utvärdera uttryck som innehåller upplevelsehändelser för den här profilen och kan innehålla kontextdata som skickats till beslutsbegäran. Ett villkor kan till exempel beskrivas så här:

> &quot;Inkludera personer som har elitstatus och som har flugit på en flygning tre gånger under den senaste sex månaden som har det aktuella flygnumret&quot;.

Instanserna skapas med schema-IDhttps://ns.adobe.com/experience/offer-management/eligibility-rule. Egenskapen `_instance` för Skapa eller uppdatera-anropet ser ut så här:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

Värdet i regelns villkorsegenskap innehåller ett PQL-uttryck. Kontextdata refereras via det speciella sökvägsuttrycket @{schemaID}.

Regler justeras naturligt mot segment i [!DNL Experience Platform] och ofta återanvänds ett segments avsikt genom att en profils `segmentMembership` egenskap testas. Egenskapen innehåller `segmentMembership` resultatet av segmentvillkor som redan har utvärderats. På så sätt kan en organisation definiera sina domänspecifika målgrupper en gång, namnge dem och utvärdera villkoren en gång.

## Hantera offertsamlingar

### Skapa taggar och taggningserbjudanden

Erbjudandena kan ordnas i samlingar där varje samling definierar filtervillkoren som ska tillämpas. För närvarande kan filteruttryck i en samling ha en av två former:

1. Erbjudandets `@id` parameter måste matcha en i en lista med identifierare för att erbjudandet ska finnas i samlingen. Det här filtret är bara en uppräkning av URI:erna för erbjudandena i samlingen.
2. Ett erbjudande kan innehålla en lista med taggreferenser och samlingens filter består av en lista med taggar. Erbjudandet gäller följande:\
   a. någon av filtertaggarna matchar någon av erbjudandets taggar\
   b. alla filtertaggar matchar någon av erbjudandets taggar

Taggar är enkla instanser som erbjuder instanser som kan länkas till. De är förekomster av sig själva med ett namn som visar dem. Namnet måste vara unikt för alla instanser för att det ska vara enklare att visa dem i användargränssnittet.

Taggobjekt används för att skapa en kategorisering av beslutsalternativ (erbjudanden). En tagg kan länkas till av många erbjudanden och ett erbjudande kan ha många taggreferenser. En kategori med erbjudanden skapas genom att hänvisa till alla erbjudanden som är relaterade till en given uppsättning tagginstanser.

Tagginstanserna skapas med schema-IDhttps://ns.adobe.com/experience/offer-management/tag. Egenskapen `_instance` för Skapa eller uppdatera-anropet ser ut så här:

```json
{
  "xdm:name": "credit card"
} 
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/tag`.


En offer-instans kan skapas med en lista över taggreferenser som:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Ett erbjudande kan även korrigeras för att ändra listan med taggar:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

I båda fallen finns information om den fullständiga cURL-syntaxen i [Uppdatera och korrigera instanser](#updating-and-patching-instances) . Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Observera att `xdm:tags` egenskapen måste finnas för att åtgärden add ska lyckas. Det finns inga taggar i en instans. PATCH-åtgärden kan först lägga till arrayegenskapen och sedan lägga till en taggreferens till arrayen.

### Definiera filter för erbjudandesamlingar

Filterinstanserna skapas med schema-IDhttps://ns.adobe.com/experience/offer-management/offer-filter. Egenskapen `_instance` för Skapa- eller uppdateringsanropet kan se ut så här:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Den här egenskapen anger om filtret är konfigurerat med hjälp av taggar eller direkt referenser till erbjudanden med deras ID:n. När filtret är inställt på att använda taggar kan filtertypen ytterligare visa om alla taggar måste matcha taggarna för ett visst erbjudande eller om någon av de angivna taggarna är tillräckliga för att erbjudandet ska kvalificera sig för filtret. Giltiga värden för den här enum-egenskapen är:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - En egenskap innehåller en array med URI:er som är referenser till instanser eller tagginstanser, beroende på värdet för `xdm:filterType`. .

Följande anrop visar hur `_instance` egenskapen för anropet create eller update ser ut om erbjudanden refereras direkt:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Hantera aktiviteter

En erbjudandeaktivitet används för att styra beslutsprocessen. Det specificerar det erbjudandefilter som tillämpas på det totala lagret för att begränsa antalet erbjudanden per ämne/kategori, placeringen för att begränsa lagret till de erbjudanden som får plats i det reserverade utrymmet och anger ett reservalternativ om de kombinerade begränsningarna skulle diskvalificera alla tillgängliga anpassningsalternativ (erbjudanden).

Aktivitetsinstanserna skapas med schema-ID`https://ns.adobe.com/experience/offer-management/offer-activity`. Egenskapen `_instance` för Skapa eller uppdatera-anropet ser ut så här:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Den här obligatoriska egenskapen innehåller aktivitetsnamn. Namnet visas i olika användargränssnitt.
- **`xdm:status`** - Den här egenskapen används för instansens livscykelhantering. Värdet representerar ett arbetsflödestillstånd som används för att indikera om aktiviteten fortfarande är under uppbyggnad (värde = utkast), kan vanligtvis övervägas av körningen (värde = live) eller om den inte ska användas längre (värde = arkiverad).
- **`xdm:placement`** - En obligatorisk egenskap som innehåller en referens till en erbjudandeplacering som tillämpas på lagret när ett beslut fattas i samband med den här aktiviteten. Värdet är URI (`@id`) för den erbjudandeplacering som används.
- **`xdm:filter`** - En obligatorisk egenskap som innehåller en referens till ett erbjudandefilter som tillämpas på lagret när ett beslut fattas i samband med denna aktivitet. Värdet är URI (`@id`) för erbjudandefiltret som används.
- **`xdm:fallback`** - En obligatorisk egenskap som innehåller en referens till ett reserverbjudande. Ett reserverbjudande används när beslut om den här aktiviteten inte kvalificerar något personaliseringserbjudande. Värdet är URI:n (`@id`) för en reservalternativsinstans.

### Hantera reserverbjudanden

Innan aktivitetsinstanser kan skapas måste det finnas ett reserverbjudande som kvalificerar för aktivitetens placering. Reserverbjudandeinstanserna skapas med schema-ID`https://ns.adobe.com/experience/offer-management/fallback-offer`. Egenskapen `_instance` för create eller update-anropet innehåller samma allmänna egenskaper som ett personaliseringserbjudande har, men den kan inte ha några andra begränsningar.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Se [Uppdatera och korrigera instanser](#updating-and-patching-instances) för den fullständiga cURL-syntaxen. Parametern `schemaId` måste vara `https://ns.adobe.com/experience/offer-management/fallback-offer`.

