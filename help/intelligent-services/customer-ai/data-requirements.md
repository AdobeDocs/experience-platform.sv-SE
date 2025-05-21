---
keywords: Experience Platform;komma igång;kundinformation;populära ämnen;kundindata;kunddata;datakrav
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Datakrav för kund-AI
topic-legacy: Getting started
description: Läs mer om de händelser, inmatningar och utmatningar som Kundens AI använder.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2539'
ht-degree: 0%

---


# Indata och utdata i kundens AI

I följande dokument beskrivs de olika händelser, indata och utdata som krävs och som används i kundens AI.

## Komma igång {#getting-started}

Här är stegen för att bygga benägenhetsmodeller och identifiera målgrupper för personaliserad marknadsföring i kundens AI:

1. Användningsexempel: Hur skulle benägenhetsmodeller hjälpa till att identifiera målgrupper för personaliserad marknadsföring? Vilka är mina affärsmål och motsvarande strategier för att uppnå målet? Var kan benägenhetsmodellering passa in i den här processen?

2. Prioritera användningsexempel: Vilka är de högsta prioriteringarna för företaget?

3. Bygg modeller i kundens AI: Titta på den här [snabbsjälvstudiekursen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=sv-SE) och se vår [gränssnittshandbok](../customer-ai/user-guide/configure.md) för en steg-för-steg-process för att skapa en modell.

4. [Skapa segment](../customer-ai/user-guide/create-segment.md) med hjälp av modellresultat.

5. Målinriktade affärsåtgärder baserade på dessa segment. Övervaka resultaten och iterera över åtgärderna för att förbättra dem.

Här är några exempelkonfigurationer för din första modell.  Exemplmodellen, som är inbyggd i det här dokumentet, använder en AI-modell för att förutsäga vem som kan komma att konvertera för en detaljhandelsverksamhet inom de kommande 30 dagarna. Indatauppsättningen är en Adobe Analytics-datauppsättning.

| Steg | Definition | Exempel |
| ---- | ------ | ------- |
| Konfigurera | Ange grundläggande information om modellen. | **Namn**: Förhållandemodell för pennköp <br> **Modelltyp**: Konvertering |
| Välj data | Ange de datauppsättningar som används för att skapa modellen. | **Datauppsättning**: Adobe Analytics-datauppsättning <br> **Identitet**: Kontrollera att identitetskolumnen för varje datauppsättning är inställd på en gemensam identitet. |
| Definiera mål | Definiera mål, berättigad population, anpassade händelser och profilattribut. | **Förutsägelsemål**: Markera `commerce.purchases.value` är lika med penna <br> **Resultatfönster**: 30 dagar. |
| Ange alternativ | Ställ in schemat för modelluppdatering och aktivera bakgrundsmusik för profil | **Schema**: Varje vecka <br> **Aktivera för profilen**: Detta måste aktiveras för att modellutdata ska kunna användas i segmentering. |

## Dataöversikt {#data-overview}

I följande avsnitt beskrivs de olika händelser, indata och utdata som krävs och som används i kundens AI.

Kundens AI fungerar genom att analysera följande datauppsättningar för att förutsäga bortfall (när en kund sannolikt kommer att sluta använda produkten) eller konvertering (när en kund sannolikt kommer att göra ett köp).

