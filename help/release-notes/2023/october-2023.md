---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation från oktober 2023 för Adobe Experience Platform.
source-git-commit: 4ab89ef7cabc9d808fd9dab24b6dbe3fe23e53f3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 oktober 2023**

Uppdateringar av befintliga funktioner i Experience Platform:

- [Datainsamling](#data-collection)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | [!DNL Meta] Förbättring av konverterings-API | Det finns tre förbättringar i [Meta Conversions API](/help/tags/extensions/server/meta/overview.md) tillägg: <ul><li>Integrering med [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Skapar en sömlös inloggning genom att du kan dela ditt pixelID och få åtkomst till token för Conversions API-integrering med Adobe.</li><li>Integrering med [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Gör det möjligt för er att leverera annonser till personer som är mer benägna att slutföra en önskad åtgärd och länka tillbaka åtgärden till de annonser som levereras.</li><li>Integrering med [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Gör att du kan skicka LiveRamp-ID:t i CIP-fältet, vilket eliminerar behovet av att dela PII direkt med partners eller Meta. </li></ul> |

Mer information om datainsamling finns i [datainsamling, översikt](../../tags/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Ny funktion**

| Funktion | Beskrivning |
| --- | --- |
| Verktyg i sandlådan | Med sandlådeverktygen kan du förbättra konfigurationsnoggrannheten över sandlådor och smidigt exportera och importera sandlådekonfigurationer mellan sandlådor. Du kan använda sandlådeverktygen för att markera olika objekt och exportera dem till ett paket. Mer information finns i [gränssnittshandbok för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md). |

Mer information om sandlådor finns i [översikt över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] som rör enskilda (t.ex. kunder, prospects, användare eller organisationer) till målgrupper. Du kan skapa målgrupper genom segmentdefinitioner eller andra källor från [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

**Ny funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontomålgrupper (Limited GA GA) | I Real-time Customer Data Platform B2B Edition kan du nu använda kontosegmentering för att göra marknadsföringssegmenteringen från personbaserade målgrupper till kontobaserade målgrupper så enkel och avancerad som möjligt. Mer information om den här funktionen finns i [kontomålgrupper - översikt](../../segmentation/ui/account-audiences.md). |

Läs mer om segmenteringstjänsten i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdaterad autentisering för datalandningszon | Du kan nu se det angivna förfallodatumet för din Data Landing Zone när du visar dina inloggningsuppgifter. Du måste uppdatera din token före förfallodatumet för att kunna fortsätta använda den i programmet. Om du inte uppdaterar din token manuellt före det angivna förfallodatumet uppdateras den automatiskt och en ny token skapas nästa gång du hämtar dina inloggningsuppgifter. Mer information finns i dokumentationen om [med datalandningszonen](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
