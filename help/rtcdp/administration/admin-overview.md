---
keywords: rtcdp-administration, översikt;administration, översikt
title: Översikt över administration av kunddataplattform i realtid
seo-title: Översikt över CDP-administration i realtid
description: 'Dokumentet innehåller en översikt över administrationsfunktionerna i kunddataplattformen i realtid med Adobe Experience Platform. '
seo-description: seo-beskrivning
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Översikt över administration av kunddataplattform i realtid

Det här dokumentet innehåller en översikt över administrationsfunktionerna i [!DNL Real-time Customer Data Platform], som drivs av Adobe Experience Platform.

[!DNL Experience Platform] gör att administratörer kan hantera rollbaserad åtkomstkontroll för användare samt hantera virtuella sandlådor för programutveckling.

Följande avsnitt innehåller introduktioner till de centrala komponenterna i administrationsfunktionerna för [!DNL Experience Platform] och länkar till [!DNL Experience Platform]-dokumentation där mer detaljerad information finns.

## Åtkomstkontroll

Åtkomstkontroll administreras via [Adobe Admin Console](http://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i [!DNL Admin Console], vilket gör att du kan länka användare med behörigheter och sandlådor. Med den här funktionen kan administratörer ge eller begränsa åtkomst till specifika CDP-funktioner i realtid för definierade användaruppsättningar.

Mer information om åtkomstkontroll finns i [översikten över åtkomstkontroll](../../access-control/home.md) i dokumentationen för [!DNL Experience Platform].

>[!IMPORTANT]
>
>Om du vill ha en detaljerad guide om hur du beviljar åtkomst till CDP-funktioner i realtid, inklusive hur du aktiverar synlighet i användargränssnittet, följer du stegen i [användarhandboken för åtkomstkontroll](../../access-control/ui/overview.md), särskilt för hantering av detaljer och ytterligare tjänster för en produktprofil.

## Sandlådor

Adobe Experience Platform (och CDP i realtid som tillägg) är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Adobe Experience Platform&quot;sandlådor&quot;, vilket gör att du kan partitionera en enskild [!DNL Platform]-instans i separata virtuella miljöer som kan användas för att utveckla och utveckla program för digitala upplevelser.

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md) i dokumentationen för [!DNL Experience Platform].