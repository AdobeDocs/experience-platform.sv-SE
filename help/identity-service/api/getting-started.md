---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Komma igång
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Utvecklarhandbok för Identity Service API

Adobe Experience Platform Identity Service hanterar identifieringen av era kunder i realtid över olika enheter, kanaler och nära nog alla kanaler i det som kallas identitetsdiagram inom Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Identitetstjänst](../home.md): Lös den grundläggande utmaning som fragmenteringen av kundprofildata innebär. Det gör man genom att överbrygga identiteter mellan enheter och system där kunderna interagerar med ert varumärke.
- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa API:t för identitetstjänsten.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

### Regionbaserad routning

Identitetstjänstens API använder regionspecifika slutpunkter som kräver att en del `{REGION}` ingår i sökvägen för begäran. Under etableringen av din IMS-organisation bestäms en region och lagras i din IMS-organisationsprofil. Genom att använda rätt region för varje slutpunkt ser du till att alla begäranden som görs med hjälp av API:t för identitetstjänsten dirigeras till rätt region.

Det finns för närvarande två regioner som stöds av API:er för identitetstjänsten: VA7 och NLD2.

Tabellen nedan visar exempelsökvägar som använder regioner:

| Tjänst | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| Identitetstjänstens API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API för identitetsnamnområde | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Begäranden som görs utan att ange en region kan leda till att anrop dirigeras till fel region eller orsaka att anrop misslyckas oväntat.

Om du inte kan hitta regionen i din IMS-organisationsprofil kontaktar du systemadministratören för att få hjälp.

## Använda Identity Service API

Identitetsparametrar som används i dessa tjänster kan uttryckas på ett av två sätt. sammansatt eller XID.

Sammansatta identiteter är konstruktioner som innehåller både ID-värdet och namnutrymmet. När du använder sammansatta identiteter kan namnutrymmet anges med antingen namn (`namespace.code`) eller ID (`namespace.id`).

När en identitet är beständig genererar och tilldelar identitetstjänsten ett ID till den identiteten, som kallas ursprungligt ID eller XID. Alla variationer av kluster- och mappnings-API:er har stöd för både sammansatta identiteter och XID i sina begäranden och svar. En av parametrarna krävs - `xid` eller en kombination av [`ns` eller `nsid`] och `id` för att använda dessa API:er.

För att begränsa nyttolasten i svaren anpassar API:erna sina svar till den typ av identitetskonstruktion som används. Det vill säga, om du skickar XID:n kommer svaren att ha XID:n, och om du skickar sammansatta identiteter kommer svaret att följa den struktur som används i begäran.

Exemplen i det här dokumentet omfattar inte den fullständiga funktionaliteten för API:t för identitetstjänsten. Den fullständiga API:n finns i [Swagger API Reference](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE] Alla returnerade identiteter kommer att ha ett ursprungligt XID-format när ett ursprungligt XID används i begäran. Vi rekommenderar att du använder ID-/namnutrymmesformuläret. Mer information finns i avsnittet [Hämta XID för en identitet](./create-custom-namespace.md).

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna **API-formatet**, en **exempelbegäran** med obligatoriska huvuden och korrekt formaterade nyttolaster samt ett **exempelsvar** för ett lyckat anrop.
