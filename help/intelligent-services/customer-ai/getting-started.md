---
keywords: Experience Platform;komma igång;kundinformation;populära ämnen
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Komma igång med kundens AI
description: Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Komma igång med kundens AI

Handböckerna för kundens AI kräver en fungerande förståelse för de olika Experience Platform-tjänster som använder kundens AI. Läs följande dokument innan du börjar:

- [Systemöversikt för Experience Data Model (XDM)](../../xdm/home.md): XDM är det grundläggande ramverk som gör att [!DNL Adobe Experience Cloud], som drivs av Experience Platform, kan leverera rätt budskap till rätt person i rätt kanal vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, XDM System, använder Experience Data Model-scheman för Experience Platform tjänster.
- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Det här dokumentet innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att komponera scheman som ska användas i [!DNL Adobe Experience Platform].
- [Skapar scheman](../../xdm/tutorials/create-schema-ui.md): Den här självstudiekursen beskriver stegen för att skapa ett schema med Schemaredigeraren i Experience Platform.
- [Översikt över kundprofiler i realtid](../../rtcdp/overview.md): Adobe Real-Time Customer Data Platform (Real-Time CDP) är byggt på [!DNL Adobe Experience Platform] och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. Real-Time CDP kombinerar flera olika datakällor för företag för att skapa enhetliga profiler i realtid som kan användas för att leverera personliga personaliserade kundupplevelser i alla kanaler och enheter.
- [Översikt över segmenteringstjänsten](../../segmentation/home.md): Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en säljbar grupp av personer från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp. Med olika segment kan ni fokusera på olika målgrupper och leverera en mer anpassad marknadsföringsupplevelse.
- [Användarhandbok för Segment Builder](../../segmentation/tutorials/create-a-segment.md): Med Experience Platform kan du enkelt skapa och komma åt segment, samt använda olika byggstenar för att ytterligare karakterisera dina segment.

## Hämtar AI-poäng för kunder

>[!NOTE]
>
>Om du inte behöver hämta råresultat kan du hoppa över det här steget och gå vidare till [konfigurationsguiden](./user-guide/configure.md).

Hämtning av kundens AI-poäng görs via en kombination av API-anrop. För att kunna anropa Experience Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Experience Platform API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Experience Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Nästa steg

När du har slutfört stegen som beskrivs i dokumentet ovan kan du gå till dokumentationen för [Indata och utdata](./data-requirements.md). I det här dokumentet ges en kort översikt över vilka typer av data som används och produceras i kundens AI.
