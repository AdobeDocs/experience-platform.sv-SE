---
keywords: Experience Platform;komma igång;kundinformation;populära ämnen
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Komma igång med AI
topic-legacy: Getting started
description: Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: b3c331821e2df17380edbc673066f6b10a06d65f
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Komma igång med kundens AI

Handböckerna för kundens AI kräver en fungerande förståelse för de olika plattformstjänster som används för att använda kundens AI. Läs följande dokument innan du börjar:

- [Experience Data Model (XDM) - systemöversikt](../../xdm/home.md): XDM är den grundläggande miljön som [!DNL Adobe Experience Cloud]som drivs av Experience Platform för att leverera rätt budskap till rätt person, i rätt kanal, vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster.
- [Grunderna för schemakomposition](../../xdm/schema/composition.md): Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i [!DNL Adobe Experience Platform].
- [Byggscheman](../../xdm/tutorials/create-schema-ui.md): I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.
- [Översikt över kundprofiler i realtid](../../rtcdp/overview.md): Inbyggt [!DNL Adobe Experience Platform]Real-time Customer Data Platform (CDP i realtid) hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. CDP i realtid kombinerar flera datakällor för företag för att skapa enhetliga profiler i realtid som kan användas för att leverera personliga personaliserade kundupplevelser i alla kanaler och enheter.
- [Översikt över segmenteringstjänsten](../../segmentation/home.md): Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp. Med olika segment kan ni fokusera på olika målgrupper och leverera en mer anpassad marknadsföringsupplevelse.
- [Användarhandbok för Segment Builder](../../segmentation/tutorials/create-a-segment.md): Med Platform kan ni enkelt skapa och komma åt segment, samt använda olika byggstenar för att ytterligare karakterisera era era era segment.

## Hämtar AI-poäng för kunder

>[!NOTE]
>
>Om du inte behöver ladda ned bakgrundsmusik kan du hoppa över det här steget och gå vidare till [konfigurationsguide](./user-guide/configure.md).

Hämtning av kundens AI-poäng görs via en kombination av API-anrop. För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Behörigheter

När du använder åtkomstkontroll **Visa kund-AI** och **Hantera kund-AI** ger åtkomst till olika funktioner i Customer AI. The **Hantera kund-AI** behörighet ger dig **skapa**,**uppdatera**, **delete**, **enable**, eller **disable** en instans while **Visa kund-AI** gör att du kan läsa eller visa den. The **skapa**, **uppdatera** och **delete** åtgärder registreras av granskningsloggar.

Läs dokumentationen för att lära dig mer [tilldela behörigheter för åtkomstkontroll](../../../help/access-control/home.md) eller hur [använda granskningsloggar för att övervaka åtkomst och aktivitet](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nästa steg

När du är klar med stegen som beskrivs i dokumentet ovan kan du gå till [Indata och utdata](./input-output.md) dokumentation. I det här dokumentet ges en kort översikt över vilka typer av data som används och produceras i kundens AI.
