---
description: Den här konfigurationen avgör hur Adobe Experience Platform-användare autentiserar till målslutpunkten för att aktivera data.
title: Konfigurationsalternativ för autentiseringsuppgifter i mål-SDK
source-git-commit: 11f6421665acc2041aa9483b1e0efb6fe48b6dfb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Autentiseringskonfiguration {#credentials}

## Autentiseringstyper som stöds {#supported-authentication-types}

Adobe Experience Platform stöder flera autentiseringstyper:

* Bärarautentisering
* OAuth 2 med auktoriseringskod
* OAUth 2 med lösenordsbeviljande
* OAuth 2 med klientautentiseringsuppgifter

Information om vilka OAuth 2-flöden som stöds, samt om anpassat OAuth 2-stöd, finns i dokumentationen för mål-SDK om [OAuth 2-autentisering](./oauth2-authentication.md).

Du kan konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations`-parametrarna för `/destinations`-slutpunkten. Se avsnittet [konfigurationer för kundautentisering](./destination-configuration.md#customer-authentication-configurations) i målkonfigurationsartikeln.

## När ska API-slutpunkten `/credentials` användas {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall behöver du *inte* använda API-slutpunkten `/credentials`. Du kan i stället konfigurera autentiseringsinformationen för målet via `customerAuthenticationConfigurations`-parametrarna för `/destinations`-slutpunkten.

Använd API-slutpunkten `activation/authoring/credentials` och välj `PLATFORM_AUTHENTICATION` i [målkonfigurationen](./destination-configuration.md#destination-delivery) om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med API-slutpunkten `/credentials`. Läs [API-slutpunktsåtgärder för autentiseringsuppgifter](./credentials-configuration-api.md) om du vill se en fullständig lista över åtgärder som du kan utföra på `/credentials`-slutpunkten.