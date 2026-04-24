---
solution: Real-Time Customer Data Platform
product: real-time customer data platform
title: Arbeta med MCP-klienter (Beta)
description: Lär dig ansluta Adobe Real-Time CDP till MCP-klienter med MCP-servern
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: b340d118051e2c38e1098b601e9944a7029129dc
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# Arbeta med MCP-klienter (Beta) {#rtcdp-mcp}

Du kan använda integreringen med Adobe Real-Time CDP MCP för att fråga efter målgrupper, mål och aktiveringshälsa med vanliga språk - utan att behöva skriva API-anrop eller navigera på produktskärmar. På den här sidan beskrivs hur integreringen fungerar, vad du kan göra med den och hur du kommer igång.

>[!AVAILABILITY]
>
>Real-Time CDP MCP-servern distribueras som en **fjärrserver för HTTP-transport** som användare installerar och konfigurerar i MCP-klienter och appplattformar som stöds (till exempel Claude, ChatGPT, Claude Code, Codex, Cursor eller VS Code). Autentisering hanteras via ett **webbläsarbaserat inloggningsflöde** - när klienten först ansluter till servern öppnas standardwebbläsaren så att du kan logga in med dina Adobe-inloggningsuppgifter och auktorisera åtkomst. Kontakta Adobe för att få tillgång till detta Beta-program.

## Beta, säkerhet och juridiska meddelanden {#mcp-notices}

**Beta-dokumentationsmeddelande:** Den här dokumentationen omfattar en Beta-funktion och utgör ingen slutgiltig dokumentation. Innehållet som beskrivs här gäller en Beta-release och kan komma att ändras före den allmänna tillgängligheten. Adobe lämnar inga utfästelser om att denna dokumentation är fullständig eller korrekt.

Genom att använda Adobe Real-Time CDP MCP Server (Beta) (&quot;Beta&quot;) bekräftar du härmed att Beta tillhandahålls **som det är&quot; utan någon garanti av något slag**. Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt stödja Beta. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att sådana Beta och/eller medföljande material fungerar korrekt eller fungerar korrekt. Beta betraktas som Konfidentiell information om Adobe. All &quot;Feedback&quot; (information om Beta, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder Beta, förslag, förbättringar och rekommendationer) som du ger Adobe tilldelas härmed till Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

>[!WARNING]
>
>Model Context Protocol (MCP) är en ny öppen källkodsstandard som kan utgöra säkerhets- eller tillförlitlighetsrisker. Adobe MCP-serverintegreringar och relaterad dokumentation tillhandahålls &quot;i befintligt skick&quot; utan garantier av något slag.
>
>Att ansluta MCP-klienter eller servrar till Adobe-produkter är en konfiguration som kunden valt. Kunderna ansvarar för att utvärdera säkerheten och lämpligheten för alla MCP-integreringar. Adobe ansvarar inte för problem som uppstår vid felkonfigurering, felanvändning av MCP, säkerhetsluckor i implementeringar från tredje part eller oavsiktliga åtgärder som utförs via MCP-aktiverade arbetsflöden.
>
>För att minska riskerna rekommenderar Adobe att man testar integreringar i en sandlådemiljö innan de används effektivt, och att man noggrant granskar och validerar alla MCP-initierade åtgärder och svar innan man bekräftar eller förlitar sig på dem.

## Vad är modellkontextprotokollet? {#mcp-overview}

Marknadsföring, data och kundupplevelseteam använder i allt större utsträckning chattbaserade applikationer och utvecklingsverktyg - som Anthropic Claude, OpenAI ChatGPT, Cursor och Microsoft Copilot Studio - för att effektivisera sitt dagliga arbete. Dessa program stöder **Model Context Protocol (MCP)**, en öppen standard som gör att program kan visa back-end-verktyg för stora språkmodeller (LLM) på ett enhetligt sätt.

