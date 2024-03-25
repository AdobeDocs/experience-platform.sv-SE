---
keywords: Experience Platform;hemanvändare;populära ämnen;datastyrning;dataanvändningsetikett;policytjänst;användarhandbok för dataanvändningsetiketter
solution: Experience Platform
title: Hantera dataanvändningsetiketter i användargränssnittet
description: Den här guiden innehåller steg för hur du arbetar med dataanvändningsetiketter i Adobe Experience Platform användargränssnitt.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: ea58ece75d2208ae96bd71c2f51e14279769640f
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---

# Hantera etiketter för dataanvändning i användargränssnittet {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Styrd dataanvändning i plattformen"
>abstract="<h2>Beskrivning</h2><p>Med ramverket för datastyrning i Experience Platform kan ni märka attribut och scheman enligt dataanvändningsbegränsningar och skapa policyer som identifierar och följer dessa begränsningar för specifika marknadsföringsåtgärder.</p>"

Den här användarhandboken innehåller steg för att arbeta med dataanvändningsetiketter i [!DNL Experience Platform] användargränssnitt.

## Hantera etiketter {#manage-labels}

Om du vill använda etiketter på dina data måste du ha **[!UICONTROL Manage Usage Labels]** behörighet för användning i standardproduktionssandlådan prod. Om du vill skapa en anpassad etikett måste du även ha administratörsbehörighet för produktprofilen. Varje organisation har bara en lista över tillämpliga etiketter, och för närvarande stöds inte borttagning av etiketter.

Se guiden om hur man [konfigurera behörigheter](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html) eller [åtkomstkontroll - översikt](../../access-control/home.md) för mer information om hur du tilldelar en behörighet. Kontakta din organisations administratör om du inte har tillgång till Admin Console för din organisation.

## Hantera etiketter på schemanivå

Du kan lägga till etiketter direkt i ett eller flera scheman inom det schemat. Alla fält som används på schemanivå sprids till alla datauppsättningar som baseras på det schemat.

