---
title: Versionsinformation om Adobe Experience Platform – februari 2026
description: Versionsinformationen för Adobe Experience Platform från februari 2026.
source-git-commit: afb1e0266b4c5485ba574f95aab3a56485d176b3
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 52%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 17 februari 2026**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [Mål](#destinations)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Integrering av [!DNL Slack] för kundtillvända aviseringar | Du kan nu leverera kundorienterade aviseringar till [!DNL Slack]. Följ den [stegvisa självstudiekursen](../../observability/alerts/slack-integration.md) för att konfigurera [!DNL Slack]-integreringen och få varningsmeddelanden direkt på arbetsytan i [!DNL Slack]. |

{style="table-layout:auto"}

Mer information finns i [[!DNL Observability Insights] översikten](../../observability/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [[!DNL Snowflake] Batch](../../destinations/catalog/warehouses/snowflake-batch.md) är allmänt tillgänglig | Batchmålet [!DNL Snowflake] är nu allmänt tillgängligt. Real-Time CDP-kunder över hela världen kan nu använda denna anslutning för att aktivera data på sina Snowflake-konton utan att behöva kopiera data fysiskt. Alla begränsningar från den begränsade versionen har hävts (endast för kunder i USA, stöd för målgrupper som tillhör standardprincipen för sammanslagning). |

{style="table-layout:auto"}

**Korrigeringar och förbättringar**

| Korrigera | Beskrivning |
| --- | --- |
| Aktiveringen misslyckades, hastigheten överskreds | Målaviseringen för misslyckad aktivering överskrider nu korrekt det tröskelvärde som du konfigurerar när du utvärderar och skickar aviseringen. Tidigare utlöstes varningen med en felfrekvens på 1 % oavsett hur många procent du konfigurerade. Mer information om den här varningen finns i [standardvarningsregler](../../observability/alerts/rules.md#destinations). |
| Rapportering om utelämnade identiteter enligt Google kundmatchning | Korrigerade ett fel i inventeringslogiken för hoppade poster som gjorde att inflaterade uteslutna profiler visades för Google kundmatchningsmål. Aktiverings- och exportbeteendet påverkades inte, endast de rapporterade siffrorna var felaktiga. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| Stöd för Unity Catalog i [!DNL Databricks]-källanslutning | Källkopplingen [!DNL Databricks] har nu stöd för Unity Catalog. Läs den uppdaterade [[!DNL Databricks]](../../sources/connectors/databases/databricks.md)-dokumentationen och lär dig hur du använder Unity Catalog när du konfigurerar källanslutningen. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).
