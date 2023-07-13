---
solution: Experience Platform
title: Utforska, verifiera och bearbeta Dashboard-datauppsättningar med hjälp av frågetjänsten
type: Documentation
description: Lär dig hur du använder frågetjänsten för att utforska och bearbeta rådatauppsättningar som ger möjlighet att skapa profiler, målgrupper och målpaneler i Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Utforska, verifiera och bearbeta dashboard-dataset med [!DNL Query Service]

Adobe Experience Platform tillhandahåller viktig information om organisationens profil, målgrupp och destinationsdata via kontrollpaneler som är tillgängliga i användargränssnittet för Experience Platform. Du kan sedan använda Adobe Experience Platform [!DNL Query Service] för att utforska, verifiera och bearbeta de rådatauppsättningar som styr dessa instrumentpaneler i datasjön.

## Komma igång med [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] stöder marknadsförare i att få insikter från sina data genom att aktivera användningen av standard-SQL för att fråga efter data i sjön. [!DNL Query Service] har ett användargränssnitt och ett API som kan användas för att ansluta till valfri datauppsättning i datasjön och samla in frågeresultaten som nya datauppsättningar som kan användas för rapportering, maskininlärning eller för att matas in i kundprofilen i realtid.

Mer information om [!DNL Query Service] och dess roll i Experience Platform, vänligen väl börja med att läsa [[!DNL Query Service] översikt](../query-service/home.md).

## Åtkomst till tillgängliga datauppsättningar

Du kan använda [!DNL Query Service] för att fråga efter rådatauppsättningar för kontrollpaneler för profil, målgrupp och mål. Om du vill visa tillgängliga datauppsättningar väljer du **Datauppsättningar** i den vänstra navigeringen för att öppna kontrollpanelen för datauppsättningar. Kontrollpanelen visar alla tillgängliga datauppsättningar för din organisation. Information visas för varje datamängd som anges, inklusive namn, schema som datauppsättningen följer och status för den senaste importen.

![Kontrollpanelen Bläddra bland datauppsättningar med fliken Datauppsättningar markerad i den vänstra navigeringen.](./images/query/browse-datasets.png)

### Systemgenererade datauppsättningar

>[!IMPORTANT]
>
>Systemgenererade datauppsättningar är dolda som standard. Som standard är [!UICONTROL Browse] -fliken visar bara datauppsättningar som du har inkapslat data i.

Om du vill visa systemgenererade datauppsättningar väljer du filterikonen (![En filterikon.](./images/query/filter.png)) till vänster om sökfältet.

![Fliken Bläddra bland datauppsättningar med filterikonen markerad.](./images/query/filter-datasets.png)

En sidospalt med två växlar visas, [!UICONTROL Included in Profile] och [!UICONTROL Show system datasets]. Välj alternativ för [!UICONTROL Show system datasets] för att inkludera systemgenererade datauppsättningar i den bläddringsbara listan med datauppsättningar.

![Fliken Bläddra bland datauppsättningar med växlingsknappen Visa systemdatauppsättningar markerad.](./images/query/show-system-datasets.png)

### Datauppsättningar för profilattribut

Insikter på profilkontrollpanelen är knutna till sammanfogningsprinciper som har definierats av din organisation. För varje aktiv sammanfogningsprincip finns det en profilattributdatauppsättning tillgänglig i datasjön.

Namnkonventionen för dessa datauppsättningar är **Profile-Snapshot-Export** följt av ett systemgenererat slumpmässigt alfanumeriskt värde. Exempel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Om du vill förstå det fullständiga schemat för varje ögonblicksbildsexportdatauppsättning kan du förhandsgranska och utforska datauppsättningarna [med datamängdsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet i Experience Platform.

![En förhandsgranskning av datamängden Profile-Snapshot-Export.](images/query/profile-attribute.png)

#### Kopplar profilattributsdatauppsättningar till sammanfogade princip-ID:n

Det alfanumeriska värdet som tilldelas till varje systemgenererad profilattributdatauppsättning är en slumpmässig sträng som mappas till ett sammanfogningsprincip-ID för en av de sammanfogningsprinciper som din organisation har skapat. Mappningen av varje ID för sammanfogningsprincip till den relaterade datauppsättningssträngen för profilattribut behålls i `adwh_dim_merge_policies` datauppsättning.

The `adwh_dim_merge_policies` datauppsättningen innehåller följande fält:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Den här datauppsättningen kan utforskas med hjälp av användargränssnittet i Frågeredigeraren i Experience Platform. Mer information om hur du använder Frågeredigeraren finns i [Användargränssnittshandbok för frågeredigeraren](../query-service/ui/user-guide.md).

### Målgruppsmetadata

Det finns en samling metadata för målgrupper i datasjön som innehåller metadata för alla era målgrupper.

Namnkonventionen för den här datauppsättningen är **Segmentdefinition-Snapshot-Export** följt av ett alfanumeriskt värde. Exempel: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Om du vill förstå det fullständiga schemat för varje segmentdefinitionsögonblicksbilds exportdatauppsättning kan du förhandsgranska och utforska datauppsättningarna [med datamängdsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet i Experience Platform.

### Metadatadatamängd för mål

Metadata för alla era aktiverade destinationer är tillgängliga som en rådatamängd i datasjön.

Namnkonventionen för den här datauppsättningen är **DIM_Destination**.

Om du vill förstå det fullständiga schemat för DIM-måldatauppsättningen kan du förhandsgranska och utforska datauppsättningen [med datamängdsvisningsprogrammet](../catalog/datasets/user-guide.md) i användargränssnittet i Experience Platform.

![En förhandsgranskning av DIM_Destination-datauppsättningen.](images/query/destinations-metadata.png)

## (Beta) Insiktsrapporter för kunddataplattformen (CDP)

>[!IMPORTANT]
>
>Funktionen CDP Insights Data Models är en betaversion. Dess funktioner och dokumentation kan komma att ändras.

CDP Insights Data Models-funktionen visar SQL som ger insikter om olika profil-, mål- och segmenteringswidgetar. Du kan anpassa de här SQL-frågemallarna för att skapa CDP-rapporter för marknadsförings- och KPI-användningsfall.

CDP-rapportering ger insikter i era profildata och dess relation till målgrupper och destinationer. Mer information om hur du gör det finns i dokumentationen om CDP Insights-datamodellen [tillämpa CDP Insights-datamodeller på dina specifika KPI-användningsfall](./cdp-insights-data-model.md).

## Exempelfrågor

Följande exempelfrågor innehåller exempel på SQL som kan användas i [!DNL Query Service] för att utforska, verifiera och bearbeta de rådatauppsättningar som ligger till grund för dina instrumentpaneler.

### Antal profiler efter identitet

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

### Antal profiler per målgrupp

Denna målgruppsinsikter ger det totala antalet sammanfogade profiler inom varje målgrupp i datauppsättningen. Det här numret är resultatet av att målgruppssammanfogningsprincipen har tillämpats på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person i målgruppen.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Nästa steg

Genom att läsa den här guiden kan du nu använda [!DNL Query Service] för att utföra flera frågor för att utforska och bearbeta de rådatauppsättningar som styr er profil, målgrupp och målpaneler.

Om du vill veta mer om varje kontrollpanel och dess mätvärden väljer du en kontrollpanel i listan över tillgängliga kontrollpaneler i dokumentationsnavigeringen.
