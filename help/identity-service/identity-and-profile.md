---
title: Identitetstjänst och kundprofil i realtid
description: Läs mer om relationen mellan identitetstjänsten och kundprofilen i realtid
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Förstå relationen mellan identitetstjänsten och kundprofilen i realtid

>[!IMPORTANT]
>
>Den här sidan förutsätter att sammanfogningsprincipen använder identitetsdiagrammet. Mer information om sammanfogningsprinciper i kundprofilen i realtid finns i dokumentationen om [sammanfogningsprinciper och identitetssammanfogning](../profile/merge-policies/overview.md#identity-stitching).

Du kan använda identitetstjänsten och kundprofilen i realtid samtidigt, men de två funktionerna i Adobe Experience Platform är inte desamma.

* Du kan använda Identity Service för att generera och underhålla identitetsdiagrammet som sammanför en enskild kunds olika identiteter.
* Du kan använda kundprofilen i realtid för att sammanfoga olika profilfragment och skapa en sammanfogad profil. Den här processen kräver att identitetsdiagrammet används.

I det här dokumentet beskrivs likheter, skillnader och förhållandet mellan identitetstjänsten och kundprofilen i realtid.

## Identitetstjänst kontra kundprofil i realtid

De viktigaste skillnaderna mellan identitetstjänsten och kundprofilen i realtid är följande:

| | Identitetstjänst | Kundprofil i realtid |
| --- | --- |--- |
| **Syfte** | <ul><li>Du kan använda identitetstjänsten för att skapa och hantera identitetsdiagram.</li></ul> | Du kan använda kundprofilen i realtid för att: <ul><li>Skapa en helhetsbild av en kundprofil.</li><li>Visa och hantera profiler.</li></ul> |
| **Indata** | <ul><li>Om du vill använda identitetstjänsten måste du ange postdata eller händelser för tidsserier som har minst två fält som är markerade som identitet. Fälten som du markerar som identitet hämtas sedan till identitetstjänsten.</li></ul> | <ul><li>Profilfragment: representerar en unik primär identitet och motsvarande post- eller händelsedata för det ID:t inom en given datauppsättning.</li><li>Identitetsdiagram: Profilen refererar till identitetsdiagrammet för en viss kundprofil för att identifiera alla profilfragment med samma primära identiteter.</li></ul> |
| **Process** | <ul><li>När du har importerat minst två identiteter länkar identitetstjänsten dem tillsammans.</li></ul> | <ul><li>Kundprofil i realtid sammanfogar profilfragment med referenser till motsvarande identitetsdiagram.</li></ul> |
| **Utdata** | <ul><li>Resultatet är ett identitetsdiagram, som är en uppsättning identiteter som relaterar till en individ.</li></ul> | <ul><li>Resultatet är en sammanfogad profil, som är en samlad och heltäckande bild av en viss kund. Den här profilen kan sedan kvalificera sig för ett segment.</li></ul> |

{style="table-layout:auto"}

## Processen för att skapa sammanfogade profiler

Läs stegen nedan för att få en bättre förståelse för hur du skapar en sammanfogad profil:

* För det första refererar kundprofilen i realtid till ett identitetsdiagram och hämtar alla identiteter.
* Därefter hämtar profil profilfragment med primära identiteter i identitetsdiagrammet.
* Profilera än sammanfogar alla befintliga händelser och attribut när det är klart.
   * Om attributinformation är i konflikt väljs attribut baserat på sammanfogningsmetoden. Mer information finns i översikten [Sammanslagningsprinciper](../profile/merge-policies/overview.md).

![Ett flödesdiagram som beskriver hur identitetstjänsten och profilsammanslagningen fungerar.](./images/merge-profile-process.png)

## Ange ett fält som en identitet

I Experience Data Model (XDM) är det en instruktion för Experience Platform att importera ett visst fält till identitetstjänsten att markera eller ange ett fält som identitet. Med den här beteckningen kan sedan profilfragment sammanfogas i kundprofilen i realtid. Om det inte finns några profilfragment associerade med identiteten ska du inte ange den som identitet.

### Förstå primära och sekundära identiteter

När du har markerat fält som identiteter kan de sedan definieras som antingen primära eller sekundära identiteter. Primära och sekundära identiteter är begrepp som ingår i kundprofilen i realtid.

* Den primära identiteten (kallas ibland&quot;primärnyckel&quot;) är den identitet i vilken profilfragment lagras.
* Om det bara finns en identitet i en viss datarad, anges den enskilda identiteten som primär.
* Om det finns två eller flera identiteter kommer en att anges som primär och de återstående kommer att anges som sekundära.

Identitetstjänsten upprättar länkar mellan identiteter så länge det finns minst två fält markerade som identitet. Identitetstjänsten lagrar inte information om huruvida en identitet är primär eller sekundär.

