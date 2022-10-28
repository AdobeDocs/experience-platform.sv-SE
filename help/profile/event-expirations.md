---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;tid att leva;ttl;time-to-live;
solution: Experience Platform
title: Händelseförfallodatum för upplevelser
description: Det här dokumentet innehåller allmän vägledning om hur du konfigurerar förfallotider för enskilda Experience Events i en Adobe Experience Platform-datauppsättning.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# Förfallodatum för upplevelsehändelser

I Adobe Experience Platform kan du konfigurera förfallotider för alla Experience Events-händelser som är inkapslade i en datauppsättning som är aktiverad för [Kundprofil i realtid](./home.md). På så sätt kan du automatiskt ta bort data från datasjön och profilarkivet som inte längre är giltiga eller användbara för dina användningsfall.

Händelseförfallotider för upplevelser kan inte konfigureras via plattformens gränssnitt eller API:er. Istället måste ni kontakta supporten för att aktivera Experience Event-förfallotider för era nödvändiga datauppsättningar.

>[!IMPORTANT]
>
>Händelseförfallodatum för upplevelser ska inte förväxlas med datauppsättningens förfallodatum, vilket innebär att hela datauppsättningen tas bort efter förfallodatumet. Dessa konfigureras manuellt via [Adobe Experience Platform Data Hygiene](../hygiene/home.md).

## Automatiserad förfalloprocess

När Experience Event-förfallotider har aktiverats för en profilaktiverad datauppsättning tillämpar Platform automatiskt utgångsvärdena för varje hämtad händelse i en tvåstegsprocess:

1. För alla nya data som matas in i datauppsättningen tillämpas utgångsvärdet vid intag.
1. Alla befintliga data i datauppsättningen har förfallovärdet retroaktivt tillämpat som en engångsåtgärd i systemet för efterfyllnad. När utgångsvärdet har placerats i datauppsättningen kommer händelser som är äldre än utgångsvärdet att omedelbart tas bort så fort som systemjobbet körs. Alla andra händelser avbryts så snart de når sina förfallovärden från händelsens tidsstämpel.

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
