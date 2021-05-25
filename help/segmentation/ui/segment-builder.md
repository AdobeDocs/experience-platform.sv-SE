---
keywords: Experience Platform;hem;populära ämnen;Segmenteringstjänst;segmenteringstjänst;segmenteringstjänst;användarhandbok;ui guide;segmenteringsguide;segmentbyggare;segmentbyggare;
solution: Experience Platform
title: Användargränssnittshandbok för Segment Builder
topic-legacy: ui guide
description: Segmentbyggaren i Adobe Experience Platform-användargränssnittet har en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1936'
ht-degree: 0%

---

# [!DNL Segment Builder] Användargränssnittsguide

[!DNL Segment Builder] innehåller en omfattande arbetsyta som gör att du kan interagera med  [!DNL Profile] dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.

![](../images/ui/segment-builder/segment-builder.png)

## Byggstenar för segmentdefinitioner

De grundläggande byggstenarna för segmentdefinitioner är attribut och händelser. Dessutom kan attribut och händelser i befintliga målgrupper också användas som komponenter för nya definitioner.

Dessa byggstenar visas i **[!UICONTROL Fields]**-avsnittet till vänster på arbetsytan [!DNL Segment Builder]. **[!UICONTROL Fields]** innehåller en flik för varje huvudbyggsten: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; och &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attribut

