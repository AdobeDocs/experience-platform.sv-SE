---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Användargränssnittsguide för segmentbyggare
topic: ui guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Användarhandbok för Segment Builder

Adobe Experience Platform Segmentation Service tillhandahåller ett RESTful API och användargränssnitt för att skapa segmentdefinitioner utifrån kundprofildata i realtid.

## Komma igång

Att arbeta med segmentdefinitioner kräver förståelse för de olika Experience Platform-tjänsterna som är involverade i segmenteringen. Innan du läser den här användarhandboken bör du läsa dokumentationen för följande tjänster:

- [Segmenteringstjänst](../home.md): Med segmenteringstjänsten kan ni dela upp data som lagras i Experience Platform och som rör enskilda personer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper som delar liknande egenskaper och som kommer att svara på marknadsstrategier.
- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Identitetstjänst](../../identity-service/home.md): Möjliggör kundprofil i realtid genom att överbrygga identiteter från olika datakällor som hämtas in till Platform.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

Det är också viktigt att känna till två nyckeltermer som används i det här dokumentet och förstå skillnaden mellan dem:
- **Segmentdefinition**: Den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden för en målgrupp.
- **Målgrupp**: Den resulterande uppsättningen profiler som uppfyller villkoren för en segmentdefinition.

## Åtkomst till segmentdefinitioner

Om du vill börja arbeta med segmentdefinitioner i Adobe Experience Platform klickar du på **Segment** i den vänstra navigeringen. Om du vill visa alla segmentdefinitioner för din organisation klickar du på fliken *Bläddra* . I den här vyn visas information om segmentdefinitionen, inklusive utvärderingsmetod, skapad den och senaste ändringsdatum.

Utvärderingsmetoden kan antingen vara direktuppspelning eller batch. Direktuppspelningssegment utvärderas ständigt när data kommer in i systemet. Gruppsegmenten utvärderas enligt ett angivet schema.

Gruppsegmenten har ytterligare information som visas, både det senaste utvärderingsdatumet och nästa utvärderingsdatum för gruppen.

Om du klickar på **Skapa segment** i det övre högra hörnet öppnas arbetsytan i Segment Builder, där du kan börja skapa en segmentdefinition.

![](../images/segment-builder/segment-browse.png)

## Arbetsytan Segment Builder

I Segment Builder finns en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.

![](../images/segment-builder/segment-builder.png)

## Byggstenar för segmentdefinitioner

De grundläggande byggstenarna för segmentdefinitioner är **Attribut** och **Händelser**. Dessutom kan de attribut och händelser som finns i befintliga **målgrupper** också användas som komponenter för nya definitioner.

Dessa byggstenar visas i avsnittet *Fält* till vänster på arbetsytan i Segment Builder. *Fälten* innehåller en flik för varje huvudbyggsten: **Attribut**, **Händelser** och **Publiker**.

![](../images/segment-builder/segment-fields.png)

### Attribut

