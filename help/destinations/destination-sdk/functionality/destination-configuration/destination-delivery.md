---
description: Lär dig hur du konfigurerar leveransinställningar för mål som skapats med Destination SDK för att ange var exporterade data ska skickas och vilken autentiseringsregel som används på den plats där data ska landas.
title: Destinationsleverans
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Destinationsleverans

Om du vill ha större kontroll över var data som exporteras till destinationen hamnar, kan du ange inställningar för destinationsleverans i Destination SDK.

Målleveransavsnittet anger var exporterade data skickas och vilken autentiseringsregel som används på den plats där data kommer att landas.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Om du vill veta var den här komponenten passar in i en integrering som skapats med Destination SDK kan du läsa diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller följande sidor med en översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Du kan konfigurera inställningar för destinationsleverans via slutpunkten `/authoring/destinations`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla målleveransalternativ som stöds och som du kan använda för ditt mål.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## parametrar som stöds {#supported-parameters}

När du konfigurerar inställningarna för destinationsleverans kan du använda de parametrar som beskrivs i tabellen nedan för att definiera var exporterade data ska skickas.

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authenticationRule` | Sträng | Anger hur [!DNL Experience Platform] ska ansluta till ditt mål. Värden som stöds:<ul><li>`CUSTOMER_AUTHENTICATION`: Använd det här alternativet om Experience Platform-kunder loggar in på ditt system med någon av de autentiseringsmetoder som beskrivs [här](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Använd det här alternativet om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och kunden [!DNL Experience Platform] inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av [API:t för autentiseringsuppgifter](../../credentials-api/create-credential-configuration.md)-konfigurationen. </li><li>`NONE`: Använd det här alternativet om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationServerId` | Sträng | `instanceId` för den [målserver](../../authoring-api/destination-server/create-destination-server.md) som du vill exportera data till. |
| `deliveryMatchers.type` | Sträng | <ul><li>När målleverans konfigureras för filbaserade mål ska du alltid ange det här till `SOURCE`.</li><li>När destinationsleveransen konfigureras för ett direktuppspelningsmål krävs inte avsnittet `deliveryMatchers`.</li></ul> |
| `deliveryMatchers.value` | Sträng | <ul><li>När målleverans konfigureras för filbaserade mål ska du alltid ange det här till `batch`.</li><li>När destinationsleveransen konfigureras för ett direktuppspelningsmål krävs inte avsnittet `deliveryMatchers`.</li></ul> |

{style="table-layout:auto"}

## Inställningar för destinationsleverans för direktuppspelningsmål {#destination-delivery-streaming}

I exemplet nedan visas hur leveransinställningarna för målet ska konfigureras för ett direktuppspelningsmål. Observera att avsnittet `deliveryMatchers` inte krävs för direktuppspelningsmål.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Inställningar för destinationsleverans för filbaserade destinationer {#destination-delivery-file-based}

I exemplet nedan visas hur leveransinställningarna för målet ska konfigureras för ett filbaserat mål. Observera att avsnittet `deliveryMatchers` krävs för filbaserade mål.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur du kan konfigurera de platser där målet ska exportera data, både för direktuppspelning och filbaserade mål.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Kunddatafält](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
