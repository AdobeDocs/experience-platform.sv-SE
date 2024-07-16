---
title: Kundens tidsstämpelordning
description: Lär dig hur du lägger till kundens tidsstämpelordning i datauppsättningarna för att säkerställa konsekvens i profildata.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Kundens tidsstämpelordning

I Adobe Experience Platform garanteras inte dataordningen som standard när data hämtas via direktuppspelning till profilarkivet. Med tidsstämpelsortering kan ni garantera att det senaste meddelandet, enligt den angivna kundtidsstämpeln, kommer att behållas i profilbutiken. Alla inaktuella meddelanden tas sedan bort och **inte** kommer att vara tillgängliga för användning i underordnade tjänster som använder profildata som segmentering och destinationer. Detta gör att profildata blir konsekventa och att profildata förblir synkroniserade med källsystemen.

Använd fältet `extSourceSystemAudit.lastUpdatedDate` i fältgruppen [Externa Source-systemgranskningsattribut](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) för att aktivera kundens tidsstämpelordning och kontakta din tekniska kontohanterare på Adobe eller Adobe kundtjänst för din sandlåda och datauppsättningsinformation.

## Begränsningar

Under den här privata betaversionen gäller följande begränsningar när kundens tidsstämpelordning används:

- Du kan bara använda kundens tidsstämpelordning med **profilattribut** som är inkapslade med **direktuppspelningsinmatning** i profilarkivet.
   - Det finns **inga** beställningsgarantier för data i datasjön eller identitetstjänsten.
- Du kan bara använda kundens tidsstämpelordning i **icke-produktion** -sandlådor.
- Du kan bara tillämpa kundens tidsstämpelordning på **5**-datauppsättningar per sandlåda.
- Du **kan inte** använda direktuppspelande uppdateringar för att skicka uppdateringar på en del rader i en datauppsättning där kundens tidsstämpelordning är aktiverad.
- Fältet `extSourceSystemAudit.lastUpdatedDate` **måste** vara i formatet [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). När du använder ISO 8601-formatet måste **vara** som en fullständig datetime i formatet `yyyy-MM-ddTHH:mm:ss.sssZ` (till exempel `2028-11-13T15:06:49.001Z`).
- Alla rader med data som har infogats **måste** innehålla fältet `extSourceSystemAudit.lastUpdatedDate` som en fältgrupp på den översta nivån. Det innebär att fältet **måste** inte kapslas i XDM-schemat. Om det här fältet saknas eller har ett felaktigt format, kommer den felaktiga posten **inte** att kapslas och ett motsvarande felmeddelande skickas.
- Alla datauppsättningar som är aktiverade för kundens tidsstämpelsortering **måste** vara en ny datauppsättning utan tidigare inkapslade data.
- Endast rader som innehåller en senare `extSourceSystemAudit.lastUpdatedDate` kommer att kapslas för alla angivna profilfragment. Rader som innehåller en `extSourceSystemAudit.lastUpdatedDate` som är antingen äldre eller lika gammal ignoreras.

## Rekommendationer

Tänk på följande när du implementerar kundens tidsstämpelordning:

- Du ansvarar för att synkronisera klockorna på alla interna system som skickar data till profilarkivet.
- Du bör ha millisekundnivåprecision i ISO 8061-formaterade tidsstämplar.
