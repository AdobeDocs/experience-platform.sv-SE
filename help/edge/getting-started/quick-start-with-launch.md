---
title: Snabbstart med Launch
seo-title: Adobe Experience Platform Web SDK snabbstart med Launch
description: Snabbstartsguide för hur du använder Experience Platform Web SDK-tillägget för att samla in data
seo-description: Snabbstartsguide för hur du använder Experience Platform Web SDK-tillägget för att samla in data
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Välkommen

Den här guiden leder dig igenom de olika sätten att konfigurera Adobe Experience Platform Web SDK i Launch. Du måste vitlistas för att kunna använda den här funktionen. Om du vill komma med på väntelistan kontaktar du din CSM.

- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME för Analytics bör du använda den. Testning under utveckling fungerar utan CNAME, men du behöver en innan du går till produktion.
- Var berättigad till Adobe Experience Platform. Om du inte har köpt Platform kommer Adobe att förse dig med Experience Platform Data Services Foundation för användning med SDK utan extra kostnad.
- Använd den senaste versionen av Visitor ID-tjänsten.

## Förbered ett schema

Experience Platform Edge Network tar data som XDM. XDM är ett dataformat som gör att du kan definiera scheman. Schemat definierar hur Edge Network förväntar sig att data ska formateras. Om du vill skicka data måste du definiera ditt schema.

1. [Skapa ett schema](../../xdm/tutorials/create-schema-ui.md)
2. Lägg till AEP- [!DNL Web SDK ExperienceEvent] mixin i det schema du skapade.
3. Skapa en datauppsättning från det schema du skapade.

Följande video är avsedd att stödja dig när du skapar ett schema, en datauppsättning och en direktuppspelningskälla för dina [!DNL Web SDK] data.

Logga in på Starta och installera `AEP Web SDK` tillägget. När du installerar SDK uppmanas du att konfigurera tillägget. Ange det konfigurations-ID som du begärde ovan. Tillägget fyller automatiskt i ditt organisations-ID.


Mer information om olika konfigurationsalternativ finns i [Konfigurera SDK](../fundamentals/configuring-the-sdk.md).

## Skapa ett konfigurations-ID

Du kan skapa ett konfigurations-ID med [Edge-konfigurationsverktyget](../fundamentals/edge-configuration.md) i Launch. På så sätt kan du aktivera Edge Network för att skicka data till de olika lösningarna. Information om hur du hittar de olika alternativen finns på sidan [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Din organisation måste vitlistas för den här funktionen. Kontakta din CSM för att komma med i listan för eventuell vitlistning.

## Skapa ett dataelement baserat på ditt schema

I Launch skapar du ett dataelement som refererar till schemat genom att ändra tillägget till AEP Web SDK och ange typen till `XDM Object`. Detta läser in ditt schema och gör att du kan mappa dataelement till olika delar av schemat.

![Datumelement i start](../../assets/edge_data_element.png)

## Skicka en händelse

När tillägget har installerats börjar du skicka händelser genom att lägga till en åtgärd från AEP Web SDK-tillägget till en regel. `sendEvent` Lägg till det dataelement du nyss skapade i händelsen som XDM-data. Adobe rekommenderar att du skickar minst en händelse varje gång en sida läses in.

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
