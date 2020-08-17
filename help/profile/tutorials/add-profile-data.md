---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
solution: Adobe Experience Platform
title: Lägg till data i kundprofilen i realtid
topic: tutorial
description: I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Lägg till data i [!DNL Real-time Customer Profile]

I den här självstudiekursen beskrivs de steg som krävs för att lägga till data i [!DNL Real-time Customer Profile].

## Aktivera ett schema för [!DNL Real-time Customer Profile]

Data som hämtas in [!DNL Experience Platform] för användning av måste överensstämma med ett [!DNL Real-time Customer Profile] (XDM)-schema som är aktiverat för [!DNL Experience Data Model] [!DNL Profile]. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen [!DNL XDM Individual Profile] eller [!DNL XDM ExperienceEvent] klassen.

Du kan aktivera ett schema för användning i [!DNL Real-time Customer Profile] med [!DNL Schema Registry] API:t eller [!DNL Schema Editor] användargränssnittet. Kom igång genom att följa självstudiekurserna för att [skapa ett schema med API:er](../../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av gränssnittet](../../xdm/tutorials/create-schema-ui.md)i Schemaredigeraren.

## Lägg till data med batchinmatning

Alla data som överförs till [!DNL Platform] med batchöverföring överförs till enskilda datauppsättningar. Innan dessa data kan användas av [!DNL Real-time Customer Profile]måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar finns i självstudiekursen om hur du [konfigurerar en datauppsättning för profil- och identitetstjänsten](dataset-configuration.md).

När datauppsättningen har konfigurerats kan du börja inhämta data i den. I utvecklarhandboken för [batchimport finns detaljerade anvisningar](../../ingestion/batch-ingestion/api-overview.md) om hur du överför filer i olika format.

## Lägg till data med direktuppspelning

Alla ströminkapslade data som är kompatibla med ett [!DNL Profile]aktiverat XDM-schema lägger automatiskt till eller skriver över rätt post i [!DNL Real-time Customer Profile]. Om fler än en identitet anges i posten, eller om tidsseriedata används, mappas dessa identiteter i identitetsdiagrammet utan ytterligare konfiguration. Läs mer i [utvecklarhandboken](../../ingestion/tutorials/streaming-record-data.md) för direktuppspelning.

## Bekräfta att överföringen lyckades

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt.

Med hjälp av [!DNL Real-time Customer Profile] Access API kan du hämta batchdata när de läses in till en datauppsättning. Om du inte kan hämta någon av de enheter som du förväntar dig, kanske din datauppsättning inte är aktiverad för [!DNL Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar.

Detaljerade instruktioner om hur du får åtkomst till enheter med [!DNL Real-time Customer Profile] API finns i [entiteternas slutpunktshandbok](../api/entities.md), som också kallas&quot;[!DNL Profile Access] API&quot;.