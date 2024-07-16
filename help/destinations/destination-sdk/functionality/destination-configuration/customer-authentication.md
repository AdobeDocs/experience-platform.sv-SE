---
description: Lär dig hur du konfigurerar en autentiseringsmekanism för ditt mål och får information om vad användare ser i användargränssnittet beroende på vilken autentiseringsmetod du väljer.
title: Konfiguration av kundautentisering
exl-id: 3912012e-0870-47d2-9a6f-7f1fc469a781
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 0%

---

# Konfiguration av kundautentisering

Experience Platform erbjuder stor flexibilitet i de autentiseringsprotokoll som är tillgängliga för partners och kunder. Du kan konfigurera ditt mål så att det stöder någon av de autentiseringsmetoder som är branschstandard, som [!DNL OAuth2], autentisering med innehavartoken, lösenordsautentisering och många andra.

På den här sidan beskrivs hur du konfigurerar målet med den autentiseringsmetod du föredrar. Baserat på den autentiseringskonfiguration som du använder när du skapar målet, kommer kunderna att se olika typer av autentiseringssidor när de ansluter till målet i användargränssnittet i Experience Platform.

Om du vill veta var den här komponenten passar in i en integrering som skapats med Destination SDK kan du läsa diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller följande sidor med en översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Innan kunder kan exportera data från Platform till ditt mål måste de skapa en ny anslutning mellan Experience Platform och ditt mål genom att följa stegen som beskrivs i självstudiekursen [målanslutning](../../../ui/connect-destination.md).

