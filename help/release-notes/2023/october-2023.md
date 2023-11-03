---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation från oktober 2023 för Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f2d0848952902d94b441566da677ef174518192e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 oktober 2023**

Uppdateringar av befintliga funktioner i Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Användningsstatistik för destinationer | Nya mätvärden har lagts till i kontrollpanelen för licensanvändning. The **[!UICONTROL Audience Activation Size]** och **[!UICONTROL Data Export Size]** mätvärden är ett bekvämt sätt att spåra hur mycket data du har exporterat från Platform i förhållande till dina licensanvändningsrättigheter. Se [tillgängliga mätvärden](../../dashboards/guides/license-usage.md#available-metrics) dokumentation för beskrivningar av dessa och andra användningsvärden för licenser. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikt över instrumentpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | [!DNL Meta] Förbättring av konverterings-API | Det finns tre förbättringar i [Meta Conversions API](/help/tags/extensions/server/meta/overview.md) tillägg: <ul><li>Integrering med [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Skapar en sömlös inloggning genom att du kan dela ditt pixelID och få åtkomst till token för Conversions API-integrering med Adobe.</li><li>Integrering med [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Gör det möjligt för er att leverera annonser till personer som är mer benägna att slutföra en önskad åtgärd och länka tillbaka åtgärden till de annonser som levereras.</li><li>Integrering med [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Gör att du kan skicka LiveRamp-ID:t i CIP-fältet, vilket eliminerar behovet av att dela PII direkt med partners eller Meta. </li></ul> |
| Tillägg | [!DNL LinkedIn] Konverterings-API | The [[!DNL LinkedIn] Konverterings-API](../../tags/extensions/server/linkedin/overview.md) kan ni utvärdera hur effektiva era marknadsföringskampanjer i LinkedIn är genom att skicka händelsedata från Experience Platform till LinkedIn. |
| Hemlighet | [!DNL LinkedIn] OAuth 2 Secret | The [[!DNL LinkedIn] OAuth 2 Secret](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) gör att du kan skicka serverinteraktioner till [!DNL LinkedIn] vid vidarebefordran. |
| Vidarebefordran av händelser | Uppdatera till taggar och händelsevidarebefordran | Bevara [Taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) och [Vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) prestanda i Platform, endast de senaste byggnaderna för Development och Stage kommer att bevaras, både framgångsrika och misslyckade. Alla byggen som inte längre används tas bort. Dessutom har begränsning och hastighetsbegränsning implementerats för att säkerställa att ett fåtal tunga API-användningar inte försämrar API-prestanda för andra. |
| Tillägg | Element, regler och tillägg | [Element, regler och tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) sorteras nu i bibliotekets utdata för att säkerställa större enhetlighet mellan flera versioner och distributioner av samma bibliotek. |

Mer information om datainsamling finns i [datainsamling, översikt](../../tags/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade destinationer** {#new-updated-destinations}

| Destination | Nytt eller uppdaterat | Beskrivning |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nytt | Använd Moengage-målet för att ansluta och mappa dina Adobe-data (användarattribut, segment och händelser) till Moengage i realtid. Sedan kan kunderna agera utifrån dessa data och leverera personaliserade, målinriktade upplevelser. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nytt | Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience ID för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| (Beta) Stöd för att hash-koda funktioner i beräknade fält | Förutom de funktioner som är specifika för [exportera arrayer](../../destinations/ui/export-arrays-calculated-fields.md) eller element från en array kan du nu använda ytterligare [hash-funktioner](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) för att hash-attribut i de exporterade filerna. De hash-funktioner som stöds är: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Begränsad GA) Aktivera kontomålgrupper för vissa destinationer | Real-Time CDP B2B-kunder kan nu aktivera [kontomålgrupper](../../segmentation/ui/account-audiences.md) till vissa destinationer. Mer information om den här funktionen finns i [aktivera kontomålgrupper, självstudiekurs](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

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
