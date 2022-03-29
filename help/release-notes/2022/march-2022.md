---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: 7145867795bcd8e1093c09df3fefdee518f9578a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 mars 2022**

Nya funktioner i Adobe Experience Platform:

- [[!DNL Audit Logs]](#audit-logs)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm](#alerts)
- [Källor](#sources)

## [!DNL Audit Logs] {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Granskningsloggar för datauppsättning, schema, klass, fältgrupp, datatyp, sandlåda, mål, segment, sammanfogningsprincip, beräknat attribut, produktprofil och konto (Adobe) | Detta är de resurser som registreras av granskningsloggar. Om funktionen är aktiverad samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt. |
| Exportera granskningsloggar | Granskningsloggarna kan hämtas som en `CSV` eller `JSON` -fil. De genererade filerna sparas direkt på datorn. |

Mer information om granskningsloggar i Platform finns i [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md).

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Det finns nu två nya varningsregler för källor som rör dataöverföring. Se översikten på [varningsregler](../../observability/alerts/rules.md) för den uppdaterade listan över varningstyper. |

Mer information om varningar i Platform finns i [varningsöversikt](../../observability/alerts/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nu finns nya källor för B2B-användning | Du kan nu använda alla tillgängliga källor på plattformen för B2B-användning. Se [källkatalog](../../sources/home.md) för en fullständig lista över tillgängliga källor. |
| Allmän tillgänglighet för nya [!DNL Oracle Eloqua] källa | Nu kan du använda [!DNL Oracle Eloqua] källa till smidig import av data från [!DNL Oracle Eloqua] -instans (konto, kampanj, kontakter) till Platform. Läs dokumentationen om [skapa [!DNL Oracle Eloqua] källanslutning](../../sources/connectors/oracle-eloqua.md) för mer information. |
| API-förbättringar för [!DNL Data Landing Zone] | The [!DNL Data Landing Zone] -källan har nu stöd för automatisk identifiering av filegenskaper när du använder [!DNL Flow Service] API. Läs dokumentationen om [skapa [!DNL Data Landing Zone] källanslutning](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
