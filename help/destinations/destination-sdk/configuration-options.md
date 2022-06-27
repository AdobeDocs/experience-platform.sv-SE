---
description: Måltjänsten i Adobe Experience Platform använder konfigurationsmallar för flera komponenter som bygger upp målfunktionaliteten. Tillsammans kan dessa komponenter hjälpa Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet.
title: Konfigurationsalternativ i Destinationen SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Konfigurationsalternativ i Destinationen SDK

## Översikt {#overview}

Måltjänsten i Adobe Experience Platform använder konfigurationsmallar för flera komponenter som bygger upp målfunktionaliteten. Tillsammans kan dessa komponenter hjälpa Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet. Mallarna som används i Adobe Experience Platform är:

* **Målkonfiguration**: Innehåller grundläggande information om målet. Den här konfigurationen innehåller de identitetstyper som ditt mål kan stödja och olika gränssnittsattribut för målkortet i Adobe Experience Platform-användargränssnittet.
* **Server- och mallspecifikationer**: Sammanfogar information om serverspecifikationerna och den mall som används av Adobe för att leverera nyttolaster till destinationen.
   * **Serverspecifikationer**: En mall som lagrar din slutpunktsinformation.
   * **Mallspecifikationer**: I den här mallen kan du definiera hur profilattributfält ska omformas mellan XDM-schemat och det format som din plattform stöder. Mer ingående information om vilka mallspråk, meddelandeformat och den information som Adobe behöver för att kunna konfigurera integrationen med din plattform finns i [Meddelandeformat](./message-format.md).
* **Autentiseringskonfiguration**: De här inställningarna definierar hur Adobe Experience Platform-användare ansluter till ditt mål.
* **Konfiguration av målgruppsmetadata**: Med den här mallen kan du konfigurera hur målgrupper/segment skapas, uppdateras eller tas bort programmatiskt i målet.

![Destinationer SDK och konfigurationer](./assets/self-service-configuration.png)

## Relaterade länkar {#related-links}

På sidorna nedan finns mer information om de funktioner och konfigurationsalternativ som finns i Destinationen SDK och om de motsvarande API-åtgärder som du kan utföra.

| Funktionsbeskrivning | API-referens |
|--- |--- |
| [Målkonfiguration](./destination-configuration.md) | [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) |
| [Server- och mallspecifikationer](./server-and-template-configuration.md) | [API-slutpunktsåtgärder för målservrar](./destination-server-api.md) |
| [Autentiseringskonfiguration](./authentication-configuration.md) | [API-åtgärder för slutpunkt för autentiseringsuppgifter](./credentials-configuration-api.md) |
| [Hantering av målgruppsmetadata](./audience-metadata-management.md) | [API-åtgärder för målgruppsmetadata](./audience-metadata-api.md) |
| [OAuth 2-konfiguration](./oauth2-authentication.md) | Konfigurera med `customerAuthenticationConfigurations` -parametern i [API-slutpunkt för mål](./destination-configuration-api.md). |
| [Meddelandeformat](./message-format.md) | – |
| [Destinationstestning](./test-destination.md) | [API-åtgärder för måltestning](./destination-testing-api.md) |
| [Målpublicering](./configure-destination-instructions.md#publish-destination) | [API-åtgärder för målpublicering](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
