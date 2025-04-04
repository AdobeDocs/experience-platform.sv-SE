---
keywords: rtcdp-administration, översikt;administration, översikt
title: Real-Time Customer Data Platform Administration - översikt
description: Dokumentet innehåller en översikt över administrationsfunktionerna i Adobe Real-Time Customer Data Platform, som drivs av Adobe Experience Platform.
feature: Access Control, Get Started, Sandboxes
exl-id: c5bdeac6-345a-4ef1-bc5a-a993f565b9d6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Real-Time Customer Data Platform - översikt

Det här dokumentet innehåller en översikt över administrationsfunktionerna i [!DNL Adobe Real-Time Customer Data Platform], som drivs av Adobe Experience Platform.

I [!DNL Experience Platform] kan administratörer hantera rollbaserad åtkomstkontroll för användare samt hantera virtuella sandlådor för programutveckling.

Följande avsnitt innehåller introduktioner till de centrala komponenterna i [!DNL Experience Platform]-administrationsfunktionerna och länkar till [!DNL Experience Platform]-dokumentation där mer detaljerad information tillhandahålls.

## Åtkomstkontroll

Attributbaserad åtkomstkontroll administreras via behörighetsgränssnittet. Den här funktionen utnyttjar roller i användargränssnittet för behörigheter, så att du kan länka användare med behörigheter och sandlådor. Med den här funktionen kan administratörer ge eller begränsa åtkomsten till specifika Real-Time CDP-funktioner för angivna användargrupper.

Mer information om åtkomstkontroll finns i [attributbaserad åtkomstkontroll ](/help/access-control/abac/overview.md) i [!DNL Experience Platform]-dokumentationen.

>[!IMPORTANT]
>
>Om du vill ha en detaljerad guide om hur du beviljar åtkomst till Real-Time CDP-funktioner, inklusive hur du aktiverar synlighet i användargränssnittet, följer du stegen i [användarhandboken för åtkomstkontroll](../../access-control/ui/overview.md), särskilt för hantering av information och ytterligare tjänster för en produktprofil.

## Sandlådor

Adobe Experience Platform (och Real-Time CDP som tillägg) är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Adobe Experience Platform *sandlådor*, vilket gör att du kan partitionera en enskild [!DNL Experience Platform]-instans i separata virtuella miljöer som kan användas för att utveckla och utveckla program för digitala upplevelser. Du kan använda sandlådeverktygen för att förbättra konfigurationsnoggrannheten över sandlådor och sömlöst exportera och importera sandlådekonfigurationer mellan sandlådor. Följ stegen som anges i användargränssnittsguiden för [sandlådan](../../sandboxes/ui/sandbox-tooling.md).

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md) i [!DNL Experience Platform]-dokumentationen.
