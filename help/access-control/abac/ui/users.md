---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Attributbaserad åtkomstkontroll Hantera användare
description: Det här dokumentet innehåller information om hur du hanterar användare och användargrupper via gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: afd883c530ab1b335888e79b5f4075e774fced4b
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Hantera användare {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="Vad är användare?"
>abstract="Användare är de personer som har tillgång till Experience Platform. En enskild användares åtkomst till en organisations resurser hanteras via roller."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Hantera roller"

Om du vill visa användarinformation och roller som de är tilldelade till väljer du fliken **[!UICONTROL Users]**.

![Sidan Användare visas med fliken [!UICONTROL Users] markerad.](../../images/flac-ui/flac-users-tab.png)

En lista över användare visas. Välj den användare du vill visa i listan. Du kan också använda sökfältet för att söka efter användaren genom att ange användarens namn eller e-postadress.

Fliken Detaljer innehåller en översikt över användaren. I översikten visas användarnamn, kontotyp, e-post, autentiserings-ID, kontaktinformation och platsinformation.

![Sidan med användarinformation med fliken [!UICONTROL Details] och användarprofilen markerad.](../../images/flac-ui/flac-users-details.png)

Välj fliken **[!UICONTROL Roles]** för att visa de roller som användaren är tilldelad till.

![Rollsidan visas med fliken [!UICONTROL Roles] och rollen markerad.](../../images/flac-ui/flac-users-roles.png)

## Åtkomstkontroll för utvecklare och API med Experience Platform behörigheter

>[!NOTE]
>
>Det är bara systemadministratörer som kan visa och hantera API-autentiseringsuppgifter i behörigheter.

Övergången till Adobe Experience Platform-behörigheter innehåller ytterligare steg som måste slutföras för det utvecklar-API-arbetsflöde som tidigare var baserat på roller. Mer information finns i handboken om [API-autentisering](../../../landing/api-authentication.md).

Följande video är avsedd att ge stöd för din förståelse av utvecklares och API:s autentiseringsuppgifter.

>[!VIDEO](https://video.tv.adobe.com/v/3446402/?learn=on&captions=swe)

## Nästa steg

Du har nu lärt dig hur du visar användarinformation och vilka roller de för närvarande läggs till i. Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll](../overview.md).
