---
keywords: Experience Platform;home;populära topics;access control;api;komma igång
solution: Experience Platform
title: API-guide för åtkomstkontroll
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika Experience Platform-funktioner med hjälp av Adobe Admin Console. I följande avsnitt finns ytterligare information som utvecklare behöver känna till för att kunna anropa API:t för schemaregister.
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# API-guide för [!DNL Access Control]

[!DNL Access control] för [!DNL Experience Platform] administreras via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor. Mer information finns i [åtkomstkontrollsöversikten](../home.md).

Den här utvecklarhandboken innehåller information om hur du formaterar dina begäranden till [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/) och omfattar följande åtgärder:

- [Listnamn på behörigheter och resurstyper](./permissions-and-resource-types.md)
- [Visa gällande åtkomstprinciper för den aktuella användaren](./effective-policies.md)

## Komma igång

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:t [!DNL Access Control].

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

- Content-Type: application/json

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran som visar nödvändiga huvuden och korrekt formaterade nyttolaster samt ett exempelsvar för ett lyckat anrop.
