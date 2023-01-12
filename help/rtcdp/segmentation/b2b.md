---
title: Användningsexempel för segmentering för Real-time Customer Data Platform B2B Edition
description: En översikt över de olika användningsområdena för Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# Exempel på segmenteringsanvändning för Real-time Customer Data Platform B2B Edition

Det här dokumentet innehåller exempel på segmentdefinitioner i Adobe Real-time Customer Data Platform B2B Edition och hur olika typer av attribut kan kombineras för vanliga B2B-användningsområden. Mer information om hur destinationer passar in i ert B2B-arbetsflöde finns i [självstudiekurs från början till slut](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Attributen som krävs för denna segmenteringsanvändning är endast tillgängliga för Real-time Customer Data Platform B2B Edition-kunder. Om du inte använder Real-time Customer Data Platform B2B Edition läser du [segmenteringsöversikt](./segmentation-overview.md) i stället.

## Förutsättningar {#prerequisites}

Innan du kan använda segmenteringsattributen för B2B-klasser måste du utföra följande steg:

1. Skapa scheman som använder B2B-klasserna. Klasserna för B2B Edition omfattar konto, kampanj, säljprojekt, marknadsföringslista med mera. För information om [hur du ställer in scheman för användning med B2B-klasser](../schemas/b2b.md) finns i schemadokumentationen.
1. Skapa relationer mellan era B2B-scheman i Experience Data Model (XDM). Segment baserade på B2B Edition-attribut kräver relationer mellan klasserna för att fullt ut kunna använda den utökade B2B-segmenteringsfunktionen. Läs dokumentationen om [definiera en relation mellan två B2B-scheman](../../xdm/tutorials/relationship-b2b.md) för mer information.
1. Importera data med datauppsättningar baserade på era B2B-scheman. I källdokumentationen finns mer information om [information om hur man importerar data](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Läs [Användarhandbok för segmentbyggaren](../../segmentation/ui/segment-builder.md) om du vill ha en mer detaljerad vägledning om hur du skapar segment.

När dessa krav är uppfyllda kan du kombinera dessa attribut för vanliga B2B-syften.

## Komma igång {#getting-started}

När föreningsscheman för B2B-klasserna har upprättat relationer och har använts för att importera data, blir deras attribut tillgängliga i den vänstra listen i Segment Builder.

B2B-klasser och deras attribut läggs till med en `B2B` på arbetsytan Segmentering för att skilja dem från dem som finns som standard i Real-time Customer Data Platform.

För att effektivt kunna skapa segment för B2B-användning är det viktigt att ha en god kunskap om schemat och förstå hur datamodellen ser ut. Det är också praktiskt att vara medveten om den sökväg som data tar från ett dataobjekt till ett annat.

Bilden nedan visar förhållandet mellan de B2B-klasser som finns i Real-Time CDP B2B Edition.

![ERD för B2B-klass](../assets/segmentation/b2b-classes.png)

Eftersom din datamodell kan vara komplicerad kan du använda användargränssnittet för plattformen för att visa en mer detaljerad visuell representation av din datamodell för att hitta relevanta attribut för ditt användningsfall. Börja med att gå till användargränssnittet för plattformen och välj Scheman i den vänstra navigeringen.

Välj lämpligt schema i listan och välj lämplig relation i listan [!UICONTROL Composition] sidospår. I exemplet nedan visar valet av &quot;Person&quot;-relation vilket attribut i det aktuella schemat som refererar till det relaterade &quot;Person&quot;-schemat (om det är källschemat i relationen) eller refereras av &quot;Person&quot;-schemat (om det är referensschemat i relationen).

![källnyckelsexempel med personrelationen på arbetsytan för schemat](../assets/segmentation/source-key-schema-relationship-example.png)

Den här relationen återspeglas i segmentbyggaren med hjälp av `Key` enligt bilden nedan.

![källnyckelsexempel med segmentbyggaren i segmenteringsarbetsytan](../assets/segmentation/source-key-segmentation-example.png)

Se [scheman i Real-time Customer Data Platform B2B Edition-dokumentation](../schemas/b2b.md) för mer information om tillgängliga B2B-klasser.

Användningsexemplen nedan ger information om vilka klasser som används för att upprätta relationer mellan olika scheman för att uppnå dessa resultat. De här exemplen kan användas för att skapa egna segment.

## Exempel på olika användningsområden för segmentering {#use-cases}

Följande användningsexempel finns för segmentering med B2B Edition. Varje exempel innehåller en beskrivning av vad segmentet gör och en beskrivning av de klasser som används för att skapa dem. Bilderna visar filsökvägen i [!UICONTROL Attributes] sidospår som återspeglar schemats struktur. The [!UICONTROL Segment properties] -avsnittet till höger om visningen innehåller en skriftlig beskrivning av segmentets attribut.

### Exempel 1: Hitta&quot;beslutsfattare&quot; för B2B-möjligheter {#find-decision-maker}

Hitta alla personer som är &quot;beslutsfattare&quot; för alla möjligheter. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] -klassen och [!UICONTROL XDM Business Opportunity Person Relation] klassen.

![Gränssnitt som visar exempelinställningar 1](../assets/segmentation/example-1.png)

### Exempel 2: Hitta B2B-profiler som tilldelats affärsmöjligheter till ett visst belopp {#find-opportunities-amount}

Hitta alla personer som är direkt tilldelade till alla möjligheter vars affärsmöjlighet är större än det angivna beloppet ($1 miljon). Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Opportunity Person Relation] och [!UICONTROL XDM Business Opportunity] klassen.

