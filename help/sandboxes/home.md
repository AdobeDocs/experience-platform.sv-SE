---
keywords: Experience Platform;hem;populära ämnen;sandlåda;Sandlåda;testning;Testa
solution: Experience Platform
title: Översikt över sandlådor
topic: overview
description: Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# Översikt över sandlådor

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Det här dokumentet innehåller en översikt på hög nivå över sandlådor i Experience Platform.

## Om sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. En Experience Platform-instans har stöd för en produktionssandlåda och flera icke-produktionssandlådor, där varje sandlåda har ett eget oberoende bibliotek med plattformsresurser (inklusive scheman, datamängder, profiler och så vidare).  Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor.

Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. Dessutom har icke-produktionssandlådor en återställningsfunktion som tar bort alla kundskapade resurser från sandlådan. Det går inte att konvertera icke-produktionssandlådor till produktionssandlådor. En standardlicens för Experience Platform ger dig fem sandlådor (en och fyra icke-produktioner). Du kan lägga till paket med tio icke-produktionssandlådor, upp till totalt högst 75 sandlådor. Kontakta din IMS-organisationsadministratör eller din Adobe-säljare om du vill ha mer information.

>[!NOTE]
>
>När en sandlåda skapas första gången innehåller den inga data. Eftersom varje sandlåda har ett eget isolerat datalager måste de också importera sina data separat.

Sammanfattningsvis ger sandlådor följande fördelar:

* **Programlivscykelhantering**: Skapa separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.
* **Projekt- och varumärkeshantering**: Tillåt att flera projekt körs parallellt inom samma IMS-organisation, samtidigt som isolering och åtkomstkontroll tillhandahålls. Framtida versioner kommer att ge stöd för driftsättning i flera regioner.
* **Flexibelt ekosystem** för utveckling: Tillhandahåll sandlådor på ett smidigt, skalbart och kostnadseffektivt sätt för prospektering, aktivering och demonstrationssyften.

## Åtkomstkontroll för sandlådor

Som standard har alla användare i en organisation åtkomst till en produktionssandlåda. Åtkomst till icke-produktionssandlådor måste beviljas av en systemadministratör, produktadministratör eller produktprofiladministratör via [Adobe Admin Console](https://adminconsole.adobe.com).

För att du ska kunna visa, skapa, uppdatera eller ta bort icke-produktionssandlådor måste användare även beviljas administratörsbehörighet för sandlådan.

Mer information om hur du hanterar roller och behörigheter för sandlådor finns i [översikten över åtkomstkontroll](../access-control/home.md).

## Sandlådor i användargränssnittet för Experience Platform

I [Experience Platform-användargränssnittet](https://platform.adobe.com) kan användare växla mellan de sandlådor de har åtkomst till genom att använda kontrollen **sandlådeväxlare** högst upp till vänster på skärmen.  Användare med administratörsbehörighet för sandlådan har även åtkomst till fliken **[!UICONTROL Sandboxes]** i den vänstra navigeringen, där de kan visa och hantera sandlådor för sin organisation. Mer information om hur du arbetar med sandlådor i användargränssnittet finns i [användarhandboken för sandlådan](ui/overview.md).

## Sandlådor i Experience Platform API:er

När du anropar API:er för Experience Platform måste du ange ett sandlådenamn under rubriken `x-sandbox-name`. När du till exempel anropar [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) för att visa alla datauppsättningar i produktionssandlådan, anges sandlådans namn (&quot;prod&quot;) som en rubrik i API-begäran:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Om `x-sandbox-name` inte ingår i ett API-anrop använder systemet en standardsandlåda i stället. Det bästa sättet är dock att alltid inkludera den här rubriken i alla API-anrop, även när du använder standardsandlådan. Därför behandlas `x-sandbox-name` som ett obligatoriskt huvud i API-dokumentationen för Experience Platform.

### Sandbox-API

Med sandbox-API kan du hantera sandlådor med hjälp av RESTful API-åtgärder. Mer information om hur du använder API:t finns i [utvecklarhandboken för sandlådor](api/getting-started.md), inklusive korrekt formaterade begäranden och exempelsvar.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till de viktigaste begreppen om sandlådor i Experience Platform. Detaljerade anvisningar om hur du hanterar sandlådor finns i [användarhandboken](ui/overview.md) för användargränssnittet och i [utvecklarhandboken](./api/getting-started.md) för API:t.

Sandlådor fungerar som ett värdefullt verktyg för att isolera plattformsmiljöer för utvecklingsteamet, men du kan också hantera mer detaljerad åtkomstkontroll med hjälp av Adobe Admin Console. Mer information finns i [översikten över åtkomstkontroll](../access-control/home.md).