- Adobe Analytics-data med [Analytics-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-data med [Audience Manager-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Experience Event, datamängd](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=sv-SE)
- [Data för kundupplevelsehändelser](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html?lang=sv-SE#cee-schema)

Du kan lägga till flera datauppsättningar från olika källor om varje datauppsättning har samma identitetstyp (namnutrymme), till exempel ett ECID. Mer information om hur du lägger till flera datauppsättningar finns i användarhandboken för [Kund-AI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Source-kontakter tar upp till fyra veckor att fylla i data baklänges. Om du nyligen har konfigurerat en anslutning bör du verifiera att datauppsättningen har den minsta datalängd som krävs för kundens AI. Granska avsnittet [historiska data](#data-requirements) för att verifiera att du har tillräckligt med data för ditt förutsägelsemål.

I följande tabell beskrivs några vanliga termer som används i det här dokumentet:

| Villkor | Definition |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Adobe Experience Platform, kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Experience Platform använder XDM System för att organisera data på ett visst sätt som gör det enklare att använda för Experience Platform tjänster. |
| [XDM-schema](../../xdm/schema/composition.md) | Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data. Innan data kan hämtas in till Experience Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en XDM-basklass och noll eller flera schemafältgrupper. |
| [XDM-klass](../../xdm/schema/field-constraints.md) | Alla XDM-scheman beskriver data som kan kategoriseras som `Experience Event`. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende. |
| [Fältgrupper](../../xdm/schema/composition.md) | En komponent som definierar ett eller flera fält i ett schema. Fältgrupper styr hur deras fält visas i schemats hierarki och visar därför samma struktur i varje schema som de ingår i. Fältgrupper är bara kompatibla med specifika klasser, vilket identifieras av deras `meta:intendedToExtend`-attribut. |
| [Datatyp](../../xdm/schema/composition.md) | En komponent som också kan tillhandahålla ett eller flera fält för ett schema. Till skillnad från fältgrupper är datatyperna dock inte begränsade till en viss klass. Detta gör datatyper till ett mer flexibelt alternativ för att beskriva vanliga datastrukturer som kan återanvändas i flera scheman med potentiellt olika klasser. Datatyperna som beskrivs i det här dokumentet stöds av både CEE- och Adobe Analytics-scheman. |
| [Kundprofil i realtid](../../profile/home.md) | Kundprofilen i realtid utgör en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som aggregeras över alla system, samt användbara tidsstämplade konton med händelser som involverar den person som har inträffat i något av de system som du använder med Experience Platform. |

## AI-indata för kund {#customer-ai-input-data}

För indatauppsättningar, som Adobe Analytics och Adobe Audience Manager, mappas händelser direkt i de här standardfältgrupperna (Commerce, Web, Application och Search) som standard under anslutningsprocessen. Tabellen nedan visar händelsefälten i standardfältgrupperna för kund-AI.

Mer information om mappning av Adobe Analytics-data eller Audience Manager-data finns i Analytics-fältmappningar eller i Audience Manager [handbok för fältmappningar](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Du kan använda Experience Event- eller Consumer Experience Event XDM-scheman för indatamängder som inte fylls i via någon av de ovanstående anslutningarna. Ytterligare XDM-fältgrupper kan läggas till när schemat skapas. Fältgrupperna kan tillhandahållas av Adobe, t.ex. standardfältgrupperna eller en anpassad fältgrupp, som matchar datarepresentationen i Experience Platform.

>[!IMPORTANT]
>
>Du måste se till att data fylls i i dessa indatamängder. Om inga händelser från standardfältgrupper hittas i indatauppsättningarna måste du lägga till anpassade händelser under konfigurationsarbetsflödet. Se information om anpassade händelser.

### Standardfältgrupper som används av kundens AI {#standard-events}

Experience Events används för att fastställa olika kundbeteenden. Beroende på hur era data är strukturerade kanske händelsetyperna som listas nedan inte omfattar alla kundens beteenden. Det är upp till er att avgöra vilka fält som har de data som behövs för att tydligt och entydigt identifiera webb- eller annan kanalspecifik användaraktivitet. Beroende på ditt förutsägelsemål kan de obligatoriska fälten som behövs ändras.

>[!NOTE]
>
>Om du använder data från Adobe Analytics eller Adobe Audience Manager skapas schemat automatiskt med de standardhändelser som behövs för att hämta in data. Om du skapar ett eget anpassat EE-schema för att samla in data måste du tänka på vilka fältgrupper som behövs för att hämta in data.

Kund-AI använder händelserna i dessa fyra standardfältgrupper som standard: Commerce, Web, Application och Search. Det är inte nödvändigt att ha data för varje händelse i de standardfältgrupper som anges nedan, men vissa händelser krävs för vissa scenarier. Om du har några händelser i standardfältgrupperna tillgängliga rekommenderar vi att du inkluderar dem i ditt schema. Om du till exempel vill skapa en AI-modell för kunder för att förutsäga köphändelser, kan det vara bra att ha data från fältgrupperna för Commerce och webbsidesinformation.

Om du vill visa en fältgrupp i Experience Platform-gränssnittet väljer du fliken **[!UICONTROL Schemas]** till vänster och sedan fliken **[!UICONTROL Field groups]**.

| Fältgrupp | Händelsetyp | Sökväg till XDM-fält |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | beställa | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | utcheckningar | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | köp | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpen | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web Details] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Application Details] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstallations | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Search Details] | sök | `search.keywords` |

Dessutom kan kundens AI använda prenumerationsdata för att skapa bättre kundmodeller. Prenumerationsdata krävs för varje profil som använder datatypen [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md). De flesta fälten är valfria, men för en optimal omsättningsmodell rekommenderar vi att du anger data för så många fält som möjligt, till exempel `startDate`, `endDate` och andra relevanta uppgifter. Kontakta ditt kontoteam om du vill ha ytterligare support för den här funktionen.

### Lägga till anpassade händelser och profilattribut {#add-custom-events}

Om du har information som du vill inkludera utöver standardhändelsefälten [&#128279;](#standard-events)som används av kundens AI, kan du använda den [anpassade händelsekonfigurationen](./user-guide/configure.md#custom-events) för att förstärka de data som används av modellen.

#### När anpassade händelser ska användas

Anpassade händelser är nödvändiga när de datauppsättningar som valts i datauppsättningsurvalssteget innehåller *ingen* av standardhändelsefälten som används av kundens AI. Kundens AI behöver information om minst en annan användarbeteendehändelse än resultatet.

Anpassade händelser är användbara för:

- Införliva domänkunskap eller tidigare expertis i modellen.

- Förbättra den prediktiva modellens kvalitet.

- Få ytterligare insikter och tolkningar.

De bästa kandidaterna för anpassade händelser är data som innehåller domänkunskap som kan vara prediktiv för resultatet. Exempel på anpassade händelser är:

- Registrera dig för konto

- Prenumerera på nyhetsbrevet

- Ring kundtjänst

Här följer ett urval av branschspecifika exempel på anpassade evenemang:

| Bransch | Anpassade händelser |
| --- | --- |
| Detaljhandel | Butikstransaktion<br>Registrera dig för klubbkort<br>Mobilkupong för klipp. |
| Underhållning | Video om direktuppspelning för <br>-köpsäsong. |
| Hospitalitet | Gör restaurangreservation <br> Köp förmånspoäng. |
| Resa | Lägg till känd resandeinfo Inköpsavtal. |
| Kommunikation | Uppgradera/nedgradera/avbryt plan. |

Anpassade händelser måste representera användarinitierade åtgärder för att kunna väljas. &quot;Skicka med e-post&quot; är till exempel en åtgärd som initieras av en marknadsförare och inte av användaren, så den bör inte användas som en anpassad händelse.

### Historiska data

Kunds-AI kräver historiska data för modellutbildning. Den varaktighet som krävs för att data ska finnas i systemet bestäms av två nyckelelement: resultatfönstret och den berättigade populationen.

Som standard söker AI efter en användare att ha haft aktivitet de senaste 45 dagarna om ingen tillämplig populationsdefinition anges under programkonfigurationen. Dessutom kräver kundens AI minst 500 kvalificerande och 500 icke-kvalificerande händelser (totalt 1 000) från historiska data baserat på en förutsedd måldefinition.

I följande exempel visas hur du använder en enkel formel som hjälper dig att fastställa den minsta mängden data som krävs. Om du har fler data än minimikraven är det troligt att modellen ger mer korrekta resultat. Om du har mindre än minimiantalet som krävs kommer modellen att misslyckas eftersom det inte finns tillräckligt med data för modellutbildning.

Kundens AI använder en överlevnadsmodell för att uppskatta sannolikheten för en händelse som inträffar vid en viss tidpunkt och identifiera påverkande faktorer, tillsammans med övervakad inlärning som definierar positiva och negativa populationer, och beslutsbaserade träd som `lightgbm` för att generera ett sannolikhetsresultat.

**Formel**:

Så här avgör du den minsta tid som krävs för data som finns i systemet:

- Minimikravet för att skapa funktioner är 30 dagar. Jämför uppgraderingsfönstret med 30 dagar:

   - Om behörighetsuppslagsfönstret är längre än 30 dagar är datakravet = behörighetsuppslagsfönstret + resultatfönstret.

   - I annat fall är datakravet 30 dagar + resultatfönstret.

** Om det finns fler än ett villkor för att definiera den berättigade populationen är uppföljningsfönstret längst.

>[!NOTE]
>
>30 är det minsta antal dagar som krävs för en stödberättigad population. Om detta inte anges är standardinställningen 45 dagar.

**Exempel**:

- Ni vill förutsäga om en kund sannolikt kommer att köpa en klocka inom 30 dagar för dem som har webbaktivitet de senaste 60 dagarna.

   - Rätt till uppgraderingssökning = 60 dagar

   - Resultatfönster = 30 dagar

   - Obligatoriska data = 60 dagar + 30 dagar = 90 dagar

- Du vill förutsäga om användaren sannolikt kommer att köpa en klocka inom de kommande 7 dagarna **utan att** tillhandahåller en explicit kvalificerad population. I det här fallet är den stödberättigade populationen som standard&quot;de som har haft aktivitet de senaste 45 dagarna&quot; och resultatfönstret är 7 dagar.

   - Rätt till uppgraderingssökning = 45 dagar

   - Resultatfönster = 7 dagar

   - Obligatoriska data = 45 dagar + 7 dagar = 52 dagar

- Ni vill förutsäga om kunden sannolikt kommer att köpa en klocka inom 7 dagar för dem som har webbaktivitet de senaste 7 dagarna.

   - Rätt till uppgraderingssökning = 7 dagar

   - Lägsta antal data som krävs för att skapa funktioner = 30 dagar

   - Resultatfönster = 7 dagar

   - Obligatoriska data = 30 dagar + 7 dagar = 37 dagar

Även om Kundens AI kräver en viss tid för att data ska finnas i systemet fungerar det också bäst med aktuella data. Genom att använda nyare beteendedata är det troligt att kundens AI ger en mer korrekt uppskattning av en användares framtida beteende.

## Kundens AI-utdata {#customer-ai-output-data}

Kund-AI genererar flera attribut för enskilda profiler som anses berättigade. Det finns två sätt att förbruka poängen (utdata) baserat på vad du har etablerat. Om du har en kundprofilaktiverad datauppsättning i realtid kan du ta del av insikter från kundprofilen i realtid i [segmentbyggaren](../../segmentation/ui/segment-builder.md). Om du inte har någon profilaktiverad datauppsättning kan du [hämta kundens AI-datauppsättning](./user-guide/download-scores.md) som finns tillgänglig i datasjön.

Du kan hitta utdatauppsättningen på arbetsytan för Experience Platform **datauppsättningar**. Alla AI-utdatauppsättningar för kunder börjar med namnet **AI-poäng för kund - NAME_OF_APP**. På samma sätt börjar alla kundens AI-utdatascheman med namnet **kundens AI-schema - appens_namn**.

![Namnkonventionen för utdata i kundens AI.](./images/user-guide/cai-schema-name-of-app.png)

Tabellen nedan beskriver de olika attribut som finns i utdata från kundens AI:

| Attribut | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Score] | Den relativa sannolikheten för att en kund ska uppnå det förväntade målet inom den definierade tidsramen. Detta värde ska inte behandlas som sannolikhetsprocent utan snarare som sannolikheten för en individ jämfört med den totala populationen. Poängen varierar mellan 0 och 100. |
| Sannolikhet | Det här attributet är den verkliga sannolikheten för att en profil ska uppnå det förväntade målet inom den definierade tidsramen. När du jämför utdata för olika mål bör du överväga sannolikhet över percentil eller poäng. Sannolikhet bör alltid användas vid bestämning av den genomsnittliga sannolikheten i hela den stödberättigade populationen, eftersom sannolikheten tenderar att vara på den nedre sidan för händelser som inte inträffar ofta. Värden för sannolikhetsintervallet mellan 0 och 1. |
| Procent | Det här värdet ger information om en profils prestanda i förhållande till andra profiler med liknande resultat. En profil med en percentilrankning på 99 för kurn visar till exempel att den har en större risk att kurva jämfört med 99 % av alla andra profiler som bedömdes. Proportionerna varierar mellan 1 och 100. |
| Typ av benägenhet | Den valda benägenhetstypen. |
| Resultatdatum | Det datum som poängsättningen inträffade. |
| Influensafaktorer | Detta är förutsedda orsaker till varför en profil kan konverteras eller försvinna. Dessa faktorer består av följande attribut:<ul><li>Kod: Profilen eller beteendeattributet som positivt påverkar en profils förväntade poäng. </li><li>Värde: Värdet för profilen eller beteendeattributet.</li><li>Viktigt: Anger hur viktig profilen eller beteendeattributet är för det förväntade poängvärdet (low, medium, high)</li></ul> |

## Nästa steg {#next-steps}

När du har förberett dina data och sett till att alla dina autentiseringsuppgifter och scheman finns på plats, se [Konfigurera en AI-instans](./user-guide/configure.md) som vägleder dig genom en stegvis självstudiekurs för att skapa en AI-instans för kunder.