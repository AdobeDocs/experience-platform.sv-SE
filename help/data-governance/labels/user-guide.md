---
keywords: Experience Platform;hemanvändare;populära ämnen;datastyrning;dataanvändningsetikett;policytjänst;användarhandbok för dataanvändningsetiketter
solution: Experience Platform
title: Hantera dataanvändningsetiketter i användargränssnittet
topic-legacy: labels
description: Den här guiden innehåller steg för hur du arbetar med dataanvändningsetiketter i Adobe Experience Platform användargränssnitt.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---

# Hantera etiketter för dataanvändning i användargränssnittet

Den här användarhandboken innehåller steg för att arbeta med dataanvändningsetiketter i [!DNL Experience Platform] användargränssnitt.

## Hantera etiketter på datauppsättningsnivå

>[!IMPORTANT]
>
>Användning av etiketter på datauppsättningsnivå stöds bara för datastyrningsanvändning. Om du försöker skapa åtkomstprofiler för data måste du [lägg till etiketter i schemat](../../xdm/tutorials/labels.md) som datauppsättningen baseras på. Se översikten på [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för mer information.

För att kunna hantera dataanvändningsetiketter på datauppsättningsnivå måste du välja en befintlig datauppsättning eller skapa en ny. När du har loggat in på Adobe Experience Platform väljer du **[!UICONTROL Datasets]** till vänster för att öppna **[!UICONTROL Datasets]** arbetsyta. På den här sidan visas alla skapade datauppsättningar som tillhör din organisation, tillsammans med användbar information om varje datauppsättning.

![Fliken Datauppsättning i arbetsytan Data](../images/labels/datasets-tab.png)

I nästa avsnitt beskrivs hur du skapar en ny datauppsättning som du kan använda etiketter på. Om du vill redigera etiketter för en befintlig datauppsättning markerar du datauppsättningen i listan och går vidare till [lägga till dataanvändningsetiketter i datauppsättningen](#add-labels).

### Skapa en ny datauppsättning

>[!NOTE]
>
>I det här exemplet skapas en datauppsättning med en förkonfigurerad [!DNL Experience Data Model] (XDM) schema. Mer information om XDM-scheman finns i [XDM - systemöversikt](../../xdm/home.md) och [grunderna för schemakomposition](../../xdm/schema/composition.md).

Om du vill skapa en ny datauppsättning väljer du **[!UICONTROL Create Dataset]** i det övre högra hörnet av **[!UICONTROL Datasets]** arbetsyta.

![](../images/labels/create-dataset.png)

The **[!UICONTROL Create Dataset]** visas. Här väljer du **[!UICONTROL Create Dataset from Schema]**.

![Skapa datauppsättning från schema](../images/labels/create-from-dataset.png)

The **[!UICONTROL Select Schema]** visas, där alla tillgängliga scheman som du kan använda för att skapa en datauppsättning visas. Markera alternativknappen bredvid ett schema för att markera det. The **[!UICONTROL Schemas]** till höger visas ytterligare information om det valda schemat. När du har valt ett schema väljer du **[!UICONTROL Next]**.

![Välj datauppsättningsschema](../images/labels/select-schema.png)

The **[!UICONTROL Configure Dataset]** visas. Ange ett namn (obligatoriskt) och en beskrivning (valfritt, men rekommenderas) för den nya datauppsättningen och välj sedan **[!UICONTROL Finish]**.

![Konfigurera datauppsättning med namn och beskrivning](../images/labels/configure-dataset.png)

The **[!UICONTROL Dataset Activity]** visas med information om den nya datauppsättningen. I det här exemplet heter datauppsättningen&quot;Loyalty Members&quot;, vilket innebär att den översta navigeringen visar **Datamängder > Förmånsmedlemmar**.

![Sidan Datauppsättningsaktivitet](../images/labels/dataset-created.png)

### Lägg till dataanvändningsetiketter i datauppsättningen {#add-labels}

När du har skapat en ny datauppsättning eller valt en befintlig datauppsättning i listan i **[!UICONTROL Datasets]** arbetsyta, välja **[!UICONTROL Data Governance]** för att öppna **[!UICONTROL Data Governance]** arbetsyta. På arbetsytan kan du hantera dataanvändningsetiketter på datauppsättningsnivå och fältnivå.

![Fliken Datamängdsstyrning](../images/labels/dataset-governance.png)

Om du vill redigera dataanvändningsetiketter på datauppsättningsnivå börjar du med att välja pennikonen bredvid datauppsättningsnamnet.

![Redigera etiketter på datauppsättningsnivå](../images/labels/dataset-level-edit.png)

The **[!UICONTROL Edit Governance Labels]** öppnas. I dialogrutan markerar du rutorna bredvid de etiketter du vill använda på datauppsättningen. Kom ihåg att dessa etiketter ärvs av alla fält i datauppsättningen. The **[!UICONTROL Applied Labels]** sidhuvudet uppdateras när du markerar varje ruta och visar de etiketter du har valt. När du har markerat de önskade etiketterna väljer du **[!UICONTROL Save Changes]**.

![Tillämpa styrningsetiketter på datauppsättningsnivå](../images/labels/apply-labels-dataset.png)

The **[!UICONTROL Data Governance]** arbetsytan visas igen med etiketter som du har använt på datauppsättningsnivå. Du kan också se att etiketterna ärvs ned till vart och ett av fälten i datauppsättningen.

![Datauppsättningsetiketter ärvda av fält](../images/labels/dataset-labels-applied.png)

Observera att ett&quot;x&quot; visas bredvid etiketterna på datauppsättningsnivå, vilket gör att du kan ta bort etiketterna. De ärvda etiketterna bredvid varje fält har inte något &quot;x&quot; bredvid sig och visas&quot;nedtonade&quot; utan möjlighet att ta bort eller redigera. Det beror på att **ärvda fält är skrivskyddade**, vilket innebär att de inte kan tas bort på fältnivå.

The **[!UICONTROL Show Inherited Labels]** växlingsknappen är aktiverad som standard, vilket gör att du kan se alla etiketter som ärvs ned från datauppsättningen till dess fält. Om du växlar av inaktiveringen döljs alla ärvda etiketter i datauppsättningen.

![Dölj ärvda etiketter](../images/labels/inherited-labels.png)

## Hantera etiketter på datamängdsfältnivå

>[!IMPORTANT]
>
>Användning av etiketter på datamängdsfältnivå stöds bara för datastyrningsanvändning. Om du försöker skapa åtkomstprofiler för data måste du [lägg till etiketter i schemat](../../xdm/tutorials/labels.md) som datauppsättningen baseras på. Se översikten på [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för mer information.

Fortsätta arbetsflödet för [lägga till och redigera etiketter för dataanvändning på datauppsättningsnivå](#add-labels)kan du också hantera fältetiketter i **[!UICONTROL Data Governance]** arbetsyta för den datauppsättningen.

Om du vill använda dataanvändningsetiketter på ett enskilt fält markerar du kryssrutan bredvid fältnamnet och väljer sedan **[!UICONTROL Edit Governance Labels]**.

![Redigera fältetiketter](../images/labels/field-label-edit.png)

The **[!UICONTROL Edit Governance Labels]** visas. I dialogrutan visas rubriker med markerade fält, tillämpade etiketter och ärvda etiketter. Observera att de ärvda etiketterna (C2 och C5) är nedtonade i dialogrutan. De är skrivskyddade etiketter som ärvs från datauppsättningsnivån och kan därför bara redigeras på datauppsättningsnivå.

![Redigera styrningsetiketter för ett enskilt fält](../images/labels/field-label-inheritance.png)

Välj etiketter på fältnivå genom att markera kryssrutan bredvid varje etikett som du vill använda. När du väljer etiketter visas **[!UICONTROL Applied Labels]** huvuduppdateringar för att visa etiketter som används i fälten som visas i **[!UICONTROL Selected Fields]** header. När du har valt etiketter på fältnivå väljer du **[!UICONTROL Save Changes]**.

![Använda etiketter på fältnivå](../images/labels/apply-labels-field.png)

The **[!UICONTROL Data Governance]** arbetsytan visas igen, där de markerade fältetiketterna visas på raden bredvid fältnamnet. Observera att fältnivåetiketten har ett &quot;x&quot; bredvid sig, vilket gör att du kan ta bort etiketten.

![Fält som visar etiketter på fältnivå](../images/labels/field-labels-applied.png)

Du kan upprepa de här stegen om du vill fortsätta lägga till och redigera etiketter på fältnivå för ytterligare fält, inklusive markera flera fält för att använda etiketter på fältnivå samtidigt.

![Markera flera fält om du vill använda etiketter på fältnivå samtidigt.](../images/labels/multiple-fields.png)

Det är viktigt att komma ihåg att arv endast flyttas från den översta nivån nedåt (datamängd → fält), vilket innebär att etiketter som används på fältnivå inte sprids till andra fält eller datamängder.

## Hantera etiketter på schemanivå

Du kan lägga till etiketter direkt i ett eller flera scheman inom det schemat. Alla fält som används på schemanivå sprids till alla datauppsättningar som baseras på det schemat.

Se självstudiekursen om [hantera etiketter på schemanivå](../../xdm/tutorials/labels.md) för mer information.

## Hantera anpassade etiketter {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Skapa etiketter"
>abstract="Med etiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Platform har en standarduppsättning med etiketter som du kan använda, men du kan också skapa anpassade etiketter som är specifika för din organisation."

Du kan skapa egna anpassade användningsetiketter i **[!UICONTROL Policies]** arbetsytan i [!DNL Experience Platform] Gränssnitt. Välj **[!UICONTROL Policies]** i den vänstra navigeringen väljer du **[!UICONTROL Labels]** om du vill visa en lista med befintliga etiketter. Här väljer du **[!UICONTROL Create label]**.

![](../images/labels/create-label-btn.png)

The **[!UICONTROL Create label]** visas. Här anger du följande information för den nya etiketten:

* **[!UICONTROL Identifier]**: En unik identifierare för etiketten. Detta värde används för uppslagsändamål och bör därför vara kort och koncist.
* **[!UICONTROL Name]**: Ett visningsnamn för etiketten.
* **[!UICONTROL Description]**: (Valfritt) En beskrivning av etiketten som ger ytterligare kontext.

När du är klar väljer du **[!UICONTROL Create]**.

![](../images/labels/create-label.png)

Dialogrutan stängs och den nya anpassade etiketten visas i listan under **[!UICONTROL Labels]** -fliken.

![](../images/labels/label-created.png)

Etiketten kan nu väljas under **[!UICONTROL Custom Labels]** när du redigerar användningsetiketter för datauppsättningar och fält, eller när du skapar dataanvändningsprinciper.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Nästa steg

Nu när du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till [!DNL Experience Platform]. Om du vill veta mer kan du börja med att läsa [dokumentation om dataöverföring](../../ingestion/home.md).

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i [dataanvändningsprinciper - översikt](../policies/overview.md).

## Ytterligare resurser

Följande video är avsedd att ge stöd för din förståelse av datastyrning och visar hur du använder etiketter på en datamängd och enskilda fält.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
