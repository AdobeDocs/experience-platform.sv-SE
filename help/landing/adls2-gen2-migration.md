---
title: Data Lake Migration to Gen2
description: Läs mer om de nya funktionerna i migreringen av Data Lake till Gen2 i Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake-migrering till Gen2

Adobe Experience Platform migrerar till Gen2 Data Lake. Det här är en ny generation av datasjön som ger plattformsanvändare fördelar som georegionsreplikering, finare rollbaserade åtkomstkontroller (RBAC) och bättre skalning.

## Användarpåverkan

När Adobe migrerar datasjön från Gen1 till Gen 2 kommer användare att kunna **read** från Data Lake, men med alla funktioner som **skriva** till datasjön kommer att påverkas. Nedan finns en lista över funktioner som påverkas:

- **Källor**: Data som kommer in från källorna och olika arbetsflöden för dataöverföring fördröjs. Användarna ser sina data när migreringen är klar.
- **Frågetjänst**: Användare kan utföra frågor men kan inte skriva frågans utdata till en datauppsättning.
- **Kundprofil i realtid**: Data som har skickats till profilarkivet via **batch** Intag är inte tillgängligt under migreringen. Data som hämtas in via **direktuppspelning** Intag är tillgängligt under migreringen. Dessutom kommer inte export av profiler att vara tillgänglig under migreringen.
- **Datavetenskapens arbetsyta**: Skrivningar från Data Science Workspace misslyckas.
- **Segmenteringstjänst**: Målgrupper härledda från **batch** Det går inte att aktivera segmentering under migreringen. Målgrupper härledda från **direktuppspelning** segmenteringen påverkas inte.
- **Customer Journey Analytics**: Data från Customer Journey Analytics-rapporter kan vara inaktuella och kommer inte att uppdateras under migreringen eftersom batchar inte importeras till Data Lake.

## Kommunikation med plattformsanvändare

Adobe kommer att kontakta systemadministratörer för att diskutera effekten av migreringen i detalj och för att bekräfta migreringsdatum och -tider för specifika IMS-organisationer.
