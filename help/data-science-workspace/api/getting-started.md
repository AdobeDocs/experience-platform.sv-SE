---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära ämnen;datavetenskapens arbetsyta;datavetenskap
solution: Experience Platform
title: API-guide för Sensei Machine Learning
description: Med Sensei Machine Learning API kan utvecklare utföra CRUD-åtgärder på olika Data Science Workspace-resurser. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 5%

---

# API-guide för [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

API:t [!DNL Sensei Machine Learning] innehåller en mekanism för datavetare som organiserar och hanterar maskininlärningstjänster, från algoritmregistrering till experimenterande och till tjänstdistribution.

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda [Sensei Machine Learning API](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) och demonstrerar API-anrop för att utföra CRUD-åtgärder på olika Data Science Workspace-resurser.

## Komma igång

Du måste ha slutfört självstudiekursen [authentication](https://www.adobe.com/go/platform-api-authentication-en) för att kunna komma åt följande begäranrubriker för att kunna anropa [!DNL Adobe Experience Platform] API:er:

* Behörighet: Bärare `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

* Content-Type: application/json

## Nästa steg

När du har samlat in de inloggningsuppgifter som krävs kan du fortsätta till följande avsnitt i den här utvecklarhandboken för exempel-API-anrop till följande slutpunktsgrupper:

* [Motorer](./engines.md)
* [Experimentera](./experiments.md)
* [Insikter](./insights.md)
* [MLInstances (recept)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Models](./models.md)
* [Bilaga](./appendix.md)
