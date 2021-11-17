---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: d34b3480b182b4128bb1626326b0de7bf2809985
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 17 november 2021**

## Uppdateringar av befintliga funktioner

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Kund-AI](#customer-ai)

### Attribution AI {#attribution-ai}

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktyta för marknadsföring över kundresor.

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för flera datauppsättningar | Attribution AI kan nu enkelt importera flera datauppsättningar direkt i användargränssnittet utan att behöva mappa och sätta ihop varje datauppsättning. Den nya tidsbesparingsfunktionen ger kraftfullare och exaktare resultat med mer omfattande data från flera datauppsättningar. |
| Mappning av mediekanal och kampanjfält | Attribution AI har nu stöd för mappning av mediekanal- och kampanjfält. Mediekanalmappning mellan datauppsättningar förbättrar insikterna från Attribution AI och ger tydligare resultat som är enkla att tolka. |

Mer information om Attribution AI finns i [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI {#customer-ai}

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, träna eller driftsätta.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för flera datauppsättningar | Kunds-AI kan nu enkelt importera flera datauppsättningar direkt i användargränssnittet utan att behöva mappa och sätta ihop varje datauppsättning. Den nya tidsbesparingsfunktionen ger kraftfullare och exaktare resultat med mer omfattande data från flera datauppsättningar. |
| Anpassade profilattribut | Kund-AI har nu stöd för att definiera anpassade profildatauppsättningsfält (med tidsstämplar) i dina data utöver vanliga händelsefält. Om du använder det här alternativet kan du lägga till ytterligare profilattribut som du anser vara inflytelserika, vilket kan förbättra modellens kvalitet och ge mer korrekta resultat |

Mer information om kundens AI finns i [AI-dokumentation för kund](../../intelligent-services/customer-ai/overview.md).
