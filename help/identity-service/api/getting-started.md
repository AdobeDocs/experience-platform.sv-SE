---
keywords: Experience Platform;home;populära topics;identity service api;identity service developguide;region
solution: Experience Platform
title: API-guide för identitetstjänst
description: Med Identity Service API kan utvecklare hantera identifieringen av era kunder i realtid över olika enheter, kanaler och nära nog alla kanaler med hjälp av identitetsdiagram i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 2%

---

# API-guide för [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] hanterar identifieringen av dina kunder över olika enheter, i flera kanaler och i realtid i det som kallas identitetsdiagram inom Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Lös den grundläggande utmaning som fragmenteringen av kundprofildata innebär. Det gör man genom att överbrygga identiteter mellan enheter och system där kunderna interagerar med ert varumärke.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa API:t [!DNL Identity Service].

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

- Content-Type: application/json

### Regionbaserad routning

API:t [!DNL Identity Service] använder regionspecifika slutpunkter som kräver att `{REGION}` inkluderas som en del av begäranssökvägen. Under etableringen av organisationen bestäms en region och lagras i din organisationsprofil. Genom att använda rätt region för varje slutpunkt ser du till att alla begäranden som görs med API:t [!DNL Identity Service] dirigeras till rätt region.

Det finns för närvarande två regioner som stöds av [!DNL Identity Service] API:er: VA7 och NLD2.

Tabellen nedan visar exempelsökvägar som använder regioner:

| Tjänst | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Begäranden som görs utan att ange en region kan leda till att anrop dirigeras till fel region eller orsaka att anrop misslyckas oväntat.

Om du inte kan hitta regionen i din organisationsprofil kontaktar du systemadministratören för att få hjälp.

## Använda API:t [!DNL Identity Service]

Identitetsparametrar som används i dessa tjänster kan uttryckas på ett av två sätt: sammansatt eller XID.

Sammansatta identiteter är konstruktioner som innehåller både ID-värdet och namnutrymmet. När du använder sammansatta identiteter kan namnutrymmet anges med antingen namn (`namespace.code`) eller ID (`namespace.id`).

När en identitet bevaras genererar och tilldelar [!DNL Identity Service] ett ID till den identiteten, som kallas ursprungligt ID eller XID. Alla variationer av kluster- och mappnings-API:er har stöd för både sammansatta identiteter och XID i sina begäranden och svar. En av parametrarna krävs - `xid` eller en kombination av [`ns` eller `nsid`] och `id` - för att använda dessa API:er.

För att begränsa nyttolasten i svaren anpassar API:erna sina svar till den typ av identitetskonstruktion som används. Det vill säga, om du skickar XID:n kommer svaren att ha XID:n, och om du skickar sammansatta identiteter kommer svaret att följa den struktur som används i begäran.

Exemplen i det här dokumentet täcker inte den fullständiga funktionen för API:t [!DNL Identity Service]. Fullständigt API finns i [API-referens för Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alla returnerade identiteter kommer att ha ett ursprungligt XID-format när ett ursprungligt XID används i begäran. Vi rekommenderar att du använder ID-/namnutrymmesformuläret. Mer information finns i avsnittet [Hämta XID för en identitet](./create-custom-namespace.md).

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran som visar nödvändiga huvuden och korrekt formaterade nyttolaster samt ett exempelsvar för ett lyckat anrop.
