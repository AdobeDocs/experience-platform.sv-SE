---
solution: Experience Platform
title: Utforska och bearbeta instrumentpaneler för Raw-datauppsättningar för plattform
type: Documentation
description: Lär dig hur du använder frågetjänsten för att utforska och bearbeta rådatauppsättningar som används på kontrollpaneler för profiler, segment och mål i Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

Insikter på profilkontrollpanelen är knutna till sammanfogningsprinciper som har definierats av din organisation. För varje aktiv sammanfogningsprincip finns det en profilattributdatauppsättning tillgänglig i datasjön.

Namnkonventionen för dessa datauppsättningar är **Profile-Snapshot-Export** följt av ett systemgenererat slumpmässigt alfanumeriskt värde. Exempel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Om du vill förstå det fullständiga schemat för varje profilögonblicksbilds exportdatauppsättning kan du förhandsgranska och utforska datauppsättningarna [med datamängdsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet för Experience Platform.

![](images/query/profile-attribute.png)

#### Kopplar profilattributsdatauppsättningar till sammanfogade princip-ID:n

Varje profilattributdatauppsättning har titeln **Export av ögonblicksbild av profil** följt av ett systemgenererat slumpmässigt alfanumeriskt värde. Exempel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Det här alfanumeriska värdet är en systemgenererad, slumpmässig sträng som mappas till ett sammanfogningsprincip-ID för en av sammanfogningsprinciperna som har skapats i organisationen. Mappningen av varje sammanfogningsprincip-ID till dess relaterade datauppsättningssträng för profilattribut behålls i `adwh_dim_merge_policies`-datauppsättningen.

Datamängden `adwh_dim_merge_policies` innehåller följande fält:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Den här datauppsättningen kan utforskas med hjälp av användargränssnittet i Frågeredigeraren i Experience Platform. Mer information om hur du använder Frågeredigeraren finns i [Användargränssnittsguiden för frågeredigeraren](../query-service/ui/user-guide.md).

### Datamängd för segmentmetadata

Data för segmentmetadata finns tillgängliga i datasjön med metadata för varje segment i organisationen.

Namnkonventionen för den här datauppsättningen är **Segmentdefinition-Snapshot-Export** följt av ett alfanumeriskt värde. Exempel: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Om du vill förstå det fullständiga schemat för varje ögonblicksbildsexportdatauppsättning för segmentdefinitioner kan du förhandsgranska och utforska datauppsättningarna [med datamängdsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet för Experience Platform.

![](images/query/segment-metadata.png)

### Metadatadatamängd för mål

Metadata för alla era aktiverade destinationer är tillgängliga som en rådatamängd i datasjön.

Namnkonventionen för den här datauppsättningen är **DIM_Destination**.

Om du vill förstå det fullständiga schemat för DIM-måldatauppsättningen kan du förhandsgranska och utforska datauppsättningen [med datauppsättningsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet i Experience Platform.

![](images/query/destinations-metadata.png)

## Exempelfrågor

Följande exempelfrågor innehåller exempel på SQL som kan användas i frågetjänsten för att utforska, verifiera och bearbeta rådatauppsättningar som används i dina instrumentpaneler.

### Antal profiler per identitet

Denna profilinsikt ger en uppdelning av identiteter för alla sammanfogade profiler i datauppsättningen.

>[!NOTE]
>
>Det totala antalet profiler per identitet (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kan vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Nästa steg

Genom att läsa den här guiden kan du nu använda frågetjänsten för att utföra flera frågor för att utforska och bearbeta de rådatauppsättningar som styr din profil, ditt segment och dina målinstrumentpaneler.

Om du vill veta mer om varje kontrollpanel och dess mätvärden väljer du en kontrollpanel i listan över tillgängliga kontrollpaneler i dokumentationsnavigeringen.
