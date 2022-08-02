---
keywords: Experience Platform;hem;populära ämnen;datasjösekretess;identitetsnamnutrymmen;sekretess;datasjön
solution: Experience Platform
title: Behandling av sekretessförfrågningar i datasjön
topic-legacy: overview
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt juridiska och organisatoriska sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i Data Lake.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: a713245f3228ed36f262fa3c2933d046ec8ee036
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# Behandling av sekretessförfrågningar i [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt juridiska och organisatoriska sekretessbestämmelser.

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i [!DNL Data Lake].

>[!NOTE]
>
>Den här guiden beskriver bara hur du gör sekretessförfrågningar för Data Lake i Experience Platform. Om du även planerar att göra sekretessförfrågningar för datalagret för kundprofiler i realtid, se guiden om [sekretessförfrågningsbehandling för profil](../profile/privacy.md) förutom den här självstudiekursen.
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Service](../privacy-service/experience-cloud-apps.md).

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] innan du läser den här guiden:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [[!DNL Catalog Service]](home.md): Registreringssystemet för dataplatsen och datalinje inom [!DNL Experience Platform]. Tillhandahåller ett API som kan användas för att uppdatera datauppsättningsmetadata.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] överbryggar kundidentitetsdata mellan system och enheter. [!DNL Identity Service] använder identitetsnamnutrymmen för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] I lagras globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform], se [Översikt över namnutrymmet identity](../identity-service/namespaces.md).

## Lägga till identitetsdata i datauppsättningar

När sekretessförfrågningar skapas för [!DNL Data Lake]måste giltiga identitetsvärden (och tillhörande namnutrymmen) anges för varje enskild kund för att kunna hitta deras data och bearbeta dem därefter. Därför måste alla datauppsättningar som omfattas av sekretessförfrågningar innehålla en identitetsbeskrivning i det associerade XDM-schemat.

>[!NOTE]
>
>Datauppsättningar som baseras på scheman som inte stöder metadata för identitetsbeskrivare (t.ex. ad hoc-datauppsättningar) kan för närvarande inte behandlas i sekretessförfrågningar.

