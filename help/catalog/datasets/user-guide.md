---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Användarhandbok för datauppsättningar
topic: datasets
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---


# Användarhandbok för datauppsättningar

Den här användarhandboken innehåller anvisningar om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i användargränssnittet i Adobe Experience Platform.

## Komma igång

Den här användarhandboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Datauppsättningar](overview.md): Konstruktionen för lagring och hantering av databeständighet i Experience Platform.
* [Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigerare](../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar egna anpassade XDM-scheman med Schemaredigeraren i Platform användargränssnitt.
* [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Datastyrning](../../data-governance/home.md): Se till att era kunddata är kompatibla med regler, begränsningar och policyer.

## Visa datauppsättningar

I användargränssnittet för Experience Platform klickar du på **Datauppsättningar** i den vänstra navigeringen för att öppna kontrollpanelen för *datauppsättningar* . Kontrollpanelen visar alla tillgängliga datauppsättningar för din organisation. Information visas för varje datamängd som anges, inklusive namn, schema som datauppsättningen följer och status för den senaste importen.

![](../images/datasets/user-guide/browse_datasets.png)

Klicka på namnet på en datauppsättning för att komma åt aktivitetsskärmen för *datauppsättningen* och se information om den datauppsättning du valde. Fliken Aktivitet innehåller ett diagram som visar hur många meddelanden som har förbrukats samt en lista över lyckade och misslyckade batchar.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Förhandsgranska en datauppsättning

Klicka på *Förhandsgranska datauppsättning* i det övre högra hörnet av skärmen för att förhandsgranska upp till 100 rader med data på aktivitetsskärmen för **datauppsättning** . Om datauppsättningen är tom inaktiveras förhandsgranskningslänken och det står i stället att **Förhandsvisning inte är tillgängligt**.

![](../images/datasets/user-guide/click_to_preview.png)

I förhandsgranskningsfönstret visas den hierarkiska vyn av datasetens schema till höger.

![](../images/datasets/user-guide/preview_dataset.png)

För mer robusta metoder att komma åt data erbjuder Experience Platform tjänster längre fram i kedjan, som Query Service och JupyterLab, för att utforska och analysera data. Mer information finns i följande dokument:

* [Översikt över frågetjänsten](../../query-service/home.md)
* [Användarhandbok för JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Skapa en datauppsättning {#create}

Om du vill skapa en ny datauppsättning börjar du med att klicka på **Skapa datauppsättning** på kontrollpanelen *Datauppsättningar* .

![](../images/datasets/user-guide/click_to_create.png)

På nästa skärm visas följande två alternativ för att skapa en ny datauppsättning:

* [Skapa datauppsättning från schema](#create-a-dataset-with-an-existing-schema)
* [Skapa datauppsättning från CSV-fil](#create-a-dataset-with-a-csv-file)

### Skapa en datauppsättning med ett befintligt schema

Klicka på *Skapa datauppsättning från schema* på skärmen **Skapa datauppsättning** för att skapa en ny tom datauppsättning.

![](../images/datasets/user-guide/create_dataset_schema.png)

Steget *Välj schema* visas. Bläddra i schemalistan och välj det schema som datauppsättningen ska följa innan du klickar på **Nästa**.

![](../images/datasets/user-guide/select_schema.png)

Steget *Konfigurera datauppsättning* visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **Slutför** för att skapa datauppsättningen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Skapa en datauppsättning med en CSV-fil

När en datauppsättning skapas med en CSV-fil skapas ett ad hoc-schema som ger datauppsättningen en struktur som matchar den angivna CSV-filen. På skärmen *Skapa datauppsättning* klickar du på rutan **Skapa datauppsättning från CSV-fil**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Steget *Konfigurera* visas. Ange ett namn och en valfri beskrivning för datauppsättningen och klicka sedan på **Nästa**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Steget *Lägg till data* visas. Överför CSV-filen genom att antingen dra och släppa den mitt på skärmen eller klicka på **Bläddra** för att utforska din filkatalog. Filen kan vara upp till tio gigabyte stor. När CSV-filen har överförts klickar du på **Spara** för att skapa datauppsättningen.

>[!NOTE]
>
>CSV-kolumnnamn måste börja med alfanumeriska tecken och får bara innehålla bokstäver, siffror och understreck.

![](../images/datasets/user-guide/add_csv_data.png)

## Aktivera en datauppsättning för kundprofil i realtid

Alla datauppsättningar har möjlighet att förbättra kundprofiler med inkapslade data. För att göra det måste det schema som datauppsättningen följer vara kompatibelt för användning i kundprofilen i realtid. Ett kompatibelt schema uppfyller följande krav:

* Schemat har minst ett attribut angivet som en identitetsegenskap.
* Schemat har en identitetsegenskap definierad som primär identitet.

Mer information om hur du aktiverar ett schema för profilen finns i användarhandboken [för](../../xdm/tutorials/create-schema-ui.md)schemaredigeraren.

Om du vill aktivera en datauppsättning för profil öppnar du aktivitetsskärmen för *datauppsättningen* och klickar på **profilväxlingen** i kolumnen *Egenskaper* . När den är aktiverad används även data som är inkapslade i datauppsättningen för att fylla i kundprofiler.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Om en datauppsättning redan innehåller data och sedan aktiveras för profilen, förbrukas inte befintliga data av profilen. När en datauppsättning har aktiverats för profil rekommenderar vi att du återimporterar befintliga data så att de fyller i kundprofiler.

## Hantera och tillämpa datastyrning på en datauppsättning

Varumärkning och verkställighet av dataanvändning (DULE) är huvudmekanismen för datastyrning för Experience Platform. DULE-etiketter gör att du kan kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Mer information om etiketter finns i översikten [över](../../data-governance/home.md) datastyrning, eller i användarhandboken [för](../../data-governance/labels/overview.md) dataanvändningsetiketter finns instruktioner om hur du använder etiketter på datauppsättningar.

## Ta bort en datauppsättning

Du kan ta bort en datauppsättning genom att först gå till aktivitetsskärmen för *datauppsättningen* . Klicka sedan på **Ta bort datauppsättning** för att ta bort den.

>[!NOTE]
>
>Det går inte att ta bort datauppsättningar som har skapats och använts av Adobe-program och -tjänster (som Adobe Analytics, Adobe Audience Manager eller beslutstjänsten).

![](../images/datasets/user-guide/delete_dataset.png)

En bekräftelseruta visas. Klicka på **Ta bort** för att bekräfta borttagningen av datauppsättningen.

![](../images/datasets/user-guide/confirm_delete.png)

## Ta bort en profilaktiverad datauppsättning

Om en datauppsättning är aktiverad för profil inaktiveras datauppsättningen för förtäring om den tas bort via användargränssnittet, men datauppsättningen i serverdelen tas inte bort automatiskt. För att datauppsättningen, inklusive profil- och identitetsdata som den innehåller, ska kunna tas bort helt måste ytterligare en begäran om borttagning göras. Anvisningar om hur du tar bort data på rätt sätt från profilarkivet finns i [delguiden för kundprofils-API i realtid om profilsystemjobb, som även kallas&quot;raderingsbegäranden&quot;](../../profile/api/profile-system-jobs.md).

## Övervaka datainmatning

Klicka på **Övervakning** till vänster i användargränssnittet i Experience Platform. På kontrollpanelen *Övervakning* kan du visa status för inkommande data från antingen batch- eller direktuppspelningsinmatning. Om du vill visa status för enskilda batchar klickar du antingen på *Gruppera från början till slut* eller på *Direktuppspelning från början till slut*. På kontrollpanelerna visas alla grupper- eller direktuppspelningskörningar, inklusive de som har slutförts, misslyckats eller pågår. Varje lista innehåller information om batchen, inklusive batch-ID:t, namnet på måldatauppsättningen och antalet poster som har importerats. Om måldatauppsättningen är aktiverad för Profil visas även antalet inkapslade identitets- och profilposter.

![](../images/datasets/user-guide/batch_listing.png)

Du kan klicka på ett enskilt **batch-ID** för att komma åt kontrollpanelen *Gruppöversikt* och se information om gruppen, inklusive felloggar om gruppen inte kan importeras.

![](../images/datasets/user-guide/batch_overview.png)

Om du vill ta bort gruppen kan du göra det genom att klicka på **Ta bort grupp** som finns uppe till höger på kontrollpanelen. Om du gör det tas även dess poster bort från den datauppsättning som batchen ursprungligen kopplades till.

![](../images/datasets/user-guide/delete_batch.png)

## Nästa steg

I den här användarhandboken finns anvisningar om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i användargränssnittet i Experience Platform. Anvisningar om hur du utför vanliga Platform-arbetsflöden med datauppsättningar finns i följande självstudiekurser:

* [Skapa en datauppsättning med API:er](create.md)
* [Fråga datauppsättningsdata med API:t för dataåtkomst](../../data-access/home.md)
* [Konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../../profile/tutorials/dataset-configuration.md)