---
solution: Experience Platform
title: Användargränssnittshandbok för kantsegmentering
description: Lär dig hur du använder kantsegmentering för att utvärdera segmentdefinitioner i plattformar direkt, vilket möjliggör användning av samma sida och nästa sidpersonalisering.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# Användargränssnittsguide för kantsegmentering

>[!NOTE]
>
>Kantsegmentering är nu allmänt tillgängligt för alla plattformsanvändare. Om du skapade definitioner för kantsegment under betaversionen kommer dessa segmentdefinitioner att fortsätta att fungera.

Kantsegmentering är möjligheten att omedelbart utvärdera segment i Adobe Experience Platform [på kanten](../../web-sdk/home.md), vilket möjliggör användning av samma sida och nästa sidpersonalisering.

>[!IMPORTANT]
>
> Kantdata lagras på en edge-serverplats som ligger närmast den plats där de samlades in och kan lagras på en annan plats än den som anges som Adobe Experience Platform datacenter (eller huvudserver).
>
> Dessutom kommer kantsegmenteringsmotorn endast att efterleva begäranden på kanten där det finns **en** primär markerad identitet, vilket är förenligt med icke-kantbaserade primära identiteter.

## Frågetyper för kantsegmentering {#query-types}

För närvarande kan endast utvalda frågetyper utvärderas med kantsegmentering. I följande avsnitt finns en lista med frågetyper som kan utvärderas med kantsegmentering och de som för närvarande inte stöds.

En fråga kan utvärderas med kantsegmentering om den uppfyller något av villkoren i följande tabell.

>[!NOTE]
>
>Om frågan matchar någon av frågetyperna i följande tabell utvärderas den automatiskt med kantsegmentering. Den här funktionen bestäms automatiskt av systemet baserat på frågeuttrycket.

| Frågetyp | Information | Exempel | PQL-exempel |
| ---------- | ------- | ------- | ----------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | Personer som har lagt till ett objekt i kundvagnen. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| En profil | Alla segmentdefinitioner som refererar till ett enskilt profilattribut | Folk som bor i USA. | `homeAddress.countryCode = "US"` |
| En händelse som refererar till en profil | En segmentdefinition som refererar till ett eller flera profilattribut och en enda inkommande händelse utan tidsbegränsning. | Folk som bor i USA som besökte hemsidan. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Negerad enkel händelse med ett profilattribut | En segmentdefinition som refererar till en negerad enkel inkommande händelse och ett eller flera profilattribut | Personer som bor i USA och har **not** besökte hemsidan. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| En händelse i ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse inom en angiven tidsperiod. | Personer som besökt hemsidan de senaste 24 timmarna. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| En händelse med ett profilattribut inom ett relativt tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse, med ett eller flera profilattribut, och som inträffar inom ett relativt tidsfönster på mindre än 24 timmar. | Personer som bor i USA och som har besökt hemsidan de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Negerad enkel händelse med ett profilattribut i ett tidsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad enkel inkommande händelse inom en tidsperiod. | Personer som bor i USA och har **not** besökte hemsidan de senaste 24 timmarna. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| Frekvenshändelse inom ett 24-timmarsfönster | En segmentdefinition som refererar till en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frekvenshändelse med ett profilattribut inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Negerad frekvenshändelse med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som inte har besökt hemsidan **mer** än fem gånger de senaste 24 timmarna. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Flera inkommande träffar inom en tidsprofil på 24 timmar | En segmentdefinition som refererar till flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **eller** har besökt utcheckningssidan inom de senaste 24 timmarna. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Flera händelser med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **och** har besökt utcheckningssidan inom de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. | Personer som bor i USA och som är i segmentet &quot;befintligt&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Fråga som refererar till en karta | En segmentdefinition som refererar till en egenskapskarta. | Personer som har lagt till i kundvagnen baserat på externa segmentdata. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

En segmentdefinition **not** aktiveras för kantsegmentering i följande scenario:

- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment` -händelse.
   - Om segmentdefinitionen i `inSegment` -händelsen är bara profil, segmentdefinitionen **kommer** aktiveras för kantsegmentering.
- I segmentdefinitionen används&quot;Ignorera år&quot; som en del av tidsbegränsningarna.

## Nästa steg

Den här guiden förklarar hur du utvärderar segmentdefinitioner med kantsegmentering i Adobe Experience Platform. Mer information om hur du använder användargränssnittet i Experience Platform finns i [Användarhandbok för segmentering](./overview.md). Om du vill veta hur du utför liknande åtgärder och arbetar med segmentdefinitioner med Experience Platform API:er kan du gå till [API-guide för kantsegmentering](../api/edge-segmentation.md).

## Bilaga

I följande avsnitt visas vanliga frågor om kantsegmentering:

### Hur lång tid tar det innan en segmentdefinition är tillgänglig på Edge Network?

Det tar upp till en timme innan en segmentdefinition är tillgänglig på Edge Network.
