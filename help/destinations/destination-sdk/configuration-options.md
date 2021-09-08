---
description: Måltjänsten i Adobe Experience Platform använder konfigurationsmallar för flera komponenter som bygger upp målfunktionaliteten. Tillsammans kan dessa komponenter hjälpa Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet.
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: Konfigurationsalternativ i mål-SDK
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Konfigurationsalternativ i mål-SDK

## Översikt {#overview}

Måltjänsten i Adobe Experience Platform använder konfigurationsmallar för flera komponenter som bygger upp målfunktionaliteten. Tillsammans kan dessa komponenter hjälpa Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet. Mallarna som används i Adobe Experience Platform är:

* **Målkonfiguration**: Innehåller grundläggande information om målet. Den här konfigurationen innehåller de identitetstyper som ditt mål kan stödja och olika gränssnittsattribut för målkortet i Adobe Experience Platform-användargränssnittet.
* **Server- och mallspecifikationer**: Sammanfogar information om serverspecifikationerna och den mall som används av Adobe för att leverera nyttolaster till destinationen.
   * **Serverspecifikationer**: En mall som lagrar din slutpunktsinformation.
   * **Mallspecifikationer**: I den här mallen kan du definiera hur profilattributfält ska omformas mellan XDM-schemat och det format som din plattform stöder. Mer detaljerad information om vilka mallspråk, meddelandeformat och den information som Adobe behöver för att kunna konfigurera integrationen med din plattform finns i [Meddelandeformat](./message-format.md).
* **Autentiseringskonfiguration**: De här inställningarna definierar hur Adobe Experience Platform-användare ansluter till ditt mål.
* **Konfiguration** av målgruppsmetadata: Med den här mallen kan du konfigurera hur målgrupper/segment skapas, uppdateras eller tas bort programmatiskt i målet.

![SDK-mallar och konfigurationer för mål](./assets/self-service-configuration.png)

## Relaterade länkar {#related-links}

På sidorna nedan finns mer information om de funktioner och konfigurationsalternativ som är tillgängliga i mål-SDK och om de motsvarande API-åtgärder som du kan utföra.

| Funktionsbeskrivning | API-referens |
|--- |--- |
| [Målkonfiguration](./destination-configuration.md) | [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) |
| [Server- och mallspecifikationer](./server-and-template-configuration.md) | [API-slutpunktsåtgärder för målservrar](./destination-server-api.md) |
| [Autentiseringskonfiguration](./credentials-configuration.md) | [API-åtgärder för slutpunkt för autentiseringsuppgifter](./credentials-configuration-api.md) |
| [Hantering av målgruppsmetadata](./audience-metadata-management.md) | [API-åtgärder för målgruppsmetadata](./audience-metadata-api.md) |
| [OAuth 2-konfiguration](./oauth2-authentication.md) | Konfigurera med parametern `customerAuthenticationConfigurations` i API-slutpunkten [/destination](./destination-configuration-api.md). |
| [Meddelandeformat](./message-format.md) | – |
| [Destinationstestning](./test-destination.md) | [API-åtgärder för måltestning](./destination-testing-api.md) |
| [Målpublicering](./configure-destination-instructions.md#publish-destination) | [API-åtgärder för målpublicering](./destination-publish-api.md) |
