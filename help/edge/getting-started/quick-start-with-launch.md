---
title: Snabbstart med Launch
seo-title: Adobe Experience Platform Web SDK snabbstart med Launch
description: Snabbstartsguide för användning av Experience Platform Web SDK-tillägget för att samla in data
seo-description: Snabbstartsguide för användning av Experience Platform Web SDK-tillägget för att samla in data
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Krav

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

För närvarande stöder Adobe Experience Platform Web SDK endast sändning av data till Adobe Experience Platform med hjälp av XDM. Du måste uppfylla följande krav.

- Ha en [förstapartsdomän (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiverad. Om du redan har en CNAME for Analytics bör du använda den.
- Få rätt till Adobe Experience Platform
- Använd den senaste versionen av tjänsten för besökar-ID

## Förbered plattformen

För att kunna skicka data till Adobe Experience Platform måste du skapa ett XDM-schema och en datauppsättning som använder det schemat.

- [Skapa ett schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) med följande blandningar:
   - Implementeringsinformation för ExperienceEvent
   - Information om ExperienceEvent-miljö
   - Webbinformation om ExperienceEvent
- Lägg till Adobe Experience Platform Web SDK-mixin i det schema du skapade
- [Skapa en datauppsättning](https://platform.adobe.com/dataset/overview) med ditt schema där du vill att data ska sparas

## Begär ett konfigurations-ID

Du måste ha ett konfigurations-ID för att kunna använda SDK. Konfigurations-ID:t ser till att dina data dirigeras till rätt plats. Du kan få ett konfigurations-ID från din konsult eller via Client Care. De behöver följande information:

- **Organisations-ID:** Du hittar detta på instruktionerna [här](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **Datauppsättnings-ID:** Detta är tillgängligt i datauppsättningsgränssnittet när du klickar på en datauppsättning
- **Schema-ID:** Det här är tillgängligt i URL:en för schemaskapandeskärmen
- **Eget namn:** Det här är det egna namnet som kommer att användas i framtida användargränssnitt för den här konfigurationen

## Installera SDK i Launch

Logga in på Starta och installera `AEP Web SDK` tillägget. När du installerar SDK uppmanas du att konfigurera tillägget. Ange det konfigurations-ID som du begärde ovan. Tillägget fyller automatiskt i ditt organisations-ID.

Mer information om olika konfigurationsalternativ finns i [Konfigurera SDK](../fundamentals/configuring-the-sdk.md).

## Skicka en händelse

När tillägget har installerats kan du börja skicka händelser genom att lägga till en&quot;Skicka signal&quot;-åtgärd från AEP Web SDK-tillägget. Vi rekommenderar att du skickar minst en händelse varje gång en sida läses in med alternativet &quot;finns i början av en vy&quot; markerat.

Mer information om hur du spårar händelser finns i [Spåra händelser](../fundamentals/tracking-events.md).

## Skicka data

Du kan skicka data som matchar det schema du skapade tidigare tillsammans med dina händelser. Om du till exempel äger en e-handelsplats och lägger till handelsmixen i ditt schema, skickar du följande struktur när någon visar en produkt.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
