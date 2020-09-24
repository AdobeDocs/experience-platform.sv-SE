---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Arbeta med körningsmiljön för beslutstjänsten med API:er
topic: tutorial
type: Tutorial
description: 'I det här dokumentet finns en självstudiekurs om hur du arbetar med körtidstjänsterna i beslutstjänsten med Adobe Experience Platform API:er. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---


# Arbeta med körningsmiljön för beslutstjänsten med API:er

Det här dokumentet innehåller en självstudiekurs om hur du arbetar med runtime-tjänster för att [!DNL Decisioning Service] använda Adobe Experience Platform API:er.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de tjänster som är inblandade i att fatta beslut och fastställa nästa bästa erbjudande som ska presenteras under kundupplevelserna. [!DNL Experience Platform] Innan du börjar med den här självstudiekursen bör du läsa i dokumentationen om följande:

- [[!DNL Decision Service]](./../home.md): Innehåller ett ramverk för att lägga till och ta bort erbjudanden och skapa algoritmer för att välja det bästa som ska visas under en kunds upplevelse.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
- [[!DNL Profile Query Language (PQL)]](../../segmentation/pql/overview.md): PQL används för att definiera regler och filter.
- [Hantera beslutsobjekt och regler med API:er](./entities.md): Innan du använder körningsmiljön för beslutstjänster måste du konfigurera de relaterade entiteterna.

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
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../tutorials/authentication.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Krävs också för körningsbegäranden:

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID` är en sträng i UUID-format som är globalt unik och inte får återanvändas för olika API-anrop

[!DNL Decisioning Service] styrs av ett antal affärsobjekt som är relaterade till varandra. Alla affärsobjekt lagras i [!DNL Platform’s] affärsobjektarkivet, XDM Core Object Repository. En viktig funktion i den här databasen är att API:erna är ortogonala till typen av affärsobjekt. I stället för att använda API:t POST, GET, PUT, PATCH eller DELETE som anger resurstypen i dess API-slutpunkt, finns det bara 6 generiska slutpunkter, men de accepterar eller returnerar en parameter som anger objekttypen när det behöver det. Schemat måste registreras med databasen, men utöver det kan databasen användas för en öppen uppsättning objekttyper.

Slutpunktssökvägarna för alla XDM Core Object Repository API:er börjar med `https://platform.adobe.io/data/core/ode/`.

Det första banelementet efter slutpunkten är `containerId`. Den här identifieraren hämtas via XDM Core Object Repository-rotslutpunkten `GET https://platform.adobe.io/data/core/xcore/`.

## Sammanställning av beslutsmodeller

Aktiveringen av logiska enheter sker automatiskt och kontinuerligt. Så snart ett nytt alternativ sparas i databasen och markeras som godkänt, kan det ingå i uppsättningen med tillgängliga alternativ. Så snart en beslutsregel har uppdaterats kommer regeluppsättningen att återskapas och förberedas för körning. I det här automatiska aktiveringssteget utvärderas eventuella begränsningar som definieras av affärslogiken som inte är beroende av körningssammanhanget. Resultatet av det här aktiveringssteget skickas till en cache där de är tillgängliga för [!DNL Decisioning Service] körningsmiljön.

### Effekter av placeringar, filter och livscykeltillstånd

Erbjudandena skapas kontinuerligt, ändras under deras livscykelstatus eller så kan nya innehållsrepresentationer hämtas. En aktivitets erbjudandefilter kan ändras eller matcha eller filtrera bort erbjudanden vars tagguppsättningar har uppdaterats. Den här processen kan vara ganska involverad och program och tjänster måste veta vad den resulterande uppsättningen av kandidater för en aktivitet kommer att vara. Beslutsmiljön innehåller ett API som filtrerar bort erbjudanden som inte är godkända, som inte matchar erbjudandefiltret eller som inte har någon representation för den placering som aktiviteten refererar till.

**Begäran**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Svar**

Parametern `activityId` kan upprepas i url och upp till 30 olika aktivitetsreferenser kan ges i en begäran. Svaret är användbart för att upptäcka eventuella oväntade omständigheter som kan uppstå vid installationen och ser ut så här:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Det finns en liten fördröjning på några sekunder mellan den tidpunkt då objekten uppdaterades och den tidpunkt då API-svaret reflekterar mappningen från aktivitet till erbjudande. Revideringen av varje objekt anges i svaret så att klienterna kan kontrollera om det finns en uppdatering av objekten som inte har speglats.

