---
keywords: Experience Platform;komma igång;attribuering;populära ämnen
solution: Experience Platform, Intelligent Services
title: Komma igång med Attribution AI
topic: Getting started
description: Följande handledningar kräver förståelse för de olika Adobe Experience Platform-tjänster som används för att använda Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument.
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Komma igång med Attribution AI

Följande guider kräver förståelse för de olika [!DNL Adobe Experience Platform]-tjänsterna som används för att använda Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument:

- [Experience Data Model (XDM) - systemöversikt](../../xdm/home.md): XDM är den grundläggande miljön som gör att  [!DNL Adobe Experience Cloud]Experience Platform kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster.
- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i  [!DNL Adobe Experience Platform].
- [Byggscheman](../../xdm/tutorials/create-schema-ui.md): I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.

Attribution AI kräver att datauppsättningar överensstämmer med CEE-schemat (Consumer Experience Events), som är en blandning i [Experience Data Model](../../xdm/home.md) (XDM). Kontakta Adobe support på attributionai-support@adobe.com för att implementera eller göra ändringar i dessa data. Om det finns uppgifter om medieleveranser kan du göra ytterligare analyser, till exempel inkrementella intäkter och avkastning. Om det finns tillgängliga kundprofildata kan du attribuera krediter till kundprofilnivån ytterligare.

## Terminologi

- **Konverteringshändelse:** Alla digitala event eller digitala interaktioner som kunderna gör för att ange en milstolpe i riktning mot ett mål, till exempel konferensregistreringar. Ytterligare exempel är betalda konverteringar, kostnadsfria kontoregistreringar eller kvalificering för en egenskap.

- **Kontaktpunkt:** Alla digitala händelser eller digitala interaktioner som kunderna gör på vägen mot ett mål. Exemplen omfattar tidigare köprelaterade marknadsföringssatsningar, visningar av webbannonsering och betalda sökklick.

## Hämta Attribution AI

>[!NOTE]
>
>Om du inte behöver ladda ned bakgrundsmusik kan du hoppa över det här steget och gå vidare till [nästa steg](#next-steps).

Hämtning av Attribution AI görs via en kombination av API-anrop. För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

När du är klar och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa [användargränssnittshandboken för Attribution AI](./user-guide.md). I den här guiden får du hjälp med att skapa en instans och skicka in den för utbildning och poängsättning.