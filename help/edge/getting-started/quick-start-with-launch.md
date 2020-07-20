---
title: Snabbstart med Launch
seo-title: Adobe Experience Platform Web SDK snabbstart med Launch
description: Snabbstartsguide för hur du använder Experience Platform Web SDK-tillägget för att samla in data
seo-description: Snabbstartsguide för hur du använder Experience Platform Web SDK-tillägget för att samla in data
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---


# Välkommen

Den här guiden tar dig igenom de olika stegen för hur du konfigurerar Adobe Experience Platform i Adobe Launch [!DNL Web SDK] . Du måste ha behörighet och vara på tillåtelselista för att kunna använda den här funktionen. Om du vill komma med på väntelistan kontaktar du din CSM. Om du vill använda den här funktionen måste du dessutom:

- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME för Adobe Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men du behöver en innan du går till produktion
- Använd den senaste versionen av tjänsten för besökar-ID

## Skapa ett konfigurations-ID

Du kan skapa ett konfigurations-ID med hjälp av [edge-konfigurationsverktyget](../fundamentals/edge-configuration.md) i Adobe Launch. På så sätt kan du aktivera Edge Network för att skicka data till de olika lösningarna. På sidan [Edge Configuration Tool](../fundamentals/edge-configuration.md) finns mer information om hur du hittar de olika alternativen.

>[!NOTE]
>
>Din organisation måste vara på tillåtelselista för att kunna använda funktionen. Kontakta din CSM om du vill lägga till i tillåtelselista.

## Förbered ett schema

Data tas som XDM [!DNL Experience Platform Edge Network] . XDM är ett dataformat som gör att du kan definiera scheman. Schemat definierar hur data [!DNL Edge Network] förväntas formateras. För att kunna skicka data måste du definiera ditt schema. Se till att du slutför följande:

1. [Skapa ett schema](../../xdm/tutorials/create-schema-ui.md)
2. Lägg till AEP- [!DNL Web SDK ExperienceEvent] mixin i det schema du skapade.
3. Skapa en datauppsättning från det schema du skapade.

Följande video är avsedd att stödja dig när du skapar ett schema, en datauppsättning och en direktuppspelningskälla för dina [!DNL Web SDK] data.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Installera SDK i Adobe Launch

Logga in på Adobe Launch och installera `AEP Web SDK` tillägget. När du installerar SDK uppmanas du att konfigurera tillägget. Ange det konfigurations-ID som du begärde ovan. Tillägget fyller automatiskt i ditt organisations-ID.

Mer information om olika konfigurationsalternativ finns i [Konfigurera SDK](../fundamentals/configuring-the-sdk.md).

## Skapa ett dataelement baserat på ditt schema

I Adobe Launch skapar du ett dataelement som refererar till schemat genom att ändra tillägget till AEP [!DNL Web SDK] och ange typen till XDM-objekt. Detta läser in ditt schema och gör att du kan mappa dataelement till olika delar av schemat.

![Datumelement i start](../../assets/edge_data_element.png)

## Skicka en händelse

När tillägget har installerats börjar du skicka händelser genom att lägga till en sendEvent-åtgärd från AEP- [!DNL Web SDK] tillägget i en regel. Var noga med att lägga till det dataelement du nyss skapade i händelsen som XDM-data. Vi rekommenderar att du skickar minst en händelse varje gång en sida läses in.

Mer information om hur du spårar händelser finns i [Spåra händelser](../fundamentals/tracking-events.md).

## Nästa steg

När du har data som flödar kan du göra följande:

- [Skapa ditt schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Läs mer om felsökning](../fundamentals/debugging.md)
- Lär dig [personalisera upplevelsen](../fundamentals/rendering-personalization-content.md)
- Lär dig hur du skickar data till flera lösningar
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
