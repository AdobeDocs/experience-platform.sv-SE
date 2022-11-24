---
title: Versionsinformation om Adobe Experience Platform november 2022
description: Versionsinformation november 2022 för Adobe Experience Platform.
source-git-commit: 9100597c94c21beb9d967f67061e18a9421c6674
workflow-type: tm+mt
source-wordcount: '454'
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
| [!DNL AWS] tillägg för händelsevidarebefordran | Nu kan du skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL AWS] tilläggsöversikt](../../tags/extensions/web/aws/overview.md) för mer information. |
| [!DNL Google Ads Enhanced Conversions] tillägg för händelsevidarebefordran | Nu kan du skicka konverteringsdata till [!DNL Google Ads] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Google Ads Enhanced Conversions] tilläggsöversikt](../../tags/extensions/web/google-ads-enhanced-conversions/overview.md) för mer information. |
| [!DNL Microsoft Azure] tillägg för händelsevidarebefordran | Nu kan du skicka data till [!DNL Microsoft Azure] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Microsoft Azure] tilläggsöversikt](../../tags/extensions/web/azure/overview.md) för mer information. |

Mer information om plattformens datainsamlingsfunktioner finns i [datainsamling - översikt](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tilldela fält till anpassade klasser när du lägger till direkt i ett schema | När [lägga till ett enskilt fält direkt i ett schema](../../xdm/ui/resources/schemas.md#add-individual-fields)tidigare kunde du bara tilldela fältet till en fältgrupp som överordnad resurs. Förutom fältgrupper kan du nu [tilldela fältet till en anpassad klass](../../xdm/ui/resources/schemas.md#add-to-class) som dess överordnade resurs i stället. |

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- | 
| Betaversion av Oraclets Service Cloud-källa | Använd Oraclets Service Cloud-källa för att importera data från ditt Oracle Service Cloud-konto till Experience Platform. Mer information finns i dokumentationen för [Oracle Service Cloud-källa](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Läs mer om källor i [källöversikt](../../sources/home.md).