### Diagnostik-API och felsökning

Regler för aktiviteter, erbjudanden och berättiganden kompileras till ett internt format (katalog för körningserbjudanden) som används av beslutstjänstens körningsmiljö. Kompileringen kan upptäcka fel som inte fångats upp av de kontroller som utfördes när objekten lagrades och länkar upprättades i XDM Core Object Repository.

En diagnostik-API tillhandahålls för att hämta kompileringsfel som inträffade i det steget och om det inte finns några fel som kan få information om när reglerna och aktiviteterna senast kompilerades om.

**Begäran**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

Den enda parametern för detta API-anrop är `containerId`. Resultatet av alla uppdateringar från alla klienter som har ändrat beslutsregler, erbjudanden, aktiviteter eller erbjudandefilter i den behållaren. Det finns en liten fördröjning på några sekunder mellan den tidpunkt då objekten uppdaterades och den tidpunkt då kompileringen slutfördes. Den senaste uppdateringstidsstämpeln och eventuella fel returneras som svar på diagnostikanropet.

**Svar**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## REST API-anrop för att köra beslut

REST API är en av vägarna för program som körs ovanpå [!DNL Platform] för att få nästa bästa upplevelse baserat på de regler, modeller och begränsningar som organisationen har ställt in för sina användare. Program skickar en av profilens identiteter (profil-ID och identitetsnamnutrymme) som [!DNL Decisioning Service] söker upp profilen och informationen används för att tillämpa affärslogiken. Ytterligare kontextdata kan skickas till begäran och om de anges i affärsreglerna inkluderas de data som behövs för att fatta beslutet.

Applikationer kan uppnå bättre prestanda genom att begära ett beslut om upp till 30 aktiviteter samtidigt. URI:erna för aktiviteterna skickas i samma begäran. REST API är synkront och returnerar de föreslagna alternativen för alla dessa aktiviteter eller reservalternativet om inget personaliseringsalternativ uppfyller begränsningarna.

Det är möjligt att två olika aktiviteter har samma alternativ som&quot;bäst&quot;. För att undvika att en sammansatt upplevelse upprepas, används som standard [!DNL Decisioning Service] godtyckliga hastigheter mellan de aktiviteter som refereras i samma begäran. Skiljedomsförfarande innebär att för var och en av verksamheterna övervägs deras främsta alternativ, men inget alternativ kommer att föreslås mer än en gång för dessa verksamheter. Om två aktiviteter har samma topprankade alternativ kommer en av dem att väljas till att använda sitt näst bästa val eller tredje bästa och så vidare. Dessa regler för borttagning av dubbletter försöker undvika att någon av aktiviteterna måste använda sitt reservalternativ.

Beslutsbegäran innehåller de argument som ingår i en begäran om POST. Brödtexten är formaterad som JSON- `Content-Type` rubrikvärde `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

Det begärda schemat och den version som stöds för tillfället är `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. I framtiden kommer ytterligare efterfråganscheman eller versioner att tillhandahållas.

**Begäran**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - När värdet för den här valfria egenskapen har värdet true kommer beslutsbegäran att följa begränsningen, men inte rita ned räknarna, är det en förväntan att anroparen aldrig tänker presentera förslaget för profilen. Det [!DNL Decisioning Service] registreras inte som en officiell XDM-beslutshändelse och visas inte i rapporteringsdatauppsättningar. Standardvärdet för denna egenskap är false och när egenskapen utelämnas betraktas inte beslutet som en testkörning och ska därför presenteras för slutanvändaren.
- **`xdm:validateContextData`** - Den här valfria egenskapen aktiverar eller inaktiverar validering av kontextdata. Om valideringen är aktiverad hämtas schemat (baserat på `@type` fältet) från XDM-registret för varje angivet kontextdataobjekt och objektet valideras mot det `xdm:data` .

Begäran enligt det här schemat innehåller en matris med URI:er som refererar till erbjudandeaktiviteter, en profilidentitet och en matris med kontextdataobjekt:

- **`xdm:offerActivities`** - Den här obligatoriska egenskapen är en array med objekt där varje objekt innehåller data om erbjudandeaktiviteten. Erbjudandeaktiviteten har följande egenskaper:
   - **`xdm:offerActivity`** - Aktivitetens unika identifierare (URI). Detta är värdet på `@id` egenskapen för erbjudandeaktiviteten.
