---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Lägg till data i kundprofilen i realtid
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Lägg till data i kundprofilen i realtid

I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.

## Aktivera ett schema för kundprofil i realtid

Data som hämtas in till Experience Platform för användning av kundprofilen i realtid måste överensstämma med ett XDM-schema (Experience Data Model) som är aktiverat för profilen. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen klassen XDM Individual Profile eller klassen XDM ExperienceEvent.

Du kan aktivera ett schema som ska användas i kundprofilen i realtid med API:t för schemaregister eller användargränssnittet för Schemaredigeraren. Kom igång genom att följa självstudiekurserna för att [skapa ett schema med API:er](../../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av gränssnittet](../../xdm/tutorials/create-schema-ui.md)i Schemaredigeraren.

## Lägg till data med batchinmatning

Alla data som överförs till Platform med batchöverföring överförs till enskilda datauppsättningar. Innan dessa data kan användas av kundprofilen i realtid måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar finns i självstudiekursen om hur du [konfigurerar en datauppsättning för profil- och identitetstjänsten](dataset-configuration.md).

När datauppsättningen har konfigurerats kan du börja inhämta data i den. I utvecklarhandboken för [batchimport finns detaljerade anvisningar](../../ingestion/batch-ingestion/api-overview.md) om hur du överför filer i olika format.

## Lägg till data med direktuppspelning

Alla ströminkapslade data som är kompatibla med ett profilaktiverat XDM-schema lägger automatiskt till eller skriver över rätt post i kundprofilen i realtid. Om fler än en identitet anges i posten, eller om tidsseriedata används, mappas dessa identiteter i identitetsdiagrammet utan ytterligare konfiguration. Läs mer i [utvecklarhandboken](../../ingestion/tutorials/streaming-record-data.md) för direktuppspelning.

## Bekräfta att överföringen lyckades

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt.

Med hjälp av API:t för kundprofilåtkomst i realtid kan du hämta batchdata när de läses in till en datauppsättning. Om du inte kan hämta någon av de enheter som du förväntar dig, kanske din datauppsättning inte är aktiverad för profilen. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar.

Detaljerade instruktioner om hur du får åtkomst till enheter med hjälp av kundprofils-API:t i realtid finns i [enheternas slutpunktshandbok](../api/entities.md), som också kallas &quot;API för profilåtkomst&quot;.