När [skapar ett mål](../../authoring-api/destination-configuration/create-destination-configuration.md) via Destination SDK, definierar avsnittet `customerAuthenticationConfigurations` vad kunderna ser på [autentiseringsskärmen](../../../ui/connect-destination.md#authenticate). Beroende på autentiseringstypen för målet måste kunderna tillhandahålla olika autentiseringsdetaljer, som:

* För mål som använder [grundläggande autentisering](#basic) måste användare ange ett användarnamn och lösenord direkt på Experience Platform användargränssnittets autentiseringssida.
* För mål som använder [innehavarautentisering](#bearer) måste användarna ange en innehavartoken.
* För mål som använder [OAuth2-auktorisering](#oauth2) omdirigeras användare till målets inloggningssida där de kan logga in med sina autentiseringsuppgifter.
* För [Amazon S3](#s3)-mål måste användare ange sin [!DNL Amazon S3]-åtkomstnyckel och hemlig nyckel.
* För [Azure Blob](#blob)-mål måste användarna ange sin [!DNL Azure Blob]-anslutningssträng.

Du kan konfigurera kundautentiseringsinformation via slutpunkten `/authoring/destinations`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Uppdatera en målkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

I den här artikeln beskrivs alla kompatibla konfigurationer för kundautentisering som du kan använda för ditt mål, och det som kunder ser i användargränssnittet i Experience Platform visas baserat på den autentiseringsmetod som du har ställt in för ditt mål.

>[!IMPORTANT]
>
>Konfigurationen för kundautentisering kräver inte att du konfigurerar några parametrar. Du kan kopiera och klistra in kodavsnitten som visas på den här sidan i dina API-anrop när [skapar](../../authoring-api/destination-configuration/create-destination-configuration.md) eller [uppdaterar](../../authoring-api/destination-configuration/update-destination-configuration.md) en målkonfiguration, och dina användare ser motsvarande autentiseringsskärm i plattformsgränssnittet.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

## Konfiguration av autentiseringsregel {#authentication-rule}

När du använder någon av de konfigurationer för kundautentisering som beskrivs på den här sidan ska du alltid ange parametern `authenticationRule` i [målleverans](destination-delivery.md) till `"CUSTOMER_AUTHENTICATION"`, vilket visas nedan.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Grundläggande autentisering {#basic}

Grundläggande autentisering stöds för integreringar i realtid (direktuppspelning) i Experience Platform.

När du konfigurerar den grundläggande autentiseringstypen måste användarna ange ett användarnamn och lösenord för att kunna ansluta till målet.

![Gränssnittsåtergivning med grundläggande autentisering](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Konfigurera avsnittet `customerAuthenticationConfigurations` via `/destinations`-slutpunkten så som visas nedan för att konfigurera grundläggande autentisering för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Bärarautentisering {#bearer}

När du konfigurerar typen för innehavarautentisering måste användarna ange den innehavartoken som de får från ditt mål.

![Gränssnittet återges med innehavarautentisering](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Konfigurera avsnittet `customerAuthenticationConfigurations` via `/destinations`-slutpunkten så som visas nedan om du vill konfigurera autentisering av bearer-typ för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2-autentisering {#oauth2}

Användare väljer **[!UICONTROL Connect to destination]** för att utlösa OAuth 2-autentiseringsflödet till ditt mål, vilket visas i exemplet nedan för Twitternas anpassade målgrupper. Mer information om hur du konfigurerar OAuth 2-autentisering till målslutpunkten finns på den dedikerade [Destination SDK OAuth 2-autentiseringssidan](oauth2-authorization.md).

![Gränssnittsåtergivning med OAuth 2-autentisering](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Konfigurera `customerAuthenticationConfigurations`-avsnittet via `/destinations`-slutpunkten så som visas nedan för att konfigurera [!DNL OAuth2]-autentisering för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3-autentisering {#s3}

[!DNL Amazon S3]-autentisering stöds för filbaserade mål i Experience Platform.

När du konfigurerar autentiseringstypen Amazon S3 måste användare ange sina S3-inloggningsuppgifter.

![Gränssnittsåtergivning med S3-autentisering](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Konfigurera `customerAuthenticationConfigurations`-avsnittet via `/destinations`-slutpunkten så som visas nedan för att konfigurera [!DNL Amazon S3]-autentisering för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob-autentisering  {#blob}

[!DNL Azure Blob Storage]-autentisering stöds för filbaserade mål i Experience Platform.

När du konfigurerar autentiseringstypen Azure Blob måste användarna ange anslutningssträngen.

![Användargränssnittet återges med blobautentisering](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Konfigurera parametern `customerAuthenticationConfigurations` i slutpunkten `/destinations` så som visas nedan om du vill konfigurera [!DNL Azure Blob]-autentisering för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] autentisering {#adls}

[!DNL Azure Data Lake Storage]-autentisering stöds för filbaserade mål i Experience Platform.

När du konfigurerar autentiseringstypen [!DNL Azure Data Lake Storage] måste användarna ange autentiseringsuppgifterna för Azure Service Principal och deras klientinformation.

![Gränssnittsåtergivning med [!DNL Azure Data Lake Storage] autentisering](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Konfigurera parametern `customerAuthenticationConfigurations` i slutpunkten `/destinations` så som visas nedan om du vill konfigurera [!DNL Azure Data Lake Storage]-autentisering (ADLS) för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP med lösenordsautentisering

[!DNL SFTP]-autentisering med lösenord stöds för filbaserade mål i Experience Platform.

När du konfigurerar SFTP med lösenordsautentiseringstypen måste användarna ange SFTP-användarnamn och -lösenord samt SFTP-domän och -port (standardport är 22).

![Gränssnittet återges med SFTP med lösenordsautentisering](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Konfigurera parametern `customerAuthenticationConfigurations` i slutpunkten `/destinations` så som visas nedan om du vill konfigurera SFTP-autentisering med lösenord för målet:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP med autentisering med SSH-nyckel

[!DNL SFTP]-autentisering med [!DNL SSH]-nyckel stöds för filbaserade mål i Experience Platform.

När du konfigurerar SFTP med autentiseringstypen SSH-nyckel måste användarna ange SFTP-användarnamnet och SSH-nyckeln samt SFTP-domänen och -porten (standardporten är 22).

![Gränssnittet återges med SFTP med autentisering med SSH-nyckel](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Om du vill konfigurera SFTP-autentisering med SSH-nyckel för målet konfigurerar du parametern `customerAuthenticationConfigurations` i slutpunkten `/destinations` enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] autentisering {#gcs}

[!DNL Google Cloud Storage]-autentisering stöds för filbaserade mål i Experience Platform.

När du konfigurerar autentiseringstypen [!DNL Google Cloud Storage] måste användarna ange [!DNL Google Cloud Storage] [!UICONTROL access key ID] och [!UICONTROL secret access key].

![Användargränssnittet återges med autentisering av Google Cloud-lagring](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Konfigurera parametern `customerAuthenticationConfigurations` i slutpunkten `/destinations` så som visas nedan om du vill konfigurera [!DNL Google Cloud Storage]-autentisering för ditt mål:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur du kan konfigurera användarautentisering för målplattformen.

Mer information om de andra målkomponenterna finns i följande artiklar:

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