Real-Time CDP har nu en MCP-server som kan användas för målgrupps-, mål- och aktiveringsåtgärder direkt i alla MCP-kompatibla program. Tack vare integreringen med Real-Time CDP MCP kan olika personer samarbeta kring samma segmenterings- och aktiveringsdata, utan att behöva skriva frågor mot Adobe Experience Platform REST API:er eller navigera i flera gränssnittsskärmar. Kunderna kan beskriva sin avsikt att konvertera och låta LLM anropa rätt MCP-verktyg.

## Viktiga funktioner {#mcp-capabilities}

Med Real-Time CDP MCP-server kan du inspektera, sammanfatta och felsöka målgrupper och mål direkt från AI-assistenten. Alla åtgärder är **skrivskyddade** - MCP-serverytorna hämtar API:er som vanliga svar så att du kan:

* **Få omedelbar målgruppssynlighet** - Fråga om målgruppsdefinitioner, livscykeltillstånd och namnutrymme på ett enkelt språk utan att navigera i menyer eller dra in rapporter manuellt.
* **Beräkna målgruppens storlek före aktivering** - Förhandsgranska antalet medlemskap och konfidensintervall för en PQL- eller SDD-segmentfråga innan du förbinder dig att skapa en målgrupp.
* **Granska din aktiveringsportfölj** - Granska konfigurerade mål, dataflöden som matar dem och käll-/målanslutningarna bakom varje flöde, utan att tolka JSON eller hoppa mellan produktskärmar.
* **Problem med punktaktivering tidigt** - Surface misslyckades eller en pågående målplats körs så fort du frågar, så att teamet kan agera snabbt.
* **Samarbeta kring live-data** - Marknadsförare, datatekniker och intressenter kan fråga samma live-Real-Time CDP-data via sin AI-assistent, vilket gör det enklare att justera, bestämma och flytta tillsammans.

## Tillgängliga verktyg {#mcp-tools}

Verktygets tillgänglighet förändras snabbt när vi aktiverar nya verktyg. Kontakta din Adobe-representant för att få en lista över de senaste tillgängliga verktygen.

>[!NOTE]
>
>Alla verktyg är **skrivskyddade**. Skrivåtgärder (skapa, uppdatera eller ta bort målgrupper, mål eller dataflöden) stöds inte i den aktuella Beta-versionen.

## Användningsfall {#mcp-use-cases}

I följande exempel visas hur du interagerar med MCP-servern [!DNL Adobe Real-Time CDP] med det naturliga språket:

| Mål | Exempelfråga |
| --- | --- |
| **Identifiering av målkatalog** | &quot;Finns TikTok som mål i min sandlåda?&quot; / &quot;Vilka måltyper har jag redan konfigurerat konton för?&quot; |
| **Destinationslager efter typ** | &quot;Ange alla Amazon S3-destinationer.&quot; / &quot;Har jag konfigurerat några exportmål för datauppsättningar?&quot; |
| **Granskning av målkonfiguration** | &quot;Vilken bucket skriver min `Loyalty S3 Export`-destination till?&quot; / &quot;Visa målsökvägen och filformatet för dataflödet [ID].&quot; |
| **Kontohälsa** | &quot;Vilket av mina destinationskonton har passerat autentiseringsuppgifter?&quot; /&quot;Har något Pinterest- eller Facebook-konto ett feltillstånd?&quot; |
| **Aktiveringshälsa - de senaste 24 timmarna** | &quot;Lista alla mål med misslyckade körningar de senaste 24 timmarna.&quot; /&quot;Har mina mål för datauppsättningsexport sänt några data under de senaste 24 timmarna?&quot; |
| **Aktiveringshistorik per mål** | &quot;Exporterade `Weekly Loyalty Export` något under de senaste 30 dagarna?&quot; / &quot;Visa hela körningshistoriken för målet {NAME}.&quot; |
| **Felanalys** | &quot;Vilken är den vanligaste felorsaken till mina filbaserade mål den här veckan?&quot; / &quot;Grupp senaste misslyckades av feltyp.&quot; |
| **Målgruppsidentifiering och filtrering** | &quot;Visa alla CSV-baserade målgrupper i sandlådan `marketing-prod`.&quot; /&quot;Vilka målgrupper har ett externt målgrupps-ID definierat?&quot; |
| **Granskning av målgruppsstorlek** | &quot;Visa mig alla målgrupper med storleken 0.&quot; /&quot;Vilka målgrupper är större än 1 000 profiler?&quot; |
| **Granskning av förfallodatum för målgrupp** | &quot;Vilka destinationer har målgrupper vars slutdatum redan har passerat?&quot; /&quot;Ange målgrupper som ska förfalla inom de kommande 7 dagarna.&quot; |
| **Målgruppsaktivering** | &quot;Vilka destinationer har fler än tio målgrupper aktiverade?&quot; /&quot;Vilken målgrupp aktiveras för de flesta destinationer?&quot; |
| **Flera filter: målgrupp × aktivering** | &quot;Visa mig målgrupper som är större än 1 000 och som är aktiverade på minst två destinationer.&quot; /&quot;Stora målgrupper som bara aktiveras för ett enda mål.&quot; |
| **Förhandsgranskning av målgruppsmedlemskap** | &quot;Förhandsgranska medlemsstorleken för målgruppen `High-Value Loyalty Members`.&quot; / &quot;Beräkna storleken på den här PQL-frågan innan jag sparar den: {EXPRESSION}.&quot; |

