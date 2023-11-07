---
description: Lär dig hur du konfigurerar målidentiteter som stöds för mål som skapats med Destination SDK.
title: Konfiguration av namnutrymme för identitet
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 1%

---

# Konfiguration av namnutrymme för identitet

Experience Platform använder ID-namnutrymmen för att beskriva typen av specifika identiteter. Ett identitetsnamnutrymme som till exempel kallas `Email` identifierar ett värde `name@email.com` som en e-postadress.

När du skapar ett mål via Destination SDK, förutom [konfigurera ett partnerschema](schema-configuration.md) som användare kan mappa profilattribut och identiteter till, kan du även definiera de identitetsnamnutrymmen som stöds av målplattformen.

När du gör det kan användarna välja målidentiteter, förutom målprofilsattribut, utöver målprofilsattributen.

Mer information om identitetsnamnutrymmen i Experience Platform finns i [dokumentation för identitetsnamnutrymmen](../../../../identity-service/namespaces.md).

När du konfigurerar identitetsnamnutrymmen för målet kan du finjustera den målidentitetsmappning som stöds av målet, till exempel:

* Användare kan mappa XDM-attribut till identitetsnamnutrymmen.
* Tillåta användare att mappa [standardidentitetsnamnutrymmen](../../../../identity-service/namespaces.md#standard) till dina egna ID-namnutrymmen.
* Tillåta användare att mappa [namnutrymmen för anpassad identitet](../../../../identity-service/namespaces.md#manage-namespaces) till dina egna ID-namnutrymmen.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Du kan konfigurera identitetsnamnutrymmen som stöds via `/authoring/destinations` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla konfigurationsalternativ för identitetsnamn som stöds och som du kan använda för ditt mål. Dessutom visas vad kunderna kommer att se i plattformsgränssnittet.

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

När du definierar de målidentiteter som målet stöder kan du använda parametrarna som beskrivs i tabellen nedan för att konfigurera deras beteende.

| Parameter | Typ | Obligatoriskt/valfritt | Beskrivning |
|---------|----------|---|------|
| `acceptsAttributes` | Boolean | Valfritt | Anger om kunder kan mappa standardprofilattribut till identiteten som du konfigurerar. |
| `acceptsCustomNamespaces` | Boolean | Valfritt | Anger om kunderna kan mappa anpassade ID-namnutrymmen till det ID-namnutrymme som du konfigurerar. |
| `acceptedGlobalNamespaces` | – | Valfritt | Anger vilken [standardidentitetsnamnutrymmen](../../../../identity-service/namespaces.md#standard) (till exempel [!UICONTROL IDFA]) kan kunderna mappa till identiteten som du konfigurerar. |
| `transformation` | Sträng | Valfritt | Visar [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) -kryssrutan i plattformsgränssnittet när källfältet är antingen ett XDM-attribut eller ett anpassat identitetsnamnutrymme. Använd det här alternativet om du vill att användare ska kunna hash-koda källattribut vid export. Om du vill aktivera det här alternativet anger du värdet till `sha256(lower($))`. |
| `requiredTransformation` | Sträng | Valfritt | När kunderna väljer det här namnutrymmet för källidentiteten [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) kryssrutan tillämpas automatiskt på mappningen och kunderna kan inte inaktivera den. Om du vill aktivera det här alternativet anger du värdet till `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Du måste ange vilken [!DNL Platform] identiteter som kunder kan exportera till ditt mål. Några exempel är [!DNL Experience Cloud ID], hashad e-post, enhets-ID ([!DNL IDFA], [!DNL GAID]). Dessa värden är [!DNL Platform] ID-namnutrymmen som kunder kan mappa till identitetsnamnutrymmen från destinationen.

Identitetsnamnutrymmen kräver ingen 1-till-1-korrespondens mellan [!DNL Platform] och destinationen.
Kunder kan till exempel mappa en [!DNL Platform] [!DNL IDFA] namnutrymme till ett [!DNL IDFA] namnutrymme från målet eller så kan de mappa samma [!DNL Platform] [!DNL IDFA] namnutrymme till en [!DNL Customer ID] namnutrymme i målet.

Läs mer om identiteter i [Översikt över namnutrymmet identity](../../../../identity-service/namespaces.md).

## Mappningsöverväganden

Om kunderna väljer ett namnutrymme för källidentiteten och inte väljer någon målmappning, fyller Platform automatiskt i målmappningen med ett attribut med samma namn.

## Konfigurera hash för valfritt källfält

Experience Platform-kunder kan välja att importera data till plattformen i hash-format eller i vanlig text. Om målplattformen godkänner både hash-kodade och ohashade data kan du ge kunderna möjlighet att välja om Platform ska hash-koda källfältets värden när de exporteras till destinationen.

Konfigurationen nedan aktiverar det valfria [Använd omformning](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) i plattformsgränssnittet i mappningssteget.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Markera det här alternativet om du vill att Adobe Experience Platform automatiskt ska hash-koda dem vid aktiveringen när du använder ohashed-källfält.

När du mappar ohashade källattribut till målattribut som målet förväntar sig ska hash-kodas (till exempel: `email_lc_sha256` eller `phone_sha256`), kontrollera **Använd omformning** att Adobe Experience Platform automatiskt ska hash-koda källattributen vid aktiveringen.

## Konfigurera hash för obligatoriskt källfält

Om målet bara godtar hash-kodade data kan du konfigurera de exporterade attributen så att de hashas automatiskt av Platform. Konfigurationen nedan kontrollerar automatiskt **Använd omformning** när `Email` och `Phone` identiteter mappas.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du ha en bättre förståelse för hur du konfigurerar identitetsnamnutrymmen för mål som skapats med Destination SDK.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
