---
keywords: Experience Platform;hem;populära ämnen;aktivera datauppsättning;datauppsättning;datauppsättning
solution: Experience Platform
title: Användargränssnittshandbok för datauppsättningar
topic: datasets
description: Lär dig hur du utför vanliga åtgärder när du arbetar med datauppsättningar i Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: 2b8c08dad34bcd69368c00050323835f05379c82
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---


# Användargränssnittshandbok för datauppsättningar

Den här användarhandboken innehåller anvisningar om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i Adobe Experience Platform användargränssnitt.

## Komma igång

Användarhandboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Datauppsättningar](overview.md): Konstruktionen för lagring och hantering för databeständighet i  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigerare](../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar egna anpassade XDM-scheman med hjälp av  [!DNL Schema Editor] i  [!DNL Platform] användargränssnittet.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Se till att era kunddata är kompatibla med regler, begränsningar och policyer.

## Visa datauppsättningar

I gränssnittet för [!DNL Experience Platform] klickar du på **[!UICONTROL Datasets]** i den vänstra navigeringen för att öppna kontrollpanelen för **[!UICONTROL Datasets]**. Kontrollpanelen visar alla tillgängliga datauppsättningar för din organisation. Information visas för varje datamängd som anges, inklusive namn, schema som datauppsättningen följer och status för den senaste importen.

![](../images/datasets/user-guide/browse_datasets.png)

Klicka på namnet på en datauppsättning för att komma åt dess **[!UICONTROL Dataset activity]**-skärm och se information om den datauppsättning du valde. Fliken Aktivitet innehåller ett diagram som visar hur många meddelanden som har förbrukats samt en lista över lyckade och misslyckade batchar.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Förhandsgranska en datauppsättning

Klicka på **[!UICONTROL Preview dataset]** nära skärmens övre högra hörn för att förhandsgranska upp till 100 rader med data på skärmen **[!UICONTROL Dataset activity]**. Om datauppsättningen är tom inaktiveras förhandsgranskningslänken och det står i stället att förhandsvisningen inte är tillgänglig.

![](../images/datasets/user-guide/click_to_preview.png)

I förhandsgranskningsfönstret visas den hierarkiska vyn av datasetens schema till höger.

![](../images/datasets/user-guide/preview_dataset.png)

[!DNL Experience Platform] tillhandahåller tjänster längre fram i kedjan, t.ex. [!DNL Query Service] och [!DNL JupyterLab] för att utforska och analysera data, för mer robusta metoder för att komma åt data. Mer information finns i följande dokument:

* [Översikt över frågetjänsten](../../query-service/home.md)
* [Användarhandbok för JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Skapa en datauppsättning {#create}

Om du vill skapa en ny datauppsättning börjar du med att klicka på **[!UICONTROL Create dataset]** på kontrollpanelen **[!UICONTROL Datasets]**.

![](../images/datasets/user-guide/click_to_create.png)

På nästa skärm visas följande två alternativ för att skapa en ny datauppsättning:

* [Skapa datauppsättning från schema](#schema)
* [Skapa datauppsättning från CSV-fil](#csv)

### Skapa en datauppsättning med ett befintligt schema {#schema}

Klicka på **[!UICONTROL Create dataset from schema]** på skärmen **[!UICONTROL Create dataset]** för att skapa en ny tom datauppsättning.

![](../images/datasets/user-guide/create_dataset_schema.png)

**[!UICONTROL Select schema]**-steget visas. Bläddra i schemalistan och välj det schema som datauppsättningen ska följa innan du klickar på **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

**[!UICONTROL Configure dataset]**-steget visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **[!UICONTROL Finish]** för att skapa datauppsättningen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Skapa en datauppsättning med en CSV-fil {#csv}

När en datauppsättning skapas med en CSV-fil skapas ett ad hoc-schema som ger datauppsättningen en struktur som matchar den angivna CSV-filen. Klicka i rutan **[!UICONTROL Create dataset from CSV file]** på skärmen **[!UICONTROL Create dataset]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

**[!UICONTROL Configure]**-steget visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

**[!UICONTROL Add data]**-steget visas. Överför CSV-filen genom att antingen dra och släppa den mitt på skärmen eller klicka på **[!UICONTROL Browse]** för att utforska din filkatalog. Filen kan vara upp till tio gigabyte stor. När CSV-filen har överförts klickar du på **[!UICONTROL Save]** för att skapa datauppsättningen.

>[!NOTE]
>
>CSV-kolumnnamn måste börja med alfanumeriska tecken och får bara innehålla bokstäver, siffror och understreck.

![](../images/datasets/user-guide/add_csv_data.png)

## Aktivera en datauppsättning för kundprofil i realtid

Alla datauppsättningar har möjlighet att förbättra kundprofiler med inkapslade data. Det gör du genom att schemat som datauppsättningen följer måste vara kompatibelt för användning i [!DNL Real-time Customer Profile]. Ett kompatibelt schema uppfyller följande krav:

* Schemat har minst ett attribut angivet som en identitetsegenskap.
* Schemat har en identitetsegenskap definierad som primär identitet.

Mer information om hur du aktiverar ett schema för [!DNL Profile] finns i [användarhandboken för Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md).

Om du vill aktivera en datauppsättning för profilen öppnar du skärmen **[!UICONTROL Dataset activity]** och klickar på växlingsknappen **[!UICONTROL Profile]** i kolumnen **[!UICONTROL Properties]**. När den är aktiverad används även data som är inkapslade i datauppsättningen för att fylla i kundprofiler.

>[!NOTE]
>
>Om en datauppsättning redan innehåller data och sedan aktiveras för [!DNL Profile], används inte befintliga data automatiskt av [!DNL Profile]. När en datauppsättning har aktiverats för [!DNL Profile] rekommenderar vi att du återimporterar befintliga data så att de bidrar till kundprofiler.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Hantera och tillämpa datastyrning på en datauppsättning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Mer information om etiketter finns i [översikten över datastyrning](../../data-governance/home.md). Du kan även läsa användarhandboken för [användaretiketter för dataanvändning](../../data-governance/labels/overview.md) för instruktioner om hur du använder etiketter på datauppsättningar.

## Ta bort en datauppsättning

Du kan ta bort en datauppsättning genom att först gå till dess **[!UICONTROL Dataset activity]**-skärm. Klicka sedan på **[!UICONTROL Delete dataset]** för att ta bort den.

>[!NOTE]
>
>Det går inte att ta bort datauppsättningar som har skapats och använts av program och tjänster från Adobe (till exempel Adobe Analytics, Adobe Audience Manager eller [!DNL Offer Decisioning]).

![](../images/datasets/user-guide/delete_dataset.png)

En bekräftelseruta visas. Klicka på **[!UICONTROL Delete]** för att bekräfta borttagningen av datauppsättningen.

![](../images/datasets/user-guide/confirm_delete.png)

## Ta bort en profilaktiverad datauppsättning

Om en datauppsättning är aktiverad för [!DNL Profile] tas den bort både från datasjön och profilarkivet inom plattformen om du tar bort datauppsättningen via användargränssnittet.

Du kan bara ta bort en datauppsättning från [!DNL Profile]-butiken (lämna data i Data Lake) med hjälp av kundprofils-API:t i realtid. Mer information finns i [API-slutpunktshandboken för profilsystemjobb](../../profile/api/profile-system-jobs.md).

## Övervaka datainmatning

Klicka på **[!UICONTROL Monitoring]** i det vänstra navigeringsfältet i gränssnittet för [!DNL Experience Platform]. Med kontrollpanelen **[!UICONTROL Monitoring]** kan du visa status för inkommande data från antingen batch- eller direktuppspelningsinmatning. Om du vill visa status för enskilda grupper klickar du antingen på **[!UICONTROL Batch end-to-end]** eller **[!UICONTROL Streaming end-to-end]**. På kontrollpanelerna visas alla grupper- eller direktuppspelningskörningar, inklusive de som har slutförts, misslyckats eller pågår. Varje lista innehåller information om batchen, inklusive batch-ID:t, namnet på måldatauppsättningen och antalet poster som har importerats. Om måldatauppsättningen är aktiverad för [!DNL Profile] visas även antalet inkapslade identitets- och profilposter.

![](../images/datasets/user-guide/batch_listing.png)

Du kan klicka på en enskild **[!UICONTROL Batch ID]** för att komma åt kontrollpanelen **[!UICONTROL Batch overview]** och se information om gruppen, inklusive felloggar om gruppen inte kan importeras.

![](../images/datasets/user-guide/batch_overview.png)

Om du vill ta bort gruppen kan du göra det genom att klicka på **[!UICONTROL Delete batch]** som finns uppe till höger på kontrollpanelen. Om du gör det tas även posterna bort från den datauppsättning som batchen ursprungligen skapades i.

![](../images/datasets/user-guide/delete_batch.png)

## Nästa steg

Den här användarhandboken innehåller anvisningar för hur du utför vanliga åtgärder när du arbetar med datauppsättningar i [!DNL Experience Platform]-användargränssnittet. Anvisningar om hur du utför vanliga [!DNL Platform]-arbetsflöden med datauppsättningar finns i följande självstudier:

* [Skapa en datauppsättning med API:er](create.md)
* [Fråga datauppsättningsdata med API:t för dataåtkomst](../../data-access/home.md)
* [Konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../../profile/tutorials/dataset-configuration.md)