## Förutsättningar {#mcp-prerequisites}

Innan du ansluter Real-Time CDP MCP-servern till MCP-klienten bör du kontrollera följande:

* Du har en aktiv Real-Time CDP-licens.
* Du har åtkomst till en klient som stöds och som kan ansluta till en fjärrserver för MCP eller en anpassad MCP-app, till exempel Claude, ChatGPT, Claude Code, Codex, Cursor eller VS Code.
* Du har ditt organisations-ID och namnet på den sandlåda som du vill fråga.
* Du har de behörigheter som krävs i Adobe Experience Platform för att visa målgrupper, mål och flödestjänster.

## Anslut till Real-Time CDP MCP-servern {#mcp-connect}

>[!NOTE]
>
>Integreringen sker i Beta. Klientmenyer, plankrav och administratörskontroller kan variera beroende på program och version.

Kontrollera att du har följande innan du börjar:

* MCP-serverslutpunktens URL: `Available to Beta customers through your Adobe representative`.
* Bekräftelse på att din Adobe-användare har åtkomst till Experience Platform målorganisation och sandlåda.

Real-Time CDP MCP-servern är en **HTTP MCP-fjärrserver**. I varje klient följer konfigurationen samma mönster:

1. Lägg till server-URL:en.
2. Spara eller aktivera anslutningen.
3. Slutför den **webbläsarbaserade Adobe-inloggningen** första gången klienten anropar ett verktyg.
4. Ange `imsOrgId` och `sandboxName` för varje begäran.

### Installera i UI-baserade klienter {#mcp-connect-ui}

#### Claude

För `claude.ai` och Claude Desktop lägger du till Real-Time CDP MCP-servern som en **anpassad koppling** med slutpunkten från din Adobe-representant. Lägg till det under **Anpassa > Kopplingar** i individuella Claude-planer. I Team- och Enterprise-planer kan en ägare behöva lägga till det först under **Organisationsinställningar > Kopplingar**, varefter varje användare kopplar det i sina egna Claude-inställningar. Aktivera anslutningen i en konversation när du har konfigurerat den och fyll i Adobe webbläsarinloggning första gången du använder den.

#### ChatGPT

I ChatGPT lägger du till Real-Time CDP MCP-servern som en **anpassad app/anslutning** med slutpunkten som du fått från din Adobe-representant. Beroende på din chattGPT-plan kan det här kräva **utvecklarläge** och godkännande av arbetsytans administratör. När appen/kopplingen har skapats eller aktiverats ansluter du den från **Inställningar > Appar** eller **Inställningar > Appar och anslutningar** och autentiserar den sedan via webbläsarinloggningen i Adobe när du uppmanas till det.

