---
keywords: Experience Platform;hem;populära ämnen;datasjösekretess;identitetsnamnutrymmen;sekretess;datasjön
solution: Experience Platform
title: Behandling av sekretessförfrågningar i datasjön
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt juridiska och organisatoriska sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i datasjön.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Behandling av förfrågningar om skydd av privatlivet i datasjön

Adobe Experience Platform [!DNL Privacy Service] bearbetar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av deras personuppgifter enligt juridiska och organisatoriska sekretessbestämmelser.

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i datasjön.

>[!NOTE]
>
>Den här handboken handlar bara om hur man gör förfrågningar om integritet för sjön med data i Experience Platform. Om du även planerar att göra sekretessförfrågningar för datalagret för kundprofiler i realtid, kan du förutom den här självstudiekursen läsa guiden om [bearbetning av sekretessförfrågningar för profilen](../profile/privacy.md).
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Servicens dokumentation](../privacy-service/experience-cloud-apps.md).

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform]-tjänster innan du läser den här handboken:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av deras personuppgifter mellan Adobe Experience Cloud-program.
* [[!DNL Catalog Service]](home.md): Postsystemet för dataplats och datalinje inom [!DNL Experience Platform]. Tillhandahåller ett API som kan användas för att uppdatera datauppsättningsmetadata.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan enheter och system.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] förenar data för kundidentitet mellan system och enheter. [!DNL Identity Service] använder identitetsnamnutrymmen för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] underhåller ett lager med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform] finns i [översikten över identitetsnamnrymden](../identity-service/features/namespaces.md).

## Lägga till identitetsdata i datauppsättningar

När du skapar sekretessförfrågningar för datasjön måste giltiga identitetsvärden (och tillhörande namnutrymmen) anges för varje enskild kund för att deras data ska kunna hittas och bearbetas därefter. Därför måste alla datauppsättningar som omfattas av sekretessförfrågningar innehålla en identitetsbeskrivning i det associerade XDM-schemat.

>[!NOTE]
>
>Datauppsättningar som baseras på scheman som inte stöder metadata för identitetsbeskrivare (t.ex. ad hoc-datauppsättningar) kan för närvarande inte behandlas i sekretessförfrågningar.

