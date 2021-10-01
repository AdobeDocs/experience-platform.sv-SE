---
title: Översikt över användningsexempel för segmentering för CDP B2B Edition i realtid.
description: Översikt över de olika användningsområdena för CDP B2B Edition i realtid som finns.
source-git-commit: e85d4b108e2d4a6a88772c071d9281603b695ada
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Översikt över användningen av segmentering för kunddataplattformen B2B Edition (betaversion) i realtid

<!-- This document relates to this [ticket](https://jira.corp.adobe.com/browse/PLAT-100468) -->

>[!IMPORTANT]
>
>CDP B2B Edition är i realtid i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Det här dokumentet innehåller exempel på den segmentering som är tillgänglig för CDP B2B Edition i realtid och hur de olika attributtyperna kan kombineras för vanliga B2B-användningsfall.

>[!NOTE]
>
>De attribut som krävs för denna segmenteringsanvändning är endast tillgängliga för kunder som har Real-time Customer Data Platform B2B Edition. Om du vill veta mer om CDP i realtid, inklusive de funktioner och funktioner som är tillgängliga för varje licenstyp, kan du börja med att läsa [CDP-översikt i realtid](../overview.md).

## Förutsättningar

Innan du kan använda segmenteringsattributen för B2B-klasser måste du utföra följande steg:

1. Skapa scheman som använder B2B-klasserna. Klasserna för B2B Edition omfattar konto, kampanj, säljprojekt, marknadsföringslista med mera. Mer information om [hur du ställer in scheman för användning med B2B-klasser](../schemas/b2b.md) finns i schemadokumentationen.
1. Skapa relationer mellan era B2B-scheman i Experience Data Model (XDM). Segment baserade på B2B Edition-attribut kräver relationer mellan klasserna för att fullt ut kunna använda den utökade B2B-segmenteringsfunktionen. Mer information finns i dokumentationen om [hur du definierar en relation mellan två B2B-scheman](../../xdm/tutorials/relationship-b2b.md).
1. Importera data med datauppsättningar baserade på era B2B-scheman. I källdokumentationen finns [information om hur du importerar data](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Läs [användarhandboken för segmentbyggaren](../../segmentation/ui/segment-builder.md) om du vill ha mer detaljerad information om hur du skapar segment.

När dessa krav är uppfyllda kan du kombinera dessa attribut för vanliga B2B-syften.

## Komma igång

När föreningsscheman för B2B-klasserna har upprättat relationer och har använts för att importera data, blir deras attribut tillgängliga i den vänstra listen i Segment Builder.

B2B-klasser och deras attribut läggs till med en `B2B`-etikett i arbetsytan Segmentering för att skilja dem från dem som finns som standard i kunddataplattformen i realtid.

För att effektivt kunna skapa segment för B2B-användning är det viktigt att ha en god kunskap om schemat och förstå hur datamodellen ser ut. Det är också praktiskt att vara medveten om den sökväg som data tar från ett dataobjekt till ett annat.

Bilden nedan visar förhållandet mellan de B2B-klasser som finns i CDP B2B Edition i realtid.

![ERD för B2B-klass](../assets/segmentation/b2b-classes.png)

Eftersom din datamodell kan vara komplicerad kan du använda användargränssnittet för plattformen för att visa en mer detaljerad visuell representation av din datamodell för att hitta relevanta attribut för ditt användningsfall. Börja med att gå till användargränssnittet för plattformen och välj Scheman i den vänstra navigeringen.

Välj lämpligt schema från den tillgängliga listan och välj lämplig relation från sidospåret [!UICONTROL Composition]. I exemplet nedan visar valet av &quot;Person&quot;-relation vilket attribut i det aktuella schemat som refererar till det relaterade &quot;Person&quot;-schemat (om det är källschemat i relationen) eller refereras av &quot;Person&quot;-schemat (om det är målschemat i relationen).

![källnyckelsexempel med personrelationen på arbetsytan för schemat](../assets/segmentation/source-key-schema-relationship-example.png)

Relationen återspeglas i segmentbyggaren genom att använda mapparna `Key`, vilket visas i bilden nedan.

![källnyckelsexempel med segmentbyggaren i segmenteringsarbetsytan](../assets/segmentation/source-key-segmentation-example.png)

Mer information om tillgängliga B2B-klasser finns i [scheman i dokumentationen för kunddataplattformen B2B Edition i realtid](../schemas/b2b.md).

Användningsexemplen nedan ger information om vilka klasser som används för att upprätta relationer mellan olika scheman för att uppnå dessa resultat. De här exemplen kan användas för att skapa egna segment.

## Exempel på olika användningsområden

Följande användningsexempel finns för segmentering med B2B Edition. Varje exempel innehåller en beskrivning av vad segmentet gör och en beskrivning av de klasser som används för att skapa dem. Bilderna visar filsökvägen i sidlisten [!UICONTROL Attributes] som återspeglar schemats struktur. Avsnittet [!UICONTROL Segment properties] till höger om visningen innehåller en skriven beskrivning av segmentets attribut.

### Exempel 1

Hitta alla personer som är &quot;beslutsfattare&quot; för alla möjligheter. Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile] och klassen [!UICONTROL XDM Business Opportunity Person Relation].

![Gränssnitt som visar exempelinställningar 1](../assets/segmentation/example-1.png)

### Exempel 2

Hitta alla personer som är direkt tilldelade till alla möjligheter vars affärsmöjlighet är större än det angivna beloppet ($1 miljon). Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Opportunity Person Relation] och klassen [!UICONTROL XDM Business Opportunity].

