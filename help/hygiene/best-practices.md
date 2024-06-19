---
title: Bästa praxis för avancerad livscykelhantering av data
description: Lär dig hur du effektivt hanterar förfrågningar om datahygien i Adobe Experience Platform med hjälp av API:t Advanced Data Lifecycle Management (Advanced Data Lifecycle Management) och API:t Data Hygiene. Den här guiden beskriver bästa praxis, till exempel maximering av identiteter per begäran, specificering av enskilda datauppsättningar och anpassning efter API-begränsning för att förhindra flaskhalsar. Dokumentet innehåller riktlinjer för att ställa in automatisk rensning av datauppsättningar, hur arbetsorderstatus ska övervakas samt detaljerade metoder för hämtning av svar. Följ dessa rutiner för att effektivisera behandlingen av begäranden och optimera svarstiderna.
source-git-commit: 92667fd4da093e56dcf06ae1696484671d9fdd38
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Bästa tillvägagångssätt för avancerad livscykelhantering av data

Använd API:t för avancerad livscykelhantering för data och API:t för datahygien för att effektivt hantera rensningsbegäranden och ta bort data från Adobe Experience Platform tjänster. Följ dessa metodtips för att effektivisera behandlingen av begäranden och optimera svarstiderna.

## Förhandskrav {#prerequisites}

Den här handboken kräver en fungerande förståelse av arbetsytan Datalängd och [API för datahygien](./api/overview.md). Innan du fortsätter med det här dokumentet bör du bekanta dig med guiderna på [Avancerad livscykelhantering av data](./home.md) och [skapa postborttagningsbegäranden](./ui/record-delete.md) eller [förfallodatum för datauppsättning i användargränssnittet](./ui/dataset-expiration.md)eller via API:t.

## Riktlinjer för att skapa arbetsorder {#work-order-creation-guidelines}

Du kan använda `/workorder` slutpunkt i Data Hygiene API för att programmässigt hantera begäranden om postborttagning i Experience Platform. Med den här slutpunkten kan du skapa en borttagningsbegäran, kontrollera dess status eller uppdatera en befintlig begäran. Se [Slutpunktsdokument för arbetsorder](./api/workorder.md) om du vill lära dig hur du utför dessa åtgärder med API:t.

>[!TIP]
>
>En arbetsorder är en strukturerad begäran som utför specifika datahanteringsåtgärder, t.ex. datarensning eller dataomvandling, för att säkerställa en effektiv och systematisk behandling.

Följ de här riktlinjerna för att optimera dina inskickade rensningsbegäranden:

1. **Maximera identiteter per begäran:** Inkludera upp till 100 000 identiteter per rensningsförfrågan för att öka effektiviteten. Genom att gruppera flera identiteter i en enda begäran kan du minska antalet API-anrop och minimera risken för prestandaproblem på grund av överdrivna förfrågningar om en identitet.
2. **Ange enskilda datauppsättningar:** För maximal effektivitet anger du den enskilda datauppsättning som ska bearbetas.
3. **Skicka flera förfrågningar:** Skicka in flera förfrågningar med maximalt antal identiteter för att få snabbare behandling, eftersom arbetsorder batchas för att bli effektiva.
4. **Tänk på API-begränsning:** Tänk på API-begränsning för att förhindra långsamma driftstopp. Mindre förfrågningar (&lt; 100 ID:n) med högre frekvens kan resultera i 429 svar och kräva att de skickas in igen med acceptabel frekvens.

### Hantera 429 fel {#manage-429-errors}

Om du får ett 429-fel anger det att du har överskridit det tillåtna antalet begäranden under en viss tidsperiod. Följ dessa standarder för att hantera 429 fel effektivt:

- **Läs rubriken Försök igen efter**: När ett 429-fel returneras ska du kontrollera svarsrubriken&quot;Försök igen efter&quot;. Den här rubriken anger väntetiden innan begäran görs om.
- **Implementera återförsökslogik**: Använd värdet &quot;Försök igen efter&quot; för att implementera återförsökslogik i programmet och se till att försök görs efter den angivna tiden för att undvika efterföljande 429 fel.
- **Gruppera dina förfrågningar**: Undvik att skicka in många små förfrågningar i snabb följd. Gruppera istället flera identiteter i en enda begäran för att minska antalet anrop och minimera risken för att hacka hastighetsbegränsningar.

## Utgångsdatum för datauppsättning {#dataset-expiration}

Ställ in automatisk rensning av datauppsättningar för kortlivade data. Använd `/ttl` slutpunkt i Data Hygiene API för att schemalägga förfallodatum för datauppsättningar. Använd `/ttl` slutpunkt som utlöser en rensning av en datauppsättning baserat på en angiven tid eller ett angivet datum. Läs slutpunktshandboken för datauppsättningens förfallodatum om du vill veta hur du [skapa en förfallotid för datauppsättning](./api/dataset-expiration.md) och [godkända frågeparametrar](./api/dataset-expiration.md#query-params).

## Övervaka arbetsorder och utgångsstatus för datauppsättning {#monitor}

Ni kan effektivt övervaka hur er livscykelhantering av data fortskrider med hjälp av **I/O-händelser**. En I/O-händelse är en mekanism för att ta emot meddelanden i realtid om ändringar eller uppdateringar i olika tjänster inom plattformen.

I/O-händelsemeddelanden kan skickas till en konfigurerad webkrok för att möjliggöra automatisering av aktivitetsövervakning. Om du vill få meddelanden via webkrok måste du registrera din webkrok för plattformsaviseringar i Adobe Developer Console. Se guiden på [prenumerera på händelsemeddelanden från Adobe I/O](../observability/alerts/subscribe.md) för detaljerade anvisningar.

Använd följande metoder och riktlinjer för livscykeln för data för att effektivt hämta och övervaka jobbstatus:

### I/O-händelser {#io-events}

För att effektivt kunna övervaka förloppet för dina uppgifter under datans livscykel ställer du in och använder I/O-händelser genom att följa dessa steg:

- Konfigurera webhooks för att ta emot push-meddelanden om statusändringar.
- Använd meddelanden för att övervaka förloppet och få uppdateringar när de är klara.
- Undvik att implementera avsökningsmekanismer för att minimera API-trafiken.

### Hämta detaljerade svar för en enskild arbetsorder {#retrieve-detailed-work-order-response}

Använd följande tillvägagångssätt för att få detaljerad information om enskilda arbetsorder:

- Gör en GET-förfrågan till `/workorder{work_order_id}` slutpunkt för detaljerade svarsdata.
- Hämta produktspecifika svar och framgångsmeddelanden.
- Undvik att använda den här metoden för vanliga avsökningsaktiviteter.

Genom att följa dessa standarder kan du effektivt hantera rensningsbegäranden och optimera svarstiderna inom Advanced Data Lifecycle Management.