>[!NOTE]
>
>Om dina dataanvändningsprinciper skapades innan du gav fältet en etikett kan du stöta på en dialogruta om brott mot styrningsprinciper när du tillämpar etiketter på det nya schemat. Den här dialogrutan anger att användningen av den här etiketten bryter mot en befintlig användarprofil. Använd datalänksdiagrammet för att förstå vilka andra konfigurationsändringar som behöver göras innan du kan lägga till etiketten i schemafältet.
>
>![Dialogrutan med en sammanfattning av överträdelser och datalänksdiagram har markerats vid överträdelse av datahanteringsprincipen.](../images/labels/policy-violation-dialog.png)
>
>Se [policyöverträdelse av dataanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/auto-enforcement#data-usage-violation) om du vill ha mer information om partiella policyöverträdelser.

För att kunna hantera dataanvändningsetiketter på schemanivå måste du välja ett befintligt schema eller skapa ett nytt. När du har loggat in på Adobe Experience Platform väljer du **[!UICONTROL Schemas]** till vänster för att öppna **[!UICONTROL Schemas]** arbetsyta. På den här sidan visas alla scheman som du har skapat och användbar information om varje schema.

![Adobe Experience Platform-gränssnittet med fliken Schema markerad.](../images/labels/schema-tab.png)

I nästa avsnitt beskrivs hur du skapar ett nytt schema som du kan använda etiketter på. Om du vill redigera etiketter för ett befintligt schema väljer du schemat i listan och går vidare till [lägga till etiketter för dataanvändning i schemat](#add-labels).

### Skapa ett nytt schema

Om du vill skapa ett nytt schema väljer du **[!UICONTROL Create schema]** i det övre högra hörnet av **[!UICONTROL Schemas]** arbetsyta. Se guiden på [hur du skapar ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md#create) för fullständiga instruktioner. Du kan också [skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md) vid behov.

### Lägga till dataanvändningsetiketter i ett schema {#add-labels-to-schema}

När du har skapat ett nytt schema eller valt ett befintligt schema i listan i [!UICONTROL Browse] -fliken i [!UICONTROL Schemas] på arbetsytan väljer du ett fält från schemat i Schemaredigeraren. I [!UICONTROL Field properties] sidlist, välj **[!UICONTROL Apply Access and Data Governance Labels]**.

![Fliken Struktur på arbetsytan Scheman som visar hur ditt schema ser ut med etiketterna Använd åtkomst och Datastyrning markerade.](../images/labels/schema-label-governance.png)

En dialogruta visas där du kan använda och hantera dataanvändningsetiketter på schemanivå och fältnivå. Se självstudiekursen för XDM för fullständiga instruktioner om [lägga till eller redigera dataanvändningsetiketter för XDM-scheman](../../xdm/tutorials/labels.md#select-schema-field).

### Lägga till etiketter för dataanvändning i en viss datauppsättning {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instruktioner"
>abstract="<ol><li>Välj <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html">Datauppsättningar</a> i den vänstra navigeringen markerar du den datauppsättning vars data du vill begränsa.</li><li>I vyn med datauppsättningsinformation väljer du <b>Datastyrning</b> -fliken.</li><li>Markera de datauppsättningsfält som du vill begränsa och välj sedan <b>Redigera styrningsetiketter</b> för att märka data baserat på användningsbegränsningar.</li><li>När du har etiketterat dina data väljer du <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html">Profiler</a> i den vänstra navigeringen väljer du <b>Skapa princip</b>.</li><li>Välj om du vill skapa en <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">Styrningspolicy för data</a>markerar du de dataanvändningsetiketter som profilen ska använda för profilen.</li><li>Välj de marknadsföringsåtgärder som profilen nekar för alla data som innehåller dessa etiketter. När profilen har skapats markerar du den i listan och aktiverar den med hjälp av växlingsknappen till höger.</li><li>För varje aktiverad princip förhindrar Platform att data som innehåller de angivna etiketterna används för definierade marknadsföringsåtgärder. Detta görs automatiskt när du försöker aktivera märkta data till ett mål med associerade marknadsföringsåtgärder (användningsfall).</li></ol>"

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Etiketter som tidigare använts på datauppsättningens objektnivå stöds fortfarande i plattformsgränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. I dokumentationen finns instruktioner om [hur du migrerar tidigare använda etiketter från datauppsättningen till schemanivån](../e2e.md#migrate-labels).

Etiketter kan användas på hela datauppsättningen från **[!UICONTROL Data Governance]** -fliken i **[!UICONTROL Datasets]** arbetsyta. På arbetsytan kan du hantera dataanvändningsetiketter på datauppsättningsnivå.

![The [!UICONTROL Data Governance] -fliken i [!UICONTROL Datasets] arbetsyta med datastyrning markerad.](../images/labels/dataset-governance.png)

Om du vill redigera dataanvändningsetiketter på datauppsättningsnivå börjar du med att välja pennikonen (![En pennikon.](../images/labels/edit-icon.png)) på datamängdens rad.

![The [!UICONTROL Data Governance] -fliken i [!UICONTROL Datasets] arbetsytan med ikonen Redigera penna markerad.](../images/labels/dataset-level-edit.png)

The **[!UICONTROL Edit Governance Labels]** öppnas. I dialogrutan markerar du rutorna bredvid de etiketter du vill använda på datauppsättningen. Kom ihåg att dessa etiketter ärvs av alla fält i datauppsättningen. The **[!UICONTROL Applied Labels]** sidhuvudet uppdateras när du markerar varje ruta och visar de etiketter du har valt. När du har markerat de önskade etiketterna väljer du **[!UICONTROL Save Changes]**.

![Dialogrutan Redigera styrningsetiketter med kryssrutorna Etikett och Spara ändringar markerade.](../images/labels/apply-labels-dataset.png)

The **[!UICONTROL Data Governance]** arbetsytan visas igen med de etiketter som du har använt på datauppsättningsnivå i den första raden i tabellen. Du kan också se etiketterna, som anges med enskilda kort, som ärvs ned till vart och ett av fälten i datauppsättningen.

![The [!UICONTROL Data Governance] -fliken i [!UICONTROL Datasets] arbetsyta med tillämpade etiketter på datauppsättningsnivå och ärvda etiketter för datauppsättningsfält markerade.](../images/labels/applied-dataset-labels.png)

### Ta bort etiketter från en datauppsättning {#remove-labels-from-a-dataset}

Etiketter som läggs till på datauppsättningsnivå har &quot;x&quot; bredvid kortet. På så sätt kan du ta bort etiketterna från hela datauppsättningen. Ärvda etiketter bredvid varje fält saknar&quot;x&quot; och visas&quot;nedtonade&quot;. Dessa **ärvda etiketter är skrivskyddade**, vilket innebär att de inte kan tas bort eller redigeras på fältnivå.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

The **[!UICONTROL Show Inherited Labels]** växlingsknappen är aktiverad som standard, vilket gör att du kan se alla etiketter som ärvts ned från schemat till dess fält. Om du växlar av inaktiveringen döljs alla ärvda etiketter i datauppsättningen.

![Fliken Datastyrning på arbetsytan Datauppsättningar med växeln Visa ärvda etiketter markerad.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Etiketter som tillämpades innan funktionen för datauppsättningsetiketter var föråldrad kan tas bort från datauppsättningen genom att hitta den relevanta datauppsättningen och välja ikonen för att avbryta på etiketten.
>![Fliken Datastyrning på arbetsytan Datauppsättningar med en borttagbar etikett markerad.](../images/labels/remove-governance-labels.png)
>I dokumentationen finns instruktioner om [hur du migrerar tidigare använda etiketter från datauppsättningen till schemanivån](../e2e.md#migrate-labels).

## Hantera anpassade etiketter {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Skapa etiketter"
>abstract="Med etiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Platform har en standarduppsättning med etiketter som du kan använda, men du kan också skapa anpassade etiketter som är specifika för din organisation."

Du kan skapa egna anpassade användningsetiketter i **[!UICONTROL Policies]** arbetsytan i [!DNL Experience Platform] Gränssnitt. Välj **[!UICONTROL Policies]** i den vänstra navigeringen väljer du **[!UICONTROL Labels]** om du vill visa en lista med befintliga etiketter. Välj **[!UICONTROL Create label]**.

![Arbetsytan Profiler med Skapa profil markerad.](../images/labels/create-label-btn.png)

The **[!UICONTROL Create label]** visas. Här anger du följande information för den nya etiketten:

* **[!UICONTROL Name]**: En unik identifierare för etiketten. Detta värde används för uppslagsändamål och bör därför vara kort och koncist.
* **[!UICONTROL Friendly name]**: Ett visningsnamn för etiketten.
* **[!UICONTROL Description]**: (Valfritt) En beskrivning av etiketten för att ge ytterligare kontext.

När du är klar väljer du **[!UICONTROL Create]**.

![Dialogrutan Skapa etikett med Skapa markerat på arbetsytan Profiler.](../images/labels/create-label-dialog.png)

Dialogrutan stängs och den nya anpassade etiketten visas i listan under **[!UICONTROL Labels]** -fliken.

![Fliken Etiketter på arbetsytan Profiler med den nya anpassade etiketten markerad.](../images/labels/label-created.png)

Etiketten kan nu väljas under **[!UICONTROL Custom Labels]** när du redigerar användningsetiketter för datauppsättningar och fält, eller när du skapar dataanvändningsprinciper.

![Dialogrutan Tillämpa åtkomst- och datastyrningsetiketter med anpassade etiketter markerade.](../images/labels/add-custom-label.png)

## Nästa steg

Nu när du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till [!DNL Experience Platform]. Om du vill veta mer börjar du med att läsa [dokumentation om dataöverföring](../../ingestion/home.md).

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i [dataanvändningsprinciper - översikt](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
