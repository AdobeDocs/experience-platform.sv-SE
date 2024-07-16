---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
type: Documentation
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt ett flertal sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kundprofil i realtid.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 0%

---

# Behandling av sekretessförfrågningar i [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör bearbetning av sekretessförfrågningar för [!DNL Real-Time Customer Profile] inom Adobe Experience Platform.

>[!NOTE]
>
>Den här handboken beskriver bara hur du gör sekretessförfrågningar för datalagret Profil i Experience Platform. Om du även planerar att göra sekretessförfrågningar för sjön med plattformsdata kan du läsa handboken [privacy request processing in the data Lake](../catalog/privacy.md) förutom den här självstudiekursen.
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Servicens dokumentation](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>Sekretessbegäran i den här handboken omfattar **inte** icke-personliga B2B-enheter.

## Komma igång

Handboken kräver en fungerande förståelse av följande [!DNL Platform]-komponenter:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av deras personuppgifter mellan Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan enheter och system.
* [[!DNL Real-Time Customer Profile]](home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] förenar data för kundidentitet mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform] finns i [översikten över identitetsnamnrymden](../identity-service/features/namespaces.md).

## Skicka begäranden {#submit}

Avsnitten nedan beskriver hur du gör sekretessförfrågningar för [!DNL Real-Time Customer Profile] med API:t [!DNL Privacy Service] eller gränssnittet. Innan du läser de här avsnitten bör du granska, eller känna till, dokumentationen för [Privacy Services-API](../privacy-service/api/getting-started.md) eller [Privacy Servicens användargränssnitt](../privacy-service/ui/overview.md). Dessa dokument innehåller fullständiga anvisningar om hur du skickar in ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i begärda nyttolaster.

