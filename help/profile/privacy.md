---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Behandling av sekretessförfrågningar i kundprofil i realtid

Adobe Experience Platform Privacy Service behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser såsom Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för kundprofil i realtid.

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande Experience Platform-tjänster innan du läser den här handboken:

* [Privacy Service](home.md): Hanterar kundförfrågningar om åtkomst, avanmälan från försäljning eller borttagning av personliga data mellan Adobe Experience Cloud-program.
* [Identitetstjänst](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [Kundprofil](../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform Identity Service knyter samman data om kundidentitet mellan system och enheter. Identitetstjänsten använder **ID-namnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-ID (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om namnutrymmen för identiteter i Experience Platform finns i översikten över [namnutrymmet](../identity-service/namespaces.md).

## Skicka begäranden {#submit}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du skapar sekretessförfrågningar för profildatalagret. Vi rekommenderar att du läser [Privacy Service-API](../privacy-service/api/getting-started.md) eller [Privacy Service-gränssnittets](../privacy-service/ui/overview.md) dokumentation för att få information om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för kundprofil i realtid och datasjön med hjälp av Privacy Service-API:t eller användargränssnittet.

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

När Experience Platform tar emot en raderingsbegäran från Privacy Servicen, skickar Platform en bekräftelse till Privacy Servicen om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från Data Lake eller Profile Store inom sju dagar. Under denna sjudagarsperiod tas data bort på skärmen och är därför inte tillgängliga för någon Platform-tjänst.

I framtida versioner skickar Platform en bekräftelse till Privacy Servicen när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till de viktiga koncept som används för att behandla sekretessförfrågningar i Experience Platform. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

Information om hur du hanterar sekretessbegäranden för Platform-resurser som inte används av Profil finns i dokumentet om behandling av [sekretessförfrågningar i Data Lake](../catalog/privacy.md).