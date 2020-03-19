---
title: Administration - översikt
seo-title: Översikt över CDP-administration i realtid
description: description
seo-description: seo-beskrivning
translation-type: tm+mt
source-git-commit: 33e187053790b98d2f1c36306b38c738833c4659

---


# Översikt över CDP-administration i realtid

Det här dokumentet innehåller en översikt över administrationsfunktionerna i kunddataplattformen i realtid, som bygger på Adobe Experience Platform.

Med Experience Platform kan administratörer hantera rollbaserad åtkomstkontroll för användare samt hantera virtuella sandlådor för programutveckling.

Följande avsnitt innehåller introduktioner till de centrala komponenterna i Experience Platform-administrationsfunktionerna och länkar till Experience Platform-dokumentation där mer detaljerad information tillhandahålls.

## Åtkomstkontroll

Åtkomstkontroll administreras via [Adobe Admin Console](http://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console så att du kan länka användare med behörigheter och sandlådor. Med den här funktionen kan administratörer ge eller begränsa åtkomst till specifika CDP-funktioner i realtid för definierade användaruppsättningar.

Mer information om åtkomstkontroll finns i [åtkomstkontrollsöversikten](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) i dokumentationen för Experience Platform.

>[!IMPORTANT]
>Om du vill ha en detaljerad guide om hur du ger åtkomst till CDP-funktioner i realtid, inklusive hur du aktiverar synlighet i användargränssnittet, följer du stegen i användarhandboken [för](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md)åtkomstkontroll, särskilt de som används för att hantera detaljer och ytterligare tjänster för en produktprofil.

## Sandlådor

Adobe Experience Platform (och CDP i realtid via tillägg) är byggt för att berika applikationer för digitala upplevelser i global skala. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose detta behov tillhandahåller Adobe Experience Platform&quot;sandlådor&quot;, vilket gör att du kan partitionera en enda plattformsinstans i separata virtuella miljöer som kan användas för att utveckla och utveckla program för digitala upplevelser.

Mer information om sandlådor finns i översikten över [sandlådor](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/sandboxes/sandboxes-overview.md) i dokumentationen för Experience Platform.