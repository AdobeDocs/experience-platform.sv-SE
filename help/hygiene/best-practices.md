---
title: Bästa praxis för avancerad livscykelhantering av data
description: Lär dig hur du effektivt hanterar förfrågningar om datahygien i Adobe Experience Platform med hjälp av API:t Advanced Data Lifecycle Management (Advanced Data Lifecycle Management) och API:t Data Hygiene. Den här guiden beskriver bästa praxis, till exempel maximering av identiteter per begäran, specificering av enskilda datauppsättningar och anpassning efter API-begränsning för att förhindra flaskhalsar. Dokumentet innehåller riktlinjer för att ställa in automatisk rensning av datauppsättningar, hur arbetsorderstatus ska övervakas samt detaljerade metoder för hämtning av svar. Följ dessa rutiner för att effektivisera behandlingen av begäranden och optimera svarstiderna.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Bästa tillvägagångssätt för avancerad livscykelhantering av data

Använd API:t för avancerad livscykelhantering för data och API:t för datahygien för att effektivt hantera rensningsbegäranden och ta bort data från Adobe Experience Platform tjänster. Följ dessa metodtips för att effektivisera behandlingen av begäranden och optimera svarstiderna.

## Förhandskrav {#prerequisites}

Den här handboken kräver en fungerande förståelse av arbetsytan Datalängd och [API:t för datahygien](./api/overview.md). Innan du fortsätter med det här dokumentet bör du bekanta dig med guiderna för [avancerad livscykelhantering](./home.md) och [att skapa begäranden om postborttagning](./ui/record-delete.md) eller [förfallodatum för datauppsättningar i gränssnittet](./ui/dataset-expiration.md), eller via API:t.

## Riktlinjer för att skapa arbetsorder {#work-order-creation-guidelines}

Du kan använda slutpunkten `/workorder` i API:t för datahygien för att programmässigt hantera begäranden om postborttagning i Experience Platform. Med den här slutpunkten kan du skapa en borttagningsbegäran, kontrollera dess status eller uppdatera en befintlig begäran. Läs [Slutpunktsdokumentet för arbetsorder](./api/workorder.md) om du vill veta mer om hur du utför dessa åtgärder med API:t.

>[!TIP]
>
>En arbetsorder är en strukturerad begäran som utför specifika datahanteringsåtgärder, t.ex. datarensning eller dataomvandling, för att säkerställa en effektiv och systematisk behandling.

Följ de här riktlinjerna för att optimera dina inskickade rensningsbegäranden:

1. **Maximera identiteter per begäran:** Inkludera upp till 100 000 identiteter per rensningsbegäran för att öka effektiviteten. Genom att gruppera flera identiteter i en enda begäran kan du minska antalet API-anrop och minimera risken för prestandaproblem på grund av överdrivna förfrågningar om en identitet. Skicka in förfrågningar med maximalt antal identiteter för att få snabbare behandling, eftersom arbetsorder batchas för att bli effektiva.
2. **Ange enskilda datauppsättningar:** Ange den enskilda datauppsättning som ska bearbetas för maximal effektivitet.
3. **Tänk på API-begränsning:** Tänk på API-begränsning för att förhindra långsam hämtning. Mindre förfrågningar (&lt; 100 ID:n) med högre frekvens kan resultera i 429 svar och kräva att de skickas in igen med acceptabel frekvens.

### Hantera 429 fel {#manage-429-errors}

Om du får ett 429-fel anger det att du har överskridit det tillåtna antalet begäranden under en viss tidsperiod. Följ dessa standarder för att hantera 429 fel effektivt:

- **Läs huvudet Försök igen**: När ett 429-fel returneras kontrollerar du svarsrubriken Försök igen efter. Den här rubriken anger väntetiden innan begäran görs om.
- **Implementera återförsökslogik**: Använd värdet för Försök igen efter om du vill implementera återförsökslogik i programmet och se till att försök görs efter den angivna tiden för att undvika efterföljande 429 fel.
- **Gruppera dina förfrågningar**: Undvik att skicka in många små förfrågningar i snabb följd. Gruppera istället flera identiteter i en enda begäran för att minska antalet anrop och minimera risken för att hacka hastighetsbegränsningar.

## Utgångsdatum för datauppsättning {#dataset-expiration}

Ställ in automatisk rensning av datauppsättningar för kortlivade data. Använd slutpunkten `/ttl` i API:t för datahygien för att schemalägga förfallodatum för datamängder för rensning baserat på en angiven tid eller ett angivet datum. Läs slutpunktshandboken för datauppsättningens förfallodatum om du vill veta hur du [skapar en förfallotid för en datauppsättning](./api/dataset-expiration.md) och de [godkända frågeparametrarna](./api/dataset-expiration.md#query-params).

## Övervaka arbetsorder och utgångsstatus för datauppsättning {#monitor}

Du kan effektivt övervaka förloppet för din livscykelhantering av data med hjälp av **I/O-händelser**. En I/O-händelse är en mekanism för att ta emot meddelanden i realtid om ändringar eller uppdateringar i olika tjänster inom Experience Platform.

I/O-händelsemeddelanden kan skickas till en konfigurerad webkrok för att möjliggöra automatisering av aktivitetsövervakning. Om du vill få aviseringar via webkrok måste du registrera din webkrok för Experience Platform-aviseringar i Adobe Developer Console. Detaljerade instruktioner finns i guiden om att [prenumerera på Adobe I/O-händelsemeddelanden](../observability/alerts/subscribe.md).

Använd följande metoder och riktlinjer för livscykeln för data för att effektivt hämta och övervaka jobbstatus:

### I/O-händelser {#io-events}

För att effektivt kunna övervaka förloppet för dina uppgifter under datans livscykel ställer du in och använder I/O-händelser genom att följa dessa steg:

- Konfigurera webhooks för att ta emot push-meddelanden om statusändringar.
- Använd meddelanden för att övervaka förloppet och få uppdateringar när de är klara.
- Undvik att implementera avsökningsmekanismer för att minimera API-trafiken.

### Hämta detaljerade svar för en enskild arbetsorder {#retrieve-detailed-work-order-response}

Använd följande tillvägagångssätt för att få detaljerad information om enskilda arbetsorder:

- Gör en GET-begäran till `/workorder/{work_order_id}`-slutpunkten om du vill ha detaljerade svarsdata.
- Hämta produktspecifika svar och framgångsmeddelanden.
- Undvik att använda den här metoden för vanliga avsökningsaktiviteter.

Genom att följa dessa standarder kan du effektivt hantera rensningsbegäranden och optimera svarstiderna inom Advanced Data Lifecycle Management.
