---
keywords: Experience Platform;user guide;customer ai;popular topics
solution: Experience Platform
title: Användarhandbok för AI
topic: User guide
translation-type: tm+mt
source-git-commit: 7987cec12c22e9b48ddc9fdc263d7cd28bd172f2

---


# Användarhandbok för AI

Tack vare kundens AI, som ingår i Intelligent Services, kan ni generera anpassade benägenhetspoäng utan att behöva bekymra er om maskininlärning.

Den här guiden innehåller steg för arbetet med kundens AI. Steg finns för följande ämnen:

* [Konfigurera en instans](#configure-an-instance)
* [Skapa kundsegment med förutbestämda poäng](#create-customer-segments-with-predicted-scores)

Dessutom innehåller bilagan till den här självstudiekursen information om [utdata för kundens AI](#customer-ai-output-data).

## Konfigurera en instans

Intelligenta tjänster ger kunden artificiell intelligens (AI) som en lättanvänd Adobe Sensei-tjänst som kan konfigureras för olika användningsområden. I följande avsnitt beskrivs hur du konfigurerar en instans av Kundens AI.

### Konfigurera din instans

Klicka på **Tjänster** i den vänstra navigeringen i plattformsgränssnittet. Webbläsaren **Services** visas och visar alla tillgängliga tjänster. Klicka på **Öppna** i behållaren för kundens AI.

![](./images/user-guide/navigate-to-service.png)

På *kundens AI* -skärm visas alla befintliga AI-instanser för kunder. Klicka på **Skapa instans**.

![](./images/user-guide/dashboard.png)

Arbetsflödet för att skapa instanser visas med början i *steget Konfigurera* .

Nedan finns viktig information om värden som du måste ge instansen:

* Instansens namn används på alla platser där kundens AI-poäng visas. Namnen bör därför beskriva vad förutsägelsepoängen representerar, till exempel&quot;Sannolikhet för att avbryta tidskriftsprenumeration&quot;.

* Propensitetstypen bestämmer poängsättets och den metriska polaritetens avsikt. Du kan antingen välja **Churn** eller **Conversion**. Se anteckningen under [poängsammanfattning](./discover-insights.md#scoring-summary) i dokumentet om upptäckt av insikter för mer information om hur benägenhetstypen påverkar din instans.

* Datakällan är den plats där data finns. Datauppsättningen är den indatamängd som används för att förutsäga bakgrundsmusik. Kunds-AI använder per design data om kundupplevelsehändelser för att beräkna benägenhetspoängen. När du väljer en datauppsättning i listruteväljaren visas bara de som är kompatibla med kundens AI.

* Som standard genereras benägenhetspoäng för alla profiler såvida inte en stödberättigad population anges. Du kan ange en berättigad population genom att definiera villkor för att inkludera eller exkludera profiler baserat på händelser.

Ange önskade värden och klicka sedan på **Nästa**.

![](./images/user-guide/setup.png)

### Definiera ett mål

Steget *Definiera mål* visas och innehåller en interaktiv miljö där du kan definiera ett mål visuellt. Ett mål består av en eller flera händelser, där varje händelses förekomst baseras på det villkor den innehåller. Målet för en kundens AI-instans är att fastställa sannolikheten för att uppnå dess mål inom en viss tidsram.

Klicka på **Ange fältnamn** och välj ett fält i listrutan. Klicka på den andra inmatningen och välj en sats för händelsens villkor och ange sedan ett målvärde för att slutföra händelsen. Ytterligare händelser kan konfigureras genom att klicka på **Lägg till händelse**. Slutför målet genom att tillämpa en tidsram för förutsägelse i antal dagar och klicka sedan på **Nästa**.

![](./images/user-guide/goal.png)

### Konfigurera ett schema *(valfritt)*

Det *avancerade* steget visas. Med det här valfria steget kan du konfigurera ett schema för att automatisera prediktionskörningar, definiera undantag för förutsägelser för att filtrera vissa händelser eller klicka på **Slutför** om inget behövs.

Konfigurera ett poängschema genom att konfigurera *poängfrekvensen*. Automatiserade prognoskörningar kan schemaläggas att köras antingen varje vecka eller varje månad.

![](./images/user-guide/schedule.png)

Under schemakonfigurationen kan du definiera undantag för förutsägelse för att förhindra händelser som uppfyller vissa villkor från att utvärderas när du genererar poäng. Den här funktionen kan användas för att filtrera bort irrelevanta dataindata.

Om du vill utesluta vissa händelser klickar du på **Lägg till undantag** och definierar händelsen på samma sätt som målet definieras. Om du vill ta bort ett undantag klickar du på ellipserna (**..**) längst upp till höger i händelsebehållaren och sedan på **Ta bort behållare**.

![](./images/user-guide/exclusion.png)

Uteslut händelser efter behov och klicka sedan på **Slutför** för att skapa instansen.

![](./images/user-guide/advanced.png)

Om instansen skapas utan fel utlöses en förutsägelsekörning omedelbart och efterföljande körningar utförs enligt ditt definierade schema.

>[!NOTE] Beroende på storleken på indata kan det ta upp till 24 timmar att slutföra förutsägelser.

Genom att följa det här avsnittet har du konfigurerat en instans av Kundens AI och en förutsägelsekörning utfördes. När körningen är klar fyller poängsatta insikter automatiskt i profiler med förutbestämda poäng. Vänta i upp till 24 timmar innan du fortsätter till nästa avsnitt i den här självstudiekursen.

## Skapa kundsegment med förutbestämda poäng

När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget. En mer robust självstudiekurs om hur du skapar segment finns i användarhandboken för [Segment Builder](../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Om du vill använda den här metoden måste kundprofilen i realtid aktiveras för datauppsättningen.

Klicka på **Segment** i den vänstra navigeringen i plattformsgränssnittet och klicka sedan på **Skapa segment**.

![](./images/user-guide/segments.png)

Segmentbyggaren ** visas. Klicka på mappen *XDM Individual Profile* i den vänstra kolumnen *Fält* och under fliken **Attribut** och klicka sedan på mappen med organisationens namnområde. Mappen med namnet **Customer AI** innehåller resultatet av prediktionskörningar och namnges efter den instans poängen tillhör. Klicka på en instansmapp för att komma åt resultatet av den önskade instansen.

![](./images/user-guide/results.png)

Placerad i mitten av Segment Builder, dra och släpp attributet **Score** på *regelbyggarens arbetsyta* för att definiera en regel.

Ange ett namn för segmentet under den högra kolumnen *Segmentegenskaper* .

![](./images/user-guide/properties.png)

Ovanför kolumnen med *fält* till vänster klickar du på **kugghjulsikonen** och väljer en **kopplingsprincip**. Klicka på **Spara** för att skapa segmentet.

![](./images/user-guide/merge_policy.png)

## Nästa steg

Genom att följa den här självstudiekursen har du konfigurerat en instans av kundens AI, genererat benägenhetspoäng och hittat målgrupper baserat på deras benägenhetspoäng med hjälp av Segment Builder. Nu kan ni inrikta er på era målgrupper genom att aktivera dem för destinationer. Mer information finns i [destinationsöversikten](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) .

## Bilaga

I följande avsnitt finns ytterligare information om hur kunden uppnår AI.

### Kundens AI-utdata

Kund-AI genererar flera attribut för enskilda profiler som anses berättigade. Dessa värden används av kundprofilen i realtid som kan användas för att skapa och definiera segment. Tabellen nedan beskriver de olika attribut som finns i utdata från kundens AI:

| Attribut | Beskrivning |
| ----- | ----------- |
| Poäng | Den relativa sannolikheten för att en kund ska uppnå det förväntade målet inom den definierade tidsramen. Detta värde ska inte behandlas som sannolikhetsprocent utan snarare som sannolikheten för en individ jämfört med den totala populationen. Poängen varierar mellan 0 och 100. |
| Sannolikhet | Det här attributet är den verkliga sannolikheten för att en profil ska uppnå det förväntade målet inom den definierade tidsramen. När du jämför utdata för olika mål bör du överväga sannolikhet över percentil eller poäng. Sannolikhet bör alltid användas vid bestämning av den genomsnittliga sannolikheten i hela den stödberättigade populationen, eftersom sannolikheten tenderar att vara på den nedre sidan för händelser som inte inträffar ofta. Värden för sannolikhetsintervallet mellan 0 och 1. |
| Procent | Det här värdet ger information om en profils prestanda i förhållande till andra profiler med liknande resultat. En profil med en percentilrankning på 99 för kurn visar till exempel att den har en större risk att kurva jämfört med 99 % av alla andra profiler som bedömdes. Percentiler varierar mellan 1 och 100. |
| Typ av benägenhet | Den valda benägenhetstypen. |
| Resultatdatum | Det datum som poängsättningen inträffade. |
| Influensafaktorer | Förväntade orsaker till varför en profil kan konverteras eller försvinna. Faktorer består av följande attribut:<ul><li>Kod: Profilen eller beteendeattributet som positivt påverkar en profils förväntade poäng. </li><li>Värde: Värdet på profilen eller beteendeattributet.</li><li>Prioritet: Anger hur viktig profilen eller beteendeattributet är för det förväntade poängvärdet (låg, medel, hög)</li></ul> |