>[!IMPORTANT]
>
>Privacy Servicen kan bara bearbeta [!DNL Profile]-data med en sammanfogningsprincip som inte utför identitetssammanfogning. Mer information finns i avsnittet [begränsningar för sammanslagningsprinciper](#merge-policy-limitations).
>
>Observera att förfrågningar om sekretess behandlas asynkront i de lagstadgade kraven, och hur lång tid det tar att slutföra kan variera. Om ändringar görs i dina [!DNL Profile]-data medan en begäran fortfarande bearbetas, är det inte säkert att dessa inkommande poster också kommer att bearbetas i den begäran. Det är bara profiler som finns i datasjön eller profilarkivet när sekretessjobbet begärs som kan tas bort. Om du importerar profildata som är relaterade till ämnet för en borttagningsbegäran under borttagningsjobbet är det inte säkert att alla profilfragment tas bort.
>Det är ditt ansvar att vara medveten om inkommande data i plattforms- eller profiltjänsten vid tidpunkten för en borttagningsbegäran, eftersom dessa data kommer att infogas i dina postarkiv. Du måste vara försiktig med att ta in data som har tagits bort eller håller på att tas bort.

### Använda API:et

När du skapar jobbförfrågningar i API:t måste alla ID:n som anges i `userIDs` använda en specifik `namespace` och `type`. Ett giltigt [identitetsnamnutrymme](#namespaces) som känns igen av [!DNL Identity Service] måste anges för värdet `namespace`, medan `type` måste vara antingen `standard` eller `unregistered` (för standardnamnutrymmen respektive anpassade namnutrymmen).

>[!NOTE]
>
>Du kan behöva ange mer än ett ID för varje kund, beroende på identitetsdiagrammet och hur dina profilfragment distribueras i plattformsdatauppsättningar. Mer information finns i nästa avsnitt, [profilfragment](#fragments).

Dessutom måste matrisen `include` för nyttolasten för begäran innehålla produktvärden för de olika datalager som begäran görs till. Om du vill ta bort profildata som är associerade med en identitet måste matrisen innehålla värdet `ProfileService`. Om du vill ta bort kundens identitetsdiagramassociationer måste matrisen innehålla värdet `identity`.

>[!NOTE]
>
>Mer information om effekterna av att använda `ProfileService` och `identity` i arrayen `include` finns i avsnittet [profilförfrågningar och identitetsförfrågningar](#profile-v-identity) senare i det här dokumentet.

Följande begäran skapar ett nytt sekretessjobb för en enskild kunds data i [!DNL Profile]-butiken. Det finns två identitetsvärden för kunden i arrayen `userIDs`. Den ena använder standardnamnutrymmet för identitet `Email` och den andra använder ett anpassat namnutrymme för `Customer_ID`. Den innehåller också produktvärdet för [!DNL Profile] (`ProfileService`) i arrayen `include`:

**Begäran**

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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Plattformen behandlar sekretessförfrågningar i alla [sandlådor](../sandboxes/home.md) som tillhör din organisation. Därför ignoreras alla `x-sandbox-name`-huvuden som ingår i begäran av systemet.

**Produktsvar**

När sekretessjobbet har slutförts för profiltjänsten returneras ett svar i JSON-format med information om de användar-ID som efterfrågas.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### Använda gränssnittet

När du skapar jobbförfrågningar i användargränssnittet måste du markera **[!UICONTROL AEP Data Lake]** och/eller **[!UICONTROL Profile]** under **[!UICONTROL Products]** för att kunna bearbeta jobb för data som lagras i datasjön eller [!DNL Real-Time Customer Profile].

![En åtkomstjobbbegäran skapas i användargränssnittet med alternativet Profil markerat under Produkter](./images/privacy/product-value.png)

## Profilfragment i sekretessförfrågningar {#fragments}

I datalagret [!DNL Profile] består persondata för en enskild kund ofta av flera profilfragment som är kopplade till personen via identitetsdiagrammet. När du gör sekretessförfrågningar i [!DNL Profile]-arkivet är det viktigt att notera att förfrågningar bara behandlas på profilfragmentnivån, i stället för på hela profilen.

Tänk dig till exempel en situation där du lagrar kundattributdata i tre separata datauppsättningar, som använder olika identifierare för att associera dessa data med enskilda kunder:

| Namn på datauppsättning | Primärt identitetsfält | Lagrade attribut |
| --- | --- | --- |
| Datauppsättning 1 | `customer_id` | `address` |
| Datauppsättning 2 | `email_id` | `firstName`, `lastName` |
| Datauppsättning 3 | `email_id` | `mlScore` |

En av datauppsättningarna använder `customer_id` som primär identifierare, medan de andra använder `email_id`. Om du skulle skicka en sekretessförfrågan (åtkomst eller borttagning) med endast `email_id` som användar-ID-värde, skulle bara attributen `firstName`, `lastName` och `mlScore` bearbetas, medan `address` inte skulle påverkas.

För att säkerställa att dina sekretessförfrågningar behandlar alla relevanta kundattribut måste du ange de primära identitetsvärdena för alla tillämpliga datauppsättningar där dessa attribut kan lagras (upp till högst nio ID:n per kund). Mer information om fält som vanligtvis markeras som identiteter finns i avsnittet om identitetsfält i [grunderna för schemakomposition](../xdm/schema/composition.md#identity).

## Ta bort bearbetning av begäran {#delete}

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort när sekretessjobbet har slutförts.

>[!IMPORTANT]
>
>Begäran om borttagning av sekretess är inte omedelbar och kan variera beroende på vilka tjänster som används och andra faktorer som påverkar t.ex. geografisk placering. Tidsramen för slutförande av sekretessjobb kan vara mellan 15 och 45 dagar, men är inte garanterad.

Beroende på om du även inkluderade identitetstjänsten (`identity`) och datasjön (`aepDataLake`) som produkter i din sekretessbegäran för profilen (`ProfileService`), tas olika datauppsättningar som är relaterade till profilen bort från systemet vid potentiellt olika tidpunkter:

| Produkter ingår | Effekter |
| --- | --- |
| Endast `ProfileService` | Profilen tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning har tagits emot. Profilens identitetsdiagram finns dock fortfarande kvar och profilen kan rekonstrueras när nya data med samma identiteter importeras. De data som är associerade med profilen finns också kvar i datasjön. |
| `ProfileService` och `identity` | Profilen och dess associerade identitetsdiagram tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot. De data som är associerade med profilen finns kvar i datasjön. |
| `ProfileService` och `aepDataLake` | Profilen tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning har tagits emot. Profilens identitetsdiagram finns dock fortfarande kvar och profilen kan rekonstrueras när nya data med samma identiteter importeras.<br><br>När datasjöprodukten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform]-tjänst. När jobbet är klart tas data bort helt från datasjön. |
| `ProfileService`, `identity` och `aepDataLake` | Profilen och dess associerade identitetsdiagram tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot.<br><br>När datasjöprodukten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform]-tjänst. När jobbet är klart tas data bort helt från datasjön. |

Mer information om att spåra jobbstatus finns i [[!DNL Privacy Service] dokumentationen](../privacy-service/home.md#monitor).

### Profilförfrågningar kontra identitetsförfrågningar {#profile-v-identity}

Om en borttagningsbegäran görs för profilen (`ProfileService`) men inte för identitetstjänsten (`identity`), tar det resulterande jobbet bort de insamlade attributdata för en kund (eller en uppsättning kunder), men tar inte bort associationerna som har upprättats i identitetsdiagrammet.

En borttagningsbegäran som använder en kunds `email_id` och `customer_id` tar bort alla attributdata som lagras under dessa ID:n. Alla data som därefter importeras under samma `customer_id` kommer dock fortfarande att kopplas till rätt `email_id`, eftersom associationen fortfarande finns.

Om du vill ta bort profilen och alla identitetsassociationer för en viss kund måste du ta med både profil- och identitetstjänsten som målprodukter i borttagningsförfrågningarna.

### Begränsningar för sammanfogningsprincip {#merge-policy-limitations}

Privacy Servicen kan bara bearbeta [!DNL Profile]-data med en sammanfogningsprincip som inte utför identitetssammanfogning. Om du använder användargränssnittet för att bekräfta om dina sekretessförfrågningar behandlas kontrollerar du att du använder en princip med **[!DNL None]** som [!UICONTROL ID stitching]-typ. Du kan med andra ord inte använda en sammanfogningsprincip där [!UICONTROL ID stitching] är inställd på [!UICONTROL Private graph].

>![Sammanfogningsprincipens ID-sammanfogning är inställd på Ingen](./images/privacy/no-id-stitch.png)

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till de viktiga begrepp som används för att bearbeta sekretessförfrågningar i [!DNL Experience Platform]. Om du vill få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb kan du fortsätta att läsa dokumentationen som finns i den här handboken.

Mer information om hur du hanterar sekretessbegäranden för [!DNL Platform]-resurser som inte används av [!DNL Profile] finns i dokumentet om [bearbetning av sekretessförfrågningar i datasjön](../catalog/privacy.md).
