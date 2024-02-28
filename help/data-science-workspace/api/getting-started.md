---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära topics;data science workspace;data science
solution: Experience Platform
title: API-guide för Sensei Machine Learning
description: Med Sensei Machine Learning API kan utvecklare utföra CRUD-åtgärder på olika datavetenskapliga Workspace-resurser. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 7%

---

# [!DNL Sensei Machine Learning] API-guide

The [!DNL Sensei Machine Learning] API erbjuder en mekanism för datavetare att organisera och hantera maskininlärningstjänster, från algoritmintroduktion till experimenterande och driftsättning.

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), och visar API-anrop för att utföra CRUD-åtgärder på olika resurser för datavetenskapen.

## Komma igång

Du måste ha slutfört [autentisering](https://www.adobe.com/go/platform-api-authentication-en) självstudiekurs för att få tillgång till följande begäranrubriker för att ringa [!DNL Adobe Experience Platform] API:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Content-Type: application/json

## Nästa steg

När du har samlat in de inloggningsuppgifter som krävs kan du fortsätta till följande avsnitt i den här utvecklarhandboken för exempel-API-anrop till följande slutpunktsgrupper:

* [Motorer](./engines.md)
* [Experimentera](./experiments.md)
* [Insikter](./insights.md)
* [MLInstances (recept)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modeller](./models.md)
* [Bilaga](./appendix.md)
