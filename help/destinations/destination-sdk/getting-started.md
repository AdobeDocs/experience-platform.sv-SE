---
description: På den här sidan beskrivs hur du autentiserar och börjar använda Adobe Experience Platform Destination SDK. Det innehåller instruktioner om hur du får inloggningsuppgifter för Adobe I/O, ett sandlådenamn och åtkomstkontrollbehörighet för målredigering.
title: Komma igång med Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---

# Komma igång

## Översikt {#overview}

På den här sidan beskrivs hur du autentiserar och börjar använda Adobe Experience Platform Destination SDK. Det innehåller instruktioner om hur du får inloggningsuppgifter för Adobe I/O, ett sandlådenamn och åtkomstkontrollbehörighet för målredigering.

## Terminologi {#terminology}

I den här handboken används plattformsspecifika begrepp, som IMS-organisation och sandlådor. Läs [Experience Platform ordlista](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) för definitioner av dessa och andra termer.

## Hämta nödvändiga autentiseringsuppgifter {#obtain-authentication-credentials}

Destinationen SDK använder [Adobe I/O](https://www.adobe.io/) gateway för autentisering. Om du vill göra API-anrop till Destinationens SDK slutpunkter måste du ange vissa rubriker i dina API-anrop. Samarbeta med Adobe Exchange-teamet för att konfigurera autentisering för dig till [Adobe Developer Console](https://developer.adobe.com/console).

Om du vill anropa Destination SDK API-slutpunkter följer du [Självstudiekurs om autentisering av Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Starta självstudiekursen från &quot;[Generera en API-nyckel, IMS-org-ID och klienthemlighet](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot; steg. Adobe Exchange-teamet hanterar de föregående stegen åt dig. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Destination SDK-API-anrop, vilket visas nedan:

* `x-api-key: {API_KEY}`, även kallat klient-ID
* `x-gw-ims-org-id: {ORG_ID}`, även kallat organisations-ID
* `Authorization: Bearer {ACCESS_TOKEN}`. Åtkomsttoken har en förfallotid på 24 timmar, uttryckt i millisekunder, så du måste uppdatera den. Uppdatera åtkomsttoken genom att upprepa stegen som beskrivs i självstudiekursen för autentisering.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Ägarskap och sandlådor för mål {#destination-ownership}

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till Destination SDK kräver rubriker som anger namnet på sandlådan som åtgärden utförs i:

* `x-sandbox-name: {SANDBOX_NAME}`

Adobe Exchange-teamet tillhandahåller ditt sandlådenamn, som du måste använda i anrop till Destination SDK API-slutpunkter.

## Rollbaserad åtkomstkontroll (RBAC) {#rbac}

Använda Destination SDK-API-slutpunkterna som beskrivs i [referensdokumentation](./configuration-options.md)behöver du **[!UICONTROL Destination Authoring]** behörighet för åtkomstkontroll. Arbeta med Adobe Exchange-teamet för att få den här behörigheten tilldelad dig i [Adobe Admin Console](https://adminconsole.adobe.com/).

![Behörighet för målredigering](./assets/destination-authoring-permission.png)

Mer information finns i följande dokument för Experience Platform Access Control:

* [Hantera behörigheter för en produktprofil](/help/access-control/ui/permissions.md)
* [Tillgängliga behörigheter för Experience Platform](/help/access-control/home.md#permissions)
* [Adobe Admin Console-dokumentation](https://helpx.adobe.com/se/enterprise/using/admin-console.html)

## Ytterligare överväganden {#additional-considerations}

* Alla ändringar du gör i målkonfigurationer, oavsett om du skapar eller redigerar en destinationskonfiguration, måste granskas och godkännas av Adobe. Ändringarna återspeglas i destinationerna först när granskningen är klar.
* Endast användare som tillhör samma organisation och har åtkomst till sandlådan kan redigera målkonfigurationen.

## Nästa steg {#next-steps}

Genom att följa stegen i den här artikeln fick du inloggningsuppgifter för Adobe I/O, ett sandlådenamn och åtkomstkontrollbehörighet för målredigering. Sedan kan du konfigurera ett mål med Destination SDK.

* Läs följande konfigurationsguider, beroende på måltyp:

   * [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](./configure-destination-instructions.md)
   * [Använd Destination SDK för att konfigurera ett filbaserat mål](./configure-file-based-destination-instructions.md)

* För alla åtgärder, se [API-dokumentation för målredigering](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Använd [Postman-samling för målredigerings-API](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) för att konfigurera destinationen med Destination SDK API-slutpunkterna. Om du vill komma igång med Postman går du till [steg för att importera miljöer och samlingar](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) och [videoguide för att skapa Postman-miljön](https://video.tv.adobe.com/v/28832).
