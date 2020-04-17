---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för Integritetstjänst
description: Använd RESTful API för att hantera persondata för dina registrerade i alla Adobe Experience Cloud-program
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Utvecklarhandbok för Integritetstjänst

Integritetstjänsten för Adobe Experience Platform erbjuder ett RESTful API och användargränssnitt som gör att du kan hantera (få tillgång till och ta bort) personuppgifter för dina registrerade (kunder) i alla Adobe Experience Cloud-program. Integritetstjänsten erbjuder även en central gransknings- och loggningsmekanism som gör att du kan komma åt status och resultat för jobb som innefattar Experience Cloud-program.

I den här handboken beskrivs hur du använder API:t för sekretesstjänsten. Mer information om hur du använder användargränssnittet finns i översikten över användargränssnittet i [sekretesstjänsten](../ui/overview.md). En fullständig lista över alla tillgängliga slutpunkter i sekretesstjänstens API finns i [API-referensen](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Komma igång

Den här guiden kräver en fungerande förståelse av följande Experience Platform-funktioner:

* [Integritetstjänst](../home.md): Tillhandahåller ett RESTful-API och användargränssnitt som gör att du kan hantera förfrågningar från registrerade (kunder) i alla Adobe Experience Cloud-program.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ringa anrop till API:t för sekretesstjänsten.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Nästa steg

Nu när du förstår vilka rubriker du ska använda kan du börja ringa anrop till API:t för sekretesstjänsten. Dokumentet om [sekretessjobb](privacy-jobs.md) går igenom de olika API-anrop du kan göra med API:t för sekretesstjänsten. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.
