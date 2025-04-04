---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera profil;Aktivera profil
title: Lägg till data i kundprofilen i realtid
type: Tutorial
description: I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Lägg till data i [!DNL Real-Time Customer Profile]

I den här självstudien beskrivs stegen som krävs för att lägga till data i [!DNL Real-Time Customer Profile].

## Aktivera ett schema för [!DNL Real-Time Customer Profile]

Data som importeras till [!DNL Experience Platform] för användning av [!DNL Real-Time Customer Profile] måste överensstämma med ett [!DNL Experience Data Model] (XDM)-schema som är aktiverat för [!DNL Profile]. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen klassen [!DNL XDM Individual Profile] eller klassen [!DNL XDM ExperienceEvent].

Du kan aktivera ett schema för användning i [!DNL Real-Time Customer Profile] med [!DNL Schema Registry] API:t eller användargränssnittet i [!DNL Schema Editor]. Kom igång genom att följa självstudiekurserna för att [skapa ett schema med API:er](../../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av schemaredigerarens gränssnitt](../../xdm/tutorials/create-schema-ui.md).

## Lägg till data med batchinmatning

Alla data som har överförts till [!DNL Experience Platform] med batchöverföring överförs till enskilda datauppsättningar. Innan dessa data kan användas av [!DNL Real-Time Customer Profile] måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar finns i självstudiekursen [Konfigurera en datauppsättning för profil- och identitetstjänsten](dataset-configuration.md).

När datauppsättningen har konfigurerats kan du börja inhämta data i den. Mer information om hur du överför filer i olika format finns i [Utvecklarhandbok för gruppimport](../../ingestion/batch-ingestion/api-overview.md).

## Lägg till data med direktuppspelning

Alla ströminkapslade data som är kompatibla med ett [!DNL Profile]-aktiverat XDM-schema lägger automatiskt till eller skriver över lämplig post i [!DNL Real-Time Customer Profile]. Om fler än en identitet anges i posten, eller om tidsseriedata används, mappas dessa identiteter i identitetsdiagrammet utan ytterligare konfiguration. Mer information finns i [Utvecklarhandboken för direktuppspelning av inmatning](../../ingestion/tutorials/streaming-record-data.md).

## Bekräfta att överföringen lyckades

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt.

Med åtkomst-API:t [!DNL Real-Time Customer Profile] kan du hämta batchdata när de läses in till en datamängd. Om du inte kan hämta någon av de entiteter som du förväntar dig, kanske din datauppsättning inte är aktiverad för [!DNL Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar.

Detaljerade instruktioner om hur du får åtkomst till entiteter med API:t [!DNL Real-Time Customer Profile] finns i [entitetens slutpunktshandbok](../api/entities.md), som också kallas [!DNL Profile Access] API.

## Uppdatera data i profilarkivet

Ibland kan det vara nödvändigt att uppdatera data i din organisations profilarkiv. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [att aktivera en datauppsättning för profil och uppdatering](../../catalog/datasets/enable-upsert.md).
