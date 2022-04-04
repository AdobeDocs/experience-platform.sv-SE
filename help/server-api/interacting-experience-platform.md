---
title: Interagera med Adobe Experience Platform
description: Lär dig hur du använder API:t för Edge Network Server för att interagera med Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: datainsamling, Utlopp. Analyser. Adobe Experience Platform Edge Network API;aep
exl-id: c49e40b7-9653-40f1-9db5-8941b20de8a3
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
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
