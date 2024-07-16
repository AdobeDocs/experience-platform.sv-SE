---
title: Data Lake Migration to Gen2
description: Läs mer om de nya funktionerna i migreringen av Data Lake till Gen2 i Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake-migrering till Gen2

Adobe Experience Platform migrerar till Gen2 Data Lake. Det här är en ny generation av datasjön som ger plattformsanvändare fördelar som georegionsreplikering, finare rollbaserade åtkomstkontroller (RBAC) och bättre skalning.

## Användarpåverkan

När Adobe migrerar datasjön från Gen1 till Gen2 kan användare **läsa** från datasjön, men alla funktioner som **write** har i datasjön påverkas. Nedan finns en lista över funktioner som påverkas:

- **Källor**: Data som kommer från källorna och olika arbetsflöden för dataöverföring fördröjs. Användarna ser sina data när migreringen är klar.
- **Frågetjänst**: Användare kan utföra frågor men kan inte skriva frågans utdata till en datauppsättning.
- **Kundprofil i realtid**: Data som hämtas till profilarkivet via **batch**-inmatning är inte tillgängliga under migreringen. Data som hämtas via **direktuppspelning** är dock tillgängliga under migreringen. Dessutom kommer inte export av profiler att vara tillgänglig under migreringen.
- **Data Science Workspace**: Skrivningar från Data Science Workspace kommer att misslyckas.
- **Segmenteringstjänst**: Målgrupper som härleds från **batch**-segmentering kan inte aktiveras under migreringen. Målgrupper som härleds från segmenteringen **direktuppspelning** påverkas inte.
- **Customer Journey Analytics**: Customer Journey Analytics rapporterar att data kan vara inaktuella och kommer inte att uppdateras under migreringen eftersom batchar inte importeras till Data Lake.

## Kommunikation med plattformsanvändare

Adobe kommer att kontakta systemadministratörer för att i detalj diskutera migreringens konsekvenser och bekräfta migreringsdatum och -tider för specifika organisationer.