På fliken **[!UICONTROL Attributes]** kan du bläddra bland [!DNL Profile]-attribut som tillhör klassen [!DNL XDM Individual Profile]. Varje mapp kan expanderas för att visa ytterligare attribut, där varje attribut är en platta som kan dras till regelbyggararbetsytan i mitten av arbetsytan. [Regelbyggaren canvas](#rule-builder-canvas) beskrivs mer ingående senare i den här guiden.

![](../images/ui/segment-builder/attributes.png)

### Händelser

På fliken **[!UICONTROL Events]** kan du skapa en målgrupp baserat på händelser eller åtgärder som har utförts med [!DNL XDM ExperienceEvent]-dataelement. Du kan också hitta händelsetyper på fliken **[!UICONTROL Events]**, som är en samling vanliga händelser som gör att du kan skapa segment snabbare.

Förutom att du kan bläddra efter [!DNL ExperienceEvent]-element kan du även söka efter händelsetyper. Händelsetyper använder samma kodningslogik som [!DNL ExperienceEvents], utan att du behöver söka igenom klassen [!DNL XDM ExperienceEvent] för att hitta rätt händelse. Om du till exempel använder sökfältet för att söka efter &quot;kundvagn&quot; returneras händelsetyperna &quot;[!UICONTROL AddCart]&quot; och &quot;[!UICONTROL RemoveCart]&quot;, som är två mycket vanliga kundvagnsåtgärder när du skapar segmentdefinitioner.

Du kan söka efter alla typer av komponenter genom att skriva komponentens namn i sökfältet, som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Sökresultaten fylls i när hela ord anges. Om du till exempel vill skapa en regel som baseras på XDM-fältet `ExperienceEvent.commerce.productViews` börjar du skriva &quot;produktvyer&quot; i sökfältet. När ordet &quot;product&quot; har skrivits in börjar sökresultaten visas. Varje resultat innehåller den objekthierarki som det hör till.

>[!NOTE]
>
>Det kan ta upp till 24 timmar innan anpassade schemafält som definieras av organisationen visas och blir tillgängliga för användning i byggregler.

Du kan sedan enkelt dra och släppa [!DNL ExperienceEvents] och [!UICONTROL Event Types] i segmentdefinitionen.

![](../images/ui/segment-builder/events-eventTypes.png)

Som standard visas endast ifyllda schemafält från ditt datalager. Det inkluderar &quot;[!UICONTROL Event Types]&quot;. Om listan [!UICONTROL Event Types] inte visas, eller om du bara kan välja [!UICONTROL Any] som [!UICONTROL Event Type], väljer du **kugghjulsikonen** bredvid **[!UICONTROL Fields]** och sedan **[!UICONTROL Show full XDM schema]** under **[!UICONTROL Available Fields]**. Välj **kugghjulsikonen** igen om du vill gå tillbaka till fliken **[!UICONTROL Fields]** och du bör nu kunna visa flera [!UICONTROL Event Types]- och schemafält, oavsett om de innehåller data eller inte.

![](../images/ui/segment-builder/show-populated.png)

### Målgrupper

På fliken **[!UICONTROL Audiences]** visas alla målgrupper som importerats från externa källor, till exempel Adobe Audience Manager, samt målgrupper som skapats i [!DNL Experience Platform].

På fliken **[!UICONTROL Audiences]** kan du se alla tillgängliga källor som en grupp med mappar. När du markerar mapparna visas tillgängliga undermappar och målgrupper. Dessutom kan du välja mappikonen (som visas längst till höger) för att visa mappstrukturen (en bock anger den mapp du befinner dig i) och enkelt navigera tillbaka genom mapparna genom att välja namnet på en mapp i trädet.

Du kan hovra över ⓘ bredvid en målgrupp för att visa information om målgruppen, inklusive dess ID, beskrivning och mapphierarkin för att hitta målgruppen.

![](../images/ui/segment-builder/audience-folder-structure.png)

Du kan också söka efter målgrupper med hjälp av sökfältet, som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om du väljer en mapp på den översta nivån på fliken **[!UICONTROL Audiences]** visas sökfältet så att du kan söka i den mappen. Sökresultaten fylls bara i när hela ord anges. Om du till exempel vill hitta en målgrupp med namnet `Online Shoppers` börjar du skriva &quot;Online&quot; i sökfältet. När ordet &quot;Online&quot; har skrivits in fullständigt visas sökresultat som innehåller ordet &quot;Online&quot;.

## Regelbyggarens arbetsyta {#rule-builder-canvas}

En segmentdefinition är en samling regler som används för att beskriva viktiga egenskaper eller beteenden hos en målgrupp. Dessa regler skapas med regelbyggarens arbetsyta, som finns i mitten av [!DNL Segment Builder].

Om du vill lägga till en ny regel i segmentdefinitionen drar du en platta från fliken **[!UICONTROL Fields]** och släpper den på regelbyggarens arbetsyta. Därefter visas sammanhangsspecifika alternativ beroende på vilken typ av data som läggs till. Tillgängliga datatyper: strängar, datum, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; och målgrupper.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>De senaste ändringarna av Adobe Experience Platform har uppdaterat användningen av de logiska operatorerna `OR` och `AND` mellan händelser. Dessa uppdateringar påverkar inte befintliga segment. Alla efterföljande uppdateringar av befintliga segment och nya segment kommer dock att påverkas av dessa ändringar. Läs [uppdateringen av tidskonstanter](./segment-refactoring.md) om du vill ha mer information.

### Lägga till målgrupper

Du kan dra och släppa en målgrupp från fliken **[!UICONTROL Audience]** till regelbyggararbetsytan för att referera till målgruppsmedlemskap i den nya segmentdefinitionen. På så sätt kan du inkludera eller exkludera målgruppsmedlemskap som ett attribut i den nya segmentregeln.

För [!DNL Platform]-målgrupper som skapats med [!DNL Segment Builder] kan du konvertera målgruppen till den uppsättning regler som användes i segmentdefinitionen för den målgruppen. Den här konverteringen skapar en kopia av regellogiken som sedan kan ändras utan att den ursprungliga segmentdefinitionen påverkas. Kontrollera att du har sparat alla senaste ändringar av segmentdefinitionen innan du konverterar den till regellogik.

>[!NOTE]
>
>När du lägger till en målgrupp från en extern källa refereras endast målgruppsmedlemskapet. Du kan inte konvertera målgruppen till regler, och därför kan reglerna som används för att skapa den ursprungliga målgruppen inte ändras i den nya segmentdefinitionen.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Om det uppstår några konflikter när målgrupper konverteras till regler försöker [!DNL Segment Builder] att bevara de befintliga alternativen så att de blir så bra som möjligt.

### kodvyn

Du kan också visa en kodbaserad version av en regel som skapats i [!DNL Segment Builder]. När du har skapat regeln på arbetsytan i regelbyggaren kan du välja **[!UICONTROL Code view]** för att se ditt segment som PQL.

![](../images/ui/segment-builder/code-view.png)

I kodvyn finns en knapp som du kan använda för att kopiera segmentets värde för API-anrop. Kontrollera att du har sparat dina senaste ändringar i segmentet för att få den senaste versionen av segmentet.

![](../images/ui/segment-builder/copy-code.png)

### Sammanställningsfunktioner

En aggregering i [!DNL Segment Builder] är en beräkning för en grupp av XDM-attribut vars datatyp är ett tal (antingen en dubbel eller ett heltal). De fyra aggregeringsfunktionerna som stöds i Segment Builder är SUM, AVERAGE, MIN och MAX.

Om du vill skapa en aggregeringsfunktion väljer du en händelse från den vänstra listen och infogar den i [!UICONTROL Events]-behållaren.

![](../images/ui/segment-builder/select-event.png)

När du har placerat händelsen i händelsebehållaren markerar du ellipsikonen (..) följt av **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

Aggregeringsvärdet har nu lagts till. Nu kan du välja sammanställningsfunktionen, välja vilket attribut som ska sammanställas, likhetsfunktionen samt värdet. I exemplet nedan kvalificerar det här segmentet alla profiler som har en summa köpta värden som är större än 100 USD, även om varje enskilt köp är mindre än 100 USD.

![](../images/ui/segment-builder/filled-aggregation.png)

### Räkningsfunktioner {#count-functions}

Räkningsfunktioner i Segment Builder används för att söka efter angivna händelser och räkna antalet gånger de är klara. De räkningsfunktioner som stöds i Segment Builder är &quot;Minst&quot;, &quot;Högst&quot;, &quot;Exakt&quot;, &quot;Mellan&quot; och &quot;Alla&quot;.

Om du vill skapa en räkningsfunktion markerar du en händelse från den vänstra listen och infogar den i [!UICONTROL Events]-behållaren.

![](../images/ui/segment-builder/add-event.png)

När du har placerat händelsen i händelsebehållaren väljer du knappen [!UICONTROL At least 1].

![](../images/ui/segment-builder/add-count.png)

Funktionen count har nu lagts till. Nu kan du välja funktionen count och värdet för funktionen. Exemplet nedan är att inkludera alla händelser som har minst ett klick.

![](../images/ui/segment-builder/select-count.png)

## Behållare

Segmentregler utvärderas i den ordning som de listas. Behållare ger kontroll över körningsordningen med hjälp av kapslade frågor.

När du har lagt till minst en platta på regelbyggararbetsytan kan du börja lägga till behållare. Om du vill skapa en ny behållare markerar du ellipserna (..) i rutans övre högra hörn och väljer sedan **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

En ny behållare visas som underordnad till den första behållaren, men du kan justera hierarkin genom att dra och flytta behållarna. Standardbeteendet för en behållare är att &quot;[!UICONTROL Include]&quot; är attributet, händelsen eller målgruppen som anges. Du kan ställa in regeln på profiler som matchar behållarvillkoren genom att välja **[!UICONTROL Include]** i rutans övre vänstra hörn och välja [!UICONTROL Exclude].[!UICONTROL Exclude]

En underordnad behållare kan också extraheras och läggas till i den överordnade behållaren genom att markera&quot;dela upp behållare&quot; i den underordnade behållaren. Markera ellipserna (..) i det övre högra hörnet av den underordnade behållaren för att komma åt det här alternativet.

![](../images/ui/segment-builder/include-exclude.png)

När du har valt **[!UICONTROL Unwrap container]** tas den underordnade behållaren bort och villkoren visas textbundna.

>[!NOTE]
>
>När du delar upp behållare ska du se till att logiken fortsätter att uppfylla den önskade segmentdefinitionen.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Sammanfoga profiler

[!DNL Experience Platform] gör att ni kan samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanfogar dessa data är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en profil.

Du kan välja en sammanfogningsprincip som matchar ditt marknadsföringssyfte för den här målgruppen eller använda den standardsammanfogningsprincip som finns i [!DNL Platform]. Du kan skapa flera sammanfogningsprinciper som är unika för din organisation, inklusive skapa en egen standardsammanfogningsprincip. Stegvisa instruktioner om hur du skapar sammanfogningsprinciper för din organisation finns i [översikten över sammanfogningsprinciper](../../profile/merge-policies/overview.md).

Om du vill välja en sammanfogningsprincip för segmentdefinitionen väljer du kugghjulsikonen på fliken **[!UICONTROL Fields]** och använder sedan listrutan **[!UICONTROL Merge Policy]** för att välja den sammanfogningsprincip som du vill använda.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Segmentegenskaper

När du skapar en segmentdefinition visar avsnittet **[!UICONTROL Segment Properties]** till höger om arbetsytan en uppskattning av storleken på det resulterande segmentet, så att du kan justera segmentdefinitionen efter behov innan du skapar själva målgruppen.

I avsnittet **[!UICONTROL Segment Properties]** kan du även ange viktig information om segmentdefinitionen, inklusive namn och beskrivning. Segmentdefinitionsnamn används för att identifiera ditt segment bland dem som definieras av organisationen och bör därför vara beskrivande, koncisa och unika.

När du fortsätter att skapa segmentdefinitionen kan du visa en sidnumrerad förhandsvisning av målgruppen genom att välja **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Målgruppsuppskattningar genereras med en provstorlek för den aktuella dagens exempeldata. Om det finns mindre än 1 miljon enheter i din profilbutik används hela datauppsättningen. För mellan 1 och 20 miljoner enheter används 1 miljon enheter. och för över 20 miljoner enheter används 5 % av det totala antalet enheter. Mer information om hur du genererar segmentuppskattningar finns i [uppskattningsgenereringssektionen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) i självstudiekursen för att skapa segment.

## Nästa steg {#next-steps}

Segment Builder har ett omfattande arbetsflöde som gör att du kan isolera marknadsföringsbara målgrupper från [!DNL Real-time Customer Profile]-data. När du har läst den här guiden bör du nu kunna:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använd regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmentreglerna körs.
- Visa uppskattningar av er presumtiva målgrupp, så att ni kan justera era segmentdefinitioner efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktivera angivna segmentdefinitioner för direktuppspelningssegmentering.

Om du vill veta mer om [!DNL Segmentation Service] kan du fortsätta läsa dokumentationen och komplettera din inlärning genom att titta på relaterade videor. Läs [[!DNL Segmentation Service] användarhandboken](./overview.md) om du vill veta mer om de andra delarna i användargränssnittet[!DNL Segmentation Service]
