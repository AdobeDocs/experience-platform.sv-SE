---
keywords: Experience Platform;hem;populära ämnen;kantsegmentering;Segmentering;Segmenteringstjänst;segmenteringstjänst;ui guide;streaming edge;
solution: Experience Platform
title: Användargränssnittshandbok för kantsegmentering
topic-legacy: ui guide
description: Kantsegmentering är möjligheten att utvärdera segment i plattformen direkt, vilket möjliggör användning av samma sida och nästa sida.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Användargränssnittsguide för kantsegmentering (beta)

>[!IMPORTANT]
>
>Kantsegmentering är för närvarande en betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Kantsegmentering är möjligheten att omedelbart utvärdera segment i Adobe Experience Platform [på kanten](../../edge/home.md), vilket möjliggör användning av samma sida och nästa sidpersonalisering.

## Frågetyper för kantsegmentering

För närvarande kan endast utvalda frågetyper utvärderas med kantsegmentering. I följande avsnitt finns en lista med frågetyper som kan utvärderas med kantsegmentering och de som för närvarande inte stöds.

### Frågetyper som stöds

En fråga kan utvärderas med kantsegmentering om den uppfyller något av villkoren i följande tabell.

>[!NOTE]
>
>Om frågan matchar någon av frågetyperna i följande tabell utvärderas den automatiskt med kantsegmentering. Den här funktionen bestäms automatiskt av systemet baserat på frågeuttrycket.

| Frågetyp | Detaljer | Exempel |
| ---------- | ------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | Personer som har lagt till ett objekt i kundvagnen. |
| En händelse som refererar till en profil | En segmentdefinition som refererar till ett eller flera profilattribut och en enda inkommande händelse utan tidsbegränsning. | Folk som bor i USA som besökte hemsidan. |
| Negerad enkel händelse med ett profilattribut | En segmentdefinition som refererar till en negerad enkel inkommande händelse och ett eller flera profilattribut | Personer som bor i USA och har **not** besökte hemsidan. |
| En händelse inom ett 24-timmarsfönster | En segmentdefinition som refererar till en enda inkommande händelse inom 24 timmar. | Personer som besökt hemsidan de senaste 24 timmarna. |
| En händelse med ett profilattribut i ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad enkel inkommande händelse inom 24 timmar. | Personer som bor i USA och som har besökt hemsidan de senaste 24 timmarna. |
| Negerad enkel händelse med ett profilattribut inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad enkel inkommande händelse inom 24 timmar. | Personer som bor i USA och har **not** besökte hemsidan de senaste 24 timmarna. |
| Frekvenshändelse inom ett 24-timmarsfönster | En segmentdefinition som refererar till en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. |
| Frekvenshändelse med ett profilattribut inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. |
| Negerad frekvenshändelse med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som inte har besökt hemsidan **mer** än fem gånger de senaste 24 timmarna. |
| Flera inkommande träffar inom en tidsprofil på 24 timmar | En segmentdefinition som refererar till flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **eller** har besökt utcheckningssidan inom de senaste 24 timmarna. |
| Flera händelser med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **och** har besökt utcheckningssidan inom de senaste 24 timmarna. |

## Nästa steg

Den här guiden förklarar hur du utvärderar segment med kantsegmentering på Adobe Experience Platform. Mer information om hur du använder användargränssnittet i Experience Platform finns i [Användarhandbok för segmentering](./overview.md). Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Experience Platform API:er kan du gå till [API-guide för kantsegmentering](../api/edge-segmentation.md).
