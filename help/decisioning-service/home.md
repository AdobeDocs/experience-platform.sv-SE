---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beslutstjänst
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Översikt över beslutstjänsten

Beslutstjänsten ger möjlighet att skapa personaliserade, optimerade och samordnade upplevelser i program som körs på Adobe Experience Platform. Med hjälp av beslutstjänsten kan du fastställa det bästa *alternativet* bland en uppsättning tillgängliga alternativ. Dessa alternativ, som också kallas alternativ, kan vara erbjudanden, produktrekommendationer, innehållskomponenter för en webbupplevelse, konversationsskript och åtgärder som ska vidtas. För närvarande stöds användningsexempel och domän för *offertbeslut* , där beslutsalternativen utformas specifikt som erbjudanden, med stöd för fler användningsfall.

Med Beslutstjänsten kan kunderna återanvända affärslogik och dela en katalog med alternativ i olika kanaler och i olika tillämpningar. I stället för att hantera beslutsalternativ - och strategier för att välja ut dem - på djupet i en applikation kan de nu utnyttjas oavsett när, hur och på vilken kanal en kunds slutanvändare interagerar med ett företag eller en organisation.

Beslutsstrategier kan påverka de många interaktioner en kund har haft, i många kanaler och i många tillämpningar. Anropscentrets programaktivitet kan t.ex. aktivera eller inaktivera ett marknadsföringsmeddelande under en tid efter ett klagomål, och själva meddelandet kan vara baserat på inköp och recensioner som kunden gjort.

Beslutstjänsten underlättar en utvecklad upplevelsepersonalisering.

| Före Experience Decision | Efter Experience Decision |
| --- | --- |
| Personalisera och optimera användarens upplevelser i en enda kanal eller i en liten uppsättning upplevelsekontaktytor. | Erfarenheter är samordnade svar över alla interaktioner. |
| Optimeringarna är inriktade på en enda och vanligtvis kort fas av slutanvändarens resa | Besluten baseras på hela interaktionshistoriken, från beteenden som upptäckts tidigare till den senaste situationen. |
| Alternativen, och strategierna för att välja vilka som ska visas under en kunds upplevelse, kodas vanligtvis djupt inuti programmet. | Strategier för att välja det bästa alternativet definieras utanför de kanalspecifika programmen och blir återanvändbara. |
| Kundupplevelserna är personaliserade och optimerade i enlighet med ett förenklat mål, t.ex. öka antalet lyckade utcheckningar på en webbsida eller acceptera ett erbjudande som presenteras i en interaktion med en representant. | Kundupplevelserna optimeras baserat på en helhetsförståelse av kundens aktuella behov och anpassas till alla upplevelser som användaren hade, både bra och dåliga. En marknadsföringskampanj kanske inte passar en kund som nyligen har gjort ett klagomål om en produkt eller tjänst. |

Beslutsfattartjänsten flyttar era funktioner för upplevelseanpassning från målinriktning i en enda kanal till att fastställa det övergripande stadiet i era kunders interaktion med ert varumärke oberoende av kanaler. Ett livscykelstadium är mycket mer komplext än ett segmentmedlemskap och är nästan alltid baserat på komplexa händelseströmmar, affärsregler och förväntade attribut.

Andra termer som används av produkter och tjänster som syftar till liknande användningsområden:

- Interaktionshantering i realtid (RTIM)
- Resehantering
- Flerkanalsmarknadsföring och personalisering
- Realtidsbeslut

## Hur fungerar beslutstjänsten?

Upplevelserna kan anpassas med hjälp av beslutstjänsten i realtid när kunden interagerar med ert varumärke via en inkommande kanal, som er webbplats eller mobilapp. Beslutsfattandet kan också användas för att anpassa meddelanden via utgående kanal, som ett e-postmeddelande eller push-meddelande.

Beslut kan fattas på många sätt. Ett tillvägagångssätt är att ta bort alternativ stegvis tills antingen bara ett är kvar eller alternativen har parsats ihop och det finns en delmängd kvar eller så väljs en vinnare slumpmässigt ur den reducerade uppsättningen. En variant av den här metoden för att välja det vinnande alternativet enligt en beräknad formel. Rangordna valbara alternativ med en funktion. Vid beslut om erbjudanden kan funktionen beräkna kostnaden, värdet på erbjudandet till företaget och använda en i förväg bestämd sannolikhet att erbjudandet godtas av slutanvändaren. Resultatpoängen kan användas för att beställa erbjudandena.

Alternativt eller ytterligare kan en strategi baseras på resultat som samlats in från tidigare interaktioner med liknande kunder som föreslogs liknande alternativ. I den här strategin lär sig funktionen som beräknade prioritetsvärdena. Det optimala resultatvärdet är knutet till aktivitetens mål och resultatindikatorn för förutsägelsen är hur ofta resultatet uppnåddes efter att alternativet hade föreslagits.

### Beslutsstrategi

Beslutsstrategier konfigureras via objekt som kallas _aktiviteter_. Varje beslutsstrategi är i princip en algoritm eller en funktion som tar N-alternativen {o1, o2, ...oN} som indata och skapar en ordnad lista med alternativ (o1, o2,...oK) där det första alternativet i listan anses vara det bästa enligt ett optimeringskriterier, det andra alternativet i resultatlistan betraktas sedan som det näst bästa alternativet o.s.v.

Vid en given tidpunkt under kundresan utvärderas det bästa alternativet för en viss aktivitet på nytt baserat på den senaste uppsättningen sammanhangsvariabler, regler och begränsningar. Sammanhangsvariabler innehåller de poster som lagras i kundprofilen i realtid. En central postenhet är en kunds profil, men andra enheter som affärsdata är lika tillgängliga för aktiviteten.

