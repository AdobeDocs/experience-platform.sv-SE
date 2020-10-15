---
title: Förbered XDM-schemat
seo-title: Förbered XDM-schemat
description: En guide som hjälper dig att skapa XDM-schema i Adobe Experience Platform
seo-description: En guide som hjälper dig att skapa XDM-schema i Adobe Experience Platform
keywords: XDM;schema;create schema;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Förbered ett schema

Experience Platform Edge Network använder Experience Data Model (XDM). XDM är ett dataformat som gör att du kan definiera scheman. Schemat definierar hur Edge Network förväntar sig att data ska formateras. Om du vill skicka data måste du definiera ditt schema.

1. [Skapa ett schema](../../xdm/tutorials/create-schema-ui.md)
2. Lägg till AEP- [!DNL Web SDK ExperienceEvent] mixin i det schema du skapade.
3. Skapa en datauppsättning från det schema du skapade.

Följande video är avsedd att stödja dig när du skapar ett schema, en datauppsättning och en direktuppspelningskälla för dina [!DNL Web SDK] data.


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

Logga in på Adobe Experience Platform Launch och installera AEP Web SDK-tillägget. När du installerar SDK uppmanas du att konfigurera tillägget. Ange det konfigurations-ID som du begärde ovan. Tillägget fyller automatiskt i ditt organisations-ID.

Mer information om olika konfigurationsalternativ finns i [Konfigurera SDK](../fundamentals/configuring-the-sdk.md).

[Läs mer om hur du skapar ditt schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
