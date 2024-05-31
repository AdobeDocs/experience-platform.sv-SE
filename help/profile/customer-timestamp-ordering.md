---
title: Kundens tidsstämpelordning
description: Lär dig hur du lägger till kundens tidsstämpelordning i datauppsättningarna för att säkerställa konsekvens i profildata.
badgePrivateBeta: label="Privat beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Kundens tidsstämpelordning

I Adobe Experience Platform garanteras inte dataordningen som standard när data hämtas via direktuppspelning till profilarkivet. Med tidsstämpelsortering kan ni garantera att det senaste meddelandet, enligt den angivna kundtidsstämpeln, kommer att behållas i profilbutiken. Alla inaktuella meddelanden tas sedan bort och kommer att **not** vara tillgängliga för användning i tjänster i senare led som använder profildata som segmentering och destinationer. Detta gör att profildata blir konsekventa och att profildata förblir synkroniserade med källsystemen.

Använd kommandot `extSourceSystemAudit.lastUpdatedDate` fält i [Datatypen External Source System Audit Attributes](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) och kontakta Adobe Technical Account Manager eller Adobe Customer Care med information om din sandlåda och datauppsättning.

## Begränsningar

Under den här privata betaversionen gäller följande begränsningar när kundens tidsstämpelordning används:

- Du kan bara använda kundens tidsstämpelordning med **profilattribut** inkapslad med **direktuppspelning** i profilarkivet.
   - Det finns **no** Beställningsgarantier för data i sjön eller identitetstjänsten.
- Du kan bara använda kundens tidsstämpelordning på **icke-produktion** sandlådor.
- Du kan bara tillämpa kundens tidsstämpelordning på **5** datauppsättningar per sandlåda.
- Du **inte** använda direktuppspelande upserts för att skicka uppdateringar av delar av rader i en datauppsättning där kundens tidsstämpelordning är aktiverad.
- The `extSourceSystemAudit.lastUpdatedDate` fält **måste** finns i [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. När formatet ISO 8601 används är det **måste** vara som en fullständig datetime i formatet `yyyy-MM-ddTHH:mm:ss.sssZ` (till exempel `2028-11-13T15:06:49.001Z`).
- Alla rader med data har skickats **måste** innehåller `extSourceSystemAudit.lastUpdatedDate` som en fältgrupp på den översta nivån. Detta innebär att det här fältet **måste** inte kapslas i XDM-schemat. Om det här fältet saknas eller har ett felaktigt format kommer den felaktiga posten att **not** hämtas och ett motsvarande felmeddelande skickas.
- Alla datauppsättningar aktiverade för kundens tidsstämpelordning **måste** vara en ny datauppsättning utan tidigare inkapslade data.
- För varje givet profilfragment är det bara rader som innehåller ett senare `extSourceSystemAudit.lastUpdatedDate` kommer att förtäras. Rader som innehåller `extSourceSystemAudit.lastUpdatedDate` antingen är äldre eller också kommer samma ålder att kastas.

## Recommendations

Tänk på följande när du implementerar kundens tidsstämpelordning:

- Du ansvarar för att synkronisera klockorna på alla interna system som skickar data till profilarkivet.
- Du bör ha millisekundnivåprecision i ISO 8061-formaterade tidsstämplar.
