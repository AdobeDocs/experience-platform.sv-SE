---
keywords: Experience Platform;home;popular topics;segment;Segment;segment builder;Segment builder
solution: Experience Platform
title: Användarhandbok för Segmentering Service Segment Builder
topic: ui guide
description: 'I Segment Builder finns en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. '
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 0%

---


# [!DNL Segment Builder] användarhandbok

[!DNL Segment Builder] innehåller en omfattande arbetsyta som gör att du kan interagera med [!DNL Profile] dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.

![](../images/ui/segment-builder/segment-builder.png)

## Byggstenar för segmentdefinitioner

De grundläggande byggstenarna för segmentdefinitioner är **[!UICONTROL Attributes]** och **[!UICONTROL Events]**. Dessutom **[!UICONTROL Audiences]** kan attributen och händelserna som finns i befintliga komponenter också användas som komponenter för nya definitioner.

Dessa byggstenar visas i **[!UICONTROL Fields]** avsnittet till vänster på [!DNL Segment Builder] arbetsytan. **[!UICONTROL Fields]** innehåller en flik för varje huvudbyggsten: **[!UICONTROL Attributes]**, **[!UICONTROL Events]** och **[!UICONTROL Audiences]**.

![](../images/ui/segment-builder/segment-fields.png)

### Attribut

