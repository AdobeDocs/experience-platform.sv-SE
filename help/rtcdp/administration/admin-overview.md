---
keywords: rtcdp-administration, översikt;administration, översikt
title: Real-time Customer Data Platform Administration - översikt
description: Dokumentet innehåller en översikt över administrationsfunktionerna i Adobe Real-time Customer Data Platform, som drivs av Adobe Experience Platform.
feature: Access Control, Get Started, Sandboxes
exl-id: c5bdeac6-345a-4ef1-bc5a-a993f565b9d6
source-git-commit: a8c9543bb003a99dcd85712d202482511c0a5608
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Real-time Customer Data Platform - översikt

Dokumentet innehåller en översikt över administrationsfunktionerna i [!DNL Adobe Real-Time Customer Data Platform], som drivs av Adobe Experience Platform.

[!DNL Experience Platform] gör att administratörer kan hantera rollbaserad åtkomstkontroll för användare samt hantera virtuella sandlådor för programutveckling.

I följande avsnitt beskrivs de centrala komponenterna i [!DNL Experience Platform] administrationsfunktioner och innehåller länkar till [!DNL Experience Platform] dokumentation där mer detaljerad information tillhandahålls.

## Åtkomstkontroll

Attributbaserad åtkomstkontroll administreras via behörighetsgränssnittet. Den här funktionen utnyttjar roller i användargränssnittet för behörigheter, så att du kan länka användare med behörigheter och sandlådor. Med den här funktionen kan administratörer ge eller begränsa åtkomsten till specifika Real-Time CDP-funktioner för angivna användargrupper.

Mer information om åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](/help/access-control/abac/overview.md) i [!DNL Experience Platform] dokumentation.

>[!IMPORTANT]
>
>Om du vill ha en detaljerad guide om hur du ger åtkomst till Real-Time CDP-funktioner, inklusive hur du aktiverar synlighet i användargränssnittet, följer du stegen i [användarhandbok för åtkomstkontroll](../../access-control/ui/overview.md), särskilt för hantering av detaljer och ytterligare tjänster för en produktprofil.

## Sandlådor

Adobe Experience Platform (och Real-Time CDP som tillägg) är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

Adobe Experience Platform tillhandahåller *sandlådor*, vilket gör att du kan partitionera en enda [!DNL Platform] till separata virtuella miljöer som kan användas för att utveckla och utveckla applikationer för digitala upplevelser. Du kan använda sandlådeverktygen för att förbättra konfigurationsnoggrannheten över sandlådor och sömlöst exportera och importera sandlådekonfigurationer mellan sandlådor. Följ stegen i [gränssnittshandbok för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md).

Mer information om sandlådor finns i [översikt över sandlådor](../../sandboxes/home.md) i [!DNL Experience Platform] dokumentation.
