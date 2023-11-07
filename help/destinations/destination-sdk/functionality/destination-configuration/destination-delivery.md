---
description: Lär dig hur du konfigurerar destinationsleveransinställningarna för mål som skapats med Destination SDK, för att ange var exporterade data ska skickas och vilken autentiseringsregel som används på den plats där data ska landas.
title: Destinationsleverans
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Destinationsleverans

Om du vill ha större kontroll över var data som exporteras till destinationen hamnar kan du med Destination SDK ange inställningar för destinationsleverans.

Målleveransavsnittet anger var exporterade data skickas och vilken autentiseringsregel som används på den plats där data kommer att landas.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se följande sidor med översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Du kan konfigurera inställningar för destinationsleverans via `/authoring/destinations` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla målleveransalternativ som stöds och som du kan använda för ditt mål.

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

När du konfigurerar inställningarna för destinationsleverans kan du använda de parametrar som beskrivs i tabellen nedan för att definiera var exporterade data ska skickas.

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authenticationRule` | Sträng | Anger hur [!DNL Platform] ska ansluta till ditt mål. Värden som stöds:<ul><li>`CUSTOMER_AUTHENTICATION`: Använd det här alternativet om plattformskunder loggar in på ditt system via någon av de autentiseringsmetoder som beskrivs [här](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Använd det här alternativet om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [API för autentiseringsuppgifter](../../credentials-api/create-credential-configuration.md) konfiguration. </li><li>`NONE`: Använd det här alternativet om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationServerId` | Sträng | The `instanceId` i [målserver](../../authoring-api/destination-server/create-destination-server.md) som du vill exportera data till. |
| `deliveryMatchers.type` | Sträng | <ul><li>När destinationsleverans konfigureras för filbaserade mål ska detta alltid anges som `SOURCE`.</li><li>När destinationsleveransen konfigureras för ett direktuppspelningsmål `deliveryMatchers` -avsnittet är inte obligatoriskt.</li></ul> |
| `deliveryMatchers.value` | Sträng | <ul><li>När destinationsleverans konfigureras för filbaserade mål ska detta alltid anges som `batch`.</li><li>När destinationsleveransen konfigureras för ett direktuppspelningsmål `deliveryMatchers` -avsnittet är inte obligatoriskt.</li></ul> |

{style="table-layout:auto"}

## Inställningar för destinationsleverans för direktuppspelningsmål {#destination-delivery-streaming}

I exemplet nedan visas hur leveransinställningarna för målet ska konfigureras för ett direktuppspelningsmål. Observera att `deliveryMatchers` -avsnittet krävs inte för direktuppspelningsmål.

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

I exemplet nedan visas hur leveransinställningarna för målet ska konfigureras för ett filbaserat mål. Observera att `deliveryMatchers` -avsnittet krävs för filbaserade mål.

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
* [OAuth2-autentisering](oauth2-authorization.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Kunddatafält](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