![Gränssnitt som visar exempelinställningar 2](../assets/segmentation/example-2.png)

### Exempel 3

Hitta alla personer som är direkt tilldelade till affärsmöjligheter där kontot finns på en viss plats (Kanada). Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Opportunity Person Relation], klassen [!UICONTROL XDM Business Opportunity] och klassen [!UICONTROL XDM Business Account].

![Gränssnitt som visar exempelinställningar 3](../assets/segmentation/example-3.png)

### Exempel 4

Hitta alla personer som är en&quot;beslutsfattare&quot; för alla möjligheter där kontot finns i&quot;finansbranschen&quot; och som har besökt prissidan de senaste tre dagarna. Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Opportunity Person Relation], klassen [!UICONTROL XDM Business Opportunity] och klassen [!UICONTROL XDM Business Account] och klassen [!UICONTROL XDM ExperienceEvent].

![Gränssnitt som visar exempel 4 inställningar](../assets/segmentation/example-4.png)

### Exempel 5

Hitta alla personer som arbetar på en HR-avdelning och som är kopplade till ett konto som har minst en öppen möjlighet till ett visst belopp ($1 miljon) eller mer. Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Account] och klassen [!UICONTROL XDM Business Opportunity].

![Gränssnitt som visar exempelinställningar för 5](../assets/segmentation/example-5.png)

### Exempel 6

Hitta alla personer vars befattning är Vice President och som är kopplade till ett konto med en årsomsättning på ett visst belopp ($100 miljoner) eller mer, och som har besökt prissidan minst tre gånger den senaste månaden. Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Account] och klassen [!UICONTROL XDM ExperienceEvent].

![Gränssnitt som visar exempel 6 inställningar](../assets/segmentation/example-6.png)

### Exempel 7

Hitta alla personer som är en &quot;beslutsfattare&quot; för alla stängda affärsmöjligheter och besökte prissidan förra veckan. Det här segmentet kräver en länk mellan klassen [!UICONTROL XDM Individual Profile], klassen [!UICONTROL XDM Business Opportunity Person Relation], klassen [!UICONTROL XDM Business Opportunity] och klassen [!UICONTROL XDM ExperienceEvent].

![Gränssnitt som visar exempelinställningar 7](../assets/segmentation/example-7.png)

## Nästa steg

Efter att ha läst den här översikten har du nu en förståelse för de segmenteringsmöjligheter som finns med CDP, B2B Edition i realtid. Mer information om segmenteringstjänsten finns i [Segmenteringsdokumentationen](../../segmentation/home.md).
