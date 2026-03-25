---
description: För att kunna använda Destination SDK måste partnerföretaget uppfylla de krav som anges i det här dokumentet.
title: Krav för integrering
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Krav för integrering

Om du vill använda Destination SDK måste du uppfylla de tekniska kraven och villkoren för partnerskap som anges i avsnitten nedan.

## Tekniska krav/API-krav för direktuppspelningsmål {#streaming-prerequisites}

1. Du har en REST API-slutpunkt för [!DNL Adobe Experience Platform] som kan leverera följande typer av data till:
   * information om målgruppsmedlemskap,
   * Profilidentitetsinformation.
   * (Valfritt) Ytterligare attribut för profilberikning.
2. REST API-slutpunkten har stöd för grundläggande token, innehavartoken eller OAuth 2.0-autentiseringsprotokoll.
3. (Valfritt) Du har en målgrupp som skapar/uppdaterar/tar bort API eller API-slutpunkt för programmatisk metadatahantering.

## Tekniska krav för gruppmål {#batch-prerequisites}

1. Du har en målplats på [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud] eller en privat [!DNL Data Landing Zone], där du kan ta emot filer som exporterats från Experience Platform.
2. Målplattformen kan importera filer i det format som konfigurerats via [filformateringsalternativen](functionality/destination-server/file-formatting.md) i Destination SDK för gruppmål.
3. (Valfritt) Du har en målgrupp som skapar/hämtar/uppdaterar/tar bort ([!DNL CRUD]) API eller API-slutpunkt för programmatisk metadatahantering.

## Partnerskapskrav {#partnership-prerequisites}

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som vill använda Destination SDK, läser du Partnerskapskraven för ISV och SI i [åtkomstavsnittet](overview.md#get-access).
