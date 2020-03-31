---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Felsökningsguide för åtkomstkontroll
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Felsökningsguide för åtkomstkontroll

Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform. För frågor och felsökning som rör andra plattformstjänster, se felsökningsguiden för [Experience Platform](../landing/troubleshooting.md).

Experience Platform utnyttjar produktprofiler i [Adobe Admin Console](http://adminconsole.adobe.com) för att tillhandahålla rollbaserad **åtkomstkontroll** som länkar användare med behörigheter och sandlådor.  Mer information finns i [åtkomstkontrollsöversikten](home.md) .

## Var hittar jag mina nuvarande åtkomstbehörigheter?

Om du är systemadministratör, produktadministratör eller produktprofiladministratör för din IMS-organisation kan du visa den tilldelade produktprofilen och de behörigheter som den ger i Adobe Admin Console. I användarhandboken [för](./ui/overview.md) åtkomstkontroll finns anvisningar om hur du navigerar i Admin Console för att visa en produktprofils behörigheter.

Om du inte är administratör kan du fortfarande visa dina nuvarande åtkomstbehörigheter genom att skicka en begäran till `/acl/effective-policies` slutpunkten i API:t för åtkomstkontroll. Mer information finns i avsnittet&quot;Visa gällande principer&quot; i [utvecklarhandboken](./api/effective-policies.md) för åtkomstkontroll.

## Vissa funktioner i plattformsgränssnittet är inte tillgängliga. Hur styrs åtkomsten till dessa funktioner av behörigheter?

Om du inte har åtkomstbehörighet för en viss plattformsfunktion kommer den funktionen att döljas eller nedtonas i Experience Platform-gränssnittet. Om du till exempel vill visa fliken Profiler måste du ha behörigheterna Visa profiler eller Hantera profiler. Kontakta administratören om du behöver ytterligare behörigheter för Experience Platform-funktionerna.

## Hur grupperas behörigheter och vilken grupp innehåller den behörighet jag vill använda?

Behörigheter grupperas och kategoriseras efter de plattformsfunktioner som de gäller (t.ex. datahantering och profilhantering). En fullständig lista över tillgängliga behörigheter och vilka grupper de tillhör finns i avsnittet [](home.md#permissions) Behörigheter i åtkomstkontrollsöversikten.

Mer information om [rollbaserad åtkomstkontroll finns i översikten](home.md) för åtkomstkontroll.