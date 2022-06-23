---
description: Använd autentiseringskonfigurationerna som stöds i Adobe Experience Platform Destination SDK för att autentisera användare och aktivera data till målslutpunkten.
title: Autentiseringskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 631c0ac02cb7f4f95500897ca224aa532393c109
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Autentiseringskonfiguration {#credentials}

## Autentiseringstyper som stöds {#supported-authentication-types}

Den autentiseringskonfiguration som du väljer avgör hur Experience Platform ska autentisera till ditt mål i plattformsgränssnittet.

Adobe Experience Platform Destination SDK stöder flera autentiseringstyper:

* [Bärarautentisering](#bearer)
* [(Beta) Amazon S3-autentisering](#s3)
* [(Beta) Azure Blob Storage](#blob)
* [(Beta) Azure Data Lake Storage](#adls)
* [(Beta) Google Cloud-lagring](#gcs)
* [(Beta) SFTP med SSH-nyckel](#sftp-ssh)
* [(Beta) SFTP med lösenord](#sftp-password)
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

## (Beta) [!DNL Amazon S3] autentisering {#s3}

[!DNL Amazon S3] autentisering stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Om du vill konfigurera Amazon S3-autentisering för ditt mål konfigurerar du `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## (Beta) [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] autentisering stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Konfigurera [!DNL Azure Blob] autentisering för ditt mål, konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## (Beta) [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] autentisering stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Konfigurera [!DNL Azure Data Lake Storage] (ADLS) autentisering för ditt mål, konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## (Beta) [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] autentisering stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## (Beta) [!DNL SFTP] autentisering med [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] autentisering med [!DNL SSH] -nyckeln stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## (Beta) [!DNL SFTP] autentisering med lösenord {#sftp-password}

[!DNL SFTP] autentisering med lösenord stöds för filbaserade mål i Experience Platform.

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

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

Mer information om hur du ställer in de olika OAuth 2-flödena som stöds, samt om anpassat OAuth 2-stöd, finns i Destinationens SDK dokumentation på [OAuth 2-autentisering](./oauth2-authentication.md).


## När ska du använda `/credentials` API-slutpunkt {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall *inte* måste du använda `/credentials` API-slutpunkt. I stället kan du konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt.

The `/credentials` API-slutpunkten anges till målutvecklare för de fall det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform] kunder behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål.

I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av `/credentials` API-slutpunkt. Du måste också välja `PLATFORM_AUTHENTICATION` i [målkonfiguration](./destination-configuration.md#destination-delivery). Läs [API-slutpunktsåtgärder för autentiseringsuppgifter](./credentials-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på `/credentials` slutpunkt.
