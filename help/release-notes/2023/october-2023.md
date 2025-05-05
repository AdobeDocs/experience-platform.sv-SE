---
title: Versionsinformation om Adobe Experience Platform oktober 2023
description: Versionsinformationen för Adobe Experience Platform i oktober 2023.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 36%

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

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Användningsstatistik för destinationer | Nya mätvärden har lagts till i kontrollpanelen för licensanvändning. Måtten **[!UICONTROL Audience Activation Size]** och **[!UICONTROL Data Export Size]** är ett bekvämt sätt att spåra hur mycket data du har exporterat från Experience Platform i förhållande till dina licensanvändningsrättigheter. I dokumentationen för [tillgängliga mätvärden](../../dashboards/guides/license-usage.md#available-metrics) finns beskrivningar av dessa och andra användningsvärden för licenser. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | Förbättring av konverterings-API för [!DNL Meta] | Det finns tre förbättringar i tillägget [Metakonverterings-API](/help/tags/extensions/server/meta/overview.md): <ul><li>Integrering med [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Skapar en sömlös inloggning genom att du kan dela ditt pixelID och din åtkomsttoken för Conversions API-integrering med Adobe.</li><li>Integrering med [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Gör att du kan leverera annonser till personer som troligtvis kommer att slutföra en önskad åtgärd och länka åtgärden tillbaka till de annonser som levereras.</li><li>Integrering med [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Gör att du kan skicka LiveRamp-ID:t i CIP-fältet, vilket eliminerar behovet av att dela PII direkt med partner eller Meta. </li></ul> |
| Tillägg | API för konvertering av [!DNL LinkedIn] | Med [[!DNL LinkedIn] API:t för konvertering](../../tags/extensions/server/linkedin/overview.md) kan du utvärdera effekten av dina LinkedIn-marknadsföringskampanjer genom att skicka händelsedata från Experience Platform till LinkedIn. |
| Hemlighet | [!DNL LinkedIn] OAuth 2-hemlighet | Med [[!DNL LinkedIn] OAuth2-hemligheten](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) kan du skicka server-server-interaktioner till [!DNL LinkedIn] vid händelsevidarebefordran. |
| Vidarebefordran av händelser | Uppdatera till taggar och händelsevidarebefordran | Om du vill bevara prestanda för [taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) och [händelsevidarebefordran](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE) i Experience Platform behålls endast de senaste byggnaderna för utveckling och scenen, både lyckade och misslyckade,. Alla byggen som inte längre används tas bort. Dessutom har begränsning och hastighetsbegränsning implementerats för att säkerställa att ett fåtal tunga API-användningar inte försämrar API-prestanda för andra. |
| Tillägg | Element, regler och tillägg | [Element, regler och tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html?lang=sv-SE) sorteras nu i bibliotekets utdata för att säkerställa mer konsekvens mellan flera versioner och distributioner av samma bibliotek. |

Mer information om datainsamling finns i [översikten över datainsamlingar](../../tags/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Nytt eller uppdaterat | Beskrivning |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nyhet | Använd Moengage-målet för att ansluta och mappa dina Adobe-data (användarattribut, segment och händelser) till Moengage i realtid. Sedan kan kunderna agera utifrån dessa data och leverera personaliserade, målinriktade upplevelser. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nyhet | Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience ID för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| (Beta) Stöd för hash-funktioner i beräknade fält | Förutom de funktioner som är specifika för [att exportera arrayer](../../destinations/ui/export-arrays-maps-objects.md) eller element från en array, kan du nu använda ytterligare [hash-funktioner](../../destinations/ui/export-arrays-maps-objects.md#hashing-functions) för att hash-formatera attribut i de exporterade filerna. De hash-funktioner som stöds är: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Begränsad GA) Aktivera kontomålgrupper för vissa destinationer | Real-Time CDP B2B-kunder kan nu aktivera [kontomålgrupper](../../segmentation/types/account-audiences.md) för vissa destinationer. Mer information om den här funktionen finns i självstudiekursen [Aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

Mer allmän information om destinationer finns i [översikten över destinationer](../../destinations/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Ny funktion**

| Funktion | Beskrivning |
| --- | --- |
| Verktyg i sandlådan | Med sandlådeverktygen kan du förbättra konfigurationsnoggrannheten över sandlådor och smidigt exportera och importera sandlådekonfigurationer mellan sandlådor. Du kan använda sandlådeverktygen för att markera olika objekt och exportera dem till ett paket. Mer information finns i användargränssnittsguiden för [sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md). |

Mer information om sandlådor finns i översikten över [sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Experience Platform] och är tillgängliga för alla Adobe-lösningar.

**Ny funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontomålgrupper (Limited GA GA) | I Real-Time Customer Data Platform B2B edition kan ni nu använda kontosegmentering för att göra marknadsföringssegmenteringen från personbaserade målgrupper till kontobaserade målgrupper så enkel och avancerad som möjligt. Mer information om den här funktionen finns i [översikten över kontomålgrupper](../../segmentation/types/account-audiences.md). |

Läs [Översikt över segmenteringstjänsten](../../segmentation/home.md) om du vill veta mer om segmenteringstjänsten.

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdaterad autentisering för datalandningszon | Du kan nu se det angivna förfallodatumet för din Data Landing Zone när du visar dina inloggningsuppgifter. Du måste uppdatera din token före förfallodatumet för att kunna fortsätta använda den i programmet. Om du inte uppdaterar din token manuellt före det angivna förfallodatumet uppdateras den automatiskt och en ny token skapas nästa gång du hämtar dina inloggningsuppgifter. Mer information finns i dokumentationen om [att använda Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Läs [Källöversikten](../../sources/home.md) om du vill veta mer om källor.