- **`xdm:identityMap`** - En obligatorisk egenskap som innehåller ett JSON-objekt som uppfyller XDM-schemat `https://ns.adobe.com/xdm/context/identitymap`. Egenskapen definierar en karta där nyckeln är en ID-namnutrymmeskod och värdet är en lista med slutanvändaridentifierare i det angivna namnutrymmet. Om jag.
- **`xdm:contextData`** - En valfri egenskap som innehåller objekt som beskrivs av en referens till deras schema. Varje kontextdataobjekt i arrayen måste ha följande egenskaper:
   - **`@type`** - En obligatorisk egenskap som refererar till objektets XDM-schema i det här objektet.
   - **`xdm:data`** - En obligatorisk egenskap som innehåller objektegenskaperna enligt XDM-schemat som anges i `@type` egenskapen.

## Dynamiska kontextdata vid beslutsbegäranden

I föregående avsnitt anges hur XDM-objekt kan skickas till en beslutsbegäran. Följande är ett exempel på en sådan kontextobjektarray:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Schemat måste ha konstruerats av din organisation. Mer information om hur du skapar scheman finns i [Schemaredigerarens självstudiekurs](../../xdm/tutorials/create-schema-ui.md). Schemat kommer att finnas i ett namnområde `https://ns.adobe.com/{TENANT_ID}/schemas`.

Utvecklarhandboken för [schemaregister-API:t för](../../xdm/tutorials/create-schema-api.md) scheman förklarar hur scheman kan nås programmatiskt och hur en utvecklare får tag på klientens ID och den numeriska identifieraren för ditt schema. Versionsnumret krävs och anges även av API:erna för schemaregister.

Ett schema som definieras av en organisation har vanligtvis en rotegenskap med namnet `_{TENANT_ID}`, som också kallas för innehavarens namnområdessträng.
Observera att egenskaperna som används från en global schemakomponent som _`https://ns.adobe.com/xdm/context/product` har ett namnområdesprefix `xdm:`. I det här fallet `productDetails` konstruerades den organisationsdefinierade egenskapen med den datatypen. Klientegenskaper kapslas i en egenskap som heter efter innehavarens namnutrymme, medan datatyper som är globalt tillgängliga använder det reserverade prefixet `xdm:` för att förhindra kollisioner med egenskapsnamn.

Flera dataobjekt kan listas i `xdm:contextData` egenskapen. Varje objekt måste identifiera sin typ via egenskapen `@type` .
Värdena för kontextdataobjekten är tillgängliga och kan användas i PQL-uttryck, till exempel i villkoret för en berättiganderegel. Kontextdataobjektet måste adresseras via det särskilda sökvägsreferensuttrycket `@{schemaId}`. Uttrycken som följer det här referensuttrycket är reguljära sökvägsuttryck som kommer åt dataobjektets egenskaper:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

I exemplet ovan `p` itererar variabeln över arrayen med objekt som markerats med `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Observera att PQL-syntaxen inte använder prefix i egenskapsnamn. Som standard refereras globala egenskaper bara utan `xdm:` prefixet. Egenskaper som din organisation definierar är kapslade i en **extra** egenskap som heter efter innehavarens namnutrymme (i det exempel som anges av variabeln `{TENANT_ID}`). Om du vill kunna referera till de anpassade egenskaperna direkt `p` är variabeln bunden till resultatet av sökvägen som avrefererar till den extra kapslingsegenskapen.

## Användning av profilposter

Alla poster för profil- och upplevelsehändelseentiteter hanteras redan i profilarkivet. Genom att skicka en eller flera profilidentiteter till begäran identifieras och slås profilen upp från butiken. Data blir sedan automatiskt tillgängliga för beslutsregler och -modeller som utvärderas av beslutsstrategin.

Om du vill hämta profil- och upplevelseposter används standardprincipen för sammanfogning.
Observera, att när du har överfört profilposter till [!DNL Platform] datalagret sker en viss fördröjning tills profilposterna kan slås upp. Detsamma gäller för inhämtning av profil- och upplevelseposter via API:erna för direktuppspelning, bara efter några sekunder kommer data att vara tillgängliga för utvärdering av beslutsregler som utvärderar profil- och upplevelsehändelsedata.