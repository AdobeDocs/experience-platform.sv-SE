---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---


# Behandling av sekretessförfrågningar i [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för [!DNL Real-time Customer Profile].

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] tjänster innan du läser den här handboken:

* [[!DNL Privacy Service]](home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] förenar data om kundidentitet mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om namnutrymmen för identiteter i [!DNL Experience Platform]finns i [översikten över](../identity-service/namespaces.md)namnutrymmen för identiteter.

## Skicka begäranden {#submit}

Avsnitten nedan beskriver hur du gör sekretessförfrågningar för [!DNL Real-time Customer Profile] användning av [!DNL Privacy Service] API eller gränssnitt. Innan du läser dessa avsnitt rekommenderar vi att du granskar [Privacy Service-API:t](../privacy-service/api/getting-started.md) eller gränssnittsdokumentationen för [Privacy Service](../privacy-service/ui/overview.md) för att få instruktioner om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i begärda nyttolaster.

>[!IMPORTANT]
>
>Privacy Servicen kan bara bearbeta [!DNL Profile] data med en sammanfogningsprincip som inte utför identitetssammanfogning. Om du använder användargränssnittet för att bekräfta om dina sekretessförfrågningar behandlas kontrollerar du att du använder en policy med&quot;[!DNL None]&quot; som [!UICONTROL ID stitching] typ. Du kan alltså inte använda en sammanfogningsprincip där [!UICONTROL ID stitching] är inställd på &quot;[!UICONTROL Private graph]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Det är också viktigt att notera att det inte går att garantera hur lång tid en sekretessbegäran kan ta att slutföra. Om ändringar sker i dina [!DNL Profile] data medan en begäran fortfarande bearbetas, kan även dessa poster inte garanteras.

### Använda API

När du skapar jobbförfrågningar i API:t måste alla ID:n som anges i `userIDs` använda ett specifikt `namespace` och `type`. Ett giltigt [ID-namnutrymme](#namespaces) som känns igen av [!DNL Identity Service] måste anges för `namespace` -värdet, medan `type` måste vara antingen `standard` eller `unregistered` (för standardnamnutrymmen respektive anpassade namnutrymmen).

>[!NOTE]
>
>Du kan behöva ange mer än ett ID för varje kund, beroende på identitetsdiagrammet och hur dina profilfragment distribueras i plattformsdatauppsättningar. Mer information finns i nästa [avsnittsprofilfragment](#fragments) .

Dessutom måste arrayen för den begärda nyttolasten innehålla produktvärdena för de olika datalager som begäran görs till. `include` När du gör förfrågningar till [!DNL Data Lake]måste arrayen innehålla värdet &quot;ProfileService&quot;.

Följande begäran skapar ett nytt sekretessjobb för en enskild kunds data i [!DNL Profile] butiken. Det finns två identitetsvärden för kunden i `userIDs` arrayen. ett med standardnamnutrymmet för `Email` identitet och det andra med ett anpassat `Customer_ID` namnutrymme. Den innehåller också produktvärdet för [!DNL Profile] (`ProfileService`) i `include` arrayen:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Använda gränssnittet

När du skapar jobbbegäranden i användargränssnittet måste du markera **[!UICONTROL AEP Data Lake]** och/eller **[!UICONTROL Profile]** under **[!UICONTROL Products]** för att kunna bearbeta jobb för data som lagras i [!DNL Data Lake] respektive [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Profilfragment i sekretessförfrågningar {#fragments}

Personuppgifterna för en enskild kund i [!DNL Profile] datalagret består ofta av flera profilfragment som kopplas till personen via identitetsdiagrammet. När du gör sekretessförfrågningar till [!DNL Profile] butiken är det viktigt att notera att förfrågningar bara behandlas på profilfragmentnivån, i stället för på hela profilen.

Tänk dig till exempel en situation där du lagrar kundattributdata i tre separata datauppsättningar, som använder olika identifierare för att associera dessa data med enskilda kunder:

| Namn på datauppsättning | Primärt identitetsfält | Lagrade attribut |
| --- | --- | --- |
| Datauppsättning 1 | `customer_id` | `address` |
| Datauppsättning 2 | `email_id` | `firstName`, `lastName` |
| Datauppsättning 3 | `email_id` | `mlScore` |

En av datauppsättningarna använder `customer_id` som primär identifierare, medan den andra använder `email_id`. Om du skulle skicka en sekretessförfrågan (åtkomst eller borttagning) med enbart `email_id` som användar-ID-värde skulle bara attributen `firstName`, `lastName`och `mlScore` bearbetas, men `address` påverkas inte.

För att säkerställa att dina sekretessförfrågningar behandlar alla relevanta kundattribut måste du ange de primära identitetsvärdena för alla tillämpliga datauppsättningar där dessa attribut kan lagras (upp till högst nio ID:n per kund). Mer information om fält som vanligtvis markeras som identiteter finns i avsnittet om identitetsfält i [grunderna för schemakomposition](../xdm/schema/composition.md#identity) .

>[!NOTE]
>
>Om du använder olika [sandlådor](../sandboxes/home.md) för att lagra dina [!DNL Profile] data måste du göra en separat sekretessförfrågan för varje sandlåda, som anger lämpligt sandlådenamn i `x-sandbox-name` rubriken.

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service]skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från [!DNL Data Lake] eller [!DNL Profile] butiken när sekretessjobbet har slutförts. Borttagningsjobbet bearbetas fortfarande, men data tas bort utan fel och är därför inte tillgängliga för någon [!DNL Platform] tjänst. Mer information om spårning av jobbstatus finns i [[!DNL Privacy Service] dokumentationen](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>En begäran om borttagning tar bort insamlade attributdata för en kund (eller en uppsättning kunder), men begäran tar inte bort de associationer som har upprättats i identitetsdiagrammet.
>
>En borttagningsbegäran som till exempel använder en kunds `email_id` och `customer_id` tar bort alla attributdata som lagras under dessa ID:n. Alla uppgifter som därefter hämtas in under samma `customer_id` metod kommer dock fortfarande att kopplas till det relevanta, `email_id`eftersom sammanslutningen fortfarande existerar.

I framtida versioner [!DNL Platform] skickas en bekräftelse till [!DNL Privacy Service] när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till i de viktiga begrepp som används för att behandla sekretessförfrågningar i [!DNL Experience Platform]. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

Information om hur du hanterar sekretessbegäranden för [!DNL Platform] resurser som inte används av [!DNL Profile]finns i dokumentet om behandling av [sekretessförfrågningar i Data Lake](../catalog/privacy.md).