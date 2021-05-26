---
solution: Experience Platform
title: Utforska och bearbeta rådatauppsättningar på Experience Platform-paneler
type: Documentation
description: Lär dig hur du använder frågetjänsten för att utforska och bearbeta rådatauppsättningar som används på kontrollpaneler för profiler, segment och mål i Experience Platform.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Utforska, verifiera och bearbeta instrumentpanelsdatauppsättningar med hjälp av frågetjänsten

Adobe Experience Platform tillhandahåller viktig information om din organisations profil-, segment- och destinationsdata via kontrollpaneler som är tillgängliga i användargränssnittet för Experience Platform. Du kan sedan använda Adobe Experience Platform Query Service för att utforska, verifiera och bearbeta de rådatauppsättningar som styr dessa instrumentpaneler i datasjön.

## Komma igång med frågetjänsten

Adobe Experience Platform Query Service stöder marknadsförare i deras insikt genom att aktivera användningen av standard-SQL för att fråga data i datasjön. Frågetjänsten erbjuder ett användargränssnitt och ett API som kan användas för att ansluta till valfri datauppsättning i datasjön och samla in frågeresultaten som nya datauppsättningar som kan användas för rapportering, maskininlärning eller för förtäring i kundprofilen i realtid.

Om du vill veta mer om frågetjänsten och dess roll i Experience Platform börjar du med att läsa översikten över frågetjänsten](../query-service/home.md).[

## Tillgängliga datauppsättningar

Du kan använda frågetjänsten för att fråga efter rådatauppsättningar för kontrollpaneler för profil, segment och mål. I följande avsnitt beskrivs de Raw-datauppsättningar som du kan hitta i datasjön.

### Datauppsättningar för profilattribut

För varje aktiv sammanfogningsprincip i kundprofilen i realtid finns det en profilattributsdatauppsättning tillgänglig i datasjön.

Namnkonventionen för den här datauppsättningen är **Profilattribut** följt av ett alfanumeriskt värde. Exempel: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Om du vill förstå datasetens fullständiga schema kan du förhandsgranska och utforska schemat med hjälp av datamängdsvisningsprogrammet i användargränssnittet i Experience Platform.

### Datamängd för segmentmetadata

Det finns en datauppsättning för segmentmetadata tillgänglig i datasjön för varje segment i din organisation.

Namnkonventionen för den här datauppsättningen är **Profilsegmentsdefinition** följt av ett alfanumeriskt värde. Exempel: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

Följande bild visar schemat för segmentets metadatatauppsättning.

![](images/query/segment-metadata.png)

### Metadatadatamängd för mål

Metadata för dina aktiverade destinationer är tillgängliga som en Raw-datauppsättning i datarjön.

Namnkonventionen för den här datauppsättningen är **DIM_Destination**.

Följande bild visar schemat för målmetadatadatauppsättningen.

![](images/query/destinations-metadata.png)

## Exempelfrågor

Följande exempelfrågor innehåller exempel på SQL som kan användas i frågetjänsten för att utforska, verifiera och bearbeta rådatauppsättningar som används i dina instrumentpaneler.

### Antal profiler per identitet

Denna profilinsikt ger en uppdelning av identiteter för alla sammanfogade profiler i datauppsättningen. Det totala antalet profiler per identitet (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kan vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

**Fråga**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Antal profiler per segment

Denna målgruppsinsikter ger det totala antalet sammanfogade profiler inom varje segment i datauppsättningen. Det här numret är resultatet av att du har tillämpat segmentsammanfogningsprincipen på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person i segmentet.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### Antal aktiverade segment per mål för alla mål

## Nästa steg

Genom att läsa den här guiden kan du nu använda frågetjänsten för att utföra flera frågor för att utforska och bearbeta de rådatauppsättningar som styr din profil, ditt segment och dina målinstrumentpaneler.

Om du vill veta mer om varje kontrollpanel och dess mätvärden väljer du en kontrollpanel i listan över tillgängliga kontrollpaneler i dokumentationsnavigeringen.
