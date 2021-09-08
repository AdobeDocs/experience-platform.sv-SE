---
description: Med den här konfigurationen kan du ange grundläggande information som målnamn, kategori, beskrivning, logotyp och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål.
title: Alternativ för destinationskonfiguration för mål-SDK
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 2%

---

# Målkonfiguration {#destination-configuration}

## Översikt {#overview}

Med den här konfigurationen kan du ange grundläggande information som målnamn, kategori, beskrivning, logotyp och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål.

Du kan konfigurera de funktioner som beskrivs i det här dokumentet med API-slutpunkten `/authoring/destinations`. Läs [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Exempelkonfiguration {#example-configuration}

Nedan visas ett exempel på konfiguration för en fiktiv destination, Moviestar, som har slutpunkter på fyra platser i världen. Målet tillhör kategorin för mobila destinationer. Avsnitten nedan beskriver hur konfigurationen är konstruerad.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   }
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Anger målets namn i Experience Platform-katalogen. |
| `description` | Sträng | Ange en beskrivning som Adobe ska använda i Experience Platform-destinationskatalogen för ditt destinationskort. Rikta dig för högst 4-5 meningar. |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED` och `DELETED`. Använd `TEST` när du först konfigurerar målet. |

## Konfigurationer för kundautentisering {#customer-authentication-configurations}

I det här avsnittet genereras kontosidan i användargränssnittet i Experience Platform, där användare ansluter Experience Platform till konton som de har med ditt mål. Beroende på vilket autentiseringsalternativ du anger i fältet `authType`, genereras Experience Platform-sidan för användarna enligt följande:

**Bärarautentisering**

Användarna måste ange den innehavartoken som de får från ditt mål.

![Gränssnittsåtergivning med innehavarautentisering](./assets/bearer-authentication-ui.png)

**OAuth 2-autentisering**

Användare väljer **[!UICONTROL Connect to destination]** för att utlösa OAuth 2-autentiseringsflödet till ditt mål.

![Gränssnittsåtergivning med OAuth 2-autentisering](./assets/oauth2-authentication-ui.png)


| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder mot servern. Se `authType` nedan för godkända värden. |
| `authType` | Sträng | Godkända värden är `OAUTH2, BEARER`. <br><ul><li> Om målet har stöd för OAuth 2-autentisering väljer du `OAUTH2`-värdet och lägger till de obligatoriska fälten för OAuth 2, vilket visas på autentiseringssidan för mål-SDK OAuth 2. Du bör dessutom välja `authenticationRule=CUSTOMER_AUTHENTICATION` i [målleveransavsnittet](./destination-configuration.md). </li><li>För innehavarautentisering väljer du `BEARER` och väljer `authenticationRule=CUSTOMER_AUTHENTICATION` i [målleveransavsnittet](./destination-configuration.md).</li></ul> |

## Kunddatafält {#customer-data-fields}

I det här avsnittet kan partners lägga in anpassade fält. I exempelkonfigurationen ovan kräver `customerDataFields` att användarna väljer en slutpunkt i autentiseringsflödet och anger sitt kund-ID med målet. Konfigurationen återspeglas i autentiseringsflödet enligt nedan:

![Anpassat fältautentiseringsflöde](./assets/custom-field-authentication-flow.png)

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer`. |
| `title` | Sträng | Anger fältets namn, så som det visas för kunder i användargränssnittet i Experience Platform. |
| `description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID till exempel inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i det här fältet. |

## Gränssnittsattribut {#ui-attributes}

Det här avsnittet hänvisar till de gränssnittselement i konfigurationen ovan som Adobe ska använda för ditt mål i Adobe Experience Platform användargränssnitt. Se nedan:

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `documentationLink` | Sträng | Refererar till dokumentationssidan i [målkatalogen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog). Använd `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på målet. För ett mål som heter Moviestar använder du `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Sträng | `Server-to-server` är för närvarande det enda tillgängliga alternativet. |
| `frequency` | Sträng | `Streaming` är för närvarande det enda tillgängliga alternativet. |

## Schemakonfiguration i mappningssteget {#schema-configuration}

![Aktivera mappningssteg](./assets/enable-mapping-step.png)

Använd parametrarna i `schemaConfig` för att aktivera mappningssteget i arbetsflödet för målaktivering. Genom att använda de parametrar som beskrivs nedan kan du bestämma om användare av Experience Platform kan mappa profilattribut och/eller identiteter till det önskade schemat på målsidan.

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `profileFields` | Array | *Visas inte i exempelkonfigurationen ovan.* När du lägger till fördefinierade  `profileFields`kan användare mappa Experience Platform-attribut till de fördefinierade attributen på målsidan. |
| `profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `identityRequired` | Boolean | Använd `true` om användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |

## Identiteter och attribut {#identities-and-attributes}

Parametrarna i det här avsnittet avgör hur målidentiteterna och -attributen fylls i mappningssteget i användargränssnittet i Experience Platform, där användare mappar sina XDM-scheman till schemat i målplatsen.

Adobe måste veta vilka [!DNL Platform]-identiteter som kunder kan exportera till ditt mål. Några exempel är [!DNL Experience Cloud ID], hash-kodad e-post, enhets-ID ([!DNL IDFA], [!DNL GAID]). Dessa värden är [!DNL Platform] identitetsnamnutrymmen som kunder kan mappa till identitetsnamnutrymmen från målet.

Identitetsnamnutrymmen kräver ingen 1-till-1-korrespondens mellan [!DNL Platform] och ditt mål.
Kunder kan till exempel mappa ett [!DNL Platform] [!DNL IDFA]-namnutrymme till ett [!DNL IDFA]-namnutrymme från målet, eller mappa samma [!DNL Platform] [!DNL IDFA]-namnutrymme till ett [!DNL Customer ID]-namnutrymme i målet.

Läs mer i översikten [Identity Namespace](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv).

![Återge målidentiteter i användargränssnittet](./assets/target-identities-ui.png)

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `acceptsAttributes` | Boolean | Anger om målet accepterar standardprofilattribut. Normalt framhävs dessa attribut i våra partners dokumentation. |
| `acceptsCustomNamespaces` | Boolean | Anger om kunderna kan ställa in anpassade namnutrymmen i målet. |
| `allowedAttributesTransformation` | Sträng | *Visas inte i exempelkonfigurationen*. Används till exempel när [!DNL Platform]-kunden har oformaterade e-postadresser som attribut och din plattform bara accepterar hash-kodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `acceptedGlobalNamespaces` | – | *Visas inte i exempelkonfigurationen*. Används för fall där plattformen accepterar [standardnamnutrymmen för identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (till exempel IDFA), så du kan begränsa plattformsanvändare till att endast välja dessa ID-namnutrymmen. |

## Destinationsleverans {#destination-delivery}

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authenticationRule` | Sträng | Anger hur [!DNL Platform]-kunder ansluter till ditt mål. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du skulle till exempel välja det här alternativet om du även valde `authType: OAUTH2` eller `authType:BEARER` i `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av konfigurationen [Credentials](./credentials-configuration.md). </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationServerId` | Sträng | `instanceId` för [målserverkonfigurationen](./destination-server-api.md) som används för det här målet. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`:  [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`:  [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |

## Konfiguration av segmentmappning {#segment-mapping}

![Konfigurationsavsnitt för segmentmappning](./assets/segment-mapping-configuration.png)

Det här avsnittet av målkonfigurationen gäller hur segmentmetadata, som segmentnamn eller ID:n, ska delas mellan Experience Platform och målet.

Genom `audienceTemplateId` knyter det här avsnittet även samman den här konfigurationen med [konfigurationen av målgruppsmetadata](./audience-metadata-management.md).

Parametrarna som visas i konfigurationen ovan beskrivs i [API-referens för målslutpunkt](./destination-configuration-api.md).

## Samlingsprincip {#aggregation}

![Samlingsprincip i konfigurationsmallen](./assets/aggregation-configuration.png)

I det här avsnittet kan du ange de sammanställningsprofiler som Experience Platform ska använda när data exporteras till ditt mål.

En sammanställningsprofil avgör hur de exporterade profilerna kombineras i dataexporten. Tillgängliga alternativ är:
* Bästa ansträngningsaggregering
* Konfigurerbar aggregering (visas i konfigurationen ovan)

### Bästa ansträngningsaggregering {#best-effort-aggregation}

>[!TIP]
>
>Använd det här alternativet om API-slutpunkten accepterar färre än 100 profiler per API-anrop.

Det här alternativet fungerar bäst för destinationer som föredrar färre profiler per begäran och som hellre vill ta fler förfrågningar med mindre data än mindre förfrågningar med mer data.

Använd parametern `maxUsersPerRequest` för att ange det maximala antalet profiler som ditt mål kan ta i en begäran.

### Konfigurerbar aggregering {#configurable-aggregation}

Det här alternativet fungerar bäst om du hellre vill ta stora grupper med tusentals profiler på samma samtal. Med det här alternativet kan du också sammanfoga de exporterade profilerna baserat på komplexa sammanställningsregler.

Med det här alternativet kan du:
* Ange maximal tid och maximalt antal profiler som ska samlas innan ett API-anrop görs till målet.
* Sammanställ de exporterade profilerna som är mappade till målet baserat på:
   * segment-ID
   * segmentstatus
   * identitet eller grupper av identiteter

Detaljerade förklaringar av aggregeringsparametrarna finns på [API-målets slutpunktsåtgärder](./destination-configuration-api.md) referenssida, där varje parameter beskrivs.

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
