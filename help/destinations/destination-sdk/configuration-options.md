---
description: Destinationstjänsten i Adobe Experience Platform använder konfigurationsslutpunkter för flera komponenter som bygger upp målfunktionaliteten. Tillsammans kan dessa komponenter hjälpa Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet.
title: Konfigurationsalternativ i Destinationen SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Konfigurationsalternativ i Destinationen SDK

## Översikt {#overview}

Destinationstjänsten i Adobe Experience Platform använder konfigurationsslutpunkter för flera komponenter som bygger upp målfunktionaliteten. Tillsammans gör dessa komponenter det möjligt för Experience Platform att ansluta till målplattformar, skicka anpassade meddelanden, exportera anpassade filer och aktivera profildata i hela det digitala ekosystemet. Konfigurationerna som används i Adobe Experience Platform Destination SDK är:

* **Målkonfiguration**: Innehåller grundläggande information om målet. Den här konfigurationen innehåller de identitetstyper som ditt mål kan hantera, det önskade formatet för exporterade filer (för filbaserade mål) och olika gränssnittsattribut för målkortet i Adobe Experience Platform användargränssnitt.
* **Server-, fil- och mallspecifikationer**: Sammanfogar information om serverspecifikationerna och den mall som används av Adobe för att leverera nyttolaster till destinationen. För filbaserade mål innehåller den här konfigurationen även de filformat och komprimeringsformat som stöds för destinationen.
   * **Serverspecifikationer**: En konfigurationsmall som innehåller information om lagringsplatsen eller HTTP-slutpunkten dit data skickas.&quot;
   * **Filspecifikationer**: En konfigurationsmall som innehåller filformatering och komprimeringsalternativ för gruppmålet.
   * **Mallspecifikationer**: I den här mallen kan du definiera hur profilattributfält ska omformas mellan XDM-schemat och det format som din plattform stöder. Mer ingående information om vilka mallspråk, meddelandeformat och den information som Adobe behöver för att kunna konfigurera integrationen med din plattform finns i [Meddelandeformat](./message-format.md).
* **Autentiseringskonfiguration**: De här inställningarna definierar hur Adobe Experience Platform-användare ansluter till ditt mål.
* **Konfiguration av målgruppsmetadata**: Med den här konfigurationsslutpunkten kan du konfigurera hur målgrupper/segment skapas, uppdateras eller tas bort i ditt mål. För gruppmål kan du konfigurera ett meddelande när filerna har levererats till ditt mål.

![Diagram som visar Destinationens SDK konfigurationsslutpunkter och hur dessa används tillsammans.](./assets/self-service-configuration.png)

## Relaterade länkar {#related-links}

På sidorna nedan finns mer information om de funktioner och konfigurationsalternativ som finns i Destinationen SDK och om de motsvarande API-åtgärder som du kan utföra.

| Funktionalitetsbeskrivning (direktuppspelningsmål) | Funktionalitetsbeskrivning (gruppmål) | API-referens |
|--- |--- |--- |
| [Alternativ för målkonfiguration](./destination-configuration.md) | [Filbaserade konfigurationsalternativ för mål](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) |
| [Server- och mallspecifikationer](./server-and-template-configuration.md) | [Konfigurationsspecifikationer för server och fil](/help/destinations/destination-sdk/server-and-file-configuration.md) | [API-slutpunktsåtgärder för målservrar](./destination-server-api.md) |
| [Autentiseringskonfiguration](./authentication-configuration.md) | Samma som för direktuppspelningsmål. | Du kan konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt. Mer information om [direktuppspelning](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) och [batch](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinationer. |
| [Hantering av målgruppsmetadata](./audience-metadata-management.md) | Samma som för direktuppspelning. Se [filbaserat exempel](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) för att förstå hur målgruppsmetadata kan användas i ett batchmålsammanhang. | [API-åtgärder för målgruppsmetadata](./audience-metadata-api.md) |
| [OAuth 2-konfiguration](./oauth2-authentication.md) | Samma som för direktuppspelningsmål | Konfigurera med `customerAuthenticationConfigurations` -parametern i [API-slutpunkt för mål](./destination-configuration-api.md). |
| [Meddelandeformat](./message-format.md) | – | – |
| [Testverktyg för direktuppspelningsmål](./test-destination.md) | [Testverktyg för filbaserade mål](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [API-åtgärder för måltestning](./destination-testing-api.md) |
| [Målpublicering](./configure-destination-instructions.md#publish-destination) | Samma som för direktuppspelningsmål | [API-åtgärder för målpublicering](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

## Nästa steg {#next-steps}

Genom att läsa den här artikeln får du nu en allmän översikt över de funktioner som Destinationen SDK tillhandahåller och vilka sidor som ska läsas för mer information om specifika konfigurationer. Därefter kan du läsa stödlinjerna som innehåller alla steg i [konfigurera en direktuppspelning](/help/destinations/destination-sdk/configure-destination-instructions.md) eller en [filbaserat mål](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) genom att använda Destination SDK.