I det här avsnittet går vi igenom stegen för att lägga till en identitetsbeskrivare i ett befintligt datamängds XDM-schema. Om du redan har en datauppsättning med en identitetsbeskrivning kan du hoppa fram till [nästa avsnitt](#nested-maps).

>[!IMPORTANT]
>
>När du bestämmer vilka schemafält som ska anges som identiteter bör du tänka på [begränsningarna med att använda kapslade mappningsfält](#nested-maps).

Det finns två metoder för att lägga till en identitetsbeskrivning i ett dataset-schema:

* [Använda gränssnittet](#identity-ui)
* [Använda API:et](#identity-api)

### Använda gränssnittet {#identity-ui}

I [!DNL Experience Platform]användargränssnittet kan du redigera befintliga XDM-scheman med arbetsytan i **[!UICONTROL Schemas]**. Om du vill lägga till en identitetsbeskrivning till ett schema väljer du schemat från listan och följer stegen för [att ange ett schemafält som ett identitetsfält](../xdm/tutorials/create-schema-ui.md#identity-field) i självstudiekursen [!DNL Schema Editor].

När du har angett rätt fält i schemat som identitetsfält kan du fortsätta till nästa avsnitt om [att skicka sekretessförfrågningar](#submit).

### Använda API:et {#identity-api}

>[!NOTE]
>
>I det här avsnittet antas du känna till det unika URI-ID-värdet för datauppsättningens XDM-schema. Om du inte känner till det här värdet kan du hämta det med API:t [!DNL Catalog Service]. När du har läst avsnittet [getting started](./api/getting-started.md) i utvecklarhandboken följer du stegen som beskrivs i för [listning](./api/list-objects.md) eller [sökning](./api/look-up-object.md) [!DNL Catalog] -objekt för att hitta din datauppsättning. Schemats-ID finns under `schemaRef.id`
>
>I det här avsnittet förutsätts även att du vet hur du anropar API:t för schemaregister. Viktig information om hur du använder API:t, inklusive hur du känner till `{TENANT_ID}` och konceptet med behållare, finns i avsnittet [Komma igång](../xdm/api/getting-started.md) i API-handboken.

Du kan lägga till en identitetsbeskrivning i en datamängds XDM-schema genom att göra en POST-förfrågan till `/descriptors`-slutpunkten i [!DNL Schema Registry] API.

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
| `xdm:sourceSchema` | Unikt URI-ID för datauppsättningens XDM-schema. |
| `xdm:sourceVersion` | Den version av XDM-schemat som har angetts i `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Sökvägen till det schemafält som beskrivningen tillämpas på. |
| `xdm:namespace` | Ett av [standardnamnutrymmena för identiteter](../privacy-service/api/appendix.md#standard-namespaces) som känns igen av [!DNL Privacy Service], eller ett anpassat namnutrymme som definieras av din organisation. |
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
>I det här avsnittet beskrivs hur du formaterar sekretessförfrågningar för datasjön. Vi rekommenderar att du läser dokumentationen för [[!DNL Privacy Service] användargränssnittet](../privacy-service/ui/overview.md) eller [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) för att få information om hur du skickar ett sekretessjobb, inklusive hur du formaterar inskickade användaridentitetsdata i nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för datasjön med hjälp av användargränssnittet eller API:t [!DNL Privacy Service].

>[!IMPORTANT]
>
>Det går inte att garantera hur lång tid en sekretessbegäran kan ta att slutföra. Om det sker ändringar i datasjön medan en begäran fortfarande bearbetas, kan även dessa poster inte garanteras.

### Använda gränssnittet

När du skapar jobbbegäranden i användargränssnittet måste du markera **[!UICONTROL AEP Data Lake]** under **[!UICONTROL Products]** för att kunna bearbeta jobb för data som lagras i datasjön.

![Bild som visar den Data Lake-produkt som valts i dialogrutan för att skapa sekretessbegäran](./images/privacy/product-value.png)

### Använda API:et

När du skapar jobbförfrågningar i API:t måste alla `userIDs` som anges använda en specifik `namespace` och `type` beroende på vilket datalager de gäller för. ID:n för datasjön måste använda `unregistered` för sitt `type`-värde och ett `namespace`-värde som matchar en av de [sekretessetiketter](#privacy-labels) som har lagts till i tillämpliga datamängder.

Dessutom måste matrisen `include` för nyttolasten för begäran innehålla produktvärden för de olika datalager som begäran görs till. När du gör förfrågningar till datasjön måste matrisen innehålla värdet `aepDataLake`.

Följande begäran skapar ett nytt sekretessjobb för datasjön med det oregistrerade namnområdet `email_label`. Den innehåller också produktvärdet för datasjön i arrayen `include`:

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
>Plattformen behandlar sekretessförfrågningar i alla [sandlådor](../sandboxes/home.md) som tillhör din organisation. Därför ignoreras alla `x-sandbox-name`-huvuden som ingår i begäran av systemet.

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Registren tas sedan bort från sjön inom sju dagar. Under det sju dagar långa fönstret tas data bort utan att vara tillgängliga för någon [!DNL Platform]-tjänst.

Om du även inkluderade `ProfileService` eller `identity` i sekretessbegäran hanteras deras associerade data separat. Mer information finns i avsnittet [Ta bort begärandebearbetning för profilen](../profile/privacy.md#delete).

## Nästa steg

Genom att läsa det här dokumentet har du lagts till i de viktiga koncept som rör behandling av sekretessförfrågningar för datasjön. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

I dokumentet om [behandling av sekretessförfrågningar för kundprofil i realtid](../profile/privacy.md) finns anvisningar om hur du hanterar sekretessförfrågningar för butiken [!DNL Profile].

## Bilaga

Följande avsnitt innehåller ytterligare information för att behandla sekretessförfrågningar i datasjön.

### Märka kapslade mappningsfält {#nested-maps}

Det är viktigt att komma ihåg att det finns två typer av kapslade mappningsfält som inte har stöd för sekretessetiketter:

* Ett mappningsfält i ett matristypsfält
* Ett mappningsfält i ett annat mappningsfält

Bearbetning av sekretessjobb för något av de två exemplen ovan kommer så småningom att misslyckas. Därför rekommenderar vi att du undviker att använda kapslade mappningsfält för att lagra privata kunddata. Relevanta konsument-ID:n ska lagras som en datatyp som inte är mappad i fältet `identityMap` (i sig ett mappningsfält) för postbaserade datamängder, eller i fältet `endUserID` för tidsseriebaserade datamängder.
