---
keywords: Experience Platform;hem;populära ämnen
title: Behandling av sekretessförfrågningar i identitetstjänsten
description: Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter enligt ett flertal sekretessbestämmelser. Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för identitetstjänsten.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 0%

---

# Behandling av sekretessförfrågningar i [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om tillgång, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser såsom den allmänna dataskyddsförordningen (GDPR), och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för [!DNL Identity Service] inom Adobe Experience Platform.

>[!NOTE]
>
>Den här handboken beskriver bara hur du gör sekretessförfrågningar för identitetsdatalagret i Experience Platform. Om du även planerar att göra sekretessförfrågningar för plattformens datalinje eller [!DNL Real-Time Customer Profile], se guiden på [behandling av sekretessförfrågningar i datasjön](../catalog/privacy.md) och i guiden [sekretessförfrågningsbehandling för profil](../profile/privacy.md) förutom den här självstudiekursen.
>
>Anvisningar om hur du gör sekretessförfrågningar för andra Adobe Experience Cloud-program finns i [Privacy Service](../privacy-service/experience-cloud-apps.md).

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] innan du läser den här guiden:

* [[!DNL Privacy Service]](../privacy-service/home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Real-Time Customer Profile]](home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] överbryggar kundidentitetsdata mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att tillhandahålla sammanhang till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i [!DNL Experience Platform], se [Översikt över namnutrymmet identity](../identity-service/namespaces.md).

## Skicka begäranden {#submit}

Avsnitten nedan beskriver hur du gör sekretessförfrågningar för [!DNL Identity Service] med [!DNL Privacy Service] API eller gränssnitt. Innan du läser dessa avsnitt bör du granska [Privacy Services-API](../privacy-service/api/getting-started.md) eller [Privacy Servicens användargränssnitt](../privacy-service/ui/overview.md) dokumentation för fullständiga steg om hur du skickar ett sekretessjobb, inklusive hur du formaterar användardata korrekt i nyttolaster.

### Använda API:et

När du skapar jobbförfrågningar i API:t, anges alla ID:n i `userIDs` måste använda en specifik `namespace` och `type`. Ett giltigt [identity namespace](#namespaces) känns igen av [!DNL Identity Service] måste anges för `namespace` värde, medan `type` måste vara antingen `standard` eller `unregistered` (för standardnamnutrymmen respektive anpassade namnutrymmen).

Dessutom är `include` arrayen med nyttolasten för begäran måste innehålla produktvärdena för de olika datalager som begäran görs till. Vid förfrågningar till [!DNL Identity]måste arrayen innehålla värdet `Identity`.

Följande begäran skapar ett nytt sekretessjobb under GDPR för en enskild kunds data i [!DNL Identity] butik. Två identitetsvärden anges för kunden i `userIDs` array, en som använder standarden `Email` id namespace, and the other using an `ECID` namespace, It includes the product value for [!DNL Identity] (`Identity`) i `include` array:

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

När du skapar jobbförfrågningar i användargränssnittet måste du välja **[!UICONTROL Identity]** under **[!UICONTROL Products]** för att bearbeta jobb för data som lagras i [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service], [!DNL Platform] skickar bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Borttagningen av den enskilda identiteten baseras på det angivna namnutrymmet och/eller ID-värdet. Dessutom tas alla sandlådor som är kopplade till en viss organisation bort.

Beroende på om du även har inkluderat kundprofil i realtid (`ProfileService`) och datasjön (`aepDataLake`) som produkter i din sekretesspolicy för identitetstjänst (`identity`) tas olika datauppsättningar som är relaterade till identiteten bort från systemet vid potentiellt olika tidpunkter:

| Produkter som ingår | Effekter |
| --- | --- |
| `identity` endast | Identitetsdiagrammet som är associerat med den angivna identiteten tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot. Profilen som skapats från det identitetsdiagrammet finns fortfarande kvar, men uppdateras inte eftersom nya data har importerats eftersom identitetsassociationerna nu har tagits bort. De data som är associerade med profilen finns också kvar i datasjön. |
| `identity` och `ProfileService` | Identitetsdiagrammet och dess associerade profil tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot. De data som är associerade med profilen finns kvar i datasjön. |
| `identity` och `aepDataLake` | Identitetsdiagrammet som är associerat med den angivna identiteten tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot. Profilen som skapats från det identitetsdiagrammet finns fortfarande kvar, men uppdateras inte eftersom nya data har importerats eftersom identitetsassociationerna nu har tagits bort.<br><br>När Data Lake-produkten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort utan fel och är därför inte tillgängliga för någon [!DNL Platform] service. När jobbet är klart tas data bort helt från datasjön. |
| `identity`, `ProfileService`och `aepDataLake` | Identitetsdiagrammet och dess associerade profil tas bort omedelbart när Platform skickar en bekräftelse på att begäran om borttagning togs emot.<br><br>När Data Lake-produkten svarar att begäran har tagits emot och bearbetas, tas data som är kopplade till profilen bort utan fel och är därför inte tillgängliga för någon [!DNL Platform] service. När jobbet är klart tas data bort helt från datasjön. |

Se [[!DNL Privacy Service] dokumentation](../privacy-service/home.md#monitor) för mer information om spårning av jobbstatus.

## Nästa steg

Genom att läsa det här dokumentet har du introducerat de viktiga begrepp som används för att behandla sekretessförfrågningar i [!DNL Identity Service]. För information om behandling av sekretessförfrågningar för andra [!DNL Experience Cloud] program, se dokumentet om [[!DNL Privacy Service] and [!DNL Experience Cloud] program](../privacy-service/experience-cloud-apps.md).
