---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera profil;Aktivera profil
title: Lägg till data i kundprofilen i realtid
type: Tutorial
description: I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Lägg till data i [!DNL Real-Time Customer Profile]

I den här självstudien beskrivs de steg som krävs för att lägga till data i [!DNL Real-Time Customer Profile].

## Aktivera ett schema för [!DNL Real-Time Customer Profile]

Data som hämtas in till [!DNL Experience Platform] för användning av [!DNL Real-Time Customer Profile] måste överensstämma med [!DNL Experience Data Model] (XDM) schema som är aktiverat för [!DNL Profile]. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen [!DNL XDM Individual Profile] eller [!DNL XDM ExperienceEvent] klassen.

Du kan aktivera ett schema för användning i [!DNL Real-Time Customer Profile] med [!DNL Schema Registry] API eller [!DNL Schema Editor] användargränssnitt. Kom igång genom att följa självstudiekurserna för [skapa ett schema med API:er](../../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med hjälp av gränssnittet i schemaredigeraren](../../xdm/tutorials/create-schema-ui.md).

## Lägg till data med batchinmatning

Alla data har överförts till [!DNL Platform] att använda batchmatning överförs till enskilda datauppsättningar. Innan dessa data kan användas av [!DNL Real-Time Customer Profile]måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar finns i självstudiekursen på [konfigurera en datauppsättning för profil- och identitetstjänsten](dataset-configuration.md).

När datauppsättningen har konfigurerats kan du börja inhämta data i den. Se [Utvecklarhandbok för batchintag](../../ingestion/batch-ingestion/api-overview.md) för detaljerade steg om hur du överför filer i olika format.

## Lägg till data med direktuppspelning

Alla ströminkapslade data som är kompatibla med en [!DNL Profile]-aktiverat XDM-schema lägger automatiskt till eller skriver över lämplig post i [!DNL Real-Time Customer Profile]. Om fler än en identitet anges i posten, eller om tidsseriedata används, mappas dessa identiteter i identitetsdiagrammet utan ytterligare konfiguration. Se [Utvecklarhandbok för direktuppspelning](../../ingestion/tutorials/streaming-record-data.md) om du vill veta mer.

## Bekräfta att överföringen lyckades

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt.

Använda [!DNL Real-Time Customer Profile] Med åtkomst-API kan du hämta batchdata när de läses in i en datauppsättning. Om du inte kan hämta någon av de enheter som du förväntar dig kanske din datauppsättning inte är aktiverad för [!DNL Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar.

Detaljerade instruktioner om hur du får åtkomst till enheter med [!DNL Real-Time Customer Profile] API, se [slutpunktsguide för enheter](../api/entities.md), som också kallas[!DNL Profile Access] API&quot;.

## Uppdatera profilarkivdata

Ibland kan det vara nödvändigt att uppdatera data i din organisations Profile Store. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [aktivera en datauppsättning för profil och upsert](../../catalog/datasets/enable-upsert.md).
