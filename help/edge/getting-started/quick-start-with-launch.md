---
title: Snabbstart med Launch
seo-title: Adobe Experience Platform Web SDK snabbstart med Launch
description: Snabbstartsguide för användning av Experience Platform Web SDK-tillägget för att samla in data
seo-description: Snabbstartsguide för användning av Experience Platform Web SDK-tillägget för att samla in data
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Välkommen

Den här guiden tar dig igenom de olika stegen för hur du konfigurerar Adobe Experience Platform Web SDK i Launch. För att kunna använda den här funktionen måste du ha behörighet och vara med i listan över tillåtna. Om du vill komma med på väntelistan kontaktar du din CSM.

- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME for Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men du behöver en innan du går till produktion
- Du har rätt till Adobe Experience Platform Data Platform. Om du inte har köpt Platform tillhandahåller vi dig Experience Platform Data Services Foundation för användning i begränsad omfattning med SDK utan extra kostnad.
- Använd den senaste versionen av tjänsten för besökar-ID

## Skapa ett konfigurations-ID

Du kan skapa ett konfigurations-ID med [Edge-konfigurationsverktyget](../fundamentals/edge-configuration.md) vid start. På så sätt kan du aktivera Edge Network för att skicka data till de olika lösningarna. Information om hur du hittar de olika alternativen finns på sidan [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Din organisation måste finnas i listan över tillåtna för funktionen. Kontakta din CSM för att få plats i listan över tillåtna användare.

## Förbered ett schema

Experience Platform Edge Network tar data som XDM. XDM är ett dataformat som gör att du kan definiera scheman. Schemat definierar hur Edge Network förväntar sig att data ska formateras. För att kunna skicka data måste du definiera ditt schema.

- [Skapa ett schema](../../xdm/tutorials/create-schema-ui.md)
- Lägg till Adobe Experience Platform Web SDK-mixin i det schema du skapade

## Installera SDK i Launch

Logga in på Starta och installera `AEP Web SDK` tillägget. När du installerar SDK uppmanas du att konfigurera tillägget. Ange det konfigurations-ID som du begärde ovan. Tillägget fyller automatiskt i ditt organisations-ID.

Mer information om olika konfigurationsalternativ finns i [Konfigurera SDK](../fundamentals/configuring-the-sdk.md).

## Skapa ett dataelement baserat på ditt schema

Vid start skapar du ett dataelement som refererar till schemat genom att ändra tillägget till AEP Web SDK och ange typen till XDM-objekt. Detta läser in ditt schema och gör att du kan mappa dataelement till olika delar av schemat.

![Datumelement i start](../../assets/edge_data_element.png)

## Skicka en händelse

När tillägget har installerats börjar du skicka händelser genom att lägga till en sendEvent-åtgärd från AEP Web SDK-tillägget i en regel. Var noga med att lägga till det dataelement du nyss skapade i händelsen som XDM-data. Vi rekommenderar att du skickar minst en händelse varje gång en sida läses in.

Mer information om hur du spårar händelser finns i [Spåra händelser](../fundamentals/tracking-events.md).

## Nästa steg

När du har data som flödar kan du göra följande.

- [Skapa ditt schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Läs mer om felsökning](../fundamentals/debugging.md)
- Lär dig [personalisera upplevelsen](../fundamentals/rendering-personalization-content.md)
- Lär dig hur du skickar data till flera lösningar
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
