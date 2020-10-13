---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform, oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: Oktober 2020**

- [Dataprep](#data-prep)
- [Källor](#sources)

## Dataprep {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| `is_set` funktion | Med den här `is_set` funktionen kan du kontrollera om det finns ett attribut i källdata. `is_set` kan användas tillsammans med `is_empty` för att kontrollera både förekomsten av attributet och förekomsten av värdet i attributet. |
| `get_values` funktion | Med den här funktionen kan du hämta värden från indatamappningen för en given nyckel. `get_values` |

Mer information finns i översikten över [dataförberedelser](../../data-prep/home.md).

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Hierarkisk mappning | Du kan förhandsgranska en hierarkisk källfil, som JSON eller Parquet, under dataöverföringsprocessen. |
| SSH-autentiseringsstöd för SFTP | Du kan ansluta ditt SFTP-konto till [!DNL Platform] med RSA/DSA Open SSH-nycklar. Mer information finns i [SFTP-översikten](../../sources/connectors/cloud-storage/ftp-sftp.md) . |
| UX-förbättringar | Du kan aktivera datauppsättningen för [!DNL Profile] under dataöverföringsprocessen. Mer information finns i självstudiekursen om arbetsflöde [](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) för molnlagring. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).