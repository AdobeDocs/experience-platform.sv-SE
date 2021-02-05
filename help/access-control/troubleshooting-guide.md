---
keywords: Experience Platform;hem;populära ämnen;felsökning;åtkomstkontroll
solution: Experience Platform
title: Felsökningsguide för åtkomstkontroll
topic: troubleshooting guide
description: Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Felsökningsguide för åtkomstkontroll

Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform. För frågor och felsökning som rör andra [!DNL Platform]-tjänster, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] använder produktprofiler i  [Adobe Admin ](http://adminconsole.adobe.com) Console för att tillhandahålla rollbaserad åtkomstkontroll som länkar användare med behörigheter och sandlådor.  Mer information finns i [översikten över åtkomstkontroll](home.md).

## Var hittar jag mina nuvarande åtkomstbehörigheter?

Om du är systemadministratör, produktadministratör eller produktprofiladministratör för din IMS-organisation kan du visa din tilldelade produktprofil och de behörigheter den ger inom Adobe Admin Console. Se [användarhandboken för åtkomstkontroll](./ui/overview.md) för instruktioner om hur du navigerar i [!DNL Admin Console] för att visa en produktprofils behörigheter.

Om du inte är administratör kan du fortfarande visa dina nuvarande åtkomstbehörigheter genom att skicka en begäran till `/acl/effective-policies`-slutpunkten i åtkomstkontrolls-API:t. Mer information finns i avsnittet Visa gällande principer i [Utvecklarhandbok för åtkomstkontroll](./api/effective-policies.md).

## Vissa funktioner i gränssnittet för [!DNL Platform] är inte tillgängliga. Hur styrs åtkomsten till dessa funktioner av behörigheter?

Om du inte har åtkomstbehörighet för en viss [!DNL Platform]-funktion kommer den funktionen att döljas eller nedtonas i [!DNL Experience Platform]-gränssnittet. Om du till exempel vill visa fliken [!UICONTROL Profiles] måste du ha behörigheterna [!UICONTROL View Profiles] eller [!UICONTROL Manage Profiles]. Kontakta administratören om du behöver ytterligare behörigheter för [!DNL Experience Platform]-funktioner.

## Hur grupperas behörigheter och vilken grupp innehåller den behörighet jag vill använda?

Behörigheter grupperas och kategoriseras av de [!DNL Platform]-funktioner de gäller för (till exempel [!DNL Data Management] och [!DNL Profile Management]). En fullständig lista över tillgängliga behörigheter och vilka grupper de tillhör finns i [behörighetssektionen](home.md#permissions) i åtkomstkontrollsöversikten.

Mer information om rollbaserad åtkomstkontroll finns i [översikten över åtkomstkontroll](home.md).