---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över sandlådor
topic: overview
translation-type: tm+mt
source-git-commit: 564940f37b66159c84ca7402bd3648010232182b

---


# Översikt över sandlådor

Adobe Experience Platform har tagits fram för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Experience Platform **sandlådor** som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Det här dokumentet innehåller en översikt på hög nivå över sandlådor i Experience Platform.

## Om sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform, som möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. En Experience Platform-instans har stöd för en produktionssandlåda och flera icke-produktionssandlådor, där varje sandlåda har ett eget oberoende bibliotek med plattformsresurser (inklusive scheman, datamängder, profiler och så vidare).  Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor.

Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. Dessutom har icke-produktionssandlådor en återställningsfunktion som tar bort alla kundskapade resurser från sandlådan. Det går inte att konvertera icke-produktionssandlådor till produktionssandlådor.

>[!NOTE] När en sandlåda skapas första gången innehåller den inga data. Eftersom varje sandlåda har ett eget isolerat datalager måste de också importera sina data separat.

Sammanfattningsvis ger sandlådor följande fördelar:

* **Programlivscykelhantering**: Skapa separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.
* **Projekt- och varumärkeshantering**: Tillåt att flera projekt körs parallellt inom samma IMS-organisation, samtidigt som isolering och åtkomstkontroll tillhandahålls. Framtida versioner kommer att ge stöd för driftsättning i flera regioner.
* **Flexibelt ekosystem** för utveckling: Tillhandahåll sandlådor på ett smidigt, skalbart och kostnadseffektivt sätt för prospektering, aktivering och demonstrationssyften.

## Åtkomstkontroll för sandlådor

Som standard har alla användare i en organisation åtkomst till en produktionssandlåda. Åtkomst till icke-produktionssandlådor måste beviljas av en systemadministratör, produktadministratör eller produktprofiladministratör via [Adobe Admin Console](https://adminconsole.adobe.com).

För att du ska kunna visa, skapa, uppdatera eller ta bort icke-produktionssandlådor måste användare även beviljas administratörsbehörighet för sandlådan.

Mer information om hur du hanterar roller och behörigheter för sandlådor finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Sandlådor i användargränssnittet för Experience Platform

I användargränssnittet [för](https://platform.adobe.com)Experience Platform kan användare växla mellan de sandlådor de har tillgång till genom att använda **sandlådeväxlarkontrollen** högst upp till vänster på skärmen.  Användare med administratörsbehörighet för sandlådor har även åtkomst till fliken **Sandlådor** i den vänstra navigeringen, där de kan visa och hantera sandlådor för sin organisation. Mer information om hur du arbetar med sandlådor i användargränssnittet finns i användarhandboken för [sandlådan](ui/overview.md).

## Sandlådor i Experience Platform API:er

När anrop görs till Experience Platform API:er måste ett sandlådenamn anges under rubriken `x-sandbox-name`. När du till exempel anropar [katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) för att visa alla datauppsättningar i produktionssandlådan, visas sandlådans namn (&quot;prod&quot;) som en rubrik i API-begäran:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Om `x-sandbox-name` inte ingår i ett API-anrop använder systemet en standardsandlåda i stället. Det bästa sättet är dock att alltid inkludera den här rubriken i alla API-anrop, även när du använder standardsandlådan. Därför behandlas API-dokumentationen för Experience Platform `x-sandbox-name` som ett obligatoriskt huvud.

### Sandbox-API

Med sandbox-API kan du hantera sandlådor med hjälp av RESTful API-åtgärder. Mer information om hur du använder API:t finns i [utvecklarhandboken](api/getting-started.md) för sandlådor, inklusive korrekt formaterade begäranden och exempelsvar.

## Nästa steg

Genom att läsa det här dokumentet har du lagts till de viktigaste begreppen om sandlådor i Experience Platform. Detaljerade anvisningar om hur du hanterar sandlådor finns i [användarhandboken](ui/overview.md) för användargränssnittet eller [utvecklarhandboken](./api/getting-started.md) för API:t.

Sandlådor fungerar som ett värdefullt verktyg för att isolera plattformsmiljöer för utvecklingsteamet, men du kan också hantera mer detaljerad åtkomstkontroll med hjälp av Adobe Admin Console. Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md) .