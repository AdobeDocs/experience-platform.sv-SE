---
title: Adobe Analytics for Target (A4T) Logga in på Experience Platform Web SDK
description: Lär dig hur du styr samlingen av Adobe Analytics for Target-data (A4T) med Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logga;analys;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Logga in på Experience Platform Web SDK

När du använder Adobe Target för personalisering kan du välja vilket system du vill använda för prestandamätning. Med varje [målaktivitet](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) kan du välja mellan Target-rapportering och Adobe Analytics-rapportering.

Om du använder Analytics-rapportering måste Adobe Target förmedla följande till Analytics:

* Vilken Adobe Target-aktivitet besökarna har lagt in
* Vilken upplevelse de har sett
* Vilken konvertering har nåtts

Adobe Experience Platform Web SDK har stöd för två typer av Analytics-loggning för A4T-användningsfall (Analytics for Target):

| Loggningsmetod | Beskrivning |
| --- | --- |
| Loggning av analys på serversidan | Alla Analytics-träffar som skickas via Edge Network kompletteras med Target-information på serversidan, utan att du behöver gå igenom träffstensprocessen. |
| Loggning av analys på klientsidan | Måldata returneras på klientsidan, vilket gör att du manuellt kan förstärka och skicka data till Analytics med [API:t för datainmatning](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Loggningsmetoden avgörs av om du har aktiverat Adobe Analytics på din konfigurerade [datastream](../../../../datastreams/overview.md):

![Beslutsflöde för loggningsmetod](../assets/analytics-logging.png)

## Nästa steg

Det här dokumentet innehåller en kort introduktion till de olika loggningsmetoderna för A4T-data i Web SDK. Mer information om dessa metoder finns i följande dokumentation:

* [Logga A4T-data på serversidan i Experience Platform Web SDK](./server-side.md)
* [Loggning på klientsidan för A4T-data i Experience Platform Web SDK](./client-side.md)
