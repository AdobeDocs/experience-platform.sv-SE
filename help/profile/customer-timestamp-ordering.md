---
title: Kundens tidsstämpelordning
description: Lär dig hur du lägger till kundens tidsstämpelordning i datauppsättningarna för att säkerställa konsekvens i profildata.
badgePrivateBeta: label="Privat beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Kundens tidsstämpelordning

I Adobe Experience Platform garanteras inte automatisk databeställning vid inmatning av data via direktuppspelning till profilarkivet. Med tidsstämpelsortering kan ni garantera att det senaste meddelandet, enligt den angivna kundtidsstämpeln, kommer att behållas i profilbutiken. Detta gör att profildata blir konsekventa och att profildata förblir synkroniserade med källsystemen.

För att kunna aktivera kundens tidsstämplingsbeställning måste du använda `lastUpdatedDate` fält i [Datatypen External Source System Audit Attributes](../xdm/data-types/external-source-system-audit-attributes.md) och kontakta Adobe Technical Account Manager eller Adobe Customer Care med information om din sandlåda och datauppsättning.

## Begränsningar

Under den här privata betaversionen gäller följande begränsningar när kundens tidsstämpelordning används:

- Du kan bara använda kundens tidsstämpelordning med **profilattribut** inkapslad med **direktuppspelning**.
- Du kan bara använda kundens tidsstämpelordning på **icke-produktion** sandlådor.
- Du kan bara tillämpa kundens tidsstämpelordning på **5** datauppsättningar per sandlåda.
- The `lastUpdatedDate` fältet måste finnas i [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.
- Alla rader med data har skickats **måste** innehåller `lastUpdatedDate` fält. Om det här fältet saknas eller är i ett felaktigt format, kommer det att misslyckas.
- Alla datauppsättningar aktiverade för kundens tidsstämpelordning **måste** vara en ny datauppsättning utan tidigare inkapslade data.
- För varje givet profilfragment är det bara rader som innehåller ett senare `lastUpdatedDate` kommer att förtäras. Om raden inte innehåller en nyare `lastUpdatedDate`, kommer raden att tas bort.

## Recommendations

Tänk på följande när du implementerar kundens tidsstämpelordning:

- Du ansvarar för synkroniseringen av klockorna på alla interna system som skickar data till profilarkivet.
- Du bör ha millisekundnivåprecision i ISO 8061-formaterade tidsstämplar.
- Att använda Data Prep i samordning med kundens tidsstämpelordning är **rekommenderas**, skapar den en kopia av alla inkapslade rader tillsammans med deras tidsstämplar, vilket ger bättre felsökning om det uppstår problem.
