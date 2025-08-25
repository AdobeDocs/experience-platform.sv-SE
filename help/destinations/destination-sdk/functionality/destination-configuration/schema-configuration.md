---
description: Lär dig hur du konfigurerar partnerschemat för mål som skapats med Destination SDK.
title: Konfiguration av partnerschema
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 0%

---

# Konfiguration av partnerschema

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. När data hämtas till Experience Platform är de strukturerade enligt ett XDM-schema. Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [Grunderna för schemakomposition](../../../../xdm/schema/composition.md).

När du skapar ett mål med Destination SDK kan du definiera ett eget partnerschema som ska användas av målplattformen. Detta gör det möjligt för användare att mappa profilattribut från Experience Platform till specifika fält som kan identifieras av målplattformen, allt i Experience Platform användargränssnitt.

När du konfigurerar partnerschemat för målet kan du finjustera den fältmappning som stöds av målplattformen, till exempel:

* Tillåt användare att mappa ett `phoneNumber` XDM-attribut till ett `phone`-attribut som stöds av målplattformen.
* Skapa dynamiska partnerscheman som Experience Platform kan anropa dynamiskt för att hämta en lista över alla attribut som stöds i ditt mål.
* Definiera obligatoriska fältmappningar som målplattformen kräver.

Mer information om var den här komponenten passar in i en integrering som skapats med Destination SDK finns i diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller i guiden om hur du [använder Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Du kan konfigurera schemainställningarna via slutpunkten `/authoring/destinations`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla schemakonfigurationsalternativ som stöds och som du kan använda för ditt mål. Här visas vad kunderna kommer att se i användargränssnittet för Experience Platform.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## Schemakonfiguration som stöds {#supported-schema-types}

Destination SDK stöder flera schemakonfigurationer:

* Statiska scheman definieras via arrayen `profileFields` i avsnittet `schemaConfig`. I ett statiskt schema definierar du alla målattribut som ska visas i Experience Platform-gränssnittet i `profileFields`-arrayen. Om du behöver uppdatera ditt schema måste du [uppdatera målkonfigurationen](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Dynamiska scheman använder en ytterligare målservertyp, som kallas [dynamisk schemaserver](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), för att dynamiskt hämta de målattribut som stöds och generera scheman baserat på ditt eget API. Dynamiska scheman använder inte `profileFields`-arrayen. Om du behöver uppdatera schemat behöver du inte [uppdatera målkonfigurationen](../../authoring-api/destination-configuration/update-destination-configuration.md). I stället hämtar den dynamiska schemaservern det uppdaterade schemat från ditt API.
* I schemakonfigurationen kan du lägga till obligatoriska (eller fördefinierade) mappningar. Det här är mappningar som användare kan visa i Experience Platform-gränssnittet, men de kan inte ändra dem när de konfigurerar en anslutning till ditt mål. Du kan t.ex. framtvinga att e-postadressfältet alltid skickas till målet.

Avsnittet `schemaConfig` använder flera konfigurationsparametrar, beroende på vilken typ av schema du behöver, vilket visas i avsnitten nedan.

## Skapa ett statiskt schema {#attributes-schema}

Om du vill skapa ett statiskt schema med profilattribut definierar du målattributen i `profileFields`-arrayen enligt nedan.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---------|----------|------|---|
| `profileFields` | Array | Valfritt | Definierar den array med målattribut som accepteras av målplattformen och som kunderna kan mappa sina profilattribut till. När du använder en `profileFields`-array kan du helt utelämna parametern `useCustomerSchemaForAttributeMapping`. |
| `useCustomerSchemaForAttributeMapping` | Boolean | Valfritt | Aktiverar eller inaktiverar mappningen av attribut från kundschemat till de attribut som du definierar i `profileFields`-arrayen. <ul><li>Om värdet är `true` kan användarna bara se källkolumnen i mappningsfältet. `profileFields` kan inte användas i det här fallet.</li><li>Om värdet är `false` kan användare mappa källattribut från sitt schema till de attribut du definierade i `profileFields`-arrayen.</li></ul> Standardvärdet är `false`. |
| `profileRequired` | Boolean | Valfritt | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målplattformen. |
| `segmentRequired` | Boolean | Obligatoriskt | Den här parametern krävs av Destination SDK och ska alltid anges till `true`. |
| `identityRequired` | Boolean | Obligatoriskt | Ange som `true` om användare ska kunna mappa [identitetstyper](identity-namespace-configuration.md) från Experience Platform till de attribut du definierade i arrayen `profileFields` . |
| `segmentNamespaceAllowList` | Array | Valfritt | Tillåter användare att endast mappa målgrupper från de målgruppsnamnutrymmen som definieras i arrayen till målet. <br><br> Användning av den här parametern rekommenderas inte i de flesta fall. Använd i stället `"segmentNamespaceDenyList":[]` för att tillåta att alla typer av målgrupper exporteras till ditt mål. <br><br> Om både `segmentNamespaceAllowList` och `segmentNamespaceDenyList` saknas i konfigurationen kan användarna bara exportera målgrupper som kommer från [segmenteringstjänsten](../../../../segmentation/home.md). <br><br>`segmentNamespaceAllowList` och `segmentNamespaceDenyList` utesluter varandra. |
| `segmentNamespaceDenyList` | Array | Valfritt | Begränsar användare från att mappa målgrupper från de målgruppsnamnutrymmen som definieras i arrayen till målet. <br><br>Adobe rekommenderar att alla målgrupper, oavsett ursprung, kan exporteras genom att ställa in `"segmentNamespaceDenyList":[]`. <br><br>**Viktigt!** Om du inte anger `segmentNamespaceDenyList` i `schemaConfig` och du inte använder `segmentNamespaceAllowList`, ställs `segmentNamespaceDenyList` in automatiskt på `[]`. Detta förhindrar att man förlorar sina egna målgrupper i framtiden. Av säkerhetsskäl rekommenderar Adobe att du uttryckligen anger `"segmentNamespaceDenyList":[]` i din konfiguration. <br><br>`segmentNamespaceAllowList` och `segmentNamespaceDenyList` utesluter varandra. |

{style="table-layout:auto"}

Den slutliga användarupplevelsen visas i bilderna nedan.

När användarna väljer målmappning kan de se fälten som definierats i `profileFields`-arrayen.

![Gränssnittsbild som visar skärmen för målattribut.](../../assets/functionality/destination-configuration/select-attributes.png)

När attributen har markerats kan de se dem i målfältskolumnen.

![Användargränssnittsbilden visar ett statiskt målschema med attribut](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Skapa ett dynamiskt schema {#dynamic-schema-configuration}

Destination SDK stöder skapandet av dynamiska partnerscheman. I motsats till ett statiskt schema använder inte ett dynamiskt schema en `profileFields`-matris. I stället använder dynamiska scheman en dynamisk schemaserver som ansluter till din egen API från den plats där schemakonfigurationen hämtas.

>[!IMPORTANT]
>
>Innan du skapar ett dynamiskt schema måste du [skapa en dynamisk schemaserver](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

I en dynamisk schemakonfiguration ersätts `profileFields`-arrayen av avsnittet `dynamicSchemaConfig`, vilket visas nedan.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Sträng | Obligatoriskt | Anger hur [!DNL Experience Platform]-kunder ansluter till ditt mål. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om Experience Platform-kunder loggar in på ditt system via någon av de autentiseringsmetoder som beskrivs [här](customer-authentication.md). </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och kunden [!DNL Experience Platform] inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du [skapa ett autentiseringsobjekt](../../credentials-api/create-credential-configuration.md) med hjälp av API:t för autentiseringsuppgifter och skicka ID:t för autentiseringsuppgiftsobjektet i parametern `authenticationId` i konfigurationen för [målleverans](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication). </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `dynamicEnum.destinationServerId` | Sträng | Obligatoriskt | `instanceId` för din dynamiska schemaserver. Målservern innehåller API-slutpunkten som Experience Platform anropar för att hämta det dynamiska schemat. |
| `dynamicEnum.value` | Sträng | Obligatoriskt | Namnet på det dynamiska schemat, enligt definitionen i den dynamiska schemaserverkonfigurationen. |
| `dynamicEnum.responseFormat` | Sträng | Obligatoriskt | Alltid inställt på `SCHEMA` när ett dynamiskt schema definieras. |
| `profileRequired` | Boolean | Valfritt | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målplattformen. |
| `segmentRequired` | Boolean | Obligatoriskt | Den här parametern krävs av Destination SDK och ska alltid anges till `true`. |
| `identityRequired` | Boolean | Obligatoriskt | Ange som `true` om användare ska kunna mappa [identitetstyper](identity-namespace-configuration.md) från Experience Platform till de attribut du definierade i arrayen `profileFields` . |

{style="table-layout:auto"}

## Obligatoriska mappningar {#required-mappings}

I schemakonfigurationen kan du, förutom ditt statiska eller dynamiska schema, lägga till nödvändiga (eller fördefinierade) mappningar. Det här är mappningar som användare kan visa i Experience Platform-gränssnittet, men de kan inte ändra dem när de konfigurerar en anslutning till ditt mål.

Du kan t.ex. framtvinga att e-postadressfältet alltid skickas till målet.

>[!NOTE]
>
>Följande kombinationer av obligatoriska mappningar stöds för närvarande:
>* Du kan konfigurera ett obligatoriskt källfält och ett obligatoriskt målfält. I det här fallet kan användare inte redigera eller markera något av de två fälten och bara visa markeringen.
>* Du kan bara konfigurera ett obligatoriskt målfält. I det här fallet kan användarna välja ett källfält som ska kopplas till målet.
>
> Det går för närvarande inte att konfigurera endast ett obligatoriskt källfält *och*.

Se två exempel nedan på en schemakonfiguration med obligatoriska mappningar och hur dessa ser ut i mappningssteget i [arbetsflödet för att aktivera data till batchmål](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Krävda käll- och målmappningar]

I exemplet nedan visas både obligatoriska käll- och målmappningar. När både käll- och målfält anges som obligatoriska mappningar kan användare inte markera eller redigera något av de två fälten och bara visa den fördefinierade markeringen.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---|---|---|---|
| `requiredMappingsOnly` | Boolean | Valfritt | Om värdet är true kan användare inte mappa andra attribut och identiteter i aktiveringsflödet, förutom de nödvändiga mappningarna som du definierar i `requiredMappings`-arrayen. |
| `requiredMappings.sourceType` | Sträng | Obligatoriskt | Anger typen för fältet `source`. Värden som stöds: <ul><li>`text/x.schema-path`: Använd det här värdet när fältet `source` är ett profilattribut från ett XDM-schema.</li><li>`text/x.aep-xl`: Använd det här värdet när fältet `source` definieras av ett reguljärt uttryck. Exempel: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Använd det här värdet när fältet `source` definieras av en makromall. Den enda makromall som stöds är `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Sträng | Obligatoriskt | Anger värdet för källfältet. Värdetyper som stöds: <ul><li>XDM-profilattribut. Exempel: `personalEmail.address`. När källattributet är ett XDM-profilattribut anger du parametern `sourceType` till `text/x.schema-path`.</li><li>Reguljära uttryck. Exempel: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. När källattributet är ett reguljärt uttryck anger du parametern `sourceType` till `text/x.aep-xl`.</li><li>Makromallar. Exempel:`metadata.segment.alias`. När källattributet är en makromall ställer du in parametern `sourceType` på `text/plain`. Den enda makromall som stöds är `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Sträng | Obligatoriskt | Anger målfältets värde. När både käll- och målfält har angetts som obligatoriska mappningar kan användare inte markera eller redigera något av de två fälten och bara visa markeringen. |

{style="table-layout:auto"}

Därför är både **[!UICONTROL Source field]**- och **[!UICONTROL Target field]**-avsnitten i Experience Platform-gränssnittet nedtonade.

![Bild av nödvändiga mappningar i gränssnittets aktiveringsflöde.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Obligatorisk målmappning]

I exemplet nedan visas en nödvändig målmappning. Om bara målfältet anges som obligatoriskt kan användarna välja vilket källfält som ska kopplas till det.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---|---|---|---|
| `requiredMappingsOnly` | Boolean | Valfritt | Om värdet är true kan användare inte mappa andra attribut och identiteter i aktiveringsflödet, förutom de nödvändiga mappningarna som du definierar i `requiredMappings`-arrayen. |
| `requiredMappings.destination` | Sträng | Obligatoriskt | Anger målfältets värde. När endast målfältet är angivet kan användarna välja ett källfält som ska kopplas till målet. |
| `mandatoryRequired` | Boolean | Valfritt | Anger om mappningen ska markeras som ett [obligatoriskt attribut](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Boolean | Valfritt | Anger om mappningen ska markeras som en [dedupliceringsnyckel](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Därför är **[!UICONTROL Target field]**-avsnittet i Experience Platform-användargränssnittet nedtonat, medan **[!UICONTROL Source field]**-avsnittet är aktivt och användarna kan interagera med det. Alternativen **[!UICONTROL Mandatory key]** och **[!UICONTROL Deduplication key]** är aktiva, och användare kan inte ändra dem.

![Bild av nödvändiga mappningar i gränssnittets aktiveringsflöde.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Konfigurera stöd för externa målgrupper {#external-audiences}

Om du vill konfigurera målet så att det stöder aktivering av [externt genererade målgrupper](../../../../segmentation/ui/audience-portal.md#import-audience) inkluderar du fragmentet nedan i avsnittet `schemaConfig`.

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

Mer information om funktionen [ finns i egenskapsbeskrivningarna i ](#attributes-schema)tabellen`segmentNamespaceDenyList` ovan på den här sidan.

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vilka schematyper som stöds av Destination SDK och hur du kan konfigurera ditt schema.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Kunddatafält](customer-data-fields.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
