---
title: Krav för att använda Adobe Experience Platform Web SDK
description: Läs om förutsättningarna för Adobe Experience Platform Web SDK.
keywords: 1st-party domain;CNAME;schema;skapa schema;starta;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 1ff52944be6e9475f57c62793b0e4c671ff8786b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Krav för att använda Adobe Experience Platform Web SDK

Om du vill använda Adobe Experience Platform Web SDK måste du först:

- Låt din organisation tillhandahålla den här funktionen. Om du vill ha åtkomst fyller du i följande [formulär](https://adobe.ly/websdkaccess) och Adobe ger dig tillgång till dataströmmar och Adobe Experience Platform (om det behövs). Observera att Adobe utan extra kostnad kommer att ge dig den nödvändiga tillgången att använda SDK i begränsad omfattning.
- Vi rekommenderar att CNAME (1st-party domain) är aktiverat. Om du redan har en CNAME för Adobe Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men Adobe rekommenderar att du gör det innan du går till produktion. Även om en CNAME-implementering inte ger några fördelar när det gäller cookie-livstid kan den förhindra att vissa annonsblockerare och mindre vanliga webbläsare blockerar SDK-begäranden. I sådana fall kan användning av CNAME förhindra att datainsamlingen avbryts för användare som använder dessa verktyg.

>[!IMPORTANT]
>
>**Observera att från och med 11/10/20 har CNAME-implementeringar från första part en 7-dagars utgång på alla Safari-webbläsare och mobila iOS-enheter.**

- Om webbplatsen redan använder [Experience Cloud ID-tjänst](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) på din webbplats - antingen via Visitor API eller Experience Cloud ID-tjänsttillägget i Adobe Experience Platform Launch - och du vill fortsätta använda det när du migrerar till Adobe Experience Platform Web SDK, måste du använda den senaste versionen av Visitor API eller Experience Cloud ID-tjänsttillägget. Se [ID-migrering](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) för mer information.

## Hantera behörigheter för Adobe Experience Platform Web SDK

För att börja använda Adobe Experience Platform måste du ha rätt [behörigheter](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=en) för att skapa scheman och hantera identiteter. De minimibehörigheter som krävs finns i kategorin Datamodellering och Identiteter.

![](../images/AEP-permission-categories.png)

I kategorin Datamodellering ger du användarna behörigheterna Hantera scheman och Visa scheman.

![](../images/data-modeling-permissions.png)

I kategorin Identity Management ger du användarna behörigheterna Hantera identitetsnamn och Visa identitetsnamnutrymmen.

![](../images/identity-management-permissions.png)
