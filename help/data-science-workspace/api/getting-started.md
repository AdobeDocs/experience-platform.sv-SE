---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Utvecklarhandbok för Sensei Machine Learning API
topic: Developer guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Utvecklarhandbok för Sensei Machine Learning API

API:t Sensei Machine Learning är en mekanism för datavetare som organiserar och hanterar maskininlärningstjänster, från algoritmintroduktion till experimenterande och driftsättning.

Utvecklarhandboken innehåller steg som hjälper dig att börja använda API:t för [Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)och demonstrerar API-anrop för att utföra CRUD-åtgärder på olika resurser i Data Science Workspace.

## Komma igång

Du måste ha slutfört självstudiekursen för [autentisering](../../tutorials/authentication.md) för att ha tillgång till följande begäranderubriker för att kunna ringa anrop till [!DNL Adobe Experience Platform] API:er:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Nästa steg

När du har samlat in de inloggningsuppgifter som krävs kan du fortsätta till följande avsnitt i den här utvecklarhandboken för exempel-API-anrop till följande slutpunktsgrupper:

* [Motorer](./engines.md)
* [Experimentera](./experiments.md)
* [Insikter](./insights.md)
* [MLInstances (recept)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modeller](./models.md)
* [Bilaga](./appendix.md)