---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---


# Behandling av sekretessförfrågningar i [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt juridiska och organisatoriska sekretessbestämmelser.

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kunddata som lagras i [!DNL Data Lake].

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] tjänster innan du läser den här handboken:

* [!DNL Privacy Service](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [!DNL Catalog Service](home.md): Registreringssystemet för dataplatsen och datalinje inom [!DNL Experience Platform]. Tillhandahåller ett API som kan användas för att uppdatera datauppsättningsmetadata.
* [!DNL Experience Data Model (XDM) System](../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [!DNL Identity Service](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] överbryggar kundens identitetsdata mellan system och enheter. [!DNL Identity Service] använder för **[!UICONTROL identity namespaces]** att ge sammanhang till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-ID (&quot;TNTID&quot;).

[!DNL Identity Service] I lagras globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om namnutrymmen för identiteter i [!DNL Experience Platform]finns i [översikten över](../identity-service/namespaces.md)namnutrymmen för identiteter.

## Lägga till identitetsdata i datauppsättningar

När du skapar sekretessförfrågningar för [!DNL Data Lake]måste giltiga identitetsvärden (och tillhörande namnutrymmen) anges för varje enskild kund för att deras data ska kunna hittas och bearbetas därefter. Därför måste alla datauppsättningar som omfattas av sekretessförfrågningar innehålla en **[!UICONTROL identity descriptor]** i deras associerade XDM-schema.

>[!NOTE]
>
>Datauppsättningar som baseras på scheman som inte stöder metadata för identitetsbeskrivare (t.ex. ad hoc-datauppsättningar) kan för närvarande inte behandlas i sekretessförfrågningar.

I det här avsnittet går vi igenom stegen för att lägga till en identitetsbeskrivare i ett befintligt datamängds XDM-schema. Om du redan har en datauppsättning med en identitetsbeskrivning kan du hoppa till [nästa avsnitt](#nested-maps).

>[!IMPORTANT]
>
>När du bestämmer vilka schemafält som ska anges som identiteter bör du tänka på [begränsningarna med att använda kapslade mappningsfält](#nested-maps).

Det finns två metoder för att lägga till en identitetsbeskrivning i ett dataset-schema:

* [Använda gränssnittet](#identity-ui)
* [Använda API](#identity-api)

### Använda gränssnittet {#identity-ui}

I [!DNL Experience Platform ]användargränssnittet kan du redigera befintliga XDM-scheman på _[!UICONTROL Schemas]_arbetsytan. Om du vill lägga till en identitetsbeskrivning till ett schema väljer du schemat i listan och följer stegen för att[ange ett schemafält som ett identitetsfält](../xdm/tutorials/create-schema-ui.md#identity-field)i[!DNL Schema Editor]självstudiekursen.

När du har angett rätt fält i schemat som identitetsfält kan du gå vidare till nästa avsnitt om [att skicka sekretessförfrågningar](#submit).

### Använda API {#identity-api}

>[!NOTE]
>
>I det här avsnittet antas du känna till det unika URI-ID-värdet för datauppsättningens XDM-schema. Om du inte känner till det här värdet kan du hämta det med API:t [!DNL Catalog Service] . När du har läst avsnittet [Komma igång](./api/getting-started.md) i utvecklarhandboken följer du de steg som beskrivs i för att [lista](./api/list-objects.md) eller [söka](./api/look-up-object.md) efter [!DNL Catalog] objekt för att hitta datauppsättningen. Schema-ID:t finns under `schemaRef.id`
>
> Det här avsnittet innehåller anrop till API:t för schemaregistret. Viktig information om hur du använder API:t, inklusive hur du känner till ditt innehåll `{TENANT_ID}` och konceptet med behållare, finns i avsnittet [Komma igång](../xdm/api/getting-started.md) i utvecklarhandboken.

Du kan lägga till en identitetsbeskrivning i en datamängds XDM-schema genom att göra en POST-förfrågan till `/descriptors` slutpunkten i [!DNL Schema Registry] API:t.

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
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
| `xdm:namespace` | Ett av de [standardnamnutrymmen](../privacy-service/api/appendix.md#standard-namespaces) för identiteter som känns igen av [!DNL Privacy Service]eller ett anpassat namnutrymme som definieras av din organisation. |
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
>I det här avsnittet beskrivs hur du formaterar sekretessförfrågningar för [!DNL Data Lake]. Vi rekommenderar att du läser igenom [!DNL Privacy Service UI](../privacy-service/ui/overview.md) - eller [!DNL Privacy Service API](../privacy-service/api/getting-started.md) -dokumentationen för att få information om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för [!DNL Data Lake] med hjälp av [!DNL Privacy Service] gränssnittet eller API:t.

### Använda gränssnittet

När du skapar jobbbegäranden i användargränssnittet måste du markera **[!UICONTROL AEP Data Lake]** och/eller **[!UICONTROL Profile]** under _[!UICONTROL Products]_för att kunna bearbeta jobb för data som lagras i[!DNL Data Lake]respektive[!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

### Använda API

När du skapar jobbförfrågningar i API:t måste alla `userIDs` som anges använda ett specifikt `namespace` och `type` beroende på vilket datalager de gäller för. ID:n för [!DNL Data Lake] måste använda&quot;oregistrerad&quot; för sitt `type` värde, och ett `namespace` värde som matchar en av de [sekretessetiketter](#privacy-labels) som har lagts till i tillämpliga datauppsättningar.

Dessutom måste arrayen för den begärda nyttolasten innehålla produktvärdena för de olika datalager som begäran görs till. `include` När du gör förfrågningar till [!DNL Data Lake]måste arrayen innehålla värdet `aepDataLake`.

Följande begäran skapar ett nytt sekretessjobb för [!DNL Data Lake]med namnutrymmet&quot;email_label&quot; som inte är registrerat. Den innehåller också produktvärdet för [!DNL Data Lake] i `include` arrayen:

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

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service]skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från [!DNL Data Lake] inom sju dagar. Under denna sjudagarsperiod tas data bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform] tjänst.

I framtida versioner [!DNL Platform] skickas en bekräftelse till [!DNL Privacy Service] när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till i de viktiga begrepp som används för att behandla sekretessförfrågningar för [!DNL Data Lake]. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

I dokumentet om behandling av [sekretessförfrågningar för kundprofil](../profile/privacy.md) i realtid finns information om hur du hanterar sekretessförfrågningar för [!DNL Profile] butiken.

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du hanterar sekretessförfrågningar i [!DNL Data Lake].

### Märka kapslade mappningsfält {#nested-maps}

Det är viktigt att komma ihåg att det finns två typer av kapslade mappningsfält som inte har stöd för sekretessetiketter:

* Ett mappningsfält i ett matristypsfält
* Ett mappningsfält i ett annat mappningsfält

Bearbetning av sekretessjobb för något av de två exemplen ovan kommer så småningom att misslyckas. Därför rekommenderar vi att du undviker att använda kapslade mappningsfält för att lagra privata kunddata. Relevanta konsument-ID:n ska lagras som en icke-mappad datatyp i `identityMap` fältet (i sig ett mappningsfält) för postbaserade datauppsättningar, eller i `endUserID` fältet för tidsseriebaserade datauppsättningar.