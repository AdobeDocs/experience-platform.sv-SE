---
title: Administration - översikt
seo-title: Översikt över CDP-administration i realtid
description: description
seo-description: seo-beskrivning
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Översikt över CDP-administration i realtid

Det här dokumentet innehåller en översikt över administrationsfunktionerna i kunddataplattformen i realtid, som bygger på Adobe Experience Platform.

Med Experience Platform kan administratörer hantera rollbaserad åtkomstkontroll för användare samt hantera virtuella sandlådor för programutveckling.

Följande avsnitt innehåller introduktioner till de centrala komponenterna i Experience Platform-administrationsfunktionerna och länkar till Experience Platform-dokumentation där mer detaljerad information tillhandahålls.

## Åtkomstkontroll

Åtkomstkontroll administreras via [Adobe Admin Console](http://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console så att du kan länka användare med behörigheter och sandlådor. Med den här funktionen kan administratörer ge eller begränsa åtkomst till specifika CDP-funktioner i realtid för definierade användaruppsättningar.

Mer information om åtkomstkontroll finns i [åtkomstkontrollsöversikten](../../access-control/home.md) i dokumentationen för Experience Platform.

>[!IMPORTANT]
>Om du vill ha en detaljerad guide om hur du ger åtkomst till CDP-funktioner i realtid, inklusive hur du aktiverar synlighet i användargränssnittet, följer du stegen i användarhandboken [för](../../access-control/ui/overview.md)åtkomstkontroll, särskilt de som används för att hantera detaljer och ytterligare tjänster för en produktprofil.

## Sandlådor

Adobe Experience Platform (och CDP i realtid via tillägg) är byggt för att berika applikationer för digitala upplevelser i global skala. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Adobe Experience Platform&quot;sandlådor&quot;, vilket gör att du kan partitionera en enda plattformsinstans i separata virtuella miljöer som kan användas för att utveckla och utveckla program för digitala upplevelser.

Mer information om sandlådor finns i översikten över [sandlådor](../../sandboxes/home.md) i dokumentationen för Experience Platform.