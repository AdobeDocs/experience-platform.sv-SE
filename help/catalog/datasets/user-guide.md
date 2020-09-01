---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Användarhandbok för datauppsättningar
topic: datasets
description: Den här användarhandboken för datauppsättningar innehåller anvisningar om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---


# Användarhandbok för datauppsättningar

Den här användarhandboken innehåller anvisningar om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i Adobe Experience Platform användargränssnitt.

## Komma igång

Användarhandboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Datauppsättningar](overview.md): Konstruktionen för lagring och hantering för databeständighet i [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigerare](../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar egna anpassade XDM-scheman med hjälp av [!DNL Schema Editor] i [!DNL Platform] användargränssnittet.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Data Governance]](../../data-governance/home.md): Se till att era kunddata är kompatibla med regler, begränsningar och policyer.

## Visa datauppsättningar

I [!DNL Experience Platform] användargränssnittet klickar du **[!UICONTROL Datasets]** i den vänstra navigeringen för att öppna **[!UICONTROL Datasets]** kontrollpanelen. Kontrollpanelen visar alla tillgängliga datauppsättningar för din organisation. Information visas för varje datamängd som anges, inklusive namn, schema som datauppsättningen följer och status för den senaste importen.

![](../images/datasets/user-guide/browse_datasets.png)

Klicka på namnet på en datauppsättning för att komma åt dess **[!UICONTROL Dataset activity]** skärm och se information om den datauppsättning du valde. Fliken Aktivitet innehåller ett diagram som visar hur många meddelanden som har förbrukats samt en lista över lyckade och misslyckade batchar.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Förhandsgranska en datauppsättning

På **[!UICONTROL Dataset activity]** skärmen klickar du **[!UICONTROL Preview dataset]** i skärmens övre högra hörn för att förhandsgranska upp till 100 rader med data. Om datauppsättningen är tom inaktiveras förhandsgranskningslänken och det står i stället **[!UICONTROL Preview not available]**.

![](../images/datasets/user-guide/click_to_preview.png)

I förhandsgranskningsfönstret visas den hierarkiska vyn av datasetens schema till höger.

![](../images/datasets/user-guide/preview_dataset.png)

För mer robusta metoder för att få tillgång till dina data erbjuder [!DNL Experience Platform] tjänster längre fram i kedjan, som [!DNL Query Service] [!DNL JupyterLab] att utforska och analysera data. Mer information finns i följande dokument:

* [Översikt över frågetjänsten](../../query-service/home.md)
* [Användarhandbok för JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Skapa en datauppsättning {#create}

Om du vill skapa en ny datauppsättning börjar du med att klicka **[!UICONTROL Create dataset]** på **[!UICONTROL Datasets]** instrumentpanelen.

![](../images/datasets/user-guide/click_to_create.png)

På nästa skärm visas följande två alternativ för att skapa en ny datauppsättning:

* [Skapa datauppsättning från schema](#create-a-dataset-with-an-existing-schema)
* [Skapa datauppsättning från CSV-fil](#create-a-dataset-with-a-csv-file)

### Skapa en datauppsättning med ett befintligt schema

Klicka på **[!UICONTROL Create dataset]** skärmen **[!UICONTROL Create dataset from schema]** för att skapa en ny tom datauppsättning.

![](../images/datasets/user-guide/create_dataset_schema.png)

Steget **[!UICONTROL Select schema]** visas. Bläddra i schemalistan och välj det schema som datauppsättningen ska följa innan du klickar **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

Steget **[!UICONTROL Configure dataset]** visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **[!UICONTROL Finish]** för att skapa datauppsättningen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Skapa en datauppsättning med en CSV-fil

När en datauppsättning skapas med en CSV-fil skapas ett ad hoc-schema som ger datauppsättningen en struktur som matchar den angivna CSV-filen. Klicka på rutan som anger på **[!UICONTROL Create dataset]** skärmen **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Steget **[!UICONTROL Configure]** visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Steget **[!UICONTROL Add data]** visas. Överför CSV-filen genom att antingen dra och släppa den mitt på skärmen eller klicka på **[!UICONTROL Browse]** för att utforska din filkatalog. Filen kan vara upp till tio gigabyte stor. När CSV-filen har överförts klickar du på **[!UICONTROL Save]** för att skapa datauppsättningen.

>[!NOTE]
>
>CSV-kolumnnamn måste börja med alfanumeriska tecken och får bara innehålla bokstäver, siffror och understreck.

![](../images/datasets/user-guide/add_csv_data.png)

## Aktivera en datauppsättning för kundprofil i realtid

Alla datauppsättningar har möjlighet att förbättra kundprofiler med inkapslade data. Det gör du genom att schemat som datauppsättningen följer måste vara kompatibelt för användning i [!DNL Real-time Customer Profile]. Ett kompatibelt schema uppfyller följande krav:

* Schemat har minst ett attribut angivet som en identitetsegenskap.
* Schemat har en identitetsegenskap definierad som primär identitet.

Mer information om hur du aktiverar ett schema för [!DNL Profile]finns i [användarhandboken](../../xdm/tutorials/create-schema-ui.md)för Schemaredigeraren.

Om du vill aktivera en datauppsättning för profilen öppnar du dess **[!UICONTROL Dataset activity]** skärm och klickar på **[!UICONTROL Profile]** växlingsknappen i **[!UICONTROL Properties]** kolumnen. När den är aktiverad används även data som är inkapslade i datauppsättningen för att fylla i kundprofiler.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Om en datauppsättning redan innehåller data och sedan aktiveras för [!DNL Profile]så förbrukas inte befintliga data av [!DNL Profile]. När en datauppsättning har aktiverats för [!DNL Profile]rekommenderar vi att du återimporterar befintliga data så att de fyller i kundprofiler.

## Hantera och tillämpa datastyrning på en datauppsättning

DULE (Data Usage Labeling and Enforcement) är den viktigaste mekanismen för datastyrning för [!DNL Experience Platform]. DULE-etiketter gör att du kan kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Mer information om etiketter finns i översikten [över](../../data-governance/home.md) datastyrning, eller i användarhandboken [för](../../data-governance/labels/overview.md) dataanvändningsetiketter finns instruktioner om hur du använder etiketter på datauppsättningar.

## Ta bort en datauppsättning

Du kan ta bort en datauppsättning genom att först gå till dess **[!UICONTROL Dataset activity]** skärm. Klicka sedan på **[!UICONTROL Delete dataset]** för att ta bort den.

>[!NOTE]
>
>Det går inte att ta bort datauppsättningar som skapats och använts av program och tjänster från Adobe (t.ex. Adobe Analytics, Adobe Audience Manager eller [!DNL Decisioning Service]).

![](../images/datasets/user-guide/delete_dataset.png)

En bekräftelseruta visas. Klicka **[!UICONTROL Delete]** för att bekräfta borttagningen av datauppsättningen.

![](../images/datasets/user-guide/confirm_delete.png)

## Ta bort en profilaktiverad datauppsättning

Om en datauppsättning är aktiverad för [!DNL Profile]och du tar bort den via användargränssnittet, inaktiveras datauppsättningen för förtäring, men datauppsättningen i serverdelen tas inte bort automatiskt. För att datauppsättningen, inklusive profil- och identitetsdata som den innehåller, ska kunna tas bort helt måste ytterligare en begäran om borttagning göras. Anvisningar om hur du tar bort data på rätt sätt från [!DNL Profile] butiken finns i [!DNL Real-time Customer Profile] API- [underhandboken om profilsystemjobb, som även kallas&quot;borttagningsbegäranden&quot;](../../profile/api/profile-system-jobs.md).

## Övervaka datainmatning

Klicka i det [!DNL Experience Platform] vänstra navigeringsfönstret **[!UICONTROL Monitoring]** i användargränssnittet. På **[!UICONTROL Monitoring]** kontrollpanelen kan du visa status för inkommande data från antingen batch- eller direktuppspelningsinmatning. Om du vill visa status för enskilda grupper klickar du på antingen **[!UICONTROL Batch end-to-end]** eller **[!UICONTROL Streaming end-to-end]**. På kontrollpanelerna visas alla grupper- eller direktuppspelningskörningar, inklusive de som har slutförts, misslyckats eller pågår. Varje lista innehåller information om batchen, inklusive batch-ID:t, namnet på måldatauppsättningen och antalet poster som har importerats. Om måldatauppsättningen är aktiverad för [!DNL Profile]visas även antalet inkapslade identitets- och profilposter.

![](../images/datasets/user-guide/batch_listing.png)

Du kan klicka på en person **[!UICONTROL Batch ID]** för att komma åt **[!UICONTROL Batch overview]** kontrollpanelen och se information om gruppen, inklusive felloggar om gruppen inte kan importeras.

![](../images/datasets/user-guide/batch_overview.png)

Om du vill ta bort gruppen kan du göra det genom att klicka på **[!UICONTROL Delete batch]** längst upp till höger på kontrollpanelen. Om du gör det tas även posterna bort från den datauppsättning som batchen ursprungligen skapades i.

![](../images/datasets/user-guide/delete_batch.png)

## Nästa steg

Den här användarhandboken innehåller anvisningar för hur du utför vanliga åtgärder när du arbetar med datauppsättningar i [!DNL Experience Platform] användargränssnittet. Anvisningar om hur du utför vanliga [!DNL Platform] arbetsflöden med datauppsättningar finns i följande självstudiekurser:

* [Skapa en datauppsättning med API:er](create.md)
* [Fråga datauppsättningsdata med API:t för dataåtkomst](../../data-access/home.md)
* [Konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../../profile/tutorials/dataset-configuration.md)