#### Markör

I Cursor lägger du till Real-Time CDP MCP-servern som en fjärr-MCP-server med slutpunkten från din Adobe-representant. Öppna **Inställningar > MCP**, lägg till en ny server och klistra in slutpunkts-URL:en. Aktivera servern för arbetsytan genom att välja **connect** för autentisering via webbläsaren när du har lagt till den.

#### Andra gränssnittsbaserade klienter

För klienter som VS-kod eller andra datorprogram och webbprogram med fjärrstöd för MCP lägger du till Real-Time CDP MCP-servern som en **fjärr-HTTP**-server med slutpunkten som du fått från din Adobe-representant. Om klienten har stöd för valfria rubriker eller innehavartoken lämnar du dem tomma om inte Adobe särskilt anger något annat. Autentiseringen hanteras via det webbläsarbaserade inloggningsflödet från Adobe första gången.

### Installera i tekniska klienter {#mcp-connect-technical}

#### Claude Code

Lägg till servern från terminalen:

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

Starta sedan Claude Code och kör:

```text
/mcp
```

Markera servern `rtcdp` och fyll i inloggningsflödet för Adobe i webbläsaren. Om du redan har lagt till servern i `claude.ai` kan den också visas automatiskt i Claude Code när båda använder samma konto.

#### Codex

Lägg till servern från terminalen:

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

Autentisera servern:

```bash
codex mcp login rtcdp
```

Verifiera konfigurationen:

```bash
codex mcp list
```

Du kan också lägga till servern direkt i `~/.codex/config.toml`:

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### Obligatoriska parametrar för begäran {#mcp-connect-params}

Varje verktygsanrop kräver två parametrar som omfattar begäran:

* `imsOrgId` - ditt organisations-ID, mappat till rubriken `x-gw-ims-org-id` för Experience Platform API-anrop längre fram i kedjan.
* `sandboxName` - namnet på Experience Platform-sandlådan, mappat till rubriken `x-sandbox-name`.

## Kända begränsningar (Beta) {#mcp-limitations}

Följande begränsningar gäller för den aktuella Beta-versionen av MCP-servern [!DNL Adobe Real-Time CDP]:

| Begränsning | Beskrivning | Tillfällig lösning |
| --- | --- | --- |
| **Skrivskyddad yta** | MCP-servern visar bara API:er för hämtning. Du kan inte skapa, uppdatera, aktivera eller ta bort målgrupper, mål eller dataflöden. | Använd Real-Time CDP-gränssnittet eller AEP REST API:er för skrivåtgärder. |
| **Inga engagemangs- eller leveransvärden** | MCP-servern returnerar inte leveransstatistik, engagemang eller konverteringsstatistik längre fram i kedjan från målplattformarna. | Använd målplattformens egen rapportering, Customer Journey Analytics MCP eller Adobe Analytics MCP för engagemangs- och konverteringsdata. |
| **Segmentfrågan måste skapas externt** | `Preview Audience Membership` kräver ett giltigt PQL- eller SDD-uttryck som indata. MCP-servern skapar inte frågan åt dig. | Skriv PQL/SDD-uttrycket i segmentbyggargränssnittet eller via segmenteringstjänstens API och klistra sedan in det i MCP-prompten. |
| **Sidindelning via tilläggstoken** | Listverktygen returnerar sidnumrerade resultat. Fullständig uppräkning över mycket stora sandlådor kräver att `continuationToken` anrop kopplas. | Begränsa frågor med filter (namn, läge, anslutningsspecifikation, tidsintervall) i stället för att räkna upp hela listan. |
| **Filtrering av aktiveringskörning är endast tidsbaserad** | `Inspect Activation Runs` stöder filtrering efter status och slutförandetidsstämpel (epoch ms UTC), men inte efter feltyp eller målplattform direkt. | Filtrera efter `flowId` först (hämtas från `List Configured Destinations`) så att omfånget körs till ett specifikt mål. |
| **Regionkonfiguration krävs** | Verktygsanrop misslyckas med HTTP 403 &quot;Användarregion saknas&quot; om MCP-gatewayen inte har konfigurerats för din användarregion. | Kontakta din Adobe-representant för att bekräfta att gatewayen har konfigurerats för din region innan du använder den för första gången. |

