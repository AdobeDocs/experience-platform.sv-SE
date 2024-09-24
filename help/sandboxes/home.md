---
keywords: Experience Platform;hem;populära ämnen;sandlåda;Sandlåda;testning;Testa
solution: Experience Platform
title: Översikt över sandlådor
description: Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# Översikt över sandlådor

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Det här dokumentet innehåller en översikt på hög nivå över sandlådor i Experience Platform.

## Om sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor. Det finns två typer av sandlådor som stöds i Experience Platform:

* **Produktionssandlåda**: En produktionssandlåda är avsedd att användas med profiler i din produktionsmiljö. Plattformen gör att du kan skapa flera produktionssandlådor för att tillhandahålla rätt funktionalitet för data samtidigt som driftisoleringen bibehålls. Med den här funktionen kan du dedikera specifika produktionssandlådor till olika affärsområden, varumärken, projekt eller regioner. Produktionssandlådor har stöd för en mängd produktionsprofiler upp till ditt licensierade [!DNL Profile]-åtagande (uppmätt kumulativt i alla dina auktoriserade produktionssandlådor). Du har rätt att använda hela den licensierade totala datavolymen (uppmätt kumulativt i alla dina godkända produktionssandlådor).

* **Utvecklingssandlåda**: En utvecklingssandlåda är en sandlåda som endast kan användas för utveckling och testning med icke-produktionsprofiler. Utvecklingssandlådor har stöd för en mängd icke-produktionsprofiler på upp till 10 % av ditt licensierade [!DNL Profile]-åtagande (uppmätt kumulativt i alla dina auktoriserade utvecklingssandlådor). Du har rätt till upp till
   * Ett batchsegmenteringsjobb per dag, per utvecklingssandlåda.
   * Ett genomsnitt på 120 [!DNL Profile] API-anrop, per [!DNL Profile], per år (mäts kumulativt i alla dina auktoriserade utvecklingssandlådor.

En Experience Platform-instans har stöd för flera produktions- och utvecklingssandlådor, där varje sandlåda har ett eget oberoende bibliotek med plattformsresurser (inklusive scheman, datamängder, profiler och så vidare). Dessutom har både produktions- och utvecklingssandlådor en återställningsfunktion som tar bort alla kundskapade resurser från sandlådan. Utvecklingssandlådor kan inte konverteras till produktionssandlådor.

En standardlicens för Experience Platform ger dig totalt fem sandlådor, som du kan klassificera som  eller utveckling. Du kan licensiera ytterligare paket om 10 sandlådor, upp till totalt högst 75 sandlådor. Dessa ytterligare sandlådor kan användas för att skapa både produktions- och utvecklingssandlådor. Kontakta din företagsadministratör eller din säljare på Adobe för mer information.

Slutligen är standardproduktionssandlådan den första produktionssandlådan som skapas när en organisation skapas för första gången. Med standardproduktionssandlådan kan du importera eller använda data från plattformen, samt acceptera begäranden som inte innehåller värden för ett sandlådenamn eller ett sandbox-ID.

>[!NOTE]
>
>När en sandlåda skapas första gången innehåller den inga data. Eftersom varje sandlåda har ett eget isolerat datalager måste de också importera sina data separat.

Sammanfattningsvis ger sandlådor följande fördelar:

* **Programlivscykelhantering**: Skapa separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.
* **Projekt- och varumärkeshantering**: Tillåt att flera projekt körs parallellt inom samma organisation, samtidigt som isolering och åtkomstkontroll tillhandahålls.
* **Flexibelt ekosystem för utveckling**: Tillhandahåll sandlådor på ett smidigt, skalbart och kostnadseffektivt sätt för prospektering, aktivering och demonstrationssyften.

## Åtkomstkontroll för sandlådor

Som standard har alla användare i en organisation åtkomst till en produktionssandlåda. Åtkomst till icke-produktionssandlådor måste beviljas av en systemadministratör, produktadministratör eller produktprofiladministratör via [Adobe Admin Console](https://adminconsole.adobe.com).

För att du ska kunna visa, skapa, uppdatera eller ta bort icke-produktionssandlådor måste användare även beviljas administratörsbehörighet för sandlådan.

Mer information om hur du hanterar roller och behörigheter för sandlådor finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Sandlådor i användargränssnittet för Experience Platform

I användargränssnittet [Experience Platform](https://platform.adobe.com) kan användare växla mellan de sandlådor de har åtkomst till genom att använda kontrollen **sandlådeväxlare** längst upp till vänster på skärmen.  Användare med administratörsbehörighet för sandlådan har även åtkomst till fliken **[!UICONTROL Sandboxes]** i den vänstra navigeringen, där de kan visa och hantera sandlådor för sin organisation. Mer information om hur du arbetar med sandlådor i användargränssnittet finns i användarhandboken för [sandlådan](ui/overview.md).

## Sandlådor i Experience Platform API:er

När anrop görs till API:er för Experience Platform måste ett sandlådenamn anges under rubriken `x-sandbox-name`. När du till exempel anropar [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) för att visa alla datauppsättningar i Production sandbox, anges sandlådans namn (&quot;prod&quot;) som en rubrik i API-begäran:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Om `x-sandbox-name` inte ingår i ett API-anrop använder systemet en standardsandlåda i stället. Det bästa sättet är dock att alltid inkludera den här rubriken i alla API-anrop, även när du använder standardsandlådan. Därför behandlas `x-sandbox-name` som ett obligatoriskt huvud i API-dokumentationen för Experience Platform.

### Sandbox-API

Med sandbox-API kan du hantera sandlådor med hjälp av RESTful API-åtgärder. Mer information om hur du använder API:t finns i [utvecklarhandboken för sandlådan](api/overview.md), inklusive korrekt formaterade begäranden och exempelsvar.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till de viktigaste begreppen om sandlådor i Experience Platform. Detaljerade anvisningar om hur du hanterar sandlådor finns i [användarhandboken](ui/overview.md) för användargränssnittet eller [utvecklarhandboken](./api/getting-started.md) för API:t.

Sandlådor fungerar som ett värdefullt verktyg för att isolera plattformsmiljöer för utvecklingsteamet, men du kan också hantera mer detaljerad åtkomstkontroll med hjälp av Adobe Admin Console. Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md).
