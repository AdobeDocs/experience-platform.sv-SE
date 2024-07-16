---
keywords: Experience Platform;hem;populära ämnen
title: Behandling av sekretessförfrågningar i identitetstjänsten
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt ett flertal sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för identitetstjänsten.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Behandling av sekretessförfrågningar i [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör bearbetning av sekretessförfrågningar för [!DNL Identity Service] inom Adobe Experience Platform.

>[!NOTE]
>
>Den här handboken beskriver bara hur du gör sekretessförfrågningar för identitetsdatalagret i Experience Platform. Om du även planerar att göra sekretessförfrågningar för plattformsdatasjön eller [!DNL Real-Time Customer Profile], kan du läsa [Handboken om behandling av sekretessförfrågningar i datasjön](../catalog/privacy.md) och handboken om [bearbetning av sekretessförfrågningar för profil](../profile/privacy.md) förutom den här självstudiekursen.
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Servicens dokumentation](../privacy-service/experience-cloud-apps.md).

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform]-tjänster innan du läser den här handboken:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av deras personuppgifter mellan Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan enheter och system.
* [[!DNL Real-Time Customer Profile]](home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] förenar data för kundidentitet mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform] finns i [översikten över identitetsnamnrymden](../identity-service/features/namespaces.md).

## Skicka begäranden {#submit}

Avsnitten nedan beskriver hur du gör sekretessförfrågningar för [!DNL Identity Service] med API:t [!DNL Privacy Service] eller gränssnittet. Innan du läser dessa avsnitt rekommenderar vi att du läser igenom dokumentationen för [Privacy Services-API](../privacy-service/api/getting-started.md) eller [Privacy Servicens användargränssnitt](../privacy-service/ui/overview.md) för att få instruktioner om hur du skickar ett sekretessjobb, inklusive hur du formaterar användardata korrekt i nyttolaster.

### Använda API:et

När du skapar jobbförfrågningar i API:t måste alla ID:n som anges i `userIDs` använda en specifik `namespace` och `type`. Ett giltigt [identitetsnamnutrymme](#namespaces) som känns igen av [!DNL Identity Service] måste anges för värdet `namespace`, medan `type` måste vara antingen `standard` eller `unregistered` (för standardnamnutrymmen respektive anpassade namnutrymmen).

Dessutom måste matrisen `include` för nyttolasten för begäran innehålla produktvärden för de olika datalager som begäran görs till. När du gör förfrågningar till [!DNL Identity] måste arrayen innehålla värdet `Identity`.

Följande begäran skapar ett nytt sekretessjobb under GDPR för en enskild kunds data i [!DNL Identity]-butiken. Det finns två identitetsvärden för kunden i arrayen `userIDs`. Ett som använder standardnamnutrymmet för `Email`-identitet och det andra som använder namnutrymmet `ECID` innehåller också produktvärdet för [!DNL Identity] (`Identity`) i arrayen `include`:

>[!TIP]
>
>När du tar bort ett anpassat namnutrymme med API:t måste du ange identitetssymbolen som namnutrymme i stället för visningsnamnet.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Använda gränssnittet

>[!TIP]
>
>När du tar bort ett anpassat namnutrymme med användargränssnittet måste du ange identitetssymbolen som namnutrymme i stället för visningsnamnet. Du kan inte heller ta bort anpassade namnutrymmen i användargränssnittet för icke-produktionssandlådor.

När du skapar jobbförfrågningar i användargränssnittet måste du markera **[!UICONTROL Identity]** under **[!UICONTROL Products]** för att kunna bearbeta jobb för data som lagras i [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Borttagningen av den enskilda identiteten baseras på det angivna namnutrymmet och/eller ID-värdet. Dessutom tas alla sandlådor som är kopplade till en viss organisation bort.

Beroende på om du även inkluderade kundprofil för realtid (`ProfileService`) och datasjön (`aepDataLake`) som produkter i din sekretessbegäran för identitetstjänsten (`identity`), tas olika datauppsättningar som är relaterade till identiteten bort från systemet vid potentiellt olika tidpunkter:

| Produkter ingår | Effekter |
| --- | --- |
| Endast `identity` | Den angivna identiteten tas bort så snart Platform skickar en bekräftelse på att begäran om borttagning togs emot. Profilen som skapats från det identitetsdiagrammet finns fortfarande kvar, men uppdateras inte eftersom nya data har importerats eftersom identitetsassociationerna nu har tagits bort. De data som är associerade med profilen finns också kvar i datasjön. |
| `identity` och `ProfileService` | Den angivna identiteten tas bort så snart Platform skickar en bekräftelse på att begäran om borttagning togs emot. De data som är associerade med profilen finns kvar i datasjön. |
| `identity` och `aepDataLake` | Den angivna identiteten tas bort så snart Platform skickar en bekräftelse på att begäran om borttagning togs emot. Profilen som skapats från det identitetsdiagrammet finns fortfarande kvar, men uppdateras inte eftersom nya data har importerats eftersom identitetsassociationerna nu har tagits bort.<br><br>När datasjöprodukten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform]-tjänst. När jobbet är klart tas data bort helt från datasjön. |
| `identity`, `ProfileService` och `aepDataLake` | Den angivna identiteten tas bort så snart Platform skickar en bekräftelse på att begäran om borttagning togs emot.<br><br>När datasjöprodukten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform]-tjänst. När jobbet är klart tas data bort helt från datasjön. |

Mer information om att spåra jobbstatus finns i [[!DNL Privacy Service] dokumentationen](../privacy-service/home.md#monitor).

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till de viktiga begrepp som används för att bearbeta sekretessförfrågningar i [!DNL Identity Service]. Information om hur du hanterar sekretessbegäranden för andra [!DNL Experience Cloud]-program finns i dokumentet om [[!DNL Privacy Service] och [!DNL Experience Cloud] program](../privacy-service/experience-cloud-apps.md).