## Frågor och svar {#mcp-faq}

+++Vilka MCP-klienter stöds?

Real-Time CDP MCP-server fungerar med klienter som stöds och som kan ansluta till MCP-fjärrservrar eller egna MCP-appar, inklusive Claude, ChatGPT, Claude Code, Codex, Cursor och VS Code. Konfigurationsflödet beror på klienten: UI-baserade klienter lägger vanligtvis till servern från inställningarna, medan tekniska klienter som Claude Code och Codex kan lägga till den från kommandoraden eller konfigurationsfiler.
+++

+++Hur fungerar autentiseringen?

Autentisering hanteras via en **webbläsarbaserad inloggning**. När MCP-klienten först anropar ett verktyg öppnas standardwebbläsaren på en inloggningssida för Adobe. När du har autentiserat och auktoriserat klienten etableras sessionen och efterföljande verktygsanrop återanvänder den. Inga API-nycklar eller långvariga autentiseringsuppgifter behöver lagras i din klientkonfiguration.
+++

+++Vilka Real-Time CDP-objekt kan jag få åtkomst till via MCP?

Du kan komma åt målgrupper, måltyper, konfigurerade målkonton, måldataflöden, käll- och målanslutningar samt körningshistorik för aktivering. Åtgärder är skrivskyddade (hämta API:er). Skrivåtgärder stöds inte i den aktuella versionen.
+++

+++Behöver jag utvecklaråtkomst för att kunna använda Real-Time CDP MCP-servern?

Nej. MCP-servern är utformad för både marknadsförings- och teknikprofiler. Marknadsförarna kan interagera med programmet med hjälp av naturliga språkuppmaningar i alla MCP-klienter som stöds, medan datatekniker och utvecklare kan använda det i utvecklingsverktyg som stöder MCP.
+++

+++Skickas mina data till MCP-klientprovidern?

När du skickar ett meddelande kan MCP-klienten skicka relevant kontext (inklusive Real-Time CDP-data som returneras av MCP-servern) till sin modell för bearbetning. Granska sekretess- och datahanteringsprinciperna för MCP-klientleverantören innan du ansluter till produktionsdata.
+++

+++Vilka behörigheter behöver jag i Real-Time CDP?

Du behöver minst **Visa**-behörigheter för de objekt som du vill fråga efter - målgrupper, mål och flödestjänstentiteter. Ingen skrivbehörighet krävs eftersom MCP-servern bara utför läsåtgärder. Kontakta din [!DNL Adobe Experience Platform]-administratör om du är osäker på din nuvarande åtkomstnivå.
+++

+++Kan jag använda MCP-servern i sandlådemiljöer?

Ja. Alla verktygsanrop kräver en `sandboxName`-parameter, så MCP-servern respekterar alltid din [!DNL Adobe Experience Platform] sandlådekonfiguration. Du kan fråga vilken sandlåda som du har åtkomst till genom att ange dess namn i uppmaningen.
+++

+++Vad är skillnaden mellan medlemskap för att förhandsgranska målgrupp och söka efter befintliga målgrupper?

`Search Existing Audiences` returnerar målgrupper som redan har skapats och sparats i din sandlåda. `Preview Audience Membership` tar ett obearbetat PQL- eller SDD-segmentuttryck och returnerar en storleksuppskattning för det - användbart för att ändra storlek på en fråga *innan* du sparar den som en målgrupp.
+++

+++Kan jag ställa frågor till både målgrupper och profilmålgrupper?

Ja. Både `Search Existing Audiences` och `Preview Audience Membership` har stöd för en entitetstypparameter. Profilmålgrupper kan uttryckas i PQL eller SDD. Kontomålgrupper använder alltid SDD-syntax (relativ).
+++
