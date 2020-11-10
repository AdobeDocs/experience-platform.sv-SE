---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Komma igång med kundens AI
topic: Getting started
description: Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# Komma igång med kundens AI

Handböckerna för kundens AI kräver en fungerande förståelse för de olika plattformstjänster som används för att använda kundens AI. Läs följande dokument innan du börjar:

- [Experience Data Model (XDM) - systemöversikt](../../xdm/home.md): XDM är den grundläggande miljön som gör att [!DNL Adobe Experience Cloud]Experience Platform kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster.
- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i [!DNL Adobe Experience Platform].
- [Byggscheman](../../xdm/tutorials/create-schema-ui.md): I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.
- [Översikt över](../../rtcdp/overview.md)kundprofiler i realtid: Adobe Customer Data Platform (CDP i realtid) bygger på [!DNL Adobe Experience Platform]funktioner som hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. CDP i realtid kombinerar flera datakällor för företag för att skapa enhetliga profiler i realtid som kan användas för att leverera personliga personaliserade kundupplevelser i alla kanaler och enheter.
- [Översikt över](../../segmentation/home.md)segmenteringstjänsten: Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp. Med olika segment kan ni fokusera på olika målgrupper och leverera en mer anpassad marknadsföringsupplevelse.
- [Användarhandbok](../../segmentation/tutorials/create-a-segment.md)för Segment Builder: Med Platform kan ni enkelt skapa och komma åt segment, samt använda olika byggstenar för att ytterligare karakterisera era era era segment.

## Hämtar AI-poäng för kunder

>[!NOTE]
>
>Om du inte behöver ladda ned bakgrundsmusik kan du hoppa över det här steget och gå vidare till [konfigurationsguiden](./user-guide/configure.md).

Hämtning av kundens AI-poäng görs via en kombination av API-anrop. För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Nästa steg

När du är klar med stegen som beskrivs i dokumentet ovan kan du gå till [indata- och utdatadokumentationen](./input-output.md) . I det här dokumentet ges en kort översikt över vilka typer av data som används och produceras i kundens AI.