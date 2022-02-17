---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
type: Documentation
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt ett flertal sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kundprofil i realtid.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6cb30dc9e7e76ff9ca060f83405196fa09ed0ebb
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---

# Behandling av sekretessförfrågningar i [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om tillgång, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser såsom den allmänna dataskyddsförordningen (GDPR), och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för [!DNL Real-time Customer Profile] inom Adobe Experience Platform.

>[!NOTE]
>
>Den här handboken beskriver bara hur du gör sekretessförfrågningar för datalagret Profil i Experience Platform. Om du även planerar att göra sekretessförfrågningar för Platform Data Lake, se guiden på [behandling av sekretessförfrågningar i Data Lake](../catalog/privacy.md) förutom den här självstudiekursen.
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Service](../privacy-service/experience-cloud-apps.md).

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] innan du läser den här guiden:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Real-time Customer Profile]](home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] överbryggar kundidentitetsdata mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att tillhandahålla sammanhang till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform], se [Översikt över namnutrymmet identity](../identity-service/namespaces.md).

## Skicka begäranden {#submit}

Avsnitten nedan beskriver hur du gör sekretessförfrågningar för [!DNL Real-time Customer Profile] med [!DNL Privacy Service] API eller gränssnitt. Innan du läser dessa avsnitt bör du granska [Privacy Services-API](../privacy-service/api/getting-started.md) eller [Privacy Servicens användargränssnitt](../privacy-service/ui/overview.md) dokumentation för fullständiga steg om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i begärandenyttolaster.

>[!IMPORTANT]
>
>Privacy Servicen kan bara bearbeta [!DNL Profile] data med en sammanfogningsprincip som inte utför identitetssammanfogning. Om du använder användargränssnittet för att bekräfta om dina sekretessförfrågningar behandlas kontrollerar du att du använder en profil med &quot;[!DNL None]&quot; som [!UICONTROL ID stitching] typ. Du kan alltså inte använda en sammanfogningsprincip där [!UICONTROL ID stitching] är inställd på &quot;[!UICONTROL Private graph]&quot;.
>
>![Sammanfogningsprincipens ID-sammanfogning är inställd på Ingen](./images/privacy/no-id-stitch.png)
>
>Det är också viktigt att notera att det inte går att garantera hur lång tid en sekretessbegäran kan ta att slutföra. Om ändringar inträffar i [!DNL Profile] data medan en begäran fortfarande bearbetas, oavsett om dessa poster bearbetas eller inte kan också garanteras.

### Använda API:et

