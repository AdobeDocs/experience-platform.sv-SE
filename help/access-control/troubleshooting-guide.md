---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Felsökningsguide för åtkomstkontroll
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Felsökningsguide för åtkomstkontroll

Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform. För frågor och felsökning som rör andra [!DNL Platform] tjänster, se felsökningsguiden för [Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] använder produktprofiler i [Adobe Admin Console](http://adminconsole.adobe.com) för att tillhandahålla rollbaserad **åtkomstkontroll** som länkar användare med behörigheter och sandlådor.  Mer information finns i [åtkomstkontrollsöversikten](home.md) .

## Var hittar jag mina nuvarande åtkomstbehörigheter?

Om du är systemadministratör, produktadministratör eller produktprofiladministratör för din IMS-organisation kan du visa din tilldelade produktprofil och de behörigheter den ger inom Adobe Admin Console. I användarhandboken [för](./ui/overview.md) åtkomstkontroll finns anvisningar om hur du navigerar i [!DNL Admin Console] för att visa en produktprofils behörigheter.

Om du inte är administratör kan du fortfarande visa dina nuvarande åtkomstbehörigheter genom att skicka en begäran till `/acl/effective-policies` slutpunkten i API:t för åtkomstkontroll. Mer information finns i avsnittet&quot;Visa gällande principer&quot; i [utvecklarhandboken](./api/effective-policies.md) för åtkomstkontroll.

## Vissa funktioner i [!DNL Platform] gränssnittet är inte tillgängliga. Hur styrs åtkomsten till dessa funktioner av behörigheter?

Om du inte har åtkomstbehörighet för en viss [!DNL Platform] funktion kommer den funktionen att döljas eller nedtonas i [!DNL Experience Platform] användargränssnittet. Om du till exempel vill visa fliken &quot;[!UICONTROL Profiles]&quot; måste du ha behörigheten &quot;[!UICONTROL View Profiles]&quot; eller &quot;[!UICONTROL Manage Profiles]&quot;. Kontakta administratören om du behöver ytterligare behörigheter för [!DNL Experience Platform] funktioner.

## Hur grupperas behörigheter och vilken grupp innehåller den behörighet jag vill använda?

Behörigheter grupperas och kategoriseras efter de [!DNL Platform] funktioner de gäller (till exempel [!DNL Data Management] och [!DNL Profile Management]). En fullständig lista över tillgängliga behörigheter och vilka grupper de tillhör finns i avsnittet [](home.md#permissions) Behörigheter i åtkomstkontrollsöversikten.

Mer information om [rollbaserad åtkomstkontroll finns i översikten](home.md) för åtkomstkontroll.