---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---
# Fragment

## Kvoter och bearbetningstidslinjer {#quotas}

Begäran om att radera poster omfattas av dagliga och månadsvisa gränser för hur många identifierare som får skickas in, beroende på organisationens licensberättigande. Dessa begränsningar gäller för både UI- och API-baserade borttagningsbegäranden.

>[!NOTE]
>
>Du kan skicka upp till **1 000 000 identifierare per dag**, men bara om den återstående månadskvoten tillåter det. Om din månadskvot är mindre än 1 miljon, kan din dagliga inskickning inte överstiga denna gräns.

### Möjlighet att skicka in per produkt varje månad {#quota-limits}

Tabellen nedan visar inlämningsgränser för identifierare per produkt och berättigandenivå. För varje produkt är den månatliga övre gränsen det lägsta av två värden: ett fast identifierartak eller ett procentbaserat tröskelvärde som är knutet till den licensierade datavolymen.

| Produkt | Tillståndsbeskrivning | Månatligt tak (den som är mindre) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP eller Adobe Journey Optimizer | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 5 % av den adresserbara publiken |
| Real-Time CDP eller Adobe Journey Optimizer | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 10 % av den adresserbara publiken |
| Customer Journey Analytics | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 100 identifierare per miljon CJA-rader |
| Customer Journey Analytics | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 200 identifierare per miljon CJA-rader |

>[!NOTE]
>
> De flesta organisationer har lägre månadsgränser baserat på den faktiska adresserbara målgruppen eller CJA-radrättigheterna.

Kvoterna återställs den första dagen i varje kalendermånad. Oanvänd kvot för överföring av **inte**.

>[!NOTE]
>
>Kvoterna baseras på din organisations licensierade månadsberättigande för **skickade identifierare**. Dessa används inte av systemskyddsräcken, men kan övervakas och granskas.
>
>Borttagning av post är en **delad tjänst**. Det högsta antalet licenser som gäller för Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics och eventuella tillägg till Shield.

### Bearbetar tidslinjer för identifieraröverföringar {#sla-processing-timelines}

När du har skickat in en post köas och bearbetas förfrågningar om radering baserat på din berättigandenivå.

| Produkt- och berättigandebeskrivning | Kövaraktighet | Maximal bearbetningstid (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | Upp till 15 dagar | 30 dagar |
| Med tillägget Privacy and Security Shield eller Healthcare Shield | Normalt 24 timmar | 15 dagar |

Om din organisation kräver högre gränser kontaktar du Adobe för att få en tillståndsgranskning.
