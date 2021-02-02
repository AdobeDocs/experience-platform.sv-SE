---
title: Vanliga frågor om Web SDK
seo-title: Vanliga frågor om Adobe Experience Platform Web SDK
description: Frågor och svar om Adobe Experience Platform Web SDK
seo-description: Frågor och svar om Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: f4f0b00dfd324f69aa2b4348740f6e767e86a6de
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 1%

---


# Frågor och svar

Frågor och svar innehåller frågor som ofta ställs om Adobe Web SDK.

## Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med de olika tjänsterna i Experience Cloud.

Data skickas på ett lösningsagnostiskt sätt (XDM) till Adobe Experience Platform Edge Network, som sedan mappar data till lösningsspecifika format och destinationer och skickar dem i realtid.

**Mer**
[informationPresentation av Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Hur skiljer sig Adobe Experience Platform Web SDK från tidigare lösningar?

### Före Adobe Experience Platform SDK

För närvarande måste du distribuera olika JavaScript-bibliotek baserat på varje enskild lösning.

* Varje lösning har ett eget JavaScript-bibliotek, -schema och -domän.
* Inget av dessa bibliotek har tagits fram för att fungera tillsammans.
* Samlingslösningar och Adobe Experience Platform-fall kräver att dessa olika bibliotek är beroende av varandra, vilket ger rörelsefrihet vid driftsättningen.

Även om Adobe Experience Platform Launch gör det så enkelt att driftsätta och hantera dessa bibliotek finns det fortfarande problem med:

* Biblioteksstorlek (för mycket Adobe-kod på en sida)
* Prestanda (det tar för lång tid att läsa in webbplatser)
* Flera anrop till ett och samma ärende
* Väntar på ECID-retur före personaliseringsanrop (orsakar fördröjning)
* Fraktad datainsamling (vad är en evar?)
* Schemaförväxling mellan lösningar (A4T)
* Många andra mindre optimala saker

Dessutom finns det för närvarande inget JavaScript-bibliotek som skickar data direkt till Adobe Experience Platform.

### Med Adobe Experience Platform Web SDK

Nya Web SDK skickar data för följande lösningar till ett enda mål (Adobe Experience Platform Edge Network) och löser de vanligaste användningsområdena för de ovannämnda lösningarna.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Besökar-ID
* Adobe Experience Platform

Andra lösningar kommer senare i år.

Adobe Experience Platform Web SDK kan även skicka data direkt till Adobe Experience Platform. Dessa data finns i XDM och mappas till lösningsschemat på serversidan.

## Vad är värdet med nya Web SDK?

**Prestanda:** SDK för webben är mindre än alla de aktuella Adobe-biblioteken och ger avsevärt snabbare sidinläsning.

**Enkelhet:** Kombinationen av XDM, Web SDK, Experience Platform Launch, Experience Edge, Adobe Experience Cloud och Adobe Experience Platform skapar en lättbegriplig och lättanvänd datainsamlingsberättelse.

* **XDM:** Det lösningsagnostiska schema som du använder för att skicka data till Adobe. Ingen mer taggning för variabler eller rutor.
* **Adobe Experience Platform Web SDK:** Gör det enkelt att skicka och ta emot data till Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** Förenklar driftsättning och konfigurering av Web SDK (och andra JavaScript-taggar) på en plats.
* **Experience Edge:** Skicka enkelt data till Adobe Experience Platform och lösningar i det format de behöver.
* **Adobe Experience Platform och Adobe:** Aktivera deras värdepaket.

**Kontroll:** Eftersom alla data använder en enda och sammankopplad dataström kan ni logiskt följa och styra hur data ser ut under varje millisekund av deras resa, till och från program.

**Modern och redo för framtiden:** Web SDK och dess anslutning till Experience Edge-nätverket har gjort att Adobe har kunnat modernisera hur Adobe hanterar datainsamling, personalisering, samtycke och framtiden för cookies från tredje part. (Det aktiverar en förstahandsdomän som hanteras av Adobe.)

**Time-to-value:** Adobe har jobbat hårt (och kommer att fortsätta) för att göra det så enkelt som möjligt att driftsätta Web SDK via Experience Platform Launch och mappa klientdata till XDM.  När detta arbete är klart kan alla andra Adobe-lösningar och Adobe Experience Platform-tjänster aktiveras eller inaktiveras på serversidan. Om du t.ex. använder detta för Adobe Analytics och vill aktivera Target eller Experience Platform kan du enkelt växla till Experience Edge-konfigurationen och ljusa upp de användningsexemplen.

## Vad är Alloy?

Alloy är kodnamnet för Adobe Experience Platform Web SDK. Det används i SDK:s källkod och filnamn, även om Adobe Experience Platform Web SDK är det officiella namnet.

## Behöver kunderna köpa Adobe Experience Platform för att använda Web SDK?

Nej. Alla Adobe Digital Experience-kunder kan använda den. Helt gratis. Alla kunder som vill använda Web SDK får tillgång till scheman och datauppsättningar i Adobe Experience Platform användargränssnitt.

## Vem ska använda Web SDK?

Adobe Experience Platform Web SDK har utvecklats för följande personer:

* Adobe Experience Platform

   Om du behöver skicka data direkt från en enhet till Adobe Experience Platform är detta det officiellt rekommenderade sättet.

   Adobe är medvetna om att det går snabbare att använda Adobe Analytics Connector om kunden redan har Adobe Analytics, men det är inte den långsiktiga strategin för datainsamling.

* Kunder med Adobe Experience Cloud

   Nya Adobe Analytics-, Adobe Audience Manager- och Adobe Target-kunder bör börja med nya Web SDK och inte använda äldre bibliotek.

   Befintliga kunder som vill få optimerad implementering bör använda nya Web SDK.


## Hur får jag tillgång till Adobe Experience Platform Web SDK?

Web SDK är för närvarande tillgängligt för allmänheten och kan användas för att skicka data till Adobe Experience Cloud-produkter. Möjligheten att skicka data till tredjepartslösningar kommer inom den närmaste framtiden. SDK är kostnadsfritt, hanteras av Adobe utan kostnad och kan laddas ned så att du kan ha det på dina egna servrar, om du vill, utan kostnad. För att Adobe-servrar ska kunna hantera inkommande data som kommer från SDK måste du ha tillgång till konfigurationer för plattforms-Edge Network och Schema Builder för Adobe Experience Platform XDM. Om du vill få åtkomst kontaktar du din Customer Success Manager (CSM) för att starta förfrågningsprocessen.

## Vilka användningsfall stöds för närvarande av Web SDK?

Web SDK utvecklas snabbt. Fler användningsexempel håller på att bearbetas. Du hittar listan [över användningsfall som stöds här.](https://github.com/adobe/alloy/projects/5)

## Måste befintliga kunder tagga om sina webbplatser?

Det beror på. Adobe Experience Platform Web SDK kan användas i två olika format. Ett dokument för framtida migrering innehåller ytterligare information.

* **Bara en annan tagg:** Om webbplatsen redan är taggad för lösningar och du inte kan tagga om, men du vill skicka data till Adobe Experience Platform Edge Network för Experience Platform eller kommande serverfunktioner på Experience Platform Launch (se nedan), kan du lägga till  `alloy.js` taggen på webbplatsen, där den fungerar som&quot;bara en annan tagg&quot;.

* **Den enda taggen:** Om du vill använda Web SDK för en Experience Cloud-lösning måste du använda den för  __ alla lösningar på den sidan. Om din webbplats till exempel redan är taggad för Adobe Analytics och du vill använda den för Target måste du använda den för både och för alla andra i framtiden.

Det innebär att om du bestämmer dig för att använda Adobe Experience Platform Web SDK för icke-lösningsbaserade fall kan du tagga webbplatsen med `alloy.js` och gå vidare som om det vore en ny lösning. Om du vill använda den för Adobe Analytics, Target eller Audience Manager, eller för programanvändning, kan du behöva ta bort någon av de äldre koderna på sidan.

## Kan jag migrera ECID:n när jag börjar använda Alloy så att webbplatsens besökare inte börjar visas som nya besökare?

Ja, Adobe Experience Platform Web SDK har en funktion för identitetsmigrering. Följ instruktionerna för ID-migrering i [identitetshandboken för Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) om du vill ha mer information.

## Hur skiljer sig Web SDK från Adobe Experience Platform Launch?

* **Experience Platform** Launchis the device code manager. Använd den för att enklare driftsätta koden. Det är gratis och kraftfullt.

* **Adobe Experience Platform Web** SDK är det officiella namnet på den nya koden som ska distribueras av Experience Platform Launch för Adobe. Den är också kostnadsfri och kraftfull.

* **`alloy.js`** är filnamnet på Adobe Experience Platform Web SDK-koden.

## Måste jag använda Adobe Experience Platform Launch för att installera Web SDK?

Nej. Du kan hämta `alloy.js`-filen själv.

Men:

* Adobe Experience Platform Web SDK kräver något som kallas Experience Edge-konfigurations-ID så att edge-nätverket kan identifiera strömmen och avgöra vad som ska göras med data. Detta ID skapas i Experience Platform Launch. Det innebär inte att du måste använda Experience Platform Launch för att skapa egenskaper eller distribuera JavaScript-koden, men du måste använda Experience Platform Launch för att skapa ett konfigurations-ID.

* Adobe Experience Platform Launch är inte bara den bästa tillgängliga taggen och SDK-hanteraren, utan gör det mycket enkelt att distribuera `alloy.js` och mappa data till XDM-scheman. Om du bestämmer dig för att inte använda Experience Platform Launch måste du hantera distributionen av `alloy.js`, händelser och mappning av data till XDM innan du skickar dem. Detta är en _mycket_ svårare process än att använda Experience Platform Launch.

* Vi rekommenderar att du använder Experience Platform Launch för att distribuera `alloy.js`, även om det är den enda taggen som du använder den för.

## Vad är&quot;Adobe Experience Platform Launch Server Side&quot;?

Senare under 2020 kommer Experience Platform Launch att släppa vidarebefordringsfunktioner på serversidan. Om du använder våra SDK:er och skickar XDM till Experience Edge kan du med dessa nya funktioner installera nya tillägg på serversidan och mappa dessa data till vad som helst - och skicka dem var som helst - från vårt edge-nätverk. Se det som&quot;datainsamling som en tjänst&quot;.  Detta kommer att vara kostnadsfritt och paketeras som en del av Adobe Experience Platform.

## Vad är en CNAME- eller First Party-domän och varför spelar det någon roll?

Mer information om en CNAME finns i [Adobe-dokumentationen](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/cname.html)

## Använder Adobe Experience Platform Web SDK cookies? Om så är fallet, vilka cookies använder den?

Ja, för närvarande använder Web SDK var som helst mellan 1-4 cookies beroende på implementeringen. Nedan visas en lista över de fyra cookies som du kan se med Web SDK och hur de används:

**kCct_origin_identity:** Identitetskakan används för att lagra ECID samt annan information som rör ECID.

**kndctr_original_medgivande:** Den här cookien lagrar användarens medgivandeinställning för webbplatsen.

**kndctr_orgid_personalization:** Denna cookie innehåller sessionsinformation som Adobe Target använder för att anpassa webbsidor.

**kndctr_orgid_consentcheck:** Denna sessionsbaserade cookie signalerar till servern att söka efter serversidan för medgivandeinställningarna.

## Var kan jag få mer information om Adobe Experience Platform Web SDK?

* [Dokumentation](https://docs.adobe.com/content/help/sv-SE/experience-platform/edge/home.html)
* [Källkod](https://github.com/adobe/alloy)
