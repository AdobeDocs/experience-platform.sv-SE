---
keywords: Experience Platform;hem;populära ämnen;felsökning;åtkomstkontroll
solution: Experience Platform
title: Felsökningsguide för åtkomstkontroll
topic-legacy: troubleshooting guide
description: Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Felsökningsguide för åtkomstkontroll

Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform. För frågor och felsökning relaterade till andra [!DNL Platform] tjänster, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] utnyttjar produktprofiler i [Adobe Admin Console](https://adminconsole.adobe.com) för att tillhandahålla rollbaserad åtkomstkontroll, länka användare med behörigheter och sandlådor.  Se [åtkomstkontroll - översikt](home.md) för mer information.

## Var hittar jag mina nuvarande åtkomstbehörigheter?

Om du är systemadministratör, produktadministratör eller produktprofiladministratör för din IMS-organisation kan du visa din tilldelade produktprofil och de behörigheter den ger inom Adobe Admin Console. Se [användarhandbok för åtkomstkontroll](./ui/overview.md) för instruktioner om hur du navigerar i [!DNL Admin Console] för att visa en produktprofils behörigheter.

Om du inte är administratör kan du fortfarande visa dina nuvarande åtkomstbehörigheter genom att skicka en begäran till `/acl/effective-policies` slutpunkt i åtkomstkontrolls-API. Se avsnittet&quot;Visa gällande profiler&quot; i [Utvecklarhandbok för åtkomstkontroll](./api/effective-policies.md) för mer information.

## Vissa funktioner i [!DNL Platform] Gränssnittet är inte tillgängligt. Hur styrs åtkomsten till dessa funktioner av behörigheter?

Om du inte har åtkomstbehörighet för en viss [!DNL Platform] funktionen kommer den funktionen att vara dold eller nedtonad i [!DNL Experience Platform] Gränssnitt. Om du till exempel vill visa[!UICONTROL Profiles]&quot; måste du antingen ha &quot;[!UICONTROL View Profiles]&quot; eller &quot;[!UICONTROL Manage Profiles]&quot; behörigheter. Kontakta administratören om du behöver ytterligare behörigheter för [!DNL Experience Platform] funktioner.

## Hur grupperas behörigheter och vilken grupp innehåller den behörighet jag vill använda?

Behörigheterna grupperas och kategoriseras av [!DNL Platform] funktioner som de gäller för (t.ex. [!DNL Data Management] och [!DNL Profile Management]). En fullständig lista över tillgängliga behörigheter och vilka grupper de tillhör finns i [permissions section](home.md#permissions) i översikten över åtkomstkontrollen.

Se [åtkomstkontroll - översikt](home.md) för mer information om rollbaserad åtkomstkontroll.
