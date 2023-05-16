---
description: Lär dig konfigurera inställningar för målgruppsmetadata för mål som skapats med Destination SDK.
title: Konfiguration av målgruppsmetadata
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---


# Konfiguration av målgruppsmetadata

När du exporterar data från Experience Platform till destinationen kan du behöva särskilda målgruppsmetadata, som segmentnamn eller segment-ID:n, för att kunna delas mellan Experience Platform och destinationen.

Destination SDK innehåller verktyg som du kan använda för att skapa, uppdatera eller ta bort målgrupper programmatiskt på målplattformen.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-destination-configuration).

Du kan konfigurera metadatamallen för målgruppen via `/authoring/audience-templates` slutpunkt. När du har skapat konfigurationen av målgruppsmetadata kan du använda `/authoring/destinations` slutpunkt för att konfigurera `audienceMetadataConfig` -avsnitt. I det här avsnittet anges vilka segmentmetadata som ska mappas till målgruppsmallen.

På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Skapa en målgruppsmall](../../metadata-api/create-audience-template.md)
* [Uppdatera en målgruppsmall](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## Parametrar som stöds {#supported-parameters}

När du skapar din konfiguration av målgruppsmetadata kan du använda parametrarna som beskrivs i tabellen nedan för att konfigurera inställningarna för segmentmappning.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolean | Anger om [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) värdet i målaktiveringsarbetsflödet ska vara Experience Platform-segmentnamnet. |
| `mapExperiencePlatformSegmentId` | Boolean | Anger om [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) i målaktiveringsarbetsflödet ska vara Experience Platform segment-ID. |
| `mapUserInput` | Boolean | Aktiverar eller inaktiverar användarindata för [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) i målaktiveringsarbetsflödet. Om inställt på `true`, `audienceTemplateId` kan inte finnas. |
| `audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](../../metadata-api/create-audience-template.md) används för ditt mål. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du ha en bättre förståelse för hur du kan konfigurera målgruppsmetadata för ditt mål.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Konfiguration av kundautentisering](customer-authentication.md)
* [OAuth2-autentisering](oauth2-authentication.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)