---
keywords: Experience Platform;hem;populära ämnen;felsökning;åtkomstkontroll
solution: Experience Platform
title: Felsökningsguide för åtkomstkontroll
description: Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Felsökningsguide för åtkomstkontroll

Det här dokumentet innehåller svar på vanliga frågor om åtkomstkontroll i Adobe Experience Platform. För frågor och felsökning som rör andra [!DNL Platform]-tjänster, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] använder produktprofiler i [Adobe Admin Console](https://adminconsole.adobe.com) för att tillhandahålla rollbaserad åtkomstkontroll, som länkar användare med behörigheter och sandlådor.  Mer information finns i [åtkomstkontrollsöversikten](home.md).

## Var hittar jag mina nuvarande åtkomstbehörigheter?

Om du är systemadministratör, produktadministratör eller produktprofiladministratör för din organisation kan du visa din tilldelade produktprofil och de behörigheter den ger inom Adobe Admin Console. I användarhandboken för [åtkomstkontrollen](./ui/overview.md) finns instruktioner om hur du navigerar i [!DNL Admin Console] för att visa en produktprofils behörigheter.

Om du inte är administratör kan du fortfarande visa dina nuvarande åtkomstbehörigheter genom att skicka en begäran till `/acl/effective-policies`-slutpunkten i åtkomstkontrolls-API:t. Mer information finns i avsnittet Visa gällande principer i [Utvecklarhandbok för åtkomstkontroll](./api/effective-policies.md).

## Vissa funktioner i användargränssnittet för [!DNL Platform] är inte tillgängliga. Hur styrs åtkomsten till dessa funktioner av behörigheter?

Om du inte har åtkomstbehörighet för en viss [!DNL Platform]-funktion kommer den funktionen att döljas eller nedtonas i [!DNL Experience Platform]-gränssnittet. Om du till exempel vill kunna visa fliken [!UICONTROL Profiles] måste du ha behörighet [!UICONTROL View Profiles] eller [!UICONTROL Manage Profiles]. Kontakta administratören om du behöver ytterligare behörigheter för [!DNL Experience Platform]-funktioner.

## Hur grupperas behörigheter och vilken grupp innehåller den behörighet jag vill använda?

Behörigheter grupperas och kategoriseras efter de [!DNL Platform]-funktioner de gäller för (till exempel [!DNL Data Management] och [!DNL Profile Management]). En fullständig lista över tillgängliga behörigheter och vilka grupper de tillhör finns i avsnittet [behörigheter](home.md#permissions) i åtkomstkontrollsöversikten.

Mer information om rollbaserad åtkomstkontroll finns i [åtkomstkontrollsöversikten](home.md).

## Vad händer med behörigheter efter migrering från Adobe IO till företags-ID?

Åtkomstkontrollen använder användar-ID (ett internt unikt ID som tilldelats en användare) för att bevilja behörigheter. När en organisation migreras från Adobe ID till Business ID, kommer alla behörigheter som angetts för dess användare att gå förlorade eftersom användar-ID ändras och åtkomstkontrollen kommer att använda det nyligen genererade användar-ID:t. Om din organisation migreras till ditt företags-ID kontaktar du din Adobe-representant för att migrera ditt användar-ID från Adobe ID till ditt företags-ID.
