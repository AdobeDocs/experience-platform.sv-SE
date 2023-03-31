---
title: Åtkomst till ECID
description: Lär dig hur du får åtkomst till Experience Cloud ID (ECID) i Adobe Experience Platform-taggar
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Åtkomst till ECID

The [!DNL Experience Cloud ID (ECID)] är en beständig Experience Cloud-ID som kan hjälpa dig att identifiera besökare på webbplatsen. Under vissa omständigheter, till exempel när du skickar identifieraren till en tredjepartsplattform, kan du behöva åtkomst till [!DNL ECID].

Så här öppnar du [!DNL ECID] inom -taggar, följ stegen nedan:

1. Kontrollera att egenskapen är konfigurerad med [sekvensering av regelkomponenter](../../tags/ui/managing-resources/rules.md#sequencing) aktiverat.
2. Skapa en ny regel.
3. Lägg till en [!UICONTROL Library Loaded] till regeln.
4. Lägg till en [!UICONTROL Custom Condition] åtgärd för regeln, med följande kod (förutsatt att namnet som du har konfigurerat för SDK-instansen är `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Spara regeln.

Nu bör du kunna komma åt [!DNL ECID] i efterföljande regler, använda `%ECID%` eller `_satellite.getVar("ECID")`, ungefär som hur du kommer åt andra dataelement.
