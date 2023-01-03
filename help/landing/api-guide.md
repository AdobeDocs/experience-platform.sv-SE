---
keywords: Experience Platform;startsida;populära ämnen;Adobe Experience Platform;api guide;platform api guide;introduktion till plattform;utvecklarguide
solution: Experience Platform
title: Komma igång med Adobe Experience Platform API:er
topic-legacy: api guide
description: Adobe Experience Platform tillhandahåller API-tjänster som är nära kopplade till varandra. Den här handboken innehåller information om tillgängliga tjänster, nödvändiga huvuden för CRUD-åtgärder, felmeddelanden, Postman-samlingar och exempel på API-anrop.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Komma igång med Adobe Experience Platform API:er

Adobe Experience Platform utvecklas under en&quot;API first&quot;-filosofi. Med hjälp av plattforms-API:er kan du programmässigt utföra grundläggande CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort) mot data, som att konfigurera beräknade attribut, komma åt data/enheter, exportera data, ta bort onödiga data eller batchar med mera.

API:erna för varje Experience Platform-tjänst har alla samma uppsättning autentiseringsrubriker och använder liknande syntax för sina CRUD-åtgärder. Följande guide beskriver de steg som krävs för att komma igång med plattforms-API:er.

## Autentisering och rubriker

För att kunna ringa anrop till plattformsslutpunkter måste du slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Sandlådehuvud

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till plattforms-API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

- `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i plattformen finns i [översiktsdokumentation för sandlåda](../sandboxes/home.md).

### Rubrik för innehållstyp

Alla förfrågningar med en nyttolast i begärandetexten (t.ex. samtal av typen POST, PUT och PATCH) måste innehålla en `Content-Type` header. Godkända värden är specifika för varje API-slutpunkt. Om en specifik `Content-Type` värdet behövs för en slutpunkt, och dess värde visas i de exempel-API-begäranden som tillhandahålls av [API-guider för enskilda plattformstjänster](#api-guides).

## Grundläggande om Experience Platform API

Adobe Experience Platform API:er använder flera underliggande tekniker och syntaxer som är viktiga att förstå för att effektivt hantera plattformsresurser.

Om du vill veta mer om de underliggande API-teknikerna som används i Platform, inklusive exempel på JSON-schemaobjekt, kan du besöka [Grundläggande om Experience Platform API](api-fundamentals.md) guide.

## Postman-samlingar för Experience Platform API:er

Postman är en samarbetsplattform för API-utveckling som gör att du kan konfigurera miljöer med förinställda variabler, dela API-samlingar, effektivisera CRUD-begäranden och mycket annat. De flesta Platform API-tjänster har Postman-samlingar som kan användas för att göra API-anrop.

Om du vill veta mer om Postman, t.ex. om hur du konfigurerar en miljö, en lista över tillgängliga samlingar och hur du importerar samlingar, går du till [Postman-dokumentation](postman.md).

## Läser exempel-API-anrop {#sample-api}

Format för förfrågningar varierar beroende på vilken plattform-API som används. Det bästa sättet att lära sig att strukturera API-anrop är att följa med exemplen i dokumentationen för den plattformstjänst du använder.

Dokumentationen för [!DNL Experience Platform] visar exempel på API-anrop på två olika sätt. Först presenteras samtalet i **API-format**, en mallrepresentation som endast visar operationen (GET, POST, PUT, PATCH, DELETE) och den slutpunkt som används (till exempel `/global/classes`). Vissa mallar visar också var variablerna finns för att illustrera hur ett anrop ska formuleras, till exempel `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Anropen visas sedan som cURL-kommandon i en **Begäran**, som innehåller nödvändiga rubriker och fullständig &quot;bassökväg&quot; som behövs för att interagera med API:t. Basbanan ska vara förpended för alla slutpunkter. Ovannämnda `/global/classes` slutpunkten blir `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Du kommer att se API-formatet/begäranmönstret i hela dokumentationen och förväntas använda den fullständiga sökvägen som visas i exempelbegäran när du anropar egna API:er för plattformen.

### Exempel på API-begäran

Följande är ett exempel på en API-begäran som visar vilket format du kommer att stöta på i dokumentationen.

**API-format**

API-formatet visar åtgärden (GET) och slutpunkten som används. Variabler anges med klammerparenteser (i det här fallet `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Begäran**

I den här exempelbegäran får variablerna från API-formatet faktiska värden i sökvägen för begäran. Dessutom visas alla obligatoriska rubriker som antingen exempelvärden för rubriker eller variabler där känslig information (t.ex. säkerhetstoken och åtkomst-ID) ska inkluderas.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret visar vad du förväntar dig efter ett lyckat anrop till API:t, baserat på den begäran som skickades. Ibland kortas svaret av för blanksteg, vilket innebär att du kan se mer information eller mer information än den som visas i exemplet.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Felmeddelanden