På fliken **Attribut** kan du bläddra bland profilattribut som tillhör klassen XDM Individual Profile. Varje mapp kan expanderas för att visa ytterligare attribut, där varje attribut är en platta som kan dras till regelbyggararbetsytan i mitten av arbetsytan. Arbetsytan för [regelbyggaren](#rule-builder-canvas) beskrivs mer ingående senare i den här guiden.

![](../images/segment-builder/attributes.png)

### Händelser

På fliken **Händelser** kan du skapa en målgrupp baserat på händelser eller åtgärder som har utförts med hjälp av XDM ExperienceEvent-dataelement. Du hittar också Händelsetyper på fliken **Händelser** , som är en samling vanliga händelser som gör att du kan skapa segment snabbare.

Förutom att du kan bläddra efter ExperienceEvent-element kan du även söka efter händelsetyper. Händelsetyper använder samma kodningslogik som ExperienceEvents, utan att du behöver söka igenom klassen XDM ExperienceEvent och leta efter rätt händelse. Om du till exempel använder sökfältet för att söka efter kundvagn returneras händelsetyperna AddCart och RemoveCart, som är två mycket vanliga kundvagnsåtgärder när du skapar segmentdefinitioner.

Du kan söka efter alla typer av komponenter genom att skriva deras namn i sökfältet, som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Sökresultaten fylls i när hela ord anges. Om du till exempel vill skapa en regel som baseras på XDM-fältet `ExperienceEvent.commerce.productViews`börjar du skriva&quot;produktvyer&quot; i sökfältet. När ordet &quot;product&quot; har skrivits in börjar sökresultaten visas. Varje resultat innehåller den objekthierarki som det hör till.

>[!NOTE] Det kan ta upp till 24 timmar innan anpassade schemafält som definieras av organisationen visas och blir tillgängliga för användning i byggregler.

Sedan kan du enkelt dra och släppa ExperienceEvents och Event Types i din segmentdefinition.

![](../images/segment-builder/events-eventTypes.png)

Som standard visas endast ifyllda schemafält från ditt datalager. Detta inkluderar händelsetyper. Om listan Händelsetyper inte visas, eller om du bara kan välja Valfri som händelsetyp, klickar du på kugghjulsikonen bredvid *Fält* och väljer sedan **Visa fullständigt XDM-schema** under *Tillgängliga fält*. Klicka på kugghjulsikonen igen för att gå tillbaka till fliken *Fält* och du bör nu kunna visa flera händelsetyper och schemafält, oavsett om de innehåller data eller inte.

![](../images/segment-builder/show-populated.png)

### Målgrupper

På fliken **Publiker** visas alla målgrupper som importerats från externa källor, till exempel Adobe Audience Manager, samt målgrupper som skapats i Experience Platform.

På fliken Publiker kan du se alla tillgängliga källor som en grupp med mappar. När du klickar in i dessa mappar visas tillgängliga undermappar och målgrupper. Dessutom kan du klicka på mappikonen (som visas längst till höger) för att visa mappstrukturen (en bock anger den mapp du befinner dig i) och enkelt navigera tillbaka genom mapparna genom att klicka på namnet på en mapp i trädet.

Du kan hovra över ⓘ bredvid en målgrupp för att visa information om målgruppen, inklusive dess ID, beskrivning och mapphierarkin för att hitta målgruppen.

![](../images/segment-builder/audience-folder-structure.png)

Du kan också söka efter målgrupper med sökfältet, som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om du väljer en mapp på den översta nivån på fliken *Publiker* visas sökfältet så att du kan söka i den mappen. Sökresultaten fylls bara i när hela ord anges. Om du till exempel vill hitta en publik med namnet `Online Shoppers`börjar du skriva &quot;Online&quot; i sökfältet. När ordet &quot;Online&quot; har skrivits in fullständigt visas sökresultat som innehåller ordet &quot;Online&quot;.

## Regelbyggarens arbetsyta

En segmentdefinition är en samling regler som används för att beskriva viktiga egenskaper eller beteenden hos en målgrupp. Dessa regler skapas med *regelbyggarens arbetsyta*, som finns i mitten av Segment Builder.

Om du vill lägga till en ny regel i segmentdefinitionen drar du en ruta från fliken *Fält* och släpper den på regelbyggarens arbetsyta. Därefter visas sammanhangsspecifika alternativ beroende på vilken typ av data som läggs till. Tillgängliga datatyper: strängar, datum, ExperienceEvents, händelsetyper och Publiker.

![](../images/segment-builder/rule-builder-canvas.png)

### Lägga till målgrupper

Du kan dra och släppa en målgrupp från fliken *Målgrupp* till regelbyggararbetsytan för att referera till målgruppsmedlemskap i den nya segmentdefinitionen. På så sätt kan du inkludera eller exkludera målgruppsmedlemskap som ett attribut i den nya segmentregeln.

För plattformsmålgrupper som skapats med Segment Builder får ni möjligheten att konvertera målgruppen till den uppsättning regler som användes i segmentdefinitionen för den målgruppen. Den här konverteringen skapar en kopia av regellogiken som sedan kan ändras utan att den ursprungliga segmentdefinitionen påverkas.

>[!NOTE] När du lägger till en målgrupp från en extern källa refereras endast målgruppsmedlemskapet. Du kan inte konvertera målgruppen till regler, och därför kan reglerna som används för att skapa den ursprungliga målgruppen inte ändras i den nya segmentdefinitionen.

![](../images/segment-builder/add-audience-to-segment.png)

## Behållare

Segmentregler utvärderas i den ordning som de listas. Behållare ger kontroll över körningsordningen med hjälp av kapslade frågor.

När du har lagt till minst en platta på regelbyggararbetsytan kan du börja lägga till behållare. Om du vill skapa en ny behållare klickar du på ellipserna (..) i rutans övre högra hörn och klickar sedan på **Lägg till behållare**.

![](../images/segment-builder/add-container.png)

En ny behållare visas som underordnad till den första behållaren, men du kan justera hierarkin genom att dra och flytta behållarna. Standardbeteendet för en behållare är att&quot;Inkludera&quot; det angivna attributet, händelsen eller målgruppen. Du kan ställa in regeln på&quot;Uteslut&quot;-profiler som matchar behållarvillkoren genom att klicka på **Inkludera** i rutans övre vänstra hörn och välja&quot;Uteslut&quot;.

En underordnad behållare kan också extraheras och läggas till i den överordnade behållaren genom att klicka på Bryt upp behållare i den underordnade behållaren. Klicka på ellipserna (..) i det övre högra hörnet av den underordnade behållaren för att komma åt det här alternativet.

![](../images/segment-builder/include-exclude.png)

När du klickar på **Dela upp behållare** tas den underordnade behållaren bort och villkoren visas textbundna.

>[!NOTE] När du delar upp behållare ska du se till att logiken fortsätter att uppfylla den önskade segmentdefinitionen.

![](../images/segment-builder/unwrapped-container-inline.png)

## Sammanfoga profiler

Med Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som används av Platform för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en profil.

Du kan välja en sammanfogningsprincip som matchar ditt marknadsföringssyfte för den här målgruppen eller använda standardprincipen för sammanfogning som tillhandahålls av Platform. Du kan skapa flera sammanfogningsprinciper som är unika för din organisation, inklusive skapa en egen standardsammanfogningsprincip. Stegvisa instruktioner om hur du skapar sammanfogningspolicyer för din organisation finns i självstudiekursen om hur du [arbetar med sammanfogningspolicyer med användargränssnittet](../../profile/ui/merge-policies.md).

Om du vill välja en sammanfogningsprincip för segmentdefinitionen klickar du på kugghjulsikonen på fliken *Fält* och använder sedan listrutan ** Sammanfogningsprincip för att välja den sammanfogningsprincip som du vill använda.

![](../images/segment-builder/merge-policy-selector.png)

## Segmentegenskaper

När du skapar en segmentdefinition visar avsnittet *Segmentegenskaper* till höger om arbetsytan en uppskattning av storleken på det segment som skapas, så att du kan justera segmentdefinitionen efter behov innan du skapar själva målgruppen.

I avsnittet *Segmentegenskaper* kan du även ange viktig information om segmentdefinitionen, inklusive dess *namn* och *beskrivning*. Segmentdefinitionsnamn används för att identifiera ditt segment bland dem som definieras av organisationen och bör därför vara beskrivande, koncisa och unika.

När du fortsätter att skapa en segmentdefinition kan du visa en sidnumrerad förhandsvisning av målgruppen genom att välja **Visa profiler**.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] Målgruppsuppskattningar genereras med en provstorlek för den aktuella dagens exempeldata. Om det finns mindre än 1 miljon enheter i din profilbutik används hela datauppsättningen. För mellan 1 och 20 miljoner enheter används 1 miljon enheter. och för över 20 miljoner enheter används 5 % av det totala antalet enheter. Mer information om hur du genererar segmentuppskattningar finns i avsnittet [för att generera](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) uppskattningar i självstudiekursen för att skapa segment.

