---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandling av sekretessförfrågningar i kundprofil i realtid
topic: overview
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Behandling av sekretessförfrågningar i [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] behandlar kundförfrågningar om åtkomst, avanmälan från försäljning eller radering av personuppgifter enligt sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och [!DNL California Consumer Privacy Act] (CCPA).

Det här dokumentet innehåller viktiga begrepp som rör behandling av sekretessförfrågningar för [!DNL Real-time Customer Profile].

## Komma igång

Vi rekommenderar att du har en fungerande förståelse för följande [!DNL Experience Platform] tjänster innan du läser den här handboken:

* [[!DNL-Privacy Service]](home.md): Hanterar kundförfrågningar om åtkomst, avanmälan eller radering av personuppgifter mellan olika Adobe Experience Cloud-program.
* [[!DNL Identity Service]](../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Identitetsnamnutrymmen {#namespaces}

Adobe Experience Platform [!DNL Identity Service] förenar data om kundidentitet mellan system och enheter. [!DNL Identity Service] använder **identitetsnamnutrymmen** för att ge kontext till identitetsvärden genom att koppla dem till deras ursprungssystem. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Identitetstjänsten underhåller ett arkiv med globalt definierade (standard) och användardefinierade (anpassade) identitetsnamnutrymmen. Standardnamnutrymmen är tillgängliga för alla organisationer (till exempel&quot;E-post&quot; och&quot;ECID&quot;), medan din organisation också kan skapa anpassade namnutrymmen som passar organisationens behov.

Mer information om namnutrymmen för identiteter i [!DNL Experience Platform]finns i [översikten över](../identity-service/namespaces.md)namnutrymmen för identiteter.

## Skicka begäranden {#submit}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du skapar sekretessförfrågningar för [!DNL Profile] datalagret. Vi rekommenderar att du läser [Privacy Service-API](../privacy-service/api/getting-started.md) eller [Privacy Service-gränssnittets](../privacy-service/ui/overview.md) dokumentation för att få information om hur du skickar ett sekretessjobb, inklusive hur inskickade användaridentitetsdata formateras korrekt i nyttolaster.

I följande avsnitt beskrivs hur du gör sekretessförfrågningar för [!DNL Real-time Customer Profile] och [!DNL Data Lake] använder [!DNL Privacy Service] API:t eller användargränssnittet.

### Använda API

När du skapar jobbförfrågningar i API:t måste alla `userIDs` som anges använda ett specifikt `namespace` och `type` beroende på vilket datalager de gäller för. ID:n för [!DNL Profile] butiken måste använda antingen &quot;standard&quot; eller &quot;anpassad&quot; för sitt `type` värde och ett giltigt [ID-namnutrymme](#namespaces) som känns igen [!DNL Identity Service] för deras `namespace` värde.


Dessutom måste arrayen för den begärda nyttolasten innehålla produktvärdena för de olika datalager som begäran görs till. `include` När du gör förfrågningar till [!DNL Data Lake]måste arrayen innehålla värdet &quot;ProfileService&quot;.

Följande begäran skapar ett nytt sekretessjobb för båda [!DNL Real-time Customer Profile]med standardnamnutrymmet för e-postadress. Den innehåller också produktvärdet för [!DNL Profile] i `include` arrayen:

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

När du skapar jobbbegäranden i användargränssnittet måste du markera **[!UICONTROL AEP Data Lake]** och/eller **[!UICONTROL Profile]** under _[!UICONTROL Products]_för att kunna bearbeta jobb för data som lagras i[!DNL Data Lake]respektive[!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Ta bort bearbetning av begäran

När [!DNL Experience Platform] tar emot en borttagningsbegäran från [!DNL Privacy Service]skickar [!DNL Platform] en bekräftelse till [!DNL Privacy Service] att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från [!DNL Data Lake] eller [!DNL Profile] butiken inom sju dagar. Under denna sjudagarsperiod tas data bort på skärmen och är därför inte tillgängliga för någon [!DNL Platform] tjänst.

I framtida versioner [!DNL Platform] skickas en bekräftelse till [!DNL Privacy Service] när data har tagits bort fysiskt.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till i de viktiga begrepp som används för att behandla sekretessförfrågningar i [!DNL Experience Platform]. Vi rekommenderar att du fortsätter att läsa dokumentationen som finns i den här handboken för att få en djupare förståelse för hur du hanterar identitetsdata och skapar sekretessjobb.

Information om hur du hanterar sekretessbegäranden för [!DNL Platform] resurser som inte används av [!DNL Profile]finns i dokumentet om behandling av [sekretessförfrågningar i Data Lake](../catalog/privacy.md).