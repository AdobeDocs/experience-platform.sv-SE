---
title: Implementeringshandbok för identitetstjänsten
description: Lär dig hur data som tillhandahålls till Adobe Experience Platform behandlas innan de används av identitetstjänsten för att skapa identitetsdiagram.
source-git-commit: bdda234c44b63999d7582857975afa64fdb93605
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Implementeringsguide för identitetstjänst

Det här dokumentet innehåller information om hur data som tillhandahålls till Adobe Experience Platform behandlas innan de används av identitetstjänsten för att skapa ett identitetsdiagram för en viss kund.

## Bestäm dig för identitetsfält

Beroende på er strategi för insamling av företagsdata avgör de datafält som du anger som identiteter vilka data som inkluderas i identitetskartan. För att få ut så mycket som möjligt av Experience Platform och så omfattande kundidentiteter som möjligt bör ni ladda upp både online- och offlinedata.

* Onlinedata är data som beskriver närvaro och beteende online, t.ex. användarnamn och e-postadresser.

* Offlinedata avser data som inte är direkt relaterade till onlinenärvaro, t.ex. ID:n från CRM-system. Den här typen av data gör era identiteter mer robusta och stöder datamedlemskap i olika system.

## Skapa ytterligare identitetsnamnutrymmen

Experience Platform har en mängd standardnamnutrymmen, men du kan behöva skapa ytterligare namnutrymmen för att kategorisera dina identiteter ordentligt. Mer information finns i guiden [skapa anpassade namnutrymmen för din organisation](./namespaces.md).

>[!NOTE]
>
>Identitetsnamnutrymmen är en kvalificerare för identiteter. Därför kan ett namnutrymme inte tas bort när det väl har skapats.

## Inkludera identitetsdata i Experience Data Model (XDM)

Som det standardiserade ramverk som Experience Platform organiserar kunddata inom gör Experience Data Model (XDM) det möjligt att dela och förstå data mellan Experience Platform och andra tjänster som interagerar med Experience Platform. Mer information finns i [XDM - systemöversikt](../xdm/home.md).

Både schema för inspelnings- och tidsserier ger möjlighet att inkludera identitetsdata. När data importeras skapar identitetsdiagrammet nya relationer mellan datafragment från olika namnutrymmen om de visar sig dela gemensamma identitetsdata.

## Ange etiketter för XDM-fält som identitet

Alla textfält `string` i scheman som implementerar antingen post- eller tidsseriens XDM-klasser kan märkas som ett identitetsfält. Därför betraktas alla data som hämtas in till det fältet som identitetsdata.

I identitetsfält går det också att länka identiteter om de delar gemensamma PII-data.
Genom att till exempel märka fält med telefonnummer som identitetsfält kan identitetstjänsten automatiskt skapa relationer med andra personer som använder samma telefonnummer.

>[!NOTE]
>
>* Array- och mappningstypsfält stöds inte och kan inte markeras och märkas som identitetsfält.
>* Namnutrymmet för resulterande identiteter anges när fältet etiketteras.

## Konfigurera en datauppsättning för identitetstjänsten

Under direktuppspelningsprocessen hämtar identitetstjänsten automatiskt identitetsdata från post- och tidsseriedata. Innan data kan importeras måste de dock aktiveras för identitetstjänsten. Läs självstudiekursen om  [konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../profile/tutorials/dataset-configuration.md) för mer information.

## Importera data till identitetstjänsten

Identitetstjänsten använder XDM-kompatibla data som skickas till Experience Platform antingen av [batchintag](../ingestion/batch-ingestion/overview.md) eller [direktuppspelning](../ingestion/streaming-ingestion/overview.md).

Följande video är avsedd att ge stöd för din förståelse av identitetstjänsten. I den här videon visas hur du kan märka datafält som identiteter, importera identitetsdata och sedan verifiera att data har skickats till Adobe Experience Platform Identity Service Private Graph.

>[!WARNING]
>
>Användargränssnittet för Experience Platform som visas i följande video är inaktuellt. Läs dokumentationen om de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)