## Aktivera schemalagd segmentering

När segmentdefinitionerna har skapats kan du utvärdera dem vid behov eller genom en schemalagd (kontinuerlig) utvärdering. Utvärdering innebär att flytta kundprofildata i realtid genom segmentdefinitioner för att producera motsvarande målgrupper. När målgrupperna har skapats sparas och lagras de så att de kan exporteras med Experience Platform API:er.

I On-demand-utvärderingen ingår att använda API:t för att utvärdera och bygga målgrupper efter behov, medan schemalagd utvärdering (även kallat schemalagd segmentering) gör att du kan skapa ett återkommande schema för att utvärdera segmentdefinitioner vid en viss tidpunkt (högst en gång om dagen).

Du kan aktivera dina segmentdefinitioner för schemalagd utvärdering med hjälp av gränssnittet eller API:t. Gå tillbaka till fliken *Bläddra* i **Segment** i användargränssnittet och aktivera **Utvärdera alla segment**. Detta gör att alla segment utvärderas baserat på det schema som angetts av organisationen.

>[!NOTE] Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för den enskilda XDM-profilen. Om din organisation har fler än fem sammanfogningsprinciper för den enskilda XDM-profilen i en enda sandlådemiljö, kommer du inte att kunna använda schemalagd utvärdering.

Scheman kan för närvarande bara skapas med API:t. Detaljerade anvisningar om hur du skapar, redigerar och arbetar med scheman med API:t finns i självstudiekursen för utvärdering och åtkomst av segmentresultat, särskilt avsnittet om [schemalagd utvärdering med API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Aktivera direktuppspelningssegmentering

>[!NOTE] Direktuppspelningssegmentering är en betafunktion som är tillgänglig på begäran.

Dessutom kan en segmentdefinition aktiveras för direktuppspelningssegmentering före eller efter det att den har skapats. Direktuppspelningssegmentering utvärderar omedelbart en kund så snart en händelse kommer in i en viss segmentgrupp. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till plattformen, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs. Mer information om direktuppspelningssegmentering finns i dokumentationen [för](../api/streaming-segmentation.md)direktuppspelningssegmentering.

Du kan aktivera segmentdefinitioner för direktuppspelning med gränssnittet eller API:t. Om du vill aktivera en ny eller befintlig segmentdefinition för direktuppspelning i användargränssnittet måste du växla alternativet *Direktuppspelning* till **PÅ**.

![](../images/segment-builder/enable-streaming-segmentation.png)

När direktuppspelningssegmenteringen har aktiverats måste en baslinje upprättas (detta är den första körningen efter vilken segmentet alltid är uppdaterat). Systemet hanterar baselering automatiskt, men detta är bara möjligt om schemalagd segmentering har aktiverats. Mer information om hur du aktiverar schemalagd segmentering finns [i föregående avsnitt i den här användarhandboken](#enable-scheduled-segmentation).

## Nästa steg

Segment Builder har ett omfattande arbetsflöde som gör det möjligt att isolera marknadsmässiga målgrupper från kundprofildata i realtid. När du har läst den här guiden bör du nu kunna:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använd regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmentreglerna körs.
- Visa uppskattningar av er presumtiva målgrupp, så att ni kan justera era segmentdefinitioner efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktivera angivna segmentdefinitioner för direktuppspelningssegmentering.

Stegvisa anvisningar om hur du arbetar med segmenteringstjänsten med kundprofils-API:t i realtid finns i [skapa målgruppssegment med hjälp av API:er](../tutorials/create-a-segment.md) .