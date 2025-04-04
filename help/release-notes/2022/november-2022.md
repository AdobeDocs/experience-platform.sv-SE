---
title: Versionsinformation om Adobe Experience Platform – november 2022
description: Versionsinformationen för Adobe Experience Platform från november 2022.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 51%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 23 november 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL AWS]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Se [[!DNL AWS] översikten över tillägg](../../tags/extensions/server/aws/overview.md) för mer information. |
| [!DNL Google Ads Enhanced Conversions]-tillägg för händelsevidarebefordran | Du kan nu skicka konverteringsdata till [!DNL Google Ads] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Se [[!DNL Google Ads Enhanced Conversions] översikten över tillägg](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) för mer information. |
| [!DNL Microsoft Azure]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Microsoft Azure] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Se [[!DNL Microsoft Azure] översikten över tillägg](../../tags/extensions/server/azure/overview.md) för mer information. |

Mer information om Experience Platform datainsamlingsfunktioner finns i [datainsamlingsöversikten](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tilldela fält till anpassade klasser när du lägger till direkt i ett schema | När du [lade till ett enskilt fält direkt i ett schema](../../xdm/ui/resources/schemas.md#add-individual-fields), kunde du tidigare bara tilldela fältet till en fältgrupp som dess överordnade resurs. Utöver fältgrupper kan du nu [tilldela fältet till en anpassad klass](../../xdm/ui/resources/schemas.md#add-to-class) som överordnad resurs i stället. |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- | 
| Beta tillgänglighet av Oracle Service Cloud-källa | Använd Oracle Service Cloud-källan för att importera data från ditt Oracle Service Cloud-konto till Experience Platform. Mer information finns i dokumentationen om [Oracle Service Cloud-källan](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Mer information om källor finns i [översikten över källor](../../sources/home.md).
