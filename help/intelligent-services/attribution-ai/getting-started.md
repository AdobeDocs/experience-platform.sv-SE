---
keywords: Experience Platform;komma igång;attribuering;populära ämnen
feature: Attribution AI
title: Komma igång med Attribution AI
topic-legacy: Getting started
description: Följande handledningar kräver förståelse för de olika Adobe Experience Platform-tjänster som används för att använda Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: a14f857f87482e1468211152976530c718d56e38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Komma igång med Attribution AI

Följande stödlinjer kräver förståelse för de olika [!DNL Adobe Experience Platform] tjänster som används i Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument:

- [Experience Data Model (XDM) - systemöversikt](../../xdm/home.md): XDM är den grundläggande miljön som [!DNL Adobe Experience Cloud]som drivs av Experience Platform för att leverera rätt budskap till rätt person, i rätt kanal, vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster.
- [Grunderna för schemakomposition](../../xdm/schema/composition.md): Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i [!DNL Adobe Experience Platform].
- [Byggscheman](../../xdm/tutorials/create-schema-ui.md): I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.

Attribution AI kräver att datauppsättningar följer CEE-schemat (Consumer Experience Events), som är ett [Experience Data Model (XDM)](../../xdm/home.md) schemafältgrupp. Kontakta Adobe support på attributionai-support@adobe.com för att implementera eller göra ändringar i dessa data. Om det finns uppgifter om medieleveranser kan du göra ytterligare analyser, till exempel inkrementella intäkter och avkastning. Om det finns tillgängliga kundprofildata kan du attribuera krediter till kundprofilnivån ytterligare.

## Terminologi

- **Konverteringshändelse:** Digitala event eller digital interaktion som kunderna gör för att ange en milstolpe i riktning mot ett mål, som konferensregistreringar. Ytterligare exempel är betalda konverteringar, kostnadsfria kontoregistreringar eller kvalificering för en egenskap.

- **Pekpunkt:** Alla digitala händelser eller digitala interaktioner som kunderna gör på vägen mot ett mål. Exemplen omfattar tidigare köprelaterade marknadsföringssatsningar, visningar av webbannonsering och betalda sökklick.

## Hämta Attribution AI

>[!NOTE]
>
>Om du inte behöver ladda ned bakgrundsmusik kan du hoppa över det här steget och gå vidare till [nästa steg](#next-steps).

Hämtning av Attribution AI görs via en kombination av API-anrop. För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

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

## Åtkomstkontroll {#access-control}

När rollbaserad åtkomstkontroll används **Visa Attribution AI** och **Hantera Attribution AI** behörighet ger åtkomst till olika funktioner i Attribution AI. The **Hantera Attribution AI** låter dig **skapa**, **klona**, **redigera**, **delete**, **enable**, eller **disable** en instans while **Visa Attribution AI** låter dig **read** eller **visa** den. The **skapa**, **redigera** och **delete** åtgärder registreras av granskningsloggar.

Läs dokumentationen för att lära dig mer [tilldela behörigheter för åtkomstkontroll](../../../help/access-control/home.md) eller hur [använda granskningsloggar för att övervaka åtkomst och aktivitet](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nästa steg {#next-steps}

När du är klar och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa följande [Användargränssnittshandbok](./user-guide.md). I den här guiden får du hjälp med att skapa en instans och skicka in den för utbildning och poängsättning.