I det här avsnittet går vi igenom stegen för att lägga till en identitetsbeskrivare i ett befintligt datamängds XDM-schema. Om du redan har en datauppsättning med en identitetsbeskrivning kan du hoppa fram till [nästa avsnitt](#nested-maps).

>[!IMPORTANT]
>
>När du bestämmer vilka schemafält som ska anges som identiteter bör du tänka på [begränsningar för att använda kapslade mappningsfält](#nested-maps).

Det finns två metoder för att lägga till en identitetsbeskrivning i ett dataset-schema:

* [Använda gränssnittet](#identity-ui)
* [Använda API:et](#identity-api)

### Använda gränssnittet {#identity-ui}

I [!DNL Experience Platform ]användargränssnittet, **[!UICONTROL Schemas]** kan du redigera befintliga XDM-scheman. Om du vill lägga till en identitetsbeskrivning till ett schema väljer du schemat från listan och följer stegen för [ange ett schemafält som identitetsfält](../xdm/tutorials/create-schema-ui.md#identity-field) i [!DNL Schema Editor] självstudiekurs.

När du har angett rätt fält i schemat som identitetsfält kan du fortsätta till nästa avsnitt i [skicka sekretessförfrågningar](#submit).

### Använda API:et {#identity-api}

>[!NOTE]
>
>I det här avsnittet antas du känna till det unika URI-ID-värdet för datauppsättningens XDM-schema. Om du inte känner till det här värdet kan du hämta det med [!DNL Catalog Service] API. När du har läst [komma igång](./api/getting-started.md) i utvecklarhandboken, följ stegen som beskrivs i för [lista](./api/list-objects.md) eller [söka](./api/look-up-object.md) [!DNL Catalog] objekt för att hitta datauppsättningen. Schema-ID:t finns under `schemaRef.id`
>
>I det här avsnittet förutsätts även att du vet hur du anropar API:t för schemaregister. Viktig information om hur du använder API:t finns i `{TENANT_ID}` och konceptet med behållare finns i [komma igång](../xdm/api/getting-started.md) i API-guiden.

Du kan lägga till en identitetsbeskrivning i en datauppsättnings XDM-schema genom att göra en POST-förfrågan i `/descriptors` slutpunkt i [!DNL Schema Registry] API.

**API-format**

```http
POST /descriptors
```

**Begäran**

Följande begäran definierar en identitetsbeskrivning i ett e-postadressfält i ett exempelschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som skapas. För identitetsbeskrivare måste värdet vara &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | Det unika URI-ID:t för datauppsättningens XDM-schema. |
| `xdm:sourceVersion` | Den version av XDM-schemat som anges i `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Sökvägen till schemafältet som beskrivningen tillämpas på. |
| `xdm:namespace` | En av [standardidentitetsnamnutrymmen](../privacy-service/api/appendix.md#standard-namespaces) känns igen av [!DNL Privacy Service]eller ett anpassat namnutrymme som definieras av din organisation. |
| `xdm:property` | Antingen &quot;xdm:id&quot; eller &quot;xdm:code&quot;, beroende på vilket namnutrymme som används under `xdm:namespace`. |
| `xdm:isPrimary` | Ett booleskt värde (tillval). När värdet är true anger detta att fältet är en primär identitet. Scheman får endast innehålla en primär identitet. Standardvärdet är false om det inte inkluderas. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyskapade beskrivningen.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Skicka begäranden {#submit}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du formaterar sekretessförfrågningar för [!DNL Data Lake]. Vi rekommenderar att du granskar [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) eller [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) dokumentation för fullständiga steg om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i begärandenyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för [!DNL Data Lake] med [!DNL Privacy Service] Gränssnitt eller API.

>[!IMPORTANT]
>
>Det går inte att garantera hur lång tid en sekretessbegäran kan ta att slutföra. Om det sker ändringar i datasjön medan en begäran fortfarande bearbetas, kan även dessa poster inte garanteras.

### Använda gränssnittet

När du skapar jobbförfrågningar i användargränssnittet måste du välja **[!UICONTROL AEP Data Lake]** under **[!UICONTROL Products]** för att bearbeta jobb för data som lagras i [!DNL Data Lake].

![Bild som visar den Data Lake-produkt som valts i dialogrutan för att skapa sekretessbegäran](./images/privacy/product-value.png)

### Använda API:et

När jobbförfrågningar skapas i API:t, `userIDs` som tillhandahålls måste använda en specifik `namespace` och `type` beroende på vilket datalager de gäller för. ID för [!DNL Data Lake] måste använda `unregistered` för `type` och `namespace` värde som matchar ett av [sekretessetiketter](#privacy-labels) som har lagts till i tillämpliga datauppsättningar.

Dessutom är `include` arrayen med nyttolasten för begäran måste innehålla produktvärdena för de olika datalager som begäran görs till. När förfrågningar görs till [!DNL Data Lake]måste arrayen innehålla värdet `aepDataLake`.

Följande begäran skapar ett nytt sekretessjobb för [!DNL Data Lake], med hjälp av det oregistrerade `email_label` namnutrymme. Den innehåller också produktvärdet för [!DNL Data Lake] i `include` array:

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

>[!IMPORTANT]
>
>Plattformsprocessernas sekretessförfrågningar för alla [sandlådor](../sandboxes/home.md) som tillhör din organisation. Detta resulterar i att `x-sandbox-name` huvud som ingår i begäran ignoreras av systemet.

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], [!DNL Platform] skickar bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från [!DNL Data Lake] inom sju dagar. Under denna sju-dagars period tas data bort på skärmen och är därför inte tillgängliga för alla [!DNL Platform] service.

I framtida versioner [!DNL Platform] skickar bekräftelsen till [!DNL Privacy Service] efter att data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du introducerat de viktiga begrepp som används för att behandla sekretessförfrågningar för [!DNL Data Lake]. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

Visa dokumentet på [sekretessförfrågningar för kundprofil i realtid](../profile/privacy.md) för steg vid bearbetning av sekretessförfrågningar för [!DNL Profile] butik.

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du hanterar sekretessförfrågningar i [!DNL Data Lake].

### Märka kapslade mappningsfält {#nested-maps}

Det är viktigt att komma ihåg att det finns två typer av kapslade mappningsfält som inte har stöd för sekretessetiketter:

* Ett mappningsfält i ett matristypsfält
* Ett mappningsfält i ett annat mappningsfält

Bearbetning av sekretessjobb för något av de två exemplen ovan kommer så småningom att misslyckas. Därför rekommenderar vi att du undviker att använda kapslade mappningsfält för att lagra privata kunddata. Relevanta konsument-ID:n ska lagras som en annan datatyp än en karta i `identityMap` fält (i sig ett mappningsfält) för postbaserade datamängder, eller `endUserID` för tidsseriebaserade datauppsättningar.
