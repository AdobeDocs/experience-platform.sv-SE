---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera profil;Aktivera profil
title: Lägg till data i kundprofilen i realtid
topic: tutorial
type: Tutorial
description: I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Lägg till data i [!DNL Real-time Customer Profile]

I den här självstudiekursen beskrivs de steg som krävs för att lägga till data i [!DNL Real-time Customer Profile].

## Aktivera ett schema för [!DNL Real-time Customer Profile]

Data som hämtas till [!DNL Experience Platform] för användning av [!DNL Real-time Customer Profile] måste överensstämma med ett [!DNL Experience Data Model] (XDM)-schema som är aktiverat för [!DNL Profile]. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen klassen [!DNL XDM Individual Profile] eller [!DNL XDM ExperienceEvent].

Du kan aktivera ett schema för användning i [!DNL Real-time Customer Profile] med API:t [!DNL Schema Registry] eller användargränssnittet för [!DNL Schema Editor]. Kom igång genom att följa självstudiekurserna för [att skapa ett schema med API:er](../../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av schemaredigerarens gränssnitt](../../xdm/tutorials/create-schema-ui.md).

## Lägg till data med batchinmatning

Alla data som överförs till [!DNL Platform] med batchöverföring överförs till enskilda datauppsättningar. Innan dessa data kan användas av [!DNL Real-time Customer Profile] måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar finns i självstudiekursen om att [konfigurera en datauppsättning för profil- och identitetstjänsten](dataset-configuration.md).

När datauppsättningen har konfigurerats kan du börja inhämta data i den. I [Utvecklarhandboken för gruppfrågor](../../ingestion/batch-ingestion/api-overview.md) finns detaljerade anvisningar om hur du överför filer i olika format.

## Lägg till data med direktuppspelning

Alla ströminkapslade data som är kompatibla med ett [!DNL Profile]-aktiverat XDM-schema lägger automatiskt till eller skriver över lämplig post i [!DNL Real-time Customer Profile]. Om fler än en identitet anges i posten, eller om tidsseriedata används, mappas dessa identiteter i identitetsdiagrammet utan ytterligare konfiguration. Mer information finns i [Utvecklarhandboken för direktuppspelning av intagning](../../ingestion/tutorials/streaming-record-data.md).

## Bekräfta att överföringen lyckades

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt.

Med åtkomst-API:t [!DNL Real-time Customer Profile] kan du hämta batchdata när de läses in till en datauppsättning. Om du inte kan hämta någon av de enheter du förväntar dig, kanske din datauppsättning inte är aktiverad för [!DNL Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar.

Detaljerade instruktioner om hur du får åtkomst till enheter med API:t [!DNL Real-time Customer Profile] finns i [entitetens slutpunktshandbok](../api/entities.md), som också kallas API:t [!DNL Profile Access].