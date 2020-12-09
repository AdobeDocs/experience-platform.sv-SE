---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 9 december 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013
translation-type: tm+mt
source-git-commit: 25c162f50f0a66d77eb638dbf87893af3c543ddc
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 december 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera konto- och anslutningsinformation för strömningskällor | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga direktuppspelningsanslutningar med API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [uppdaterar anslutningar med API:t](../../sources/tutorials/api/update.md) och [redigerar kontoinformation med användargränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort dataflöden | Strömmande dataflöden som innehåller fel eller har blivit onödiga kan nu tas bort med API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [tar bort dataflöden med API:t](../../sources/tutorials/api/delete-dataflows.md) och [tar bort dataflöden med gränssnittet](../../sources/tutorials/ui/delete.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).