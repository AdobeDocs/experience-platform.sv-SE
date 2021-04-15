---
keywords: Experience Platform;komma igång;kundai;populära ämnen;kundindata;kunddata
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Indata och utdata i kundens AI
topic: Komma igång
description: Läs mer om de händelser, inmatningar och utmatningar som kunden använder.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2867'
ht-degree: 0%

---

# Indata och utdata i kundens AI

I följande dokument beskrivs de olika händelser, indata och utdata som krävs och som används i kundens AI.

## Komma igång

Kundens AI fungerar genom att analysera någon av följande datauppsättningar för att förutsäga bortfall eller konverteringsbenägenhetspoäng:

- CEE-datauppsättning (Consumer Experience Event)
- Adobe Analytics-data med [Analytics-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-data med hjälp av [Audience Manager-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>Källkopplingar tar upp till fyra veckor att fylla i data baklänges. Om du nyligen har konfigurerat en anslutning bör du verifiera att datauppsättningen har den minsta datalängd som krävs för kundens AI. Granska avsnittet [historiska data](#data-requirements) för att verifiera att du har tillräckligt med data för ditt förutsägelsemål.

Det här dokumentet kräver en grundläggande förståelse för CEE-schemat. Läs igenom [dokumentationen för förberedelse av intelligenta tjänster](../data-preparation.md) innan du fortsätter.

I följande tabell beskrivs några vanliga termer som används i det här dokumentet:

| Term | Definition |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Adobe Experience Platform, kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster. |
| XDM-schema | Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data. Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en XDM-basklass och noll eller flera blandningar. |
| XDM, klass | Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende. |
| [Blandningar](../../xdm/schema/composition.md) | En komponent som definierar ett eller flera fält i ett schema. Blandningar styr hur deras fält visas i schemats hierarki och visar därför samma struktur i varje schema som de ingår i. Blandningar är bara kompatibla med specifika klasser, vilket identifieras av deras `meta:intendedToExtend`-attribut. |
| [Datatyp](../../xdm/schema/composition.md) | En komponent som också kan tillhandahålla ett eller flera fält för ett schema. Till skillnad från blandningar begränsas datatyperna inte till en viss klass. Detta gör datatyper till ett mer flexibelt alternativ för att beskriva vanliga datastrukturer som kan återanvändas i flera scheman med potentiellt olika klasser. Datatyperna som beskrivs i det här dokumentet stöds av både CEE- och Adobe Analytics-scheman. |
| Churn | Ett mått på procentandelen konton som avbryter eller väljer att inte förnya sina prenumerationer. Ett högt bortfall kan ha en negativ inverkan på den månatliga återkommande intäkten och kan också visa på missnöje med en produkt eller tjänst. |
| [Kundprofil i realtid](../../profile/home.md) | Kundprofilen i realtid utgör en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som aggregeras över alla system, samt användbara tidsstämplade konton med händelser som involverar den person som har inträffat i något av de system som du använder med Experience Platform. |

## AI-indata för kund

>[!TIP]
>
> Kundens AI avgör automatiskt vilka händelser som är användbara för prognoser och visar en varning om tillgängliga data inte räcker för att generera kvalitetsprognoser.

Kund-AI stöder datauppsättningarna CEE, Adobe Analytics och Adobe Audience Manager. CEE-schemat kräver att du lägger till blandningar när schemat skapas. Om du använder datauppsättningar från Adobe Analytics eller Adobe Audience Manager mappar källkopplingen direkt standardhändelserna (Commerce, webbsidesinformation, Application och Search) som listas nedan under anslutningsprocessen.

Mer information om mappning av Adobe Analytics-data eller Audience Manager-data finns i handboken [Analysfältmappningar](../../sources/connectors/adobe-applications/analytics.md) eller [Audience Manager fältmappningar](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

### Standardhändelser som används av kundens AI {#standard-events}

XDM Experience Events används för att fastställa olika kundbeteenden. Beroende på hur era data är strukturerade kanske händelsetyperna som listas nedan inte omfattar alla kundens beteenden. Det är upp till er att avgöra vilka fält som har de nödvändiga data som behövs för att tydligt och entydigt identifiera webbanvändaraktivitet. Beroende på ditt förutsägelsemål kan de obligatoriska fälten som behövs ändras.

Kundens AI använder olika händelsetyper för att bygga modellfunktioner. Dessa händelsetyper läggs automatiskt till i schemat med hjälp av flera XDM-mixiner.

>[!NOTE]
>
>Om du använder data från Adobe Analytics eller Adobe Audience Manager skapas schemat automatiskt med de standardhändelser som behövs för att hämta in data. Om du skapar ett eget anpassat CEE-schema för att hämta in data måste du tänka på vilka mixiner som behövs för att hämta in data.

Det är inte nödvändigt att ha data för var och en av de standardhändelser som listas nedan, men vissa händelser krävs för vissa scenarier. Om du har tillgång till någon av standardhändelsedatan rekommenderar vi att du inkluderar den i ditt schema. Om du till exempel vill skapa ett kundens AI-program för att förutsäga inköpshändelser kan det vara bra att ha data från datatyperna `Commerce` och `Web page details`.

Om du vill visa en blandning i plattformsgränssnittet väljer du fliken **[!UICONTROL Schemas]** till vänster och väljer sedan fliken **[!UICONTROL Mixins]**.


| Mixa | Händelsetyp | Sökväg till XDM-fält |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | order | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | utcheckningar | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | köp | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpen | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstallations | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | sök | search.keywords |

Dessutom kan kundens AI använda prenumerationsdata för att skapa bättre kundmodeller. Prenumerationsdata krävs för varje profil som använder datatypen [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md). De flesta fälten är valfria för en optimal omsättningsmodell, men vi rekommenderar att du anger data för så många fält som möjligt, till exempel `startDate`, `endDate` och annan relevant information.

### Historiska data {#data-requirements}

Kundens AI kräver historiska data för modellutbildning, men mängden data som krävs baseras på två nyckelelement: resultatfönstret och den berättigade populationen.

Som standard söker AI efter en användare att ha haft aktivitet de senaste 120 dagarna om ingen tillämplig populationsdefinition anges under programkonfigurationen. Dessutom kräver kundens AI minst 500 kvalificerande och 500 icke-kvalificerande händelser (totalt 1 000) av historiska data baserat på en förutsedd måldefinition.

I följande exempel används en enkel formel som hjälper dig att fastställa den minsta mängden data som krävs. Om du har mer än minimikraven är det troligt att modellen ger mer korrekta resultat. Om du har mindre än minimiantalet som krävs kommer modellen att misslyckas eftersom det inte finns tillräckligt med data för modellutbildning.

**Formel**:

Minsta längd på de data som krävs = stödberättigande population + resultatfönster

>[!NOTE]
>
> 30 är det minsta antal dagar som krävs för en stödberättigad population. Om detta inte anges är standardinställningen 120 dagar.

Exempel :

- Ni vill förutsäga om kunden sannolikt kommer att köpa en klocka inom 30 dagar. Du vill även göra poäng för användare som har viss webbaktivitet de senaste 60 dagarna. I det här fallet är den minsta tillåtna längden på de data som krävs = 60 dagar + 30 dagar. Den stödberättigade populationen är 60 dagar och resultatfönstret är 30 dagar, totalt 90 dagar.

- Du vill förutsäga om användaren sannolikt kommer att köpa en klocka inom de kommande 7 dagarna. I det här fallet är den minsta längden på de data som krävs = 120 dagar + 7 dagar. Den giltiga populationen är som standard 120 dagar och resultatfönstret är 7 dagar, totalt 127 dagar.

- Ni vill förutsäga om kunden sannolikt kommer att köpa en klocka inom de kommande 7 dagarna. Du vill även göra poäng för användare som har viss webbaktivitet de senaste 7 dagarna. I det här fallet är den minsta längden på de data som krävs = 30 dagar + 7 dagar. Den stödberättigade populationen kräver minst 30 dagar och resultatfönstret är 7 dagar, totalt 37 dagar.

Förutom de minsta data som krävs fungerar kundens AI också bäst med aktuella data. I det här fallet gör kundens AI en förutsägelse för framtiden baserat på användarens senaste beteendedata. Med andra ord är det troligt att nyare data ger en mer korrekt förutsägelse.

### Exempel på scenarier

I det här avsnittet beskrivs olika scenarier för kundens AI-instanser samt obligatoriska och rekommenderade händelsetyper. Mer information om blandningen och dess fältsökväg finns i [standardhändelsetabellen](#standard-events) ovan.

>[!NOTE]
>
> Nödvändiga händelsetyper används för att tydligt och otvetydigt identifiera webbanvändaraktivitet. Antalet nödvändiga händelsetyper ändras baserat på schemats förutsägelsemål och struktur. Om du är osäker på om en viss händelsetyp behövs bör du ta med den händelsetypen när du skapar ditt CEE-schema. Om du använder data från Adobe Analytics eller Adobe Audience Manager bör de nödvändiga standardhändelserna vara tillgängliga beroende på vilka data du direktuppspelar.

### Scenario 1: Köpkonvertering på en e-handelsplats

**Förutsägelsemål:** Förutspå konverteringsbenägenheten för de profiler som är berättigade att köpa en viss artikel med kläder på en webbplats.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- order
- utcheckningar
- köp
- webVisit
- sök

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 2: Prenumerationskonvertering på en webbplats för direktuppspelande media

**Förutsägelsemål:** Förutspå prenumerationskonverteringsbenägenheten för de berättigade profilerna att binda sig till en viss prenumerationsnivå, till exempel en standard- eller premieplan.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- order
- utcheckningar
- köp
- webVisit
- sök

I det här exemplet används `order`, `checkouts` och `purchases` för att ange att en prenumeration har köpts och dess typ.

För en korrekt modell föreslås dessutom att du använder vissa av de tillgängliga egenskaperna i [prenumerationsdatatypen](../../xdm/data-types/subscription.md).

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 3: Churn på e-handelns webbplats

**Förutsägelsemål:** Förutspå sannolikheten för att en köphändelse inte inträffar.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- order
- utcheckningar
- köp
- webVisit
- sök

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 4: Merförsäljning på en e-handelsplats

**Förutsägelsemål:** Förutspå inköpsbenägenheten för den population som har köpt en viss produkt för att köpa en ny relaterad produkt.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- order
- utcheckningar
- köp
- webVisit
- sök

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 5: Avbeställ en onlineanmälan

**Förutsägelsemål:** Förutspå sannolikheten för att den berättigade populationen avbeställer en tjänst nästa månad.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- webVisit
- sök

För en korrekt modell föreslås dessutom att du använder vissa av de tillgängliga egenskaperna i [prenumerationsdatatypen](../../xdm/data-types/subscription.md).

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 6: Starta mobilprogram

**Förutsägelsemål:** Förutspå benägenheten för berättigade profiler att starta ett betalt mobilprogram inom de kommande X dagarna. Detta liknar prediktion för KPI (Key Performance Indicator) för &quot;Monthly Active Users&quot;.

**Nödvändiga standardhändelsetyper:**

De händelsetyper som listas nedan krävs för optimala kunds-AI-utdata med just detta förutsägelsemål. Det går att utesluta en nödvändig händelse beroende på ditt förväntade mål, men om du utesluter flera händelser kan det leda till dåliga resultat.

- order
- utcheckningar
- köp
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstallations
- applicationLaunches
- applicationUpgrades

I det här exemplet används `order`, `checkouts` och `purchases` när ett mobilprogram behöver köpas.

**Ytterligare rekommenderade standardhändelsetyper:**

Alla återstående [händelsetyper](#standard-events) kan behövas baserat på hur komplext ditt mål är och vilken population som är berättigad när du konfigurerar din kundens AI-instans. Vi rekommenderar att dessa data inkluderas i ditt schema om data är tillgängliga för en viss datatyp.

### Scenario 7: Realiserade egenskaper (Adobe Audience Manager)

**Mål för förutsägelse:** Förutspå benägenheten för vissa egenskaper som ska realiseras.

**Nödvändiga standardhändelsetyper:**

För att kunna använda egenskaper från Adobe Audience Manager måste du skapa en källanslutning med [Audience Manager-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). Källkopplingen skapar automatiskt schemat med rätt blandning. Du behöver inte lägga till ytterligare händelsetyper manuellt för att schemat ska fungera med kundens AI.

När du konfigurerar en ny kund-AI-instans kan `audienceName` och `audienceID` användas för att välja ett visst värde för poängsättningen när du definierar ditt mål.

## Kundens AI-utdata

Kund-AI genererar flera attribut för enskilda profiler som anses berättigade. Det finns två sätt att använda poängen (utdata) baserat på vad du har etablerat. Om du har en kundprofilaktiverad datauppsättning i realtid kan du ta del av insikter från kundprofilen i realtid i [Segment Builder](../../segmentation/ui/segment-builder.md). Om du inte har någon profilaktiverad datauppsättning kan du [hämta kundens AI-utdata](./user-guide/download-scores.md)-datauppsättning som är tillgänglig i datasjön.

>[!NOTE]
>
> Utdatavärden används av kundprofilen i realtid som kan användas för att skapa och definiera segment.

Tabellen nedan beskriver de olika attribut som finns i utdata från kundens AI:

| Attribut | Beskrivning |
| ----- | ----------- |
| Poäng | Den relativa sannolikheten för att en kund ska uppnå det förväntade målet inom den definierade tidsramen. Detta värde ska inte behandlas som sannolikhetsprocent utan snarare som sannolikheten för en individ jämfört med den totala populationen. Poängen varierar mellan 0 och 100. |
| Sannolikhet | Det här attributet är den verkliga sannolikheten för att en profil ska uppnå det förväntade målet inom den definierade tidsramen. När du jämför utdata för olika mål bör du överväga sannolikhet över percentil eller poäng. Sannolikhet bör alltid användas vid bestämning av den genomsnittliga sannolikheten i hela den stödberättigade populationen, eftersom sannolikheten tenderar att vara på den nedre sidan för händelser som inte inträffar ofta. Värden för sannolikhetsintervallet mellan 0 och 1. |
| Procent | Det här värdet ger information om en profils prestanda i förhållande till andra profiler med liknande resultat. En profil med till exempel en percentilrankning på 99 för kurn visar att den har en större risk att kurva jämfört med 99 % av alla andra profiler som bedömdes. Percentiler varierar mellan 1 och 100. |
| Typ av benägenhet | Den valda benägenhetstypen. |
| Resultatdatum | Det datum som poängsättningen inträffade. |
| Influensafaktorer | Förväntade orsaker till varför en profil kan konverteras eller försvinna. Faktorer består av följande attribut:<ul><li>Kod: Profilen eller beteendeattributet som positivt påverkar en profils förväntade poäng. </li><li>Värde: Värdet på profilen eller beteendeattributet.</li><li>Prioritet: Anger hur viktig profilen eller beteendeattributet är för det förväntade poängvärdet (låg, medel, hög)</li></ul> |

## Nästa steg {#next-steps}

När du har förberett dina data och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa guiden [Konfigurera en kundens AI-instans](./user-guide/configure.md). Den här guiden hjälper dig att skapa en instans för kundens AI.
