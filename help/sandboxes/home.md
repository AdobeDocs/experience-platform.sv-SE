---
keywords: Experience Platform;hem;populära ämnen;sandlåda;Sandlåda;testning;Testa
solution: Experience Platform
title: Översikt över sandlådor
description: Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Översikt över sandlådor

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Det här dokumentet innehåller en översikt på hög nivå över sandlådor i Experience Platform.

## Om sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor. Det finns två typer av sandlådor som stöds i Experience Platform:

* **Produktionssandlåda**: En produktionssandlåda är avsedd att användas med profiler i din produktionsmiljö. Plattformen gör att du kan skapa flera produktionssandlådor för att tillhandahålla rätt funktionalitet för data samtidigt som driftisoleringen bibehålls. Med den här funktionen kan du dedikera specifika produktionssandlådor till olika affärsområden, varumärken, projekt eller regioner. Produktionssandlådor har stöd för en mängd produktionsprofiler upp till din licens [!DNL Profile] -engagemang (mäts kumulativt i alla dina godkända produktionssandlådor). Du har rätt att använda en licensierad genomsnittsprofil per auktoriserad [!DNL Profile] (uppmätt kumulativt i alla dina godkända produktionssandlådor).
* **Utvecklingssandlåda**: En utvecklingssandlåda är en sandlåda som endast kan användas för utveckling och testning med icke-produktionsprofiler. Utvecklingssandlådor har stöd för en mängd icke-produktionsprofiler på upp till 10 % av de licensierade [!DNL Profile] -engagemang (mäts kumulativt i alla dina godkända utvecklingssandlådor). Du har rätt till upp till:
   * En genomsnittlig icke-produktionsprofil på 75 kB per godkänd icke-produktionsprofil (uppmätt kumulativt i alla dina godkända utvecklingssandlådor).
   * Ett batchsegmenteringsjobb per dag, per utvecklingssandlåda.
   * Ett genomsnitt på 120 [!DNL Profile] API-anrop, per [!DNL Profile], per år (mäts kumulativt i alla dina godkända utvecklingssandlådor.

En Experience Platform-instans har stöd för flera produktions- och utvecklingssandlådor, där varje sandlåda har ett eget oberoende bibliotek med plattformsresurser (inklusive scheman, datamängder, profiler och så vidare). Dessutom har både produktions- och utvecklingssandlådor en återställningsfunktion som tar bort alla kundskapade resurser från sandlådan. Utvecklingssandlådor kan inte konverteras till produktionssandlådor.

En standardlicens för Experience Platform ger dig totalt fem sandlådor, som du kan klassificera som  eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor. Dessa ytterligare sandlådor kan användas för att skapa både produktions- och utvecklingssandlådor. Kontakta din IMS-organisationsadministratör eller din Adobe-säljare om du vill ha mer information.

Slutligen är standardproduktionssandlådan den första produktionssandlådan som skapas när en IMS-organisation skapas. Med standardproduktionssandlådan kan du importera eller använda data från plattformen, samt acceptera begäranden som inte innehåller värden för ett sandlådenamn eller ett sandbox-ID.

>[!NOTE]
>
>När en sandlåda skapas första gången innehåller den inga data. Eftersom varje sandlåda har ett eget isolerat datalager måste de också importera sina data separat.

Sammanfattningsvis ger sandlådor följande fördelar:

* **Hantering av programlivscykler**: Skapa separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.
* **Projekt- och varumärkeshantering**: Tillåt att flera projekt körs parallellt inom samma IMS-organisation, samtidigt som isolering och åtkomstkontroll tillhandahålls. Framtida versioner kommer att ge stöd för driftsättning i flera regioner.
* **Flexibla ekosystem för utveckling**: Tillhandahåll sandlådor på ett smidigt, skalbart och kostnadseffektivt sätt för prospektering, aktivering och demonstrationssyften.

## Åtkomstkontroll för sandlådor

Som standard har alla användare i en organisation åtkomst till en produktionssandlåda. Åtkomst till icke-produktionssandlådor måste beviljas av en systemadministratör, produktadministratör eller produktprofiladministratör via [Adobe Admin Console](https://adminconsole.adobe.com).

För att du ska kunna visa, skapa, uppdatera eller ta bort icke-produktionssandlådor måste användare även beviljas administratörsbehörighet för sandlådan.

Mer information om hur du hanterar roller och behörigheter för sandlådor finns i [åtkomstkontroll - översikt](../access-control/home.md).

## Sandlådor i användargränssnittet för Experience Platform

I [Experience Platform användargränssnitt](https://platform.adobe.com)kan användare växla mellan de sandlådor de har tillgång till genom att använda **sandlådeväxlare** överst till vänster på skärmen.  Användare med administratörsbehörighet för sandlådan har även åtkomst till **[!UICONTROL Sandboxes]** i den vänstra navigeringen, där de kan visa och hantera sandlådor för sin organisation. Mer information om hur du arbetar med sandlådor i användargränssnittet finns i [användarhandbok för sandlåda](ui/overview.md).

## Sandlådor i Experience Platform API:er

När anrop görs till API:er för Experience Platform måste ett sandlådenamn anges under rubriken `x-sandbox-name`. När du till exempel anropar [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) Om du vill visa alla datauppsättningar i Production-sandlådan anges sandlådans namn (&quot;prod&quot;) som en rubrik i API-begäran:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

If `x-sandbox-name` finns inte med i ett API-anrop. Systemet använder i stället en standardsandlåda. Det bästa sättet är dock att alltid inkludera den här rubriken i alla API-anrop, även när du använder standardsandlådan. Därför behandlas API-dokumentationen för Experience Platform `x-sandbox-name` som ett obligatoriskt sidhuvud.

### Sandbox-API

Med sandbox-API kan du hantera sandlådor med hjälp av RESTful API-åtgärder. Se [utvecklarguide för sandlådor](api/overview.md) om du vill ha detaljerad information om hur du använder API:t, inklusive korrekt formaterade begäranden och exempelsvar.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till de viktigaste begreppen om sandlådor i Experience Platform. Detaljerade steg om hur du hanterar sandlådor finns i [användarhandbok](ui/overview.md) för användargränssnittet eller [utvecklarhandbok](./api/getting-started.md) för API.

Sandlådor fungerar som ett värdefullt verktyg för att isolera plattformsmiljöer för utvecklingsteamet, men du kan också hantera mer detaljerad åtkomstkontroll med hjälp av Adobe Admin Console. Se [åtkomstkontroll - översikt](../access-control/home.md) för mer information.
