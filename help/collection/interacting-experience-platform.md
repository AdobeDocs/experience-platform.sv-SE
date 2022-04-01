---
title: Interagera med Adobe Experience Platform
description: Lär dig hur du använder API:t för Edge Network Server för att interagera med Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: datainsamling, Utlopp. Analyser. Adobe Experience Platform Edge Network API;aep
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interagera med Adobe Experience Platform

## Översikt {#overview}

Om du vill aktivera datainsamling från Experience Platform måste du först [konfigurera ditt datastream](../edge/fundamentals/datastreams.md) för att vidarebefordra händelser till datauppsättningar i Experience Platform.

När konfigurationen är klar bör datastream-konfigurationen innehålla inställningar för `com_adobe_experience_platform`, vilket visas i exemplet nedan:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
