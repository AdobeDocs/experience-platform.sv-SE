---
title: Versionsinformation om Adobe Experience Platform, augusti 2022
description: Versionsinformation från augusti 2022 för Adobe Experience Platform.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 augusti 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataprep](#data-prep)
- [Källor](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för inmatning av poster med varningar | Dataprep lokaliserar nu varningar (icke-kritiska fel) till fälten och tillåter att resten av raden importeras. Alla mappningsomformningsfel rapporteras nu som varningar och rader som är delvis inkapslade betraktas som lyckade, med en varning.  Övervakning stöds även för poster med varningar och diagnostikinformation. Det går för närvarande bara att få del av poster med varningar att strömma data. Läs dokumentationen om [importera poster med varningar](../../sources/tutorials/ui/monitor-streaming.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för olika regioner för Adobe Analytics | Du kan nu importera rapportsviter från valfri region (USA, Storbritannien eller Singapore). Rapportsviterna måste mappas till samma organisation som den Experience Platform Sandbox-instans i vilken källanslutningen skapas. Mer information finns i handboken på [skapa en Adobe Analytics-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Mer information om källor finns i [källöversikt](../../sources/home.md).
