---
title: 'Åtkomst till ECID '
description: Adobe Experience Platform Web SDK Extension Leveraging ECID in Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Åtkomst till ECID

[!DNL Experience Cloud Identity (ECID)] är en beständig identifierare för en besökare på webbplatsen. Under vissa omständigheter kanske du föredrar att få tillgång till ECID (till exempel för att skicka det till en tredje part).

För att få tillgång till ECID i Adobe Experience Platform Launch rekommenderar Adobe följande:

1. Kontrollera att din egenskap är konfigurerad med [sekvensering av regelkomponenter](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) aktiverad.
1. Skapa en ny regel.
1. Lägg till en [!UICONTROL Library Loaded]-händelse till regeln.
1. Lägg till en [!UICONTROL Custom Condition]-åtgärd i regeln med följande kod (förutsatt att namnet som du har konfigurerat för SDK-instansen är `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Spara regeln.

Du bör sedan kunna komma åt ECID i efterföljande regler med `%ECID%` eller `_satellite.getVar("ECID")` på samma sätt som andra dataelement.