När du skapar jobbförfrågningar i API:t, anges alla ID:n i `userIDs` måste använda en specifik `namespace` och `type`. Ett giltigt [identity namespace](#namespaces) känns igen av [!DNL Identity Service] måste anges för `namespace` värde, medan `type` måste vara antingen `standard` eller `unregistered` (för standardnamnutrymmen respektive anpassade namnutrymmen).

>[!NOTE]
>
>Du kan behöva ange mer än ett ID för varje kund, beroende på identitetsdiagrammet och hur dina profilfragment distribueras i plattformsdatauppsättningar. Se nästa avsnitt [profilfragment](#fragments) för mer information.

Dessutom är `include` arrayen med nyttolasten för begäran måste innehålla produktvärdena för de olika datalager som begäran görs till. När förfrågningar görs till [!DNL Data Lake]måste arrayen innehålla värdet &quot;ProfileService&quot;.

Följande begäran skapar ett nytt sekretessjobb för en enskild kunds data i [!DNL Profile] butik. Två identitetsvärden anges för kunden i `userIDs` array, en som använder standarden `Email` id namespace, and the other using a custom `Customer_ID` namnutrymme. Den innehåller också produktvärdet för [!DNL Profile] (`ProfileService`) i `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Plattformsprocessernas sekretessförfrågningar för alla [sandlådor](../sandboxes/home.md) som tillhör din organisation. Detta resulterar i att `x-sandbox-name` huvud som ingår i begäran ignoreras av systemet.

### Använda gränssnittet

När du skapar jobbförfrågningar i användargränssnittet måste du välja **[!UICONTROL AEP Data Lake]** och/eller **[!UICONTROL Profile]** under **[!UICONTROL Products]** för att bearbeta jobb för data som lagras i [!DNL Data Lake] eller [!DNL Real-time Customer Profile], respektive.

![En begäran om åtkomstjobb skapas i användargränssnittet med alternativet Profil markerat under Produkter](./images/privacy/product-value.png)

## Profilfragment i sekretessförfrågningar {#fragments}

I [!DNL Profile] personuppgifterna för en enskild kund består ofta av flera profilfragment som kopplas till personen via identitetsdiagrammet. När sekretessförfrågningar görs till [!DNL Profile] lagring är det viktigt att tänka på att begäranden bara behandlas på profilfragmentnivån i stället för på hela profilen.

Tänk dig till exempel en situation där du lagrar kundattributdata i tre separata datauppsättningar, som använder olika identifierare för att associera dessa data med enskilda kunder:

| Namn på datauppsättning | Primärt identitetsfält | Lagrade attribut |
| --- | --- | --- |
| Datauppsättning 1 | `customer_id` | `address` |
| Datauppsättning 2 | `email_id` | `firstName`, `lastName` |
| Datauppsättning 3 | `email_id` | `mlScore` |

En av datauppsättningarna använder `customer_id` som primär identifierare, medan de andra två använder `email_id`. Om du skulle skicka en begäran om sekretess (åtkomst eller radering) använder du endast `email_id` som användar-ID, endast `firstName`, `lastName`och `mlScore` attribut skulle bearbetas, medan `address` inte påverkas.

För att säkerställa att dina sekretessförfrågningar behandlar alla relevanta kundattribut måste du ange de primära identitetsvärdena för alla tillämpliga datauppsättningar där dessa attribut kan lagras (upp till högst nio ID:n per kund). Se avsnittet om identitetsfält i [grunderna för schemakomposition](../xdm/schema/composition.md#identity) för mer information om fält som vanligen markeras som identiteter.

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], [!DNL Platform] skickar bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från [!DNL Data Lake] eller [!DNL Profile] lagra när sekretessjobbet är klart. Medan borttagningsjobbet fortfarande bearbetas tas data bort och är därför inte tillgängliga för alla [!DNL Platform] service. Se [[!DNL Privacy Service] dokumentation](../privacy-service/home.md#monitor) för mer information om spårning av jobbstatus.

>[!IMPORTANT]
>
>En begäran om borttagning tar bort insamlade attributdata för en kund (eller en uppsättning kunder), men begäran tar inte bort de associationer som har upprättats i identitetsdiagrammet.
>
>En borttagningsbegäran som använder en kunds `email_id` och `customer_id` tar bort alla attributdata som lagras under dessa ID:n. Alla uppgifter som därefter importeras under samma `customer_id` kommer fortfarande att kopplas till lämplig `email_id`, eftersom associationen fortfarande finns.
>
>Dessutom kan Privacy Servicen bara bearbeta [!DNL Profile] data med en sammanfogningsprincip som inte utför identitetssammanfogning. Om du använder användargränssnittet för att bekräfta om dina sekretessförfrågningar behandlas kontrollerar du att du använder en profil med &quot;[!DNL None]&quot; som [!UICONTROL ID stitching] typ. Du kan alltså inte använda en sammanfogningsprincip där [!UICONTROL ID stitching] är inställd på &quot;[!UICONTROL Private graph]&quot;.
>
>![Sammanfogningsprincipens ID-sammanfogning är inställd på Ingen](./images/privacy/no-id-stitch.png)

I framtida versioner [!DNL Platform] skickar bekräftelsen till [!DNL Privacy Service] efter att data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du introducerat de viktiga begrepp som används för att behandla sekretessförfrågningar i [!DNL Experience Platform]. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

För information om behandling av sekretessförfrågningar för [!DNL Platform] resurser som inte används av [!DNL Profile], se dokumentet på [behandling av sekretessförfrågningar i Data Lake](../catalog/privacy.md).