Algoritmen eller funktionen som skapar listan med alternativ för översta K varierar beroende på användningsfallet. De interna komponenterna i den algoritmen är olika för olika användningsområden. Komponenterna definieras i en databas vid designtillfället och&quot;kompileras&quot; till instruktioner för den fallspecifika beslutsstrategin.

![beslutsoptimering](./images/decisioning-optimization.png)

## Arbeta med beslutstjänst

Beslutstjänsten, liksom andra plattformstjänster, antar en API:s första filosofi. Det innebär att API:t är det primära gränssnittet där alla funktioner, inklusive administrativa funktioner, är tillgängliga via API:er. Det innebär också att samma API:er används för andra plattformstjänster, Adobe-lösningar och tredjepartsintegreringar.

Du kan använda beslutstjänsten i ett synkront interaktionsläge för begäran/svar som underlättas av ett enkelt HTTP REST API. API-anropet returnerar det för närvarande bästa alternativet för en enskild profil. Det&quot;för närvarande bästa alternativet&quot;-val ändras baserat på de regler och begränsningar som tillämpas på alla alternativ som är aktuella för en viss aktivitet. Med REST API kan du få det bästa alternativet för flera aktiviteter samtidigt. Detta gör det möjligt att skilja mellan olika alternativ i olika kanaler. När svar för flera aktiviteter hämtas tillsammans kan ytterligare regler tillämpas.

![decisioning-API](./images/decisioning-API.png)

### Integrering med andra arbetsflöden för plattformar

Beslutstjänsten är valfri och kräver bara några få steg utöver de vanliga stegen som krävs för att skapa profilentiteter och hantera dem.

>[!NOTE] För att få ut så mycket som möjligt av kundprofilen i realtid integreras beslutsprocessen direkt med profilbutiken. API-anropen behöver bara ange en av identiteterna för en viss profil.

Den typiska stegsekvensen börjar med att bygga ut profiler:

- Autentisera till Experience Platform.
- Definiera ett schema baserat på profilklassen och definiera eventuellt ett schema baserat på upplevelsehändelseklassen.
- Konfigurera en datauppsättning för överföring av post- och tidsseriedata till kundprofilen.
- Lägg till data via den datauppsättning som konfigurerats i föregående steg eller strömma instansdata via Pipeline.
- Strömma upplevelsehändelser i plattformen för att berika profilen med beteendedata.

Om du vill använda beslutstjänsten gör du dessutom följande:

- Definiera beslutskomponenter med hjälp av API:er för databaser. Detta är de affärslogikenheter som utgör beslutsstrategin. Beslutskomponenterna kompileras automatiskt till ett format som används av beslutstjänstens körningsmiljö. Databas-API:erna visas till vänster i diagrammet nedan.
- Anropa körtids-API:t för att få det bästa alternativet enligt den affärslogik som definierats i föregående steg. API:erna för beslutstjänstens körningsmiljö visas till höger i diagrammet nedan.

![decisioning-API1](./images/decisioning-API1.png)

Aktiveringen av logiska enheter sker automatiskt och kontinuerligt. Så snart ett nytt alternativ sparas i databasen och markeras som godkänt, kan det ingå i uppsättningen med tillgängliga alternativ. När en beslutsregel uppdateras, kommer regeluppsättningen att återskapas och förberedas för körning. I det här automatiska aktiveringssteget utvärderas eventuella begränsningar som definieras av affärslogiken som inte är beroende av körningssammanhanget. Resultaten av aktiveringssteget skickas till en cache där de är tillgängliga för körningsmiljön för beslutstjänsten. Detta illustreras i följande diagram.

![decisioning-API2](./images/decisioning-API2.png)

När alternativet har angetts, regeluppsättningar och begränsningar har aktiverats och flyttats till noderna för beslutstjänsten, används ett enkelt API för att skicka en begäran om ett beslut. API:t anropas vanligtvis av en leveranstjänst som sedan tar det föreslagna alternativet (t.ex. nästa bästa åtgärd eller nästa bästa erbjudande) och sätter ihop upplevelsen eller utför åtgärden. Om erbjudandet är ett erbjudande slås innehållet som representerar det upp och infogas i en upplevelse som skickas till slutanvändaren. Detta illustreras i följande diagram.

![decisioning-API3](./images/decisioning-API3.png)

Delivery Service samlar in data för beslutsbegäran. Det avgör ID:t för den profilentitet som det bästa alternativet avgörs för. Den sammanställer även kontextdata som inte lagras i kundprofilen men som eventuellt används av beslutslogiken.

Beslutslogiken ordnas efter aktiviteter, där var och en anger ett filter för deluppsättningen med alternativ som ska beaktas för den här aktiviteten, tillsammans med ett enda reservalternativ.

Varje beslut fattas genom att först lägga på begränsningar för att minska antalet alternativ och sedan rangordna de återstående alternativen. Även om det mesta av logiken utvärderas i beslutstjänsten används olika tilläggstjänster för att hjälpa till med dessa två aspekter. En capping-tjänst hanterar till exempel övre gränser för hur ofta ett alternativ kan användas i vilket beslut som helst, och en annan tjänst kan vara värd för en maskininlärningsmodell som används för att beräkna poäng för en profil och ett alternativ.

Mer information om hur du använder databas-API:er finns i självstudiekursen [Hantera beslutsenheter och regel med API:er](./tutorials/entities.md)

Mer information om hur du använder körningsmiljön för beslutstjänsten finns i självstudiekursen om hur du [arbetar med körningsmiljön för beslutstjänsten med API:er](./tutorials/runtime.md)