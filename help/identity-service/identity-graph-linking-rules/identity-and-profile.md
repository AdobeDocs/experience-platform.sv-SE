---
title: Identitetstjänst och kundprofil i realtid
description: Läs mer om relationen mellan identitetstjänsten och kundprofilen i realtid
hide: true
hidefromtoc: true
source-git-commit: 03228eef47100096e98666966c4e5065eb7f478a
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Förstå relationen mellan identitetstjänsten och kundprofilen i realtid

>[!IMPORTANT]
>
>Den här sidan förutsätter att sammanfogningsprincipen använder identitetsdiagrammet. Mer information om kopplingsprofiler i kundprofilen i realtid finns i dokumentationen om [sammanfogningsprinciper och identitetssammanfogning].

Du kan använda identitetstjänsten och kundprofilen i realtid samtidigt, men de två funktionerna i Adobe Experience Platform är inte desamma.

* Du kan använda Identity Service för att generera och underhålla identitetsdiagrammet som sammanför en enskild kunds olika identiteter.
* Du kan använda kundprofilen i realtid för att sammanfoga olika profilfragment och skapa en sammanfogad profil. Den här processen kräver att identitetsdiagrammet används.

I det här dokumentet beskrivs likheter, skillnader och förhållandet mellan identitetstjänsten och kundprofilen i realtid.

## Identitetstjänst kontra kundprofil i realtid

De viktigaste skillnaderna mellan identitetstjänsten och kundprofilen i realtid är följande:

| | Identitetstjänst | Kundprofil i realtid |
| --- | --- |--- |
| **Syfte** | <ul><li>Du kan använda identitetstjänsten för att skapa och hantera identitetsdiagram.</li></ul> | Du kan använda kundprofilen i realtid för att: <ul><li>Skapa en helhetsbild av en kundprofil.</li><li>Visa och hantera profiler</li><li>Segmentprofiler för att skapa målgrupper.</li></ul> |
| **Indata** | <ul><li>Om du vill använda identitetstjänsten måste du ange postdata eller händelser för tidsserier som har minst två fält som är markerade som identitet. Fälten som du markerar som identitet hämtas sedan till identitetstjänsten.</li></ul> | **Om du vill sammanfoga profiler måste du ange**: <ul><li>Profilfragment: representerar en unik primär identitet och motsvarande post- eller händelsedata för det ID:t inom en given datauppsättning.</li><li>Identitetsdiagram: Profilen refererar till identitetsdiagrammet för en viss kundprofil för att identifiera alla profilfragment med samma primära identiteter.</li></ul> **För att kunna kvalificera segment måste du ange**: <ul><li>Sammanfogade profiler: en sammanfogad profil är en enda bild av en kund, där olika profilfragment och identiteter samlas i en heltäckande bild.</li></ul> |
| **Process** | <ul><li>När du har importerat minst två identiteter länkar identitetstjänsten dem tillsammans.</li></ul> | <ul><li>Kundprofil i realtid sammanfogar profilfragment med referenser till motsvarande identitetsdiagram.</li><li>Kvalificera profiler till segment baserat på segmenteringskriterier</li></ul> |
| **Utdata** | <ul><li>Resultatet är ett identitetsdiagram, som är en uppsättning identiteter som relaterar till en individ.</li></ul> | <ul><li>Resultatet är en sammanfogad profil, som är en samlad och heltäckande bild av en viss kund.</li><li>Profiler med segmentmedlemskap definierade</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## Hur skapas en sammanfogad profil?

Läs stegen nedan för att få en bättre förståelse för hur du skapar en sammanfogad profil:

* För det första refererar kundprofilen i realtid till ett identitetsdiagram och hämtar alla identiteter.
* Därefter hämtar profilen alla profilfragment som är relaterade till varje identitet.
* Profilera än sammanfogar alla befintliga händelser och attribut när det är klart.
   * Använd företrädesregler vid behov för att avgöra vilket attribut eller vilken händelse som ska användas

![Ett flödesdiagram som beskriver hur identitetstjänsten och profilsammanslagningen fungerar.](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### Vad innebär det att markera ett fält som identitet?

Att markera eller ange ett fält som identitet är en instruktion för Experience Platform att importera det specifika fältet till identitetstjänsten. Med den här beteckningen kan sedan profilfragment sammanfogas i kundprofilen i realtid. Om det inte finns några profilfragment associerade med identiteten ska du inte ange den som identitet.

#### Förstå primära och sekundära identiteter

När du har markerat fält som identiteter kan de sedan definieras som antingen primära eller sekundära identiteter. Primära och sekundära identiteter är begrepp som ingår i kundprofilen i realtid.

* Den primära identiteten (kallas ibland&quot;primärnyckel&quot;) är den identitet i vilken profilfragment lagras.
* Om det bara finns en identitet i en viss datarad, anges den enskilda identiteten som primär.
* Om det finns två eller flera identiteter kommer en att anges som primär och de återstående kommer att anges som sekundära.

Identitetstjänsten importerar endast fält som har angetts som identitet. Identitetstjänsten lagrar inte information om huruvida en identitet är primär eller sekundär.

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md)
* [Identitetslänkningslogik](./identity-linking-logic.md)