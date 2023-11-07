---
description: Lär dig konfigurera inställningar för målgruppsmetadata för mål som skapats med Destination SDK.
title: Konfiguration av målgruppsmetadata
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Konfiguration av målgruppsmetadata

När du exporterar data från Experience Platform till målplatsen kan du behöva särskilda målgruppsmetadata, som målgruppsnamn eller målgrupps-ID:n, för att kunna delas mellan Experience Platform och målplatsen.

Destination SDK innehåller verktyg som du kan använda för att skapa, uppdatera eller ta bort målgrupper programmatiskt på målplattformen.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-destination-configuration).

Du kan konfigurera metadatamallen för målgruppen via `/authoring/audience-templates` slutpunkt. När du har skapat en konfiguration för målgruppsmetadata kan du använda `/authoring/destinations` slutpunkt för att konfigurera `audienceMetadataConfig` -avsnitt. I det här avsnittet anges vilka målgruppsmetadata som ska mappas till målgruppsmallen.

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

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## parametrar som stöds {#supported-parameters}

När du skapar din konfiguration för målgruppsmetadata kan du använda de parametrar som beskrivs i tabellen nedan för att konfigurera inställningarna för målgruppsmappning.

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
| `mapExperiencePlatformSegmentName` | Boolean | Anger om [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) värdet i målaktiveringsarbetsflödet ska vara Experience Platform målgruppsnamnet. |
| `mapExperiencePlatformSegmentId` | Boolean | Anger om [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) värdet i målaktiveringsarbetsflödet ska vara Experience Platform målgrupps-ID. |
| `mapUserInput` | Boolean | Aktiverar eller inaktiverar användarindata för [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) i målaktiveringsarbetsflödet. Om inställt på `true`, `audienceTemplateId` kan inte finnas. |
| `audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](../../metadata-api/create-audience-template.md) används för ditt mål. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du ha en bättre förståelse för hur du kan konfigurera målgruppsmetadata för ditt mål.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Konfiguration av kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
