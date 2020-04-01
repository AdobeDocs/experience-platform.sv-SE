---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Behandling av sekretessförfrågningar i kundprofil i realtid

Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kundprofil i realtid.

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande Experience Platform-tjänster innan du läser den här handboken:

* [Integritetstjänst](home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av personliga data mellan Adobe Experience Cloud-program.
* [Identitetstjänst](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [Kundprofil](../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform Identity Service knyter samman kundidentitetsdata mellan system och enheter. Identitetstjänsten använder **ID-namnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;e-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-ID (&quot;AdCloud&quot;) eller ett Adobe Target-ID (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om identitetsnamnutrymmen i Experience Platform finns i [översikten över](../identity-service/namespaces.md)identitetsnamnrymden.

## Skicka begäranden {#submit}

>[!NOTE] I det här avsnittet beskrivs hur du formaterar sekretessförfrågningar för Data Lake. Vi rekommenderar att du läser igenom [sekretesstjänstens API](../privacy-service/api/getting-started.md) eller [sekretesstjänstens](../privacy-service/ui/overview.md) användargränssnittsdokumentation för att få information om hur du skickar ett sekretessjobb, inklusive hur du formaterar inskickade användaridentitetsdata i begärande nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för kundprofil i realtid och datasjön med hjälp av sekretesstjänstens API eller gränssnitt.

### Använda API

När du skapar jobbförfrågningar i API:t måste alla `userIDs` som anges använda ett specifikt `namespace` och `type` beroende på vilket datalager de gäller för. ID:n för profilarkivet måste använda antingen &quot;standard&quot; eller &quot;anpassad&quot; för sitt `type` värde, och ett giltigt [identitetsnamnutrymme](#namespaces) som identifieras av identitetstjänsten för deras `namespace` värde.


Dessutom måste arrayen för den begärda nyttolasten innehålla produktvärdena för de olika datalager som begäran görs till. `include` När du gör förfrågningar till Data Lake måste arrayen innehålla värdet &quot;ProfileService&quot;.

Följande begäran skapar ett nytt sekretessjobb för båda kundprofilerna i realtid med standardnamnutrymmet&quot;E-post&quot;. Det innehåller också produktvärdet för Profil i `include` arrayen:

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
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Använda gränssnittet

När du skapar jobbförfrågningar i användargränssnittet måste du välja **AEP Data Lake** och/eller **Profile** under _Products_ för att kunna bearbeta jobb för data som lagras i Data Lake respektive Real-time Customer Profile.

<img src="images/privacy/product-value.png" width="450"><br>

## Ta bort bearbetning av begäran

När Experience Platform tar emot en begäran om borttagning från Integritetstjänst skickar Platform en bekräftelse till Integritetstjänst om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från Data Lake eller Profile Store inom sju dagar. Under denna sjudagarsperiod tas data bort på skärmen och är därför inte tillgängliga för någon plattformstjänst.

I framtida versioner kommer Platform att skicka en bekräftelse till sekretesstjänsten när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till de viktiga koncept som används för att behandla sekretessförfrågningar i Experience Platform. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

Information om hur du hanterar sekretessbegäranden för plattformsresurser som inte används av profilen finns i dokumentet om behandling av [sekretessförfrågningar i Data Lake](../catalog/privacy.md).