---
description: För att kunna använda Destination SDK måste partnerföretaget uppfylla de krav som anges i det här dokumentet.
title: Krav för integrering
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Krav för integrering

Om du vill använda Destination SDK måste du uppfylla de tekniska kraven och villkoren för partnerskap som anges i avsnitten nedan.

## Tekniska krav/API-krav för direktuppspelningsmål {#streaming-prerequisites}

1. Du har en REST API-slutpunkt som Adobe Experience Platform kan använda för att leverera följande typer av data till:
   * Information om segmentmedlemskap;
   * Profilidentitetsinformation.
   * (Valfritt) Ytterligare attribut för profilberikning.
2. REST API-slutpunkten stöder autentisering av API-tokenbärare eller OAuth 2.0-autentiseringsprotokollet.
3. (Valfritt) Du har ett segment för att skapa/uppdatera/ta bort API eller API-slutpunkt för programmatisk metadatahantering.

## Tekniska krav för gruppmål {#batch-prerequisites}

1. Du har en målplats på [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], SFTP, [!DNL Google Cloud]eller en privat [!DNL Data Landing Zone], där du kan ta emot filer som exporterats utanför Experience Platform.
2. Målplattformen kan importera filer i det format som konfigurerats via [filformateringsalternativ](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) i Destination SDK för batchdestinationer.
3. (Valfritt) Du har ett segment för att skapa/hämta/uppdatera/ta bort (CRUD) API eller API-slutpunkt för programmatisk metadatahantering.

## Partnerskapskrav {#partnership-prerequisites}

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som vill använda Destination SDK, ska du läsa Partnerskapskraven för ISV och SI i [hämta åtkomstsektion](./overview.md#get-access).