![Gränssnitt som visar exempelinställningar 2](../assets/segmentation/example-2.png)

### Exempel 3: Hitta B2B-profiler som tilldelats affärsmöjligheter efter plats {#find-opportunities-location}

Hitta alla personer som är direkt tilldelade till affärsmöjligheter där kontot finns på en viss plats (Kanada). Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Opportunity Person Relation] klass, [!UICONTROL XDM Business Opportunity] och [!UICONTROL XDM Business Account] klassen.

![Gränssnitt som visar exempelinställningar 3](../assets/segmentation/example-3.png)

### Exempel 4: Hitta beslutsfattare för att hitta möjligheter utifrån bransch och surfbeteende {#find-industry-browsing-behavior}

Hitta alla personer som är en&quot;beslutsfattare&quot; för alla möjligheter där kontot finns i&quot;finansbranschen&quot; och som har besökt prissidan de senaste tre dagarna. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Opportunity Person Relation] klass, [!UICONTROL XDM Business Opportunity] och [!UICONTROL XDM Business Account] och [!UICONTROL XDM ExperienceEvent] klassen.

![Gränssnitt som visar exempel 4 inställningar](../assets/segmentation/example-4.png)

### Exempel 5: Hitta B2B-profiler för affärsmöjligheter efter avdelningens namn och affärsmöjlighetsbelopp {#find-department-opportunity-amount}

Hitta alla personer som arbetar på en HR-avdelning och som är kopplade till ett konto som har minst en öppen möjlighet till ett visst belopp ($1 miljon) eller mer. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Account] och [!UICONTROL XDM Business Opportunity] klassen.

![Gränssnitt som visar exempelinställningar för 5](../assets/segmentation/example-5.png)

### Exempel 6: Hitta B2B-profiler efter befattning och årsomsättning {#find-by-job-title-and-revenue}

Hitta alla personer vars befattning är Vice President och som är kopplade till ett konto med en årsomsättning på ett visst belopp ($100 miljoner) eller mer, och som har besökt prissidan minst tre gånger den senaste månaden. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Account] och [!UICONTROL XDM ExperienceEvent] klassen.

![Gränssnitt som visar exempel 6 inställningar](../assets/segmentation/example-6.png)

### Exempel 7: Hitta&quot;beslutsfattare&quot; efter affärsmöjlighet och webbläsarbeteende {#find-by-opportunity-status-and-browsing-behavior}

Hitta alla personer som är en &quot;beslutsfattare&quot; för alla stängda affärsmöjligheter och besökte prissidan förra veckan. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Opportunity Person Relation] klass, [!UICONTROL XDM Business Opportunity] och [!UICONTROL XDM ExperienceEvent] klassen.

![Gränssnitt som visar exempelinställningar 7](../assets/segmentation/example-7.png)

### Exempel 8: Använd relaterade konton för att utöka segmenteringsräckvidden {#related-accounts}

Hitta alla personer som arbetar på en HR-avdelning och som är kopplade till något konto *eller något av kontots relaterade konton* som har minst en öppen möjlighet till ett värde av minst 1 miljon USD. Det här segmentet kräver en länk mellan [!UICONTROL XDM Individual Profile] klass, [!UICONTROL XDM Business Account] och [!UICONTROL XDM Business Opportunity] klassen.

![Gränssnitt som visar segmentering för relaterade konton](../assets/segmentation/segmentation-related-accounts.png)

### Exempel 9: Använd lead scores och/eller account scores för att kvalificera profil {#account-scoring}

Hitta alla profiler med lead score över 80.

![Användargränssnitt som visar segmentering för prediktiv lead- och kontobedömning](../assets/segmentation/segmentation-predictive-lead-and-account-scoring.png)

## Nästa steg {#next-steps}

Efter att ha läst den här översikten har du nu en förståelse för de segmenteringsmöjligheter som är tillgängliga med Real-Time CDP, B2B Edition. Mer information om segmenteringstjänsten finns i [Segmenteringsdokumentation](../../segmentation/home.md).
