---
description: Använd autentiseringskonfigurationerna som stöds i Adobe Experience Platform Destination SDK för att autentisera användare och aktivera data till målslutpunkten.
title: Autentiseringskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Autentiseringskonfiguration {#credentials}

## Autentiseringstyper som stöds {#supported-authentication-types}

Den autentiseringskonfiguration som du väljer avgör hur Experience Platform ska autentisera till ditt mål i plattformsgränssnittet.

Adobe Experience Platform Destination SDK stöder flera autentiseringstyper:

* [Bärarautentisering](#bearer)
* [[!DNL Amazon S3] autentisering](#s3)
* [[!DNL Azure Blob] Lagring](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP med SSH-nyckel](#sftp-ssh)
* [SFTP med lösenord](#sftp-password)
* [OAuth 2 med auktoriseringskod](#oauth2)
* [OAUth 2 med lösenordsbeviljande](#oauth2)
* [OAuth 2 med klientautentiseringsuppgifter](#oauth2)

Du kan konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt.

I följande avsnitt finns information om autentiseringskonfigurationen för varje typ av mål:

* [Autentiseringskonfigurationer för direktuppspelningsmål](destination-configuration.md#customer-authentication-configurations)
* [Autentiseringskonfigurationer för filbaserade mål](file-based-destination-configuration.md#customer-authentication-configurations)

## Bärarautentisering {#bearer}

Bearer-autentisering stöds för direktuppspelningsmål i Experience Platform.

Konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] autentisering {#s3}

[!DNL Amazon S3] autentisering stöds för filbaserade mål i Experience Platform.

Konfigurera [!DNL Amazon S3] autentisering för ditt mål, konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] autentisering stöds för filbaserade mål i Experience Platform.

Konfigurera [!DNL Azure Blob] autentisering för ditt mål, konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] autentisering stöds för filbaserade mål i Experience Platform.

Konfigurera [!DNL Azure Data Lake Storage] (ADLS) autentisering för ditt mål, konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] autentisering stöds för filbaserade mål i Experience Platform.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] autentisering med [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] autentisering med [!DNL SSH] -nyckeln stöds för filbaserade mål i Experience Platform.

Konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autentisering med lösenord {#sftp-password}

[!DNL SFTP] autentisering med lösenord stöds för filbaserade mål i Experience Platform.

Konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] autentisering {#oauth2}

[!DNL OAuth 2] Autentisering stöds för direktuppspelningsmål i Experience Platform.

Information om hur du konfigurerar de olika inställningarna som stöds [!DNL OAuth 2] och för anpassade [!DNL OAuth 2] support, läs Destinationens SDK dokumentation om [[!DNL OAuth 2] autentisering](./oauth2-authentication.md).


## När ska du använda `/credentials` API-slutpunkt {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall *inte* måste du använda `/credentials` API-slutpunkt. I stället kan du konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt.

The `/credentials` API-slutpunkten anges till målutvecklare för de fall det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform] kunder behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål.

I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av `/credentials` API-slutpunkt. Du måste också välja `PLATFORM_AUTHENTICATION` i [målkonfiguration](./destination-configuration.md#destination-delivery). Läs [API-slutpunktsåtgärder för autentiseringsuppgifter](./credentials-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på `/credentials` slutpunkt.
