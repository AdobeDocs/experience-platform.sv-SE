---
description: Lär dig hur du konfigurerar inställningar för filexport för mål som skapats med Destination SDK.
title: Batchkonfiguration
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Batchkonfiguration {#batch-configuration}

Använd alternativen för gruppkonfiguration i Destination SDK för att låta användare anpassa namnen på de exporterade filerna och för att konfigurera exportschemat efter sina önskemål.

När du skapar filbaserade mål via Destination SDK kan du konfigurera standardprogram för filnamngivning och -export, eller så kan du ge användarna möjlighet att konfigurera inställningarna från Experience Platform användargränssnitt. Du kan till exempel konfigurera beteenden som:

* Inkludera specifik information i filnamnet, till exempel målgrupps-ID, mål-ID:n eller anpassad information.
* Användare kan anpassa filnamnet i Experience Platform-gränssnittet.
* Konfigurera filexporten så att den sker i angivna tidsintervall.
* Definiera vilka alternativ för filnamngivning och anpassning av exportschema som användarna kan se i Experience Platform användargränssnitt.

Batchkonfigurationsinställningarna ingår i målkonfigurationen för filbaserade mål.

Mer information om var den här komponenten passar in i en integrering som skapats med Destination SDK finns i diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller i guiden om hur du [använder Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Du kan konfigurera inställningarna för filnamngivning och exportschema via slutpunkten `/authoring/destinations`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla gruppkonfigurationsalternativ som stöds och som du kan använda för ditt mål. Artikeln innehåller även information om vad kunderna kommer att se i användargränssnittet för Experience Platform.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Nej |
| Filbaserade (batch) integreringar | Ja |

## parametrar som stöds {#supported-parameters}

Värdena som du anger här visas i steget [Schemalägg målexport](../../../ui/activate-batch-profile-destinations.md#scheduling) i det filbaserade arbetsflödet för målaktivering.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   "segmentGroupingEnabled": true
   }
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolean | Ange som `true` så att kunderna kan ange vilka profilattribut som är obligatoriska. Standardvärdet är `false`. Mer information finns i [Obligatoriska attribut](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Boolean | Ange som `true` så att kunderna kan ange dedupliceringsnycklar. Standardvärdet är `false`.  Mer information finns i [Dedupliceringsnycklar](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Enum | Definierar standardläget för filexport. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Standardvärdet är `DAILY_FULL_EXPORT`. Mer information om schemaläggning av filexport finns i [dokumentationen för batchaktivering](../../../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Lista | Definierar vilka filexportlägen som är tillgängliga för kunderna. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Definierar den filexportfrekvens som är tillgänglig för kunder. Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definierar standardexportfrekvensen för filer.Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Standardvärdet är `DAILY`. |
| `defaultStartTime` | Sträng | Definierar standardstarttiden för filexporten. Använder 24-timmars filformat. Standardvärdet är &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Sträng | *Krävs*. Lista över tillgängliga filnamnsmappar som användare kan välja mellan. Detta avgör vilka objekt som läggs till i de exporterade filnamnen (målgrupps-ID, organisationsnamn, exportdatum och exporttid med mera). När du anger `defaultFilename` bör du se till att du inte duplicerar makron. <br><br>Värden som stöds: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Oavsett i vilken ordning du definierar makrona visas de alltid i den ordning som de visas här. <br><br> Om `defaultFilename` är tom måste listan `allowedFilenameAppendOptions` innehålla minst ett makro. |
| `filenameConfig.defaultFilenameAppendOptions` | Sträng | *Krävs*. Förvalda standardmakron för filnamn som användare kan avmarkera.<br><br> Makrona i den här listan är en delmängd av de som definieras i `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Sträng | *Valfritt*. Definierar standardmakron för filnamn för de exporterade filerna. Användarna kan inte skriva över dem. <br><br>Alla makron som definieras av `allowedFilenameAppendOptions` läggs till efter makrona `defaultFilename`. <br><br>Om `defaultFilename` är tomt måste du definiera minst ett makro i `allowedFilenameAppendOptions`. |
| `segmentGroupingEnabled` | Boolean | Definierar om de aktiverade målgrupperna ska exporteras i en eller flera filer, baserat på målgruppens [sammanfogningsprincip](../../../../profile/merge-policies/overview.md). Värden som stöds: <ul><li>`true`: exporterar en fil per sammanfogningsprincip.</li><li>`false`: exporterar en fil per målgrupp, oavsett kopplingsprofilen. Detta är standardbeteendet. Du kan uppnå samma resultat genom att helt utelämna den här parametern.</li></ul> |

{style="table-layout:auto"}

## Filnamnskonfiguration {#file-name-configuration}

Använd konfigurationsmakron för filnamn för att definiera vad de exporterade filnamnen ska innehålla. Makrona i tabellen nedan beskriver element som finns i gränssnittet på skärmen [filnamnskonfiguration](../../../ui/activate-batch-profile-destinations.md#file-names).

>[!TIP]
> 
>Du bör alltid inkludera makrot `SEGMENT_ID` i de exporterade filnamnen. Segment-ID:n är unika, så om du tar med dem i filnamnet är det bästa sättet att se till att filnamnen också är unika.

| Makro | Gränssnittsetikett | Beskrivning | Exempel |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Målnamn i användargränssnittet. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment ID] | Unikt, Experience Platform-genererat målgrupps-ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segment Name] | Användardefinierat publiknamn | VIP subscriber |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Destination ID] | Unikt, Experience Platform-genererat ID för målinstansen | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Destination Name] | Användardefinierat namn för målinstansen. | Mål för My 2022 Advertising |
| `ORGANIZATION_NAME` | [!UICONTROL Organization Name] | Namn på kundorganisationen i Adobe Experience Platform. | Organisationsnamn |
| `SANDBOX_NAME` | [!UICONTROL Sandbox Name] | Namn på den sandlåda som används av kunden. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date and time] | `DATETIME` och `TIMESTAMP` definierar båda när filen skapades, men i olika format. <br><br><ul><li>`DATETIME` har följande format: YYYMMDD_HMMSS.</li><li>`TIMESTAMP` använder det 10-siffriga Unix-formatet. </li></ul> `DATETIME` och `TIMESTAMP` kan inte användas samtidigt. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Custom text] | Användardefinierad egen text som ska inkluderas i filnamnet. Kan inte användas i `defaultFilename`. | Min_egen_text |
| `TIMESTAMP` | [!UICONTROL Date and time] | 10-siffrig tidsstämpel i Unix-format för den tid då filen skapades. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL Merge Policy ID] | ID för [sammanfogningsprincipen](../../../../profile/merge-policies/overview.md) som används för att generera den exporterade målgruppen. Använd det här makrot när du grupperar exporterade målgrupper i filer, baserat på kopplingsprofilen. Använd makrot tillsammans med `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Merge Policy Name] | Namnet på [sammanfogningsprincipen](../../../../profile/merge-policies/overview.md) som används för att generera den exporterade målgruppen. Använd det här makrot när du grupperar exporterade målgrupper i filer, baserat på kopplingsprofilen. Använd makrot tillsammans med `segmentGroupingEnabled:true`. | Min egen sammanfogningsprincip |

{style="table-layout:auto"}

### Exempel på filnamnskonfiguration

I konfigurationsexemplet nedan visas korrespondensen mellan konfigurationen som används i API-anropet och alternativen som visas i användargränssnittet.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![Gränssnittsbild som visar konfigurationsskärmen för filnamn med förvalda makron](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur du kan konfigurera filnamnsscheman och exportscheman för dina filbaserade mål.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Konfiguration av kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
