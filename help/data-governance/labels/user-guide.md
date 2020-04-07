---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Användarhandbok för etiketter för dataanvändning
topic: labels
translation-type: tm+mt
source-git-commit: a19a9a31743002eb5fd3a5ecb6668b4c760faa9a

---


# Användarhandbok för etiketter för dataanvändning

Den här användarhandboken innehåller steg för att arbeta med dataanvändningsetiketter (kallas även DULE-etiketter) i användargränssnittet för Experience Platform. Innan du använder guiden bör du läsa översikten över [datastyrning](../home.md) för en mer robust introduktion till DULE-ramverket.

## Hantera dataanvändningsetiketter på datauppsättningsnivå

För att kunna hantera dataanvändningsetiketter på datauppsättningsnivå måste du välja en befintlig datauppsättning eller skapa en ny. När du har loggat in på Adobe Experience Platform väljer du **Datauppsättningar** i den vänstra navigeringen för att öppna arbetsytan _Datauppsättningar_ . På den här sidan visas alla skapade datauppsättningar som tillhör din organisation, tillsammans med användbar information om varje datauppsättning.

![Fliken Datauppsättning i arbetsytan Data](../images/labels/datasets.png)

I nästa avsnitt beskrivs hur du skapar en ny datauppsättning som du kan använda etiketter på. Om du vill redigera etiketter för en befintlig datauppsättning, markerar du datauppsättningen i listan och går vidare till att [lägga till etiketter för dataanvändning i datauppsättningen](#add-labels).

### Skapa en ny datauppsättning

>[!NOTE] I det här exemplet skapas en datauppsättning med ett förkonfigurerat XDM-schema (Experience Data Model). Mer information om XDM-scheman finns i [XDM-systemöversikten](../../xdm/home.md) och [grunderna för schemakomposition](../../xdm/schema/composition.md).

Om du vill skapa en ny datauppsättning klickar du på **Skapa datauppsättning** i det övre högra hörnet av arbetsytan _Datauppsättningar_ .

![](../images/labels/create_dataset.png)

Skärmen _Skapa datauppsättning_ visas. Klicka här på **Skapa datauppsättning från schema**.

![Skapa datauppsättning från schema](../images/labels/dataset_create.png)

Skärmen _Välj schema_ visas med alla tillgängliga scheman som du kan använda för att skapa en datauppsättning. Klicka på alternativknappen bredvid ett schema för att markera det. I avsnittet _Scheman_ till höger visas ytterligare information om det valda schemat. När du har valt ett schema klickar du på **Nästa**.

![Välj datauppsättningsschema](../images/labels/dataset_schema.png)

Skärmen _Konfigurera datauppsättning_ visas. Ange ett **namn** (obligatoriskt) och en **beskrivning** (valfritt, men rekommenderas) för den nya datauppsättningen och klicka sedan på **Slutför**.

![Konfigurera datauppsättning med namn och beskrivning](../images/labels/dataset_configure.png)

Sidan _Datauppsättningsaktivitet_ visas med information om den nya datauppsättningen. I det här exemplet heter datauppsättningen&quot;Förmånsmedlemmar&quot;, vilket innebär att den översta navigeringen visar _Datauppsättningar > Förmånsmedlemmar_.

![Sidan Datauppsättningsaktivitet](../images/labels/dataset_activity.png)

### Lägg till dataanvändningsetiketter i datauppsättningen {#add-labels}

När du har skapat en ny datauppsättning eller valt en befintlig datauppsättning i listan på arbetsytan _Datauppsättningar_ klickar du på **Datastyrning** för att öppna arbetsytan _Datastyrning_ . På arbetsytan kan du hantera dataanvändningsetiketter på datauppsättningsnivå och fältnivå.

![Fliken Datamängdsstyrning](../images/labels/dataset_data_governance.png)

Om du vill redigera dataanvändningsetiketter på datauppsättningsnivå börjar du med att klicka på pennikonen bredvid datauppsättningsnamnet.

![Redigera etiketter på datauppsättningsnivå](../images/labels/dataset_labels_edit_button.png)

Dialogrutan _Redigera styrningsetiketter_ öppnas. I dialogrutan markerar du rutorna bredvid de etiketter du vill använda på datauppsättningen. Kom ihåg att dessa etiketter ärvs av alla fält i datauppsättningen. Rubriken _Använda etiketter_ uppdateras när du markerar varje ruta och visar de etiketter du har valt. När du har markerat etiketterna klickar du på **Spara ändringar**.

<img alt="Tillämpa styrningsetiketter på datauppsättningsnivå" src="../images/labels/dataset_apply_labels.png" width="450"><br>

Arbetsytan _Datastyrning_ visas igen och visar de etiketter som du har använt på datauppsättningsnivå. Du kan också se att etiketterna ärvs ned till vart och ett av fälten i datauppsättningen.

![Datauppsättningsetiketter ärvda av fält](../images/labels/dataset_inherited_labels.png)

Observera att ett&quot;x&quot; visas bredvid etiketterna på datauppsättningsnivå, vilket gör att du kan ta bort etiketterna. De ärvda etiketterna bredvid varje fält har inte något &quot;x&quot; bredvid sig och visas&quot;nedtonade&quot; utan möjlighet att ta bort eller redigera. Detta beror på att **ärvda fält är skrivskyddade**, vilket innebär att de inte kan tas bort på fältnivån.

Växeln **Visa ärvda etiketter** är aktiverad som standard, vilket gör att du kan se alla etiketter som ärvs ned från datauppsättningen till dess fält. Om du växlar av inaktiveringen döljs alla ärvda etiketter i datauppsättningen.

![Dölj ärvda etiketter](../images/labels/hide_inherited_labels.png)

## Hantera dataanvändningsetiketter på datamängdsfältnivå

Genom att fortsätta arbetsflödet för att [lägga till och redigera dataanvändningsetiketter på datauppsättningsnivå](#add-labels)kan du även hantera fältetiketter på arbetsytan _Datastyrning_ för den datauppsättningen.

Om du vill använda dataanvändningsetiketter på ett enskilt fält markerar du kryssrutan bredvid fältnamnet och klickar sedan på **Redigera styrningsetiketter**.

![Redigera fältetiketter](../images/labels/fields_single_field.png)

Dialogrutan _Redigera styrningsetiketter_ visas. I dialogrutan visas rubriker med markerade fält, tillämpade etiketter och ärvda etiketter. Observera att de ärvda etiketterna (C2 och C5) är nedtonade i dialogrutan. De är skrivskyddade etiketter som ärvs från datauppsättningsnivån och kan därför bara redigeras på datauppsättningsnivå.

<img alt="Redigera styrningsetiketter för ett enskilt fält" src="../images/labels/fields_inherited_labels.png" width="450"><br>

Välj etiketter på fältnivå genom att klicka i kryssrutan bredvid varje etikett som du vill använda. När du väljer etiketter uppdateras rubriken _Använda etiketter_ så att etiketter som används i fälten visas i rubriken _Markerade fält_ . När du har valt etiketter på fältnivå klickar du på **Spara ändringar**.

<img alt="Använda etiketter på fältnivå" src="../images/labels/fields_field_level_label.png" width="450"><br>

Arbetsytan _Datastyrning_ visas igen och nu visas de markerade fältetiketterna på raden bredvid fältnamnet. Observera att fältnivåetiketten har ett &quot;x&quot; bredvid sig, vilket gör att du kan ta bort etiketten.

![Fält som visar etiketter på fältnivå](../images/labels/fields_show_field_level_labels.png)

Du kan upprepa de här stegen om du vill fortsätta lägga till och redigera etiketter på fältnivå för ytterligare fält, inklusive markera flera fält för att använda etiketter på fältnivå samtidigt.

![Markera flera fält om du vill använda etiketter på fältnivå samtidigt.](../images/labels/fields_select_multiple.png)

Det är viktigt att komma ihåg att arv endast flyttas från den översta nivån nedåt (datamängd → fält), vilket innebär att etiketter som används på fältnivå inte sprids till andra fält eller datamängder.

## Nästa steg

Nu när du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till Experience Platform. Om du vill veta mer kan du börja med att läsa [dokumentationen](../../ingestion/home.md)för dataöverföring.

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i översikten över [dataanvändningsprinciper](../policies/overview.md).

## Ytterligare resurser

Följande video är avsedd att ge stöd för din förståelse av datastyrning och visar hur du använder etiketter på en datamängd och enskilda fält.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