The [Felsökningsguide för plattformen](troubleshooting.md#errors-and-troubleshooting) innehåller en lista med fel som kan uppstå när du använder en Experience Platform-tjänst.

Felsökningsguider för enskilda plattformstjänster finns i [tjänstfelsökningskatalog](troubleshooting.md#service-troubleshooting-directory).

Mer information om specifika slutpunkter i plattforms-API:er, inklusive obligatoriska rubriker och begärandetexter, finns i [Plattforms-API-guider](#api-guides).

## Plattforms-API-guider {#api-guides}

| API-guide | Beskrivning |
| --- | --- |
| [[!DNL Access Control] API-guide](.././access-control/api/getting-started.md) | The [!DNL Access Control] API-slutpunkten kan hämta aktuella principer som gäller för en användare för angivna resurser inom en angiven sandlåda. Alla andra åtkomstkontrollfunktioner tillhandahålls via [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [API-guide för gruppinmatning](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] Med API kan du importera data till plattformen som gruppfiler. Data som importeras kan vara profildata från en platt fil i ett CRM-system (till exempel en Parquet-fil) eller data som överensstämmer med ett känt schema i schemaregistret (XDM). |
| [[!DNL Catalog Service] API-guide](.././catalog/api/getting-started.md) | The [!DNL Catalog Service] Med API kan utvecklare hantera datauppsättningsmetadata i Adobe Experience Platform. Detta omfattar dataplatser, bearbetningsfaser, fel som inträffade under bearbetningen samt datarapporter. |
| [[!DNL Data Access] API-guide](.././data-access/api.md) | The [!DNL Data Access] Med API kan utvecklare hämta information om inkapslade datauppsättningar i Experience Platform. Detta inkluderar åtkomst och hämtning av datauppsättningsfiler, hämtning av rubrikinformation, listning av misslyckade och slutförda grupper samt hämtning av CSV-/Parquet-filer för förhandsgranskning. |
| [[!DNL Dataset Service] API-guide](.././data-governance/labels/dataset-api.md) | Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata. |
| [[!DNL Identity Service] API-guide](.././identity-service/api/getting-started.md) | The [!DNL Identity Service] Med API kan utvecklare hantera enhetsoberoende, kanalövergripande och i stort sett realtidsidentifiering av kunder med hjälp av identitetsdiagram i Adobe Experience Platform. |
| [[!DNL Observability Insights] API-guide](.././observability/api/overview.md) | [!DNL Observability Insights] är ett RESTful-API som gör att utvecklare kan visa viktiga mätvärden för observerbarhet i Adobe Experience Platform. Dessa mätvärden ger insikter i statistik om plattformsanvändning, hälsokontroller för plattformstjänster, historiska trender och resultatindikatorer för olika plattformsfunktioner. |
| [[!DNL Policy Service] API-guide](.././data-governance/api/overview.md) <br> (Datastyrning) | The [!DNL Policy Service] Med API kan ni skapa och hantera etiketter och principer för dataanvändning för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa etiketter för dataanvändning. Om du vill använda etiketter på datauppsättningar och fält kan du läsa [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) guide |
| [[!DNL Privacy Service] API-guide](.././privacy-service/api/getting-started.md) | The [!DNL Privacy Service] Med API kan utvecklare skapa och hantera kundförfrågningar för att få tillgång till eller ta bort sina personuppgifter mellan olika Experience Cloud-program, i enlighet med gällande sekretessbestämmelser. |
| [[!DNL Query Service] API-guide](.././query-service/api/getting-started.md) | The [!DNL Query Service] Med API kan utvecklare fråga sina Adobe Experience Platform-data med hjälp av standard-SQL. |
| [[!DNL Real-Time Customer Profile] API-guide](.././profile/api/overview.md) | Med Real-Time Customer Profile API kan utvecklare utforska och arbeta med profildata, inklusive visningsprofiler, skapa och uppdatera sammanfogningsprinciper, exportera eller sampla profildata och ta bort profildata som inte längre behövs eller som har lagts till av misstag. |
| [API-guide för sandlådor](.././sandboxes/api/getting-started.md) | Med sandbox-API kan utvecklare programmässigt hantera isolerade virtuella sandlådemiljöer i Adobe Experience Platform. |
| [[!DNL Schema Registry] API-guide](.././xdm/api/overview.md) <br> (XDM) | The [!DNL Schema Registry] Med API kan utvecklare programmässigt hantera alla scheman och relaterade XDM-resurser (Experience Data Model) inom Adobe Experience Platform. |
| [[!DNL Segmentation Service] API-guide](.././segmentation/api/overview.md) | The [!DNL Segmentation Service] Med API kan utvecklare programmässigt hantera segmenteringsåtgärder i Adobe Experience Platform. Detta inkluderar att bygga segment och generera målgrupper från kundprofildata i realtid. |
| [[!DNL Sensei Machine Learning] API-guide](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | The [!DNL Sensei Machine Learning] API har en mekanism för datavetare som organiserar och hanterar maskininlärningstjänster (ML) från algoritmintroduktion, experimenterande och driftsättning. |

Mer information om specifika slutpunkter och åtgärder som är tillgängliga för respektive tjänst finns i [API-referensdokumentation](https://www.adobe.com/go/platform-api-reference-en) på Adobe I/O.

## Nästa steg

I det här dokumentet introducerades nödvändiga rubriker, tillgängliga guider och ett exempel på API-anrop. Nu när du har de rubrikvärden som krävs för att göra API-anrop på Adobe Experience Platform väljer du en API-slutpunkt som du vill utforska från [Tabell för API-guider för plattformen](#api-guides).

Svar på vanliga frågor finns i [Felsökningsguide för plattformen](troubleshooting.md).

Om du vill konfigurera en Postman-miljö och utforska de tillgängliga Postman-samlingarna kan du läsa [Plattformsguide för Postman](postman.md).
