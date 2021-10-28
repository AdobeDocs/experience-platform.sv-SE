---
description: Använd autentiseringskonfigurationerna som stöds i Adobe Experience Platform Destination SDK för att autentisera användare och aktivera data till målslutpunkten.
title: Autentiseringskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Autentiseringskonfiguration {#credentials}

## Autentiseringstyper som stöds {#supported-authentication-types}

Adobe Experience Platform mål-SDK har stöd för flera autentiseringstyper:

* Bärarautentisering
* OAuth 2 med auktoriseringskod
* OAUth 2 med lösenordsbeviljande
* OAuth 2 med klientautentiseringsuppgifter

Du kan konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt. Se [avsnittet med konfigurationer för kundautentisering](./destination-configuration.md#customer-authentication-configurations) i artikeln om målkonfigurationen och avsnitten nedan för mer ingående information om konfigurationerna för varje autentiseringstyp.

## Bärarautentisering {#bearer}

Om du vill konfigurera autentisering av bearer-typ för dina mål behöver du bara konfigurera `customerAuthenticationConfigurations` -parametern i `/destinations` slutpunkt enligt nedan:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2-autentisering {#oauth2}

Mer information om hur du ställer in de olika OAuth 2-flödena som stöds, samt om anpassat OAuth 2-stöd, finns i dokumentationen för mål-SDK på [OAuth 2-autentisering](./oauth2-authentication.md).


## När ska du använda `/credentials` API-slutpunkt {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall *inte* måste du använda `/credentials` API-slutpunkt. I stället kan du konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt.

The `/credentials` API-slutpunkten anges till målutvecklare för de fall det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform] kunder behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål.

I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av `/credentials` API-slutpunkt. Du måste också välja `PLATFORM_AUTHENTICATION` i [målkonfiguration](./destination-configuration.md#destination-delivery). Läs [API-slutpunktsåtgärder för autentiseringsuppgifter](./credentials-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på `/credentials` slutpunkt.
