---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära topics;data science workspace;data science
solution: Experience Platform
title: API-handbok för Sensei Machine Learning
topic-legacy: Developer guide
description: Med API:t Sensei Machine Learning kan utvecklare utföra CRUD-åtgärder på olika Data Science Workspace-resurser. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] API-guide

Med API:t [!DNL Sensei Machine Learning] kan datavetare ordna och hantera maskininlärningstjänster, från algoritmintroduktion till experimenterande och till driftsättning.

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda API:t [Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) och demonstrerar API-anrop för att utföra CRUD-åtgärder på olika Data Science Workspace-resurser.

## Komma igång

Du måste ha slutfört självstudiekursen [autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna få åtkomst till följande begäranderubriker för att kunna ringa anrop till API:er för [!DNL Adobe Experience Platform]:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

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
