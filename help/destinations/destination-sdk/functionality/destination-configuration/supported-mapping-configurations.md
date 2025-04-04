---
description: Lär dig hur du konfigurerar målet för de identitets- och attributmappningskonfigurationer som stöds.
title: Mappningskonfigurationer som stöds
exl-id: a477a3f2-a229-4b22-8588-ee58bd5436c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Mappningskonfigurationer som stöds

Destinationer som skapats med Destination SDK har stöd för specifika konfigurationer för identitetsnamn och attributmappning, baserat på måltypen.

I den här artikeln beskrivs alla mappningskonfigurationer som stöds och som du kan använda när du konfigurerar målet.

>[!WARNING]
>
>Alla mappningskonfigurationer som inte beskrivs i den här artikeln stöds inte av Destination SDK.

När du skapar ditt mål konfigurerar du ditt schema och dina identitetsnamnutrymmen enligt en av mappningskonfigurationerna som beskrivs på den här sidan.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Mappningar som stöds för direktuppspelningsmål {#streaming-mappings}

Destinationer för realtidsströmning som har byggts med Destination SDK stöder de mappningskonfigurationer som beskrivs i tabellen nedan.

| Source | Målfält |
| --- | --- |
| XDM-attribut | Eget attribut |
| Namnutrymme för identitet | Namnutrymme för identitet |

I konfigurationsexemplet nedan kan kunderna använda båda mappningarna i tabellen ovan.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Mappa XDM-attribut till anpassade attribut {#streaming-xdm-to-custom}

Användare kan mappa attribut från sin XDM-källprofil till anpassade attribut på målsidan.

Användarna måste ange namnet på det anpassade målattributet manuellt när de väljer målfältsmappningen.

![Experience Platform UI-skärmbild som visar val av anpassat attribut.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![Experience Platform UI-skärmbild som visar XDM-attributmappning till anpassade attribut för direktuppspelningsmål.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Mappa identitetsnamnutrymmen till partneridentitetsnamnutrymmen {#streaming-identity-to-identity}

Användare kan mappa anpassade eller globala identitetsnamnutrymmen från Experience Platform till identitetsnamnutrymmen som du har definierat.

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![Experience Platform UI-skärmbild som visar identitetsmappning till identitet för direktuppspelningsmål.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Mappningar som stöds för filbaserade mål {#batch-mappings}

Filbaserade mål som skapats med Destination SDK stöder mappningskonfigurationerna som beskrivs i tabellen nedan. I nästa avsnitt finns detaljerade mappningsexempel.

| Source | Målfält |
| --- | --- |
| XDM-attribut | Attribut/anpassat attribut |
| Namnutrymme för identitet | Attribut/anpassat attribut |
| Namnutrymme för identitet | Namnutrymme för identitet |

I konfigurationsexemplet nedan kan kunderna använda alla mappningar från tabellen ovan.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Mappa XDM-attribut till anpassade attribut {#batch-xdm-to-custom}

Användare kan mappa attribut från sin XDM-källprofil till anpassade attribut på målsidan.

För filbaserade mål fylls målfältet automatiskt i med ett standardattribut med samma namn som källfältet.

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![Experience Platform UI-skärmbild som visar XDM-mappning till anpassade attribut för filbaserade mål.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Användare kan lämna standardnamnet på plats eller ange ett eget attributnamn på urvalsskärmen för målfält.

![Experience Platform UI-skärmbild med anpassad markering av målattribut för filbaserade mål.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Mappa identitetsnamnutrymmen till anpassade attribut {#batch-identity-to-custom}

Användare kan mappa anpassade eller globala identitetsnamnutrymmen från Experience Platform till anpassade attribut på målsidan.

När du väljer ett identitetsnamnutrymme som ett källfält fylls målfältet automatiskt i med ett motsvarande identitetsnamnutrymme. Om du vill ersätta målfältet med ett anpassat attribut måste användaren ange ett anpassat attributnamn på målfältets markeringsskärm.

![Experience Platform UI-skärmbild med anpassad markering av målattribut för filbaserade mål.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![Experience Platform UI-skärmbild som visar identitetsmappning till anpassade attribut för filbaserade mål.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Mappa identitetsnamnutrymmen till partneridentitetsnamnutrymmen {#batch-identity-to-identity}

Användare kan mappa anpassade eller globala ID-namnutrymmen från Experience Platform till motsvarande ID-namnutrymmen.

När du väljer ett identitetsnamnutrymme som ett källfält fylls målfältet automatiskt i med ett motsvarande identitetsnamnutrymme.

Den resulterande gränssnittsupplevelsen visas i bilden nedan.

![Experience Platform UI-skärmbild som visar identitetsmappning för identitet för filbaserade mål.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vilka mappningar som stöds av mål som skapats med Destination SDK.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
* [Krav på historisk profil](historical-profile-qualifications.md)
