---
title: Hantera dataanvändningsetiketter för ett schema
description: Lär dig hur du lägger till dataanvändningsetiketter i XDM-schemafält (Experience Data Model) i Adobe Experience Platform-gränssnittet.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 37395e5762c8d54e6fca5c3502bdbf56f5b5472c
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Hantera dataanvändningsetiketter för ett schema

>[!IMPORTANT]
>
>Schemabaserad märkning ingår i [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md), som för närvarande finns i en begränsad version för USA-baserade vårdkunder. Den här funktionen kommer att vara tillgänglig för alla Adobe Real-time Customer Data Platform-kunder när den släpps helt.

Alla data som hämtas till Adobe Experience Platform begränsas av XDM-scheman (Experience Data Model). Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. För att ta hänsyn till detta kan du med hjälp av plattformen begränsa användningen av vissa datauppsättningar och fält genom att använda [etiketter för dataanvändning](../../data-governance/labels/overview.md).

En etikett som används i ett schemafält anger de användningsprinciper som gäller för data i det specifika fältet.

Etiketter kan användas på enskilda scheman och fält i dessa scheman. När etiketter används direkt i ett schema sprids dessa etiketter till alla befintliga och framtida datauppsättningar som baseras på det schemat.

Dessutom sprids alla fältetiketter som du lägger till i ett schema till alla andra scheman som använder samma fält från en delad klass eller fältgrupp. Detta bidrar till att säkerställa att användningsreglerna för liknande fält är konsekventa i hela datamodellen.

I den här självstudiekursen beskrivs stegen för hur du lägger till etiketter i ett schema med Schemaredigeraren i plattformsgränssnittet.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Schemaredigeraren](../ui/overview.md): Lär dig hur du skapar och hanterar scheman och andra resurser i plattformsgränssnittet.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Tillhandahåller infrastrukturen för att genomdriva begränsningar av dataanvändning för plattformsåtgärder, med hjälp av principer som definierar vilka marknadsföringsåtgärder som kan (eller inte kan) utföras på märkta data.

## Välj ett schema eller fält som etiketter ska läggas till i {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Redigera styrningsetiketter"
>abstract="Tillämpa en etikett på ett schemafält för att ange de användningsprinciper som gäller för data i det specifika fältet."

Om du vill lägga till etiketter måste du först [välj ett befintligt schema att redigera](../ui/resources/schemas.md#edit) eller [skapa ett nytt schema](../ui/resources/schemas.md#create) om du vill visa dess struktur i Schemaredigeraren.

Om du vill redigera etiketterna för ett enskilt fält kan du markera fältet på arbetsytan och sedan välja **[!UICONTROL Manage access]** i rätt spår.

>[!IMPORTANT]
>
>Högst 300 etiketter kan användas i alla scheman.

![Välj ett fält på arbetsytan i Schemaredigeraren](../images/tutorials/labels/manage-access.png)

Du kan också välja **[!UICONTROL Labels]** väljer du önskat fält i listan och väljer **[!UICONTROL Apply Access and Data Governance Labels]** i rätt spår.

![Välj ett fält på menyn [!UICONTROL Labels] tab](../images/tutorials/labels/select-field-on-labels-tab.png)

Redigera etiketterna för hela schemat i **[!UICONTROL Labels]** markerar du kryssrutan under filterikonen. Detta markerar alla tillgängliga fält i schemat. Nästa, välj **[!UICONTROL Apply Access and Data Governance Labels]** i rätt spår.

![Välj schemanamnet på menyn [!UICONTROL Labels] tab](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Ett meddelande om ansvarsfriskrivning visas när du för första gången försöker redigera etiketterna för ett schema eller fält och förklarar hur etikettanvändningen påverkar underordnade åtgärder beroende på organisationens principer. Välj **[!UICONTROL Proceed]** för att fortsätta redigera.
>
>![Ansvarsfriskrivning för etikettanvändning](../images/tutorials/labels/disclaimer.png)

## Redigera etiketterna för schemat eller fältet {#edit-labels}

En dialogruta visas där du kan redigera etiketterna för det markerade fältet. Om du har valt ett enskilt fält av objekttyp visas de delfält som de tillämpade etiketterna ska sprida sig till i den högra listen.

![Dialogrutan Tillämpa åtkomst- och datastyrningsetiketter med markerade fält markerade.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Om du redigerar fält för hela schemat listas inte de tillämpliga fälten i den högra listen och schemanamnet visas i stället.

Använd den visade listan för att välja de etiketter som du vill lägga till i schemat eller fältet. När du väljer etiketter visas **[!UICONTROL Applied labels]** så att de etiketter som har markerats hittills visas.

![Dialogrutan Tillämpa åtkomst- och datastyrningsetiketter med de använda etiketterna markerade.](../images/tutorials/labels/applied-labels.png)

Om du vill filtrera de visade etiketterna efter typ väljer du önskad kategori i den vänstra listen. Om du vill skapa en ny egen etikett väljer du **[!UICONTROL Create label]**.

![Dialogrutan Tillämpa åtkomst- och datastyrningsetiketter med ett etiketttypsfilter tillämpat och Skapa etikett markerat.](../images/tutorials/labels/filter-and-create-custom.png)

När du är nöjd väljer du **[!UICONTROL Save]** för att tillämpa dem på fältet eller schemat.

![Dialogrutan Använd åtkomst- och datastyrningsetiketter med Spara markerad.](../images/tutorials/labels/save-labels.png)

The **[!UICONTROL Labels]** visas igen och visar de använda etiketterna för schemat.

![Fliken Etiketter på arbetsytan för scheman med de använda fältetiketterna markerade.](../images/tutorials/labels/field-labels-added.png)

## Nästa steg

I den här guiden beskrivs hur du hanterar etiketter för dataanvändning för scheman och fält. Information om hur du hanterar dataanvändningsetiketter, inklusive hur du lägger till dem i specifika datauppsättningar i stället för på schemanivå, finns i [användargränssnittshandbok för dataanvändningsetiketter](../../data-governance/labels/user-guide.md).
