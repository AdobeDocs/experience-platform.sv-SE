---
title: 'Åtkomst till ECID '
description: Adobe Experience Platform Web SDK Extension Leveraging ECID in taggar
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Åtkomst till ECID

[!DNL Experience Cloud Identity (ECID)] är en beständig identifierare för en besökare på webbplatsen. Under vissa omständigheter kanske du föredrar att få tillgång till ECID (till exempel för att skicka det till en tredje part).

Adobe rekommenderar följande för att få åtkomst till ECID inom taggar:

1. Kontrollera att din egenskap är konfigurerad med [sekvensering av regelkomponenter](../../tags/ui/managing-resources/rules.md#sequencing) aktiverad.
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