På fliken **[!UICONTROL Attributes]** kan du bläddra bland [!DNL Profile] attribut som tillhör [!DNL XDM Individual Profile] klassen. Varje mapp kan expanderas för att visa ytterligare attribut, där varje attribut är en platta som kan dras till regelbyggararbetsytan i mitten av arbetsytan. Arbetsytan för [regelbyggaren](#rule-builder-canvas) beskrivs mer ingående senare i den här guiden.

![](../images/ui/segment-builder/attributes.png)

### Händelser

På fliken **[!UICONTROL Events]** kan du skapa en målgrupp baserat på händelser eller åtgärder som har utförts med [!DNL XDM ExperienceEvent] dataelement. Du hittar även Händelsetyper på fliken **[!UICONTROL Events]** , som är en samling vanliga händelser som gör att du kan skapa segment snabbare.

Förutom att du kan bläddra efter [!DNL ExperienceEvent] element kan du även söka efter händelsetyper. Händelsetyper använder samma kodningslogik som [!DNL ExperienceEvents], utan att du behöver söka igenom den klass som [!DNL XDM ExperienceEvent] söker efter rätt händelse. Om du till exempel använder sökfältet för att söka efter &quot;kundvagn&quot; returneras händelsetyperna &quot;[!UICONTROL AddCart]&quot; och &quot;[!UICONTROL RemoveCart]&quot;, som är två mycket vanliga kundvagnsåtgärder när du skapar segmentdefinitioner.

Du kan söka efter alla typer av komponenter genom att skriva deras namn i sökfältet, som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Sökresultaten fylls i när hela ord anges. Om du till exempel vill skapa en regel som baseras på XDM-fältet `ExperienceEvent.commerce.productViews`börjar du skriva&quot;produktvyer&quot; i sökfältet. När ordet &quot;product&quot; har skrivits in börjar sökresultaten visas. Varje resultat innehåller den objekthierarki som det hör till.

>[!NOTE]
>
>Det kan ta upp till 24 timmar innan anpassade schemafält som definieras av organisationen visas och blir tillgängliga för användning i byggregler.

Sedan kan du enkelt dra och släppa [!DNL ExperienceEvents] och [!UICONTROL Event Types] in i segmentdefinitionen.

![](../images/ui/segment-builder/events-eventTypes.png)

Som standard visas endast ifyllda schemafält från ditt datalager. Det inkluderar [!UICONTROL Event Types]. Om [!UICONTROL Event Types] listan inte visas, eller om du bara kan välja &quot;[!UICONTROL Any]&quot; som [!UICONTROL Event Type]en, markerar du kugghjulsikonen bredvid **[!UICONTROL Fields]** och väljer **[!UICONTROL Show full XDM schema]** under **[!UICONTROL Available Fields]**. Välj kugghjulsikonen igen om du vill gå tillbaka till **[!UICONTROL Fields]** fliken. Nu bör du kunna visa flera fält [!UICONTROL Event Types] och schemafält, oavsett om de innehåller data eller inte.

![](../images/ui/segment-builder/show-populated.png)

### Publiker

På **[!UICONTROL Audiences]** fliken visas alla målgrupper som importerats från externa källor, t.ex. Adobe Audience Manager, samt målgrupper som skapats i [!DNL Experience Platform].

På **[!UICONTROL Audiences]** fliken kan du se alla tillgängliga källor som en grupp mappar. När du markerar mapparna visas tillgängliga undermappar och målgrupper. Dessutom kan du välja mappikonen (som visas längst till höger) för att visa mappstrukturen (en bock anger den mapp du befinner dig i) och enkelt navigera tillbaka genom mapparna genom att välja namnet på en mapp i trädet.

Du kan hovra över ⓘ bredvid en målgrupp för att visa information om målgruppen, inklusive dess ID, beskrivning och mapphierarkin för att hitta målgruppen.

![](../images/ui/segment-builder/audience-folder-structure.png)

Du kan också söka efter [!UICONTROL Audiences] med sökfältet som använder [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om du väljer en mapp på den översta nivån på fliken **[!UICONTROL Audiences]** visas sökfältet så att du kan söka i mappen. Sökresultaten fylls bara i när hela ord anges. Om du till exempel vill söka efter ett [!UICONTROL Audience] namn `Online Shoppers`börjar du skriva &quot;Online&quot; i sökfältet. När ordet &quot;Online&quot; har skrivits in fullständigt visas sökresultat som innehåller ordet &quot;Online&quot;.

## Regelbyggarens arbetsyta {#rule-builder-canvas}

En segmentdefinition är en samling regler som används för att beskriva viktiga egenskaper eller beteenden hos en målgrupp. Dessa regler skapas med hjälp av regelbyggarens arbetsyta, som finns i mitten av [!DNL Segment Builder].

Om du vill lägga till en ny regel i segmentdefinitionen drar du en platta från **[!UICONTROL Fields]** fliken och släpper den på regelbyggarens arbetsyta. Därefter visas sammanhangsspecifika alternativ beroende på vilken typ av data som läggs till. Tillgängliga datatyper: strängar, datum [!DNL ExperienceEvents], [!UICONTROL Event Types]och [!UICONTROL Audiences].

![](../images/ui/segment-builder/rule-builder-canvas.png)

### Lägga till målgrupper

Du kan dra och släppa en målgrupp från fliken **[!UICONTROL Audience]** till regelbyggararbetsytan för att referera till målgruppsmedlemskap i den nya segmentdefinitionen. På så sätt kan du inkludera eller exkludera målgruppsmedlemskap som ett attribut i den nya segmentregeln.

För [!DNL Platform] målgrupper som skapats med [!DNL Segment Builder]får ni möjligheten att konvertera målgruppen till den uppsättning regler som användes i segmentdefinitionen för den målgruppen. Den här konverteringen skapar en kopia av regellogiken som sedan kan ändras utan att den ursprungliga segmentdefinitionen påverkas. Kontrollera att du har sparat alla senaste ändringar av segmentdefinitionen innan du konverterar den till regellogik.

>[!NOTE]
>
>När du lägger till en målgrupp från en extern källa refereras endast målgruppsmedlemskapet. Du kan inte konvertera målgruppen till regler, och därför kan reglerna som används för att skapa den ursprungliga målgruppen inte ändras i den nya segmentdefinitionen.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Om det uppstår några konflikter när målgrupper konverteras till regler försöker [!DNL Segment Builder] bevara de befintliga alternativen så gott de kan.

### kodvyn

Du kan också visa en kodbaserad version av en regel som har skapats i [!DNL Segment Builder]. När du har skapat regeln på arbetsytan i regelbyggaren kan du välja **[!UICONTROL Code view]** att visa ditt segment som en PQL.

![](../images/ui/segment-builder/code-view.png)

I kodvyn finns en knapp som du kan använda för att kopiera segmentets värde för API-anrop. Kontrollera att du har sparat dina senaste ändringar i segmentet för att få den senaste versionen av segmentet.

![](../images/ui/segment-builder/copy-code.png)

## Behållare

Segmentregler utvärderas i den ordning som de listas. Behållare ger kontroll över körningsordningen med hjälp av kapslade frågor.

När du har lagt till minst en platta på regelbyggararbetsytan kan du börja lägga till behållare. Om du vill skapa en ny behållare markerar du ellipserna (..) i rutans övre högra hörn och väljer sedan **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

En ny behållare visas som underordnad till den första behållaren, men du kan justera hierarkin genom att dra och flytta behållarna. Standardbeteendet för en behållare är att&quot;[!UICONTROL Include]&quot; attributet, händelsen eller målgruppen som anges. Du kan ställa in regeln på &quot;[!UICONTROL Exclude]&quot;-profiler som matchar behållarvillkoren genom att markera **[!UICONTROL Include]** i rutans övre vänstra hörn och välja &quot;[!UICONTROL Exclude]&quot;.

En underordnad behållare kan också extraheras och läggas till i den överordnade behållaren genom att markera&quot;dela upp behållare&quot; i den underordnade behållaren. Markera ellipserna (..) i det övre högra hörnet av den underordnade behållaren för att komma åt det här alternativet.

![](../images/ui/segment-builder/include-exclude.png)

När du har valt **[!UICONTROL Unwrap container]** den underordnade behållaren tas den bort och villkoren visas textbundna.

>[!NOTE]
>
>När du delar upp behållare ska du se till att logiken fortsätter att uppfylla den önskade segmentdefinitionen.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Sammanfoga profiler

[!DNL Experience Platform] gör att ni kan samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en profil.

Du kan välja en sammanfogningsprincip som matchar ditt marknadsföringssyfte för den här målgruppen eller använda den standardsammanfogningsprincip som tillhandahålls av [!DNL Platform]. Du kan skapa flera sammanfogningsprinciper som är unika för din organisation, inklusive skapa en egen standardsammanfogningsprincip. Stegvisa instruktioner om hur du skapar sammanfogningspolicyer för din organisation finns i självstudiekursen om hur du [arbetar med sammanfogningspolicyer med användargränssnittet](../../profile/ui/merge-policies.md).

Om du vill välja en sammanfogningsprincip för segmentdefinitionen väljer du kugghjulsikonen på **[!UICONTROL Fields]** fliken och väljer sedan den **[!UICONTROL Merge Policy]** nedrullningsbara menyn som du vill använda.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Segmentegenskaper

När du skapar en segmentdefinition visas en uppskattning av storleken på det *[!UICONTROL Segment Properties]* segment som skapas i avsnittet till höger om arbetsytan, så att du kan justera segmentdefinitionen efter behov innan du skapar själva målgruppen.

I det **[!UICONTROL Segment Properties]** här avsnittet kan du även ange viktig information om segmentdefinitionen, inklusive dess **[!UICONTROL Name]** och **[!UICONTROL Description]**. Segmentdefinitionsnamn används för att identifiera ditt segment bland dem som definieras av organisationen och bör därför vara beskrivande, koncisa och unika.

När du fortsätter att skapa en segmentdefinition kan du visa en sidnumrerad förhandsvisning av målgruppen genom att välja **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Målgruppsuppskattningar genereras med en provstorlek för den aktuella dagens exempeldata. Om det finns mindre än 1 miljon enheter i din profilbutik används hela datauppsättningen. För mellan 1 och 20 miljoner enheter används 1 miljon enheter. och för över 20 miljoner enheter används 5 % av det totala antalet enheter. Mer information om hur du genererar segmentuppskattningar finns i avsnittet [för att generera](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) uppskattningar i självstudiekursen för att skapa segment.

## Nästa steg och ytterligare resurser {#next-steps}

Segment Builder har ett omfattande arbetsflöde som gör det möjligt att isolera marknadsmässiga målgrupper från [!DNL Real-time Customer Profile] data. När du har läst den här guiden bör du nu kunna:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använd regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmentreglerna körs.
- Visa uppskattningar av er presumtiva målgrupp, så att ni kan justera era segmentdefinitioner efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktivera angivna segmentdefinitioner för direktuppspelningssegmentering.

Om du vill veta mer [!DNL Segmentation Service]kan du fortsätta att läsa dokumentationen och komplettera din inlärning genom att titta på filmerna nedan. Om du vill veta mer om de andra delarna av [!DNL Segmentation Service] användargränssnittet kan du läsa [[!DNL Segmentation Service] användarhandboken](./overview.md)

>[!WARNING]
>
> Gränssnittet [!DNL Platform] som visas i följande videofilmer är inaktuellt. Läs dokumentationen ovan för de senaste skärmbilderna och funktionerna i användargränssnittet.

**Skapa ett segment:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Skapa ett dynamiskt segment:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)