---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;tid att leva;ttl;time-to-live;
solution: Experience Platform
title: Händelseförfallodatum för upplevelser
description: Det här dokumentet innehåller allmän vägledning om hur du konfigurerar förfallotider för enskilda Experience Events i en Adobe Experience Platform-datauppsättning.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: bb2d0075b234ec750046e1f28cac07a58a9d7e72
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Förfallodatum för upplevelsehändelser

I Adobe Experience Platform kan du konfigurera förfallotider för alla Experience Events-händelser som är inkapslade i en datauppsättning som är aktiverad för [Kundprofil i realtid](./home.md). På så sätt kan du automatiskt ta bort data från profilarkivet som inte längre är giltiga eller användbara för dina användningsfall.

Händelseförfallotider för upplevelser kan inte konfigureras via plattformens gränssnitt eller API:er. Istället måste ni kontakta supporten för att aktivera Experience Event-förfallotider för era nödvändiga datauppsättningar.

>[!IMPORTANT]
>
>Händelseförfallodatum för upplevelser ska inte förväxlas med datauppsättningens förfallodatum, vilket innebär att hela datauppsättningen tas bort efter förfallodatumet. Dessa konfigureras manuellt via [Adobe Experience Platform Data Hygiene](../hygiene/home.md).

## Automatiserad förfalloprocess

När Experience Event-förfallotider har aktiverats för en profilaktiverad datauppsättning tillämpar Platform automatiskt utgångsvärdena för varje hämtad händelse i en tvåstegsprocess:

1. För alla nya data som hämtas in till datauppsättningen tillämpas utgångsvärdet vid inmatningstiden baserat på händelsens tidsstämpel.
1. Alla befintliga data i datauppsättningen har förfallovärdet retroaktivt tillämpat som en engångsåtgärd i systemet för efterfyllnad. När utgångsvärdet har placerats i datauppsättningen kommer händelser som är äldre än utgångsvärdet att omedelbart tas bort så fort som systemjobbet körs. Alla andra händelser avbryts så snart de når sina förfallovärden från händelsens tidsstämpel. När alla Experience Events har tagits bort och profilen inte längre har några profilattribut finns den inte längre.

>[!WARNING]
>
>När det används är alla data som är äldre än det antal dagar som utgångsvärdet tillåter. **permanent borttagen** och kan inte återställas.

Om du t.ex. angav ett förfallodatum på 30 dagar den 15 maj utförs följande steg:

1. Alla nya händelser får ett förfallovärde på 30 dagar när de importeras.
1. Alla befintliga händelser som har en tidsstämpel som är äldre än 15 april tas omedelbart bort med systemjobbet.
1. Alla befintliga händelser som har en tidsstämpel som är nyare än 15 april har ett förfallovärde 30 dagar efter händelsens tidsstämpel. Om en händelse har en tidsstämpel från den 18 april tas den bort 30 dagar efter tidsstämpelns datum, som blir den 18 maj.

## Effekter på segmentering

För att resultaten ska bli korrekta måste du se till att sökfönstren för dina segment ligger inom gränserna för deras beroende datamängder. Om du t.ex. anger ett förfallovärde på 30 dagar och har ett segment som försöker visa data för upp till 45 dagar sedan, blir den slutliga publiken antagligen felaktig.

Du bör därför behålla samma utgångsvärde för Experience Event för alla datauppsättningar, om det är möjligt, för att undvika att olika utgångsvärden påverkar olika datauppsättningar i segmenteringslogiken.

## Frågor och svar {#faq}

I följande avsnitt visas vanliga frågor om när Experience Event-data förfaller:

### Hur skiljer sig förfallodatumet för Experience Event-data från utgångsdatumet för pseudonyma profildata?

Experience Event-data förfaller och Pseudonymous Profile-data förfaller är kompletterande funktioner.

#### Kornighet

Förfallodatum för Experience Event fungerar på en **datauppsättning** nivå. Därför kan varje datauppsättning ha olika inställningar för när data förfaller.

Förfallodatum för pseudonyma profildata fungerar på en **sandlåda** nivå. Därför kommer förfallodatumet för data att påverka alla profiler i sandlådan.

#### Identitetstyper

Utgångsdatum för Experience Event-data tar bort händelser **endast** baserat på händelsepostens tidsstämpel. De identitetsnamnutrymmen som ingår är **ignorerad** för utgångsändamål.

Förfallodatum för pseudonyma profildata **endast** hanterar profiler som har identitetsdiagram som innehåller identitetsnamnutrymmen som valts av kunden, t.ex. `ECID`, `AAID`eller andra typer av cookies. Om profilen innehåller **alla** ytterligare ID-namnutrymme som **not** i kundens lista kommer profilen att **not** tas bort.

#### Borttagna objekt

Utgångsdatum för Experience Event-data **endast** tar bort händelser och gör **not** ta bort profilklassdata. Profilklassdata tas bara bort när alla data tas bort från **alla** datauppsättningar och det finns **no** återstående profilklassposter för profilen.

Förfallodatum för pseudonyma profiler tar bort **båda** händelse- och profilposter. Detta innebär att även profilklassdata tas bort.

### Hur kan Pseudonymous Profile data förfalla i samband med att Experience Event-data förfaller?

Pseudonyma utgångsdatum för profildata och utgångsdatum för Experience Event-data kan användas som komplement till varandra.

Du borde **alltid** konfigurera Experience Event-dataförfallodatum i era datauppsättningar, baserat på era behov av att lagra data om era kända kunder. När Experience Event-data har förfallit kan du använda Pseudonymous Profile data som förfaller för att automatiskt ta bort pseudonyma profiler. Vanligtvis är dataförfalloperioden för pseudonyma profiler kortare än dataförfalloperioden för Experience Events.

I ett typiskt fall kan du ange att Experience Event-data ska upphöra att gälla baserat på värdena för dina kända användardata, och du kan ange att Pseudonymous-profildata ska ha en mycket kortare varaktighet för att begränsa effekten av pseudonyma profiler på plattformslicensens efterlevnad.
