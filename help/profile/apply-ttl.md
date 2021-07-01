---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;tid att leva;ttl;time-to-live;
solution: Experience Platform
title: Time-to-live på datauppsättningar
description: Det här dokumentet innehåller allmän vägledning om TTL (time-to-live) för datauppsättningar i profilbutiken för Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# TTL (Profile Service time-to-live)

Med hjälp av profiltjänsten kan användarna lägga till TTL-värden (time-to-live) på data i profilarkivet. TTL är en mekanism som begränsar den tid som data finns i en datamängd. På så sätt kan du automatiskt ta bort data från profilarkivet som inte längre är användbara för dina användningsfall.

För närvarande har profilen bara stöd för Experience Event TTL.

## Experience Event TTL

Med Experience Event TTL kan ni tillämpa TTL på kundprofilaktiverade datauppsättningar i realtid för att ta bort data från profilarkivet som inte längre är giltiga.

>[!NOTE]
>
>Du måste kontakta supporten för att kunna aktivera Experience Event TTL för dina datauppsättningar.

När Experience Event TTL har aktiverats för en profilaktiverad datauppsättning kommer Platform automatiskt att tillämpa TTL-utgångsvärdet på Experience Event-data i två steg:

1. För alla nya data som matas in i datauppsättningen tillämpas TTL-utgångsvärdet vid intag.
2. Alla befintliga data i datauppsättningen kommer att ha TTL-förfallovärdet retroaktivt tillämpat som en engångsåtgärd i ett system för bakåtfyllnad. När TTL-utgångsvärdet har placerats i datauppsättningen, kommer händelser som är äldre än TTL-utgångsvärdet omedelbart att tas bort så fort som systemjobbet körs. Alla andra händelser avbryts så snart de når sina TTL-utgångsvärden från händelsens tidsstämpel.

>[!NOTE]
>
>När TTL har tillämpats kommer alla data som är äldre än antalet dagar att vara **permanent borttagna** och kan inte återställas.
> 
>Se även till att segmentets uppslagsfönster är inom TTL-gränsen. Annars kan segmentresultaten bli felaktiga när TTL har använts. Om du till exempel tillämpade en TTL på 30 dagar och hade ett segment som försökte visa data för upp till 45 dagar sedan, skulle segmentet skapa felaktiga profiler.
> 
>Därför bör du behålla samma TTL-värde för alla datauppsättningar, om det är möjligt, för att undvika att olika TTL-värden påverkar olika datauppsättningar i segmenteringslogiken.

Om du till exempel tillämpade ett TTL-värde på 30 dagar den 15 maj utförs följande steg:

1. Alla nya händelser får ett TTL-värde på 30 dagar när de importeras.
2. Alla befintliga händelser som har en tidsstämpel som är äldre än 15 april tas omedelbart bort med systemjobbet.
3. Alla befintliga händelser som har en tidsstämpel som är nyare än 15 april får ett TTL-utgångsvärde 30 dagar efter händelsens tidsstämpel. Om en händelse har en tidsstämpel från den 18 april tas den bort trettio dagar efter tidsstämpelns datum, som blir den 18 maj.

