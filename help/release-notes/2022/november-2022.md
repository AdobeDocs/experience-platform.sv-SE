---
title: Versionsinformation om Adobe Experience Platform november 2022
description: Versionsinformation november 2022 för Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 23 november 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL AWS]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information finns i [[!DNL AWS] tilläggsöversikten](../../tags/extensions/server/aws/overview.md). |
| [!DNL Google Ads Enhanced Conversions]-tillägg för händelsevidarebefordran | Du kan nu skicka konverteringsdata till [!DNL Google Ads] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information finns i [[!DNL Google Ads Enhanced Conversions] tilläggsöversikten](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| [!DNL Microsoft Azure]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Microsoft Azure] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information finns i [[!DNL Microsoft Azure] tilläggsöversikten](../../tags/extensions/server/azure/overview.md). |

Mer information om plattformens datainsamlingsfunktioner finns i [datainsamlingsöversikten](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tilldela fält till anpassade klasser när du lägger till direkt i ett schema | När du [lade till ett enskilt fält direkt i ett schema](../../xdm/ui/resources/schemas.md#add-individual-fields), kunde du tidigare bara tilldela fältet till en fältgrupp som dess överordnade resurs. Utöver fältgrupper kan du nu [tilldela fältet till en anpassad klass](../../xdm/ui/resources/schemas.md#add-to-class) som överordnad resurs i stället. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- | 
| Beta-tillgänglighet för Oracle Service Cloud-källa | Använd Oraclets Service Cloud-källa för att importera data från ditt Oracle Service Cloud-konto till Experience Platform. Mer information finns i dokumentationen om [Oracle Service Cloud-källan](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Läs [Källöversikten](../../sources/home.md) om du vill veta mer om källor.
