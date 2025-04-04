---
title: Adobe Experience Platform Web SDK FAQ
description: Få svar på vanliga frågor om Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 1%

---

# Vanliga frågor och svar

Den här guiden ger svar på frågor om Adobe Experience Platform Web SDK.

## Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att du kan interagera med de olika tjänsterna i Adobe Experience Cloud.

SDK på webben skickar data på ett lösningsagnostiskt sätt (XDM) till Experience Platform Edge Network, som sedan mappar data till lösningsspecifika format och destinationer och skickar dem i realtid.

Se följande video för mer information om Web SDK: [Meet Alloy.js och Never Tag for an eVar or Mbox Igen](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Hur skiljer sig Adobe Experience Platform Web SDK från tidigare lösningar?

### Före Experience Platform Web SDK

För närvarande måste du distribuera olika JavaScript-bibliotek baserat på varje enskild lösning.

* Varje lösning har ett eget JavaScript-bibliotek, schema och domän.
* Inget av dessa bibliotek har tagits fram för att fungera tillsammans.
* Samlingslösningar och Adobe Experience Platform-fall kräver att dessa olika bibliotek är beroende av varandra, vilket ger rörelsefrihet vid driftsättningen.

Även om taggar i Experience Platform gör det så enkelt att driftsätta och hantera dessa bibliotek finns det fortfarande problem med:

* Biblioteksstorlek (för mycket Adobe-kod på en sida)
* Prestanda (det tar för lång tid att läsa in webbplatser)
* Flera anrop till ett och samma ärende
* Väntar på ECID-retur före personaliseringsanrop (orsakar fördröjning)
* Fraktad datainsamling (vad är en evar?)
* Schemaförväxling mellan lösningar (A4T)
* Många andra mindre optimala saker

Dessutom finns det för närvarande inget JavaScript-bibliotek som skickar data direkt till Adobe Experience Platform.

### Med Experience Platform Web SDK

Nya Web SDK skickar data för följande lösningar till en enda målplats (Experience Platform Edge Network) och löser de vanligaste användningsområdena för de ovannämnda lösningarna.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Besökar-ID
* Adobe Experience Platform

Andra lösningar kommer att följa.

Adobe Experience Platform Web SDK kan också skicka data direkt till Adobe Experience Platform. Dessa data är i XDM-format och mappas till lösningsschemat på serversidan.

## Vad är värdet med nya Web SDK?

**Prestanda:** SDK på webben är mindre än alla Adobe-bibliotek och ger avsevärt snabbare sidinläsning.

**Enkelhet:** Kombinationen av XDM, Web SDK, taggar, Edge Network, Adobe Experience Cloud och Adobe Experience Platform skapar en lättbegriplig och lättanvänd datainsamlingsartikel.

* **XDM:** Det lösningsagnostiska schema som du använder för att skicka data till Adobe. Ingen mer taggning för variabler eller rutor.
* **Web SDK:** Gör det enkelt att skicka och ta emot data till Adobe Experience Platform Edge Network.
* **Taggar:** Förenklar distribution och konfiguration av Web SDK (och andra JavaScript-taggar) på en webbplats.
* **Edge Network:** Dirigera enkelt data till Adobe Experience Platform och lösningar i det format de behöver.
* **Adobe Experience Platform- och Adobe-lösningar:** Aktivera deras värdepaket.

**Kontroll:** Eftersom alla data använder en enda och ansluten dataström kan du logiskt följa och styra hur data ser ut under varje millisekund av resan, till och från program.

**Modern och redo för framtiden:** Web SDK och dess anslutning till Edge Network har gjort det möjligt för Adobe att avsevärt modernisera hur Adobe hanterar datainsamling, personalisering, samtycke och framtiden för cookies från tredje part. (Det aktiverar en förstahandsdomän som hanteras av Adobe.)

**Tid till värde:** Adobe har arbetat hårt (och kommer att fortsätta) för att göra det så enkelt som möjligt att distribuera Web SDK via taggar och mappa klientdata till XDM. När detta arbete är klart kan alla andra Adobe-lösningar och Adobe Experience Platform-tjänster aktiveras och inaktiveras på serversidan. Om du t.ex. använder detta för Adobe Analytics och vill aktivera Target eller Experience Platform kan du enkelt aktivera en funktion för att växla mellan olika datastream-konfigurationer och aktivera de användningsexemplen.

## Vad är [!DNL alloy.js]?

[!DNL alloy.js] är namnet på Web SDK JavaScript-biblioteket. Den refereras i SDK källkod och filnamn.

## Behöver kunderna köpa Adobe Experience Platform för att kunna använda [!DNL Web SDK]?

Nej. Alla som använder Adobe Digital Experience kan använda Adobe Experience Platform Web SDK kostnadsfritt.

* Kunder som *inte* har åtkomst till Experience Platform eller CDP i realtid och som vill använda [!DNL Web SDK] måste konfigurera rätt behörigheter för att skapa scheman och datastreams i användargränssnittet för datainsamlingen eller Experience Platform.
* Kunder som har åtkomst till Experience Platform eller CDP i realtid och som vill använda [!DNL Web SDK] måste konfigurera rätt behörigheter för att skapa scheman, datamängder, identitetsnamnutrymmen och datastreams i användargränssnittet för datainsamlingen eller Experience Platform-gränssnittet.

Mer information om hur du konfigurerar dessa behörigheter finns i vår dokumentation om [behörighetshantering för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Vem ska använda Web SDK?

Adobe Experience Platform Web SDK har utvecklats för följande kunder:

* Adobe Experience Platform
   * Om du behöver skicka data direkt från en enhet till Adobe Experience Platform är detta det officiellt rekommenderade sättet.
   * Adobe är medvetna om att det går snabbare att använda Adobe Analytics Connector om du redan har Adobe Analytics, men det är inte den långsiktiga strategin för datainsamling.

* Kunder med Adobe Experience Cloud
   * Nya Adobe Analytics-, Adobe Audience Manager- och Adobe Target-kunder bör börja med nya Web SDK och inte använda äldre bibliotek.
   * Befintliga kunder som vill få optimerad implementering bör använda nya Web SDK.

## Hur får jag tillgång till SDK på webben?

Web SDK är för närvarande tillgängligt för allmänheten och kan användas för att skicka data till Adobe Experience Cloud-produkter. Möjligheten att skicka data till tredjepartslösningar kommer inom den närmaste framtiden.

SDK kostar inget och Adobe tillhandahåller det kostnadsfritt. Om det behövs kan du ladda ned det och lägga det på dina egna servrar utan kostnad.

Web SDK kräver åtkomst till [datastream-konfigurationer](../datastreams/overview.md) och Experience Platform [XDM schema builder](../xdm/tutorials/create-schema-ui.md) för att Adobe-servrar ska kunna hantera inkommande data från SDK på rätt sätt. Om du vill få åtkomst kontaktar du ditt Adobe-kontoteam för att starta processen.

## Vilka användningsområden stöds för närvarande av Web SDK?

SDK på webben utvecklas snabbt. Fler användningsexempel håller på att bearbetas. Du hittar [listan över användningsfall som stöds här.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Måste befintliga kunder tagga om sina webbplatser?

Det beror på. Adobe Experience Platform Web SDK kan användas i två olika format. Ett dokument för framtida migrering kommer att innehålla ytterligare information.

* **Bara en annan tagg:** Om webbplatsen redan är taggad för lösningar och du inte kan tagga om, men du vill skicka data till Adobe Experience Platform Edge Network för Experience Platform-användningsfall eller kommande händelsevidarebefordringsfunktioner (se nedan), kan du lägga till taggen `alloy.js` på webbplatsen, där den fungerar som&quot;bara en annan tagg&quot;.

* **Den enda taggen:** Om du vill använda Web SDK för en Experience Cloud-lösning måste du använda den för _alla_ lösningar på den sidan. Om din webbplats till exempel redan är taggad för Adobe Analytics och du vill använda den för Target måste du använda den för både och för alla andra i framtiden.

Det innebär att om du bestämmer dig för att använda Adobe Experience Platform Web SDK för icke-lösningsbaserade användningsfall, kan du tagga webbplatsen med `alloy.js` och gå vidare som om det vore en ny lösning. Om du vill använda den för Adobe Analytics, Target eller Audience Manager, eller för programanvändning, kan du behöva ta bort någon av de äldre koderna på sidan.

## Kan jag migrera ECID:n när jag börjar använda Web SDK så att webbplatsens besökare inte börjar visas som nya besökare?

Ja, Adobe Experience Platform Web SDK har en funktion för identitetsmigrering. Följ instruktionerna för ID-migrering i [identitetshandboken för Experience Platform Web SDK](/help/web-sdk/identity/overview.md#id-migration) om du vill ha mer information.

## Hur skiljer sig Web SDK från taggar?

* **Taggar i Experience Platform** hanterar enhetskoden. Använd dem för att enklare distribuera koden. De är kostnadsfria och kraftfulla.

* **Adobe Experience Platform Web SDK** är det officiella namnet på den nya koden som ska distribueras av taggar för Adobe-användningsfall. Den är också kostnadsfri och kraftfull.

* **`alloy.js`** är filnamnet för Adobe Experience Platform Web SDK-koden.

## Måste jag använda taggar för att installera Web SDK?

Nej. Du kan hämta filen `alloy.js` själv.

Men:

* Adobe Experience Platform Web SDK kräver något som kallas dataström-ID så att edge-nätverket kan identifiera dataströmmen och avgöra vad som ska göras med data. Detta ID skapas i Experience Platform. Det innebär inte att du måste använda användargränssnittet för att skapa egenskaper eller distribuera JavaScript-koden, men du måste använda taggar för att skapa ett konfigurations-ID.

* Taggar är inte bara den bästa tillgängliga taggen och SDK-hanterare, utan gör det mycket enkelt att distribuera `alloy.js` och mappa data till XDM-scheman. Om du bestämmer dig för att inte använda taggar måste du hantera distributionen av `alloy.js`, händelsen och mappningen av dina data till XDM innan du skickar dem. Detta är en _mycket_ svårare process än att använda taggar.

* Vi rekommenderar att du använder taggar för att distribuera `alloy.js`, även om det är den enda taggen som du använder den för.

## Vad innebär vidarebefordran av händelser?

Om du använder våra SDK:er och skickar XDM till Edge Network kan du med dessa nya funktioner för händelsevidarebefordran installera nya tillägg på serversidan och mappa dessa data till vad som helst - och skicka dem var som helst - från vårt edge-nätverk. Se det som&quot;datainsamling som en tjänst&quot;. Detta kommer att vara kostnadsfritt och paketeras som en del av Adobe Experience Platform.

## Vad är en CNAME- eller First Party-domän och varför spelar det någon roll?

Mer information om CNAME finns i [Adobe-dokumentationen](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Använder Adobe Experience Platform Web SDK cookies? Om så är fallet, vilka cookies använder den?

Ja, för närvarande använder Web SDK var som helst mellan en och sju cookies beroende på implementeringen. Nedan finns en lista över de cookies som du kan se med Web SDK och hur de används:

| **Namn** | **maxAge** | **Egen ålder** | **Beskrivning** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 dagar | I identitetscookie lagras ECID och annan information om ECID. |
| **kndctr_original_medgivande_check** | 7200 | 2 timmar | Denna sessionsbaserade cookie signalerar till servern att leta upp serversidan för medgivandeinställningar. |
| **kndctr_orgid_medgivande** | 15552000 | 180 dagar | Denna cookie lagrar användarens medgivandeinställning för webbplatsen. |
| **kndctr_orgid_Cluster** | 1800 | 30 minuter | Denna cookie lagrar den Edge Network-region som betjänar den aktuella användarens begäran. Regionen används i URL-sökvägen så att Edge Network kan dirigera begäran till rätt region. Denna cookie har en livslängd på 30 minuter, så om en användare ansluter till en annan IP-adress kan begäran dirigeras till närmaste region. |
| **mbox** | 63072000 | 2 år | Den här cookien visas när inställningen för målmigrering är true. Detta gör att målcookien [mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) kan anges av Web SDK. |
| **mboxEdgeCluster** | 1800 | 30 minuter | Den här cookien visas när inställningen för målmigrering är true. Med denna cookie kan Web SDK kommunicera rätt edge-kluster till at.js så att Target-profiler kan vara synkroniserade när användare navigerar på en webbplats. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 dagar | Den här cookien visas bara när ID-migrering på Adobe Experience Platform Web SDK är aktiverat. Den här cookien är användbar när du går över till SDK medan vissa delar av webbplatsen fortfarande använder visitor.js. Mer information finns i [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md). |

När du använder Web SDK anger Edge Network en eller flera av cookies ovan. Edge Network ställer in alla cookies med attributen `secure` och `sameSite="none"`.

Om du för närvarande har både säkra och osäkra avsnitt på webbplatsen kan det störa användaridentifieringen. När en användare navigerar från ett säkert avsnitt på webbplatsen till ett osäkert avsnitt, genererar Edge Network en ny `ECID` med begäran.

## Vilka webbläsare stöder Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är utformat för att fungera optimalt i de senaste versionerna av Google Chrome, Safari, Firefox och Microsoft Edge Chromium. Du kan ha problem med att använda vissa funktioner i äldre versioner av webbläsare eller inaktuella webbläsare, som Internet Explorer.

## Var finns mer information om Adobe Experience Platform Web SDK?

* [Dokumentation](/help/web-sdk/home.md)
* [Source Code](https://github.com/adobe/alloy)
