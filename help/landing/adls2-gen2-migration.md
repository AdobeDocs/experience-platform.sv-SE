---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Adobe Experience Platform Data Lake-migrering till Gen2

Adobe Experience Platform migrerar till Gen2 Data Lake. Det här är en ny generation av datasjön som ger plattformsanvändare fördelar som georegionsreplikering, finare rollbaserade åtkomstkontroller (RBAC) och bättre skalning.

## Användarpåverkan

Medan Adobe migrerar datasjön från Gen1 till Gen2 kan användare **läsa** från datasjön, men alla funktioner som **skriver** in i datasjön påverkas. Nedan finns en lista över funktioner som påverkas:

- **Källor**: Data som kommer in från källorna och olika arbetsflöden för dataöverföring fördröjs. Användarna ser sina data när migreringen är klar.
- **Frågetjänst**: Användare kan utföra frågor men kan inte skriva frågans utdata till en datauppsättning.
- **Kundprofil** i realtid: Data som matas in till profilarkivet via **batchinmatning** är inte tillgängliga under migreringen. Data som hämtas via **direktuppspelning** blir dock tillgängliga under migreringen. Dessutom kommer inte export av profiler att vara tillgänglig under migreringen.
- **Data Science Workspace**: Skrivningar från Data Science Workspace misslyckas.
- **Segmenteringstjänst**: Målgrupper som härleds från **batchsegmentering** kan inte aktiveras under migreringen. Målgrupper som härrör från **direktuppspelad** segmentering påverkas inte.
- **Customer Journey Analytics**: Data från Customer Journey Analytics-rapporter kan vara inaktuella och kommer inte att uppdateras under migreringen eftersom batchar inte importeras till Data Lake.

## Kommunikation med plattformsanvändare

Adobe kommer att kontakta systemadministratörer för att diskutera effekten av migreringen i detalj och för att bekräfta migreringsdatum och -tider för specifika IMS-organisationer.