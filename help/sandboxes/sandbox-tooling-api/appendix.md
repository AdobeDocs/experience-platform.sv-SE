---
title: API-handbok för sandlådeverktyg
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med sandlådeverktygets API.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Sandbox API guide appendix

Det här dokumentet innehåller ytterligare information om hur du arbetar med API:t [!DNL Sandbox].

## Använda frågeparametrar {#query}

Sandbox Tooling API stöder användning av frågeparametrar för att paginera och filtrera resultat när paket listas.

>[!NOTE]
>
>`limit` kan skickas och startas individuellt.

| Parameter | Beskrivning |
| --- | --- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. Standardgränsen är 20. |
| `start` | Början på var en underordnad lista med objekt ska börja. |
| `targetSandbox` | Representerar namnet på sandlådan där du vill importera artefakter. |
| `jobType` | Typ av jobb. Värdet kan vara NEW, RESUME och ROLLBACK. |
| `jobStatus` | Jobbets status. Det här värdet kan vara PENDING, IN_PROGRESS, SUCCESS, FAILED och CANCELED. |
| `requestType` | Typ av begäran. Värdet kan vara EXPORT, IMPORT och COPY. |
| `expiryPeriod ` | Den här användarspecificerade tidsperioden definierar paketets förfallodatum (i dagar) från den tidpunkt då paketet publicerades. Värdet får inte vara negativt. Standardvärdet är 90 dagar från den tidpunkt då uppdaterings- eller publicerings-API anropas. |
