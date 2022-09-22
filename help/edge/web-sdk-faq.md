---
title: Vanliga frågor om Adobe Experience Platform Web SDK
description: Få svar på vanliga frågor om Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 1%

---

# Frågor och svar

Den här guiden ger svar på frågor som ofta ställs om Adobe Experience Platform Web SDK.

## Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med de olika tjänsterna i Experience Cloud.

Data skickas på ett lösningsagnostiskt sätt (XDM) till Adobe Experience Platform Edge Network, som sedan mappar data till lösningsspecifika format och destinationer och skickar dem i realtid.

**Mer information**
[Adobe Summit presentation](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Hur skiljer sig Adobe Experience Platform Web SDK från tidigare lösningar?

### Före Adobe Experience Platform SDK

För närvarande måste du distribuera olika JavaScript-bibliotek baserat på varje enskild lösning.

* Varje lösning har ett eget JavaScript-bibliotek, -schema och -domän.
* Inget av dessa bibliotek har tagits fram för att fungera tillsammans.
* Samlingslösningar och Adobe Experience Platform-fall kräver att dessa olika bibliotek är beroende av varandra, vilket ger rörelsefrihet vid driftsättningen.

Även om taggar i Platform gör det så enkelt att driftsätta och hantera dessa bibliotek finns det fortfarande problem med:

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

**Prestanda:** SDK för webben är mindre än för alla Adobe-bibliotek och ger avsevärt snabbare sidinläsning.

**Enkelt:** Kombinationen av XDM, Web SDK, taggar, Experience Edge, Adobe Experience Cloud-lösningar och Adobe Experience Platform skapar en lättbegriplig och lättanvänd datainsamlingsberättelse.

* **XDM:** Det lösningsagnostiska schema som du använder för att skicka data till Adobe. Ingen mer taggning för variabler eller rutor.
* **Adobe Experience Platform Web SDK:** Gör det enkelt att skicka och ta emot data till Adobe Experience Platform Edge Network.
* **Taggar:** Förenklar driftsättning och konfiguration av Web SDK (och andra JavaScript-taggar) på en plats.
* **Experience Edge:** Skicka enkelt data till Adobe Experience Platform och lösningar i det format de behöver.
* **Adobe Experience Platform och Adobe:** Aktivera deras värdeförslag.

**Kontroll:** Eftersom alla data använder en enda och sammankopplad dataström kan ni logiskt följa och styra hur data ser ut under varje millisekund av resan, till och från program.

**Modern och redo för framtiden:** Web SDK och dess anslutning till Experience Edge Network har gjort det möjligt för Adobe att avsevärt modernisera hur Adobe hanterar datainsamling, personalisering, samtycke och framtiden för cookies från tredje part. (Det aktiverar en förstahandsdomän som hanteras av Adobe.)

**Tid till värde:** Adobe har arbetat hårt (och kommer att fortsätta) för att göra det så enkelt som möjligt att driftsätta Web SDK via taggar och mappa klientdata till XDM. När detta arbete är klart kan alla andra Adobe-lösningar och Adobe Experience Platform-tjänster aktiveras eller inaktiveras på serversidan. Om du t.ex. använder detta för Adobe Analytics och vill aktivera Target eller Experience Platform kan du enkelt växla mellan olika datastream-konfigurationer och ljusa upp dessa användningsfall.

## Vad är Alloy?

Alloy är kodnamnet för Adobe Experience Platform Web SDK. Det används i SDK:s källkod och filnamn, även om Adobe Experience Platform Web SDK är det officiella namnet.

## Behöver kunderna köpa Adobe Experience Platform för att använda [!DNL Web SDK]?

Nej. Alla som använder Adobe Digital Experience kan använda Adobe Experience Platform Web SDK kostnadsfritt. Kunder som vill använda [!DNL Web SDK] måste konfigurera rätt behörigheter för att skapa scheman, datauppsättningar, identitetsnamnutrymmen och datastreams i användargränssnittet för Adobe Experience Platform Data Collection.

Mer information om hur du konfigurerar dessa behörigheter finns i vår dokumentation om [behörighetshantering för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Vem ska använda Web SDK?

Adobe Experience Platform Web SDK har utvecklats för följande personer:

* Adobe Experience Platform
   * Om du behöver skicka data direkt från en enhet till Adobe Experience Platform är detta det officiellt rekommenderade sättet.
   * Adobe är medvetna om att det går snabbare att använda Adobe Analytics Connector om kunden redan har Adobe Analytics, men det är inte den långsiktiga strategin för datainsamling.

* Kunder med Adobe Experience Cloud
   * Nya Adobe Analytics-, Adobe Audience Manager- och Adobe Target-kunder bör börja med nya Web SDK och inte använda äldre bibliotek.
   * Befintliga kunder som vill få optimerad implementering bör använda nya Web SDK.


## Hur får jag tillgång till Adobe Experience Platform Web SDK?

Web SDK är för närvarande tillgängligt för allmänheten och kan användas för att skicka data till Adobe Experience Cloud-produkter. Möjligheten att skicka data till tredjepartslösningar kommer inom den närmaste framtiden. SDK är kostnadsfritt, hanteras av Adobe utan kostnad och kan laddas ned så att du kan ha det på dina egna servrar, om du vill, utan kostnad. För att Adobe-servrar ska kunna hantera inkommande data som kommer från SDK måste du ha tillgång till konfigurationer för dataström och Adobe Experience Platform XDM-schemaverktyget. Om du vill få åtkomst kontaktar du din Customer Success Manager (CSM) för att starta förfrågningsprocessen.

## Vilka användningsfall stöds för närvarande av Web SDK?

Web SDK utvecklas snabbt. Fler användningsexempel håller på att bearbetas. Du hittar [lista över de användningsfall som stöds här.](https://github.com/adobe/alloy/projects/5)

## Måste befintliga kunder tagga om sina webbplatser?

Det beror på. Adobe Experience Platform Web SDK kan användas i två olika format. Ett dokument för framtida migrering innehåller ytterligare information.

* **Bara en annan tagg:** Om webbplatsen redan är taggad för lösningar och du inte kan tagga om, men du vill skicka data till Adobe Experience Platform Edge Network för Experience Platform eller kommande händelsevidarebefordringsfunktioner (se nedan), kan du lägga till `alloy.js` -taggen till webbplatsen, där den fungerar som&quot;bara en annan tagg&quot;.

* **Den enda taggen:** Om du vill använda Web SDK för en Experience Cloud-lösning måste du använda den för _alla_ av lösningarna på den sidan. Om din webbplats till exempel redan är taggad för Adobe Analytics och du vill använda den för Target måste du använda den för både och för alla andra i framtiden.

Med andra ord, om du bestämmer dig för att använda Adobe Experience Platform Web SDK för icke-lösningsexempel, kan du tagga webbplatsen med `alloy.js` och gå vidare som om det vore en ny lösning. Om du vill använda den för Adobe Analytics, Target eller Audience Manager, eller för programanvändning, kan du behöva ta bort någon av de äldre koderna på sidan.

## Kan jag migrera ECID:n när jag börjar använda Alloy så att webbplatsens besökare inte börjar visas som nya besökare?

Ja, Adobe Experience Platform Web SDK har en funktion för identitetsmigrering. Följ instruktionerna för ID-migrering i [Identitetsdokumentation för Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) för mer information.

## Hur skiljer sig Web SDK från taggar?

* **Taggar i Experience Platform** hantera enhetskoden. Använd dem för att enklare distribuera koden. De är kostnadsfria och kraftfulla.

* **Adobe Experience Platform Web SDK** är det officiella namnet på den nya koden som ska distribueras av taggar för Adobe-användningsfall. Den är också kostnadsfri och kraftfull.

* **`alloy.js`** är filnamnet på Adobe Experience Platform Web SDK-koden.

## Måste jag använda taggar för att distribuera Web SDK?

Nej. Du kan ladda ned `alloy.js` själv.

Men:

* Adobe Experience Platform Web SDK kräver något som kallas dataström-ID så att edge-nätverket kan identifiera dataströmmen och avgöra vad som ska göras med data. Detta ID skapas i Experience Platform. Det innebär inte att du måste använda användargränssnittet för datainsamling för att skapa egenskaper eller distribuera JavaScript-koden, men du måste använda taggar för att skapa ett konfigurations-ID.

* Taggar är inte bara den bästa tillgängliga taggen och SDK-hanteraren, det är mycket enkelt att distribuera `alloy.js` och mappa data till XDM-scheman. Om du bestämmer dig för att inte använda taggar måste du hantera distributionen `alloy.js`, händelser och mappning av data till XDM innan de skickas. Det här är en _mycket_ svårare än att använda taggar.

* Vi rekommenderar att du använder taggar för att distribuera `alloy.js`, även om det är den enda taggen som du använder den för.

## Vad innebär vidarebefordran av händelser?

Om du använder våra SDK:er och skickar XDM till Experience Edge kan du med dessa nya funktioner för händelsevidarebefordran installera nya tillägg på serversidan och mappa dessa data till vad som helst - och skicka dem var som helst - från vårt edge-nätverk. Se det som&quot;datainsamling som en tjänst&quot;. Detta kommer att vara kostnadsfritt och paketeras som en del av Adobe Experience Platform.

## Vad är en CNAME- eller First Party-domän och varför spelar det någon roll?

Mer information om CNAME finns i [Adobe dokumentation](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Använder Adobe Experience Platform Web SDK cookies? Om så är fallet, vilka cookies använder den?

Ja, för närvarande använder Web SDK var som helst mellan 1-4 cookies beroende på implementeringen. Nedan visas en lista över de fyra cookies som du kan se med Web SDK och hur de används:

**kndct_orgid_identity:** Identitetskakan används för att lagra ECID och annan information som rör ECID.

**kndctr_orgid_medgivande:** Denna cookie lagrar användarens medgivandeinställning för webbplatsen.

**kndctr_orgid_Cluster:** Denna cookie lagrar Experience Edge-regionen som betjänar den aktuella användarens begäran. Regionen används i URL-sökvägen så att Experience Edge kan dirigera begäran till rätt region. Denna cookie har en livslängd på 30 minuter, så om en användare ansluter till en annan IP-adress kan begäran dirigeras till närmaste region.

När du använder Web SDK anger Edge Network en eller flera av cookierna ovan. Edge Network ställer in alla cookies med `secure` och `sameSite="none"` attribut.

Om du för närvarande har både säkra och osäkra avsnitt på webbplatsen kan det störa användaridentifieringen. När en användare navigerar från ett säkert avsnitt på webbplatsen till ett osäkert avsnitt, genererar Edge Network ett nytt `ECID` med begäran.

## Vilka webbläsare stöder Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är utformat för att fungera optimalt i de senaste versionerna av Google Chrome, Safari, Firefox, Internet Explorer 11 och Microsoft Edge Chromium. Du kan ha problem med att använda vissa funktioner i äldre versioner av webbläsare.

## Var kan jag få mer information om Adobe Experience Platform Web SDK?

* [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Källkod](https://github.com/adobe/alloy)
