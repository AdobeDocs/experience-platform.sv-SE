---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Utforska XDM-resurser i användargränssnittet
description: Den här självstudiekursen beskriver stegen för att utforska befintliga scheman, klasser, blandningar och datatyper i användargränssnittet för Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 49d37cdf14bd03b62fe64116842bacd0f806e5ce
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Utforska XDM-resurser i användargränssnittet

I Adobe Experience Platform lagras alla XDM-resurser (Experience Data Model) i [!DNL Schema Library], inklusive standardresurser från Adobe och anpassade resurser som definierats av din organisation. I användargränssnittet i Experience Platform kan du visa strukturen och fälten för befintliga scheman, klasser, mixin och datatyper i [!DNL Schema Library]. Detta är särskilt användbart när du planerar och förbereder för dataöverföring, eftersom användargränssnittet ger information om de förväntade datatyperna och användningsexemplen för varje fält som tillhandahålls av dessa XDM-resurser.

Den här självstudiekursen beskriver stegen för att utforska befintliga scheman, klasser, blandningar och datatyper i användargränssnittet för Experience Platform.

## Söka efter en XDM-resurs {#lookup}

In the Platform UI, select **[!UICONTROL Schemas]** in the left navigation. På arbetsytan [!UICONTROL Schemas] finns en **[!UICONTROL Browse]** flik där du kan utforska alla befintliga XDM-resurser i organisationen, tillsammans med ytterligare dedikerade flikar för utforska **[!UICONTROL Classes]**, **[!UICONTROL Mixins]** och **[!UICONTROL Data types]** specifikt.

![](../images/tutorials/explore/tabs.png)

På [!UICONTROL Browse] fliken kan du använda filterikonen (![Filterikonbild](../images/tutorials/explore/icon.png)) för att visa kontroller i den vänstra listen för att begränsa listade resultat.

Om du till exempel vill filtrera listan så att endast standarddatatyper som tillhandahålls av Adobe visas, markerar du **[!UICONTROL Datatype]** och **[!UICONTROL Adobe]** under **[!UICONTROL Type]** - respektive **[!UICONTROL Owner]** -avsnitten.

Med **[!UICONTROL Included in Profile]** växlingsknappen kan du filtrera resultat så att endast resurser som används i scheman som har aktiverats för användning i [kundprofilen](../../profile/home.md)i realtid visas.

![](../images/tutorials/explore/filter.png)

Du kan också använda sökfältet för att begränsa resultaten till resurser vars namn matchar sökfrågan.

![](../images/tutorials/explore/search.png)

När du har hittat resursen som du vill utforska väljer du resursens namn i listan för att visa dess struktur på arbetsytan.

## Utforska en XDM-resurs på arbetsytan {#explore}

När du har valt en resurs öppnas dess struktur på arbetsytan.

![](../images/tutorials/explore/canvas.png)

Alla objekttypsfält som innehåller underegenskaper komprimeras som standard när de först visas på arbetsytan. Om du vill visa underegenskaperna för ett fält markerar du ikonen bredvid namnet.

![](../images/tutorials/explore/field-expand.png)

### Systemgenererade fält {#system-fields}

Vissa schemafält har ett understreck, till exempel `_repo` och `_id`. Dessa representerar platshållare för fält som systemet automatiskt genererar och tilldelar när data hämtas.

Därför bör de flesta av dessa fält exkluderas från datastrukturen när de hämtas till Platform, med det huvudsakliga undantaget är `_{TENANT_ID}` fältet som alla XDM-fält som skapats under organisationen måste namnges under.

### Datatyper {#data-types}

För varje fält som visas på arbetsytan visas dess motsvarande datatyp bredvid namnet, vilket i en snabbtitt anger vilken typ av data som fältet förväntar sig för inmatning.

Alla datatyper som läggs till med hakparenteser (`[]`) representerar en array med den aktuella datatypen. En datatyp av **[!UICONTROL String]\[]** anger till exempel att fältet förväntar sig en array med strängvärden. Datatypen **[!UICONTROL Payment Item]\[]** anger en array med objekt som överensstämmer med [!UICONTROL Payment Item] datatypen.

Om ett matrisfält baseras på en objekttyp kan du markera dess ikon på arbetsytan för att visa de förväntade attributen för varje matrisobjekt.

![](../images/tutorials/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

När du markerar namnet på ett fält på arbetsytan uppdateras den högra listen så att information om det fältet visas under **[!UICONTROL Field properties]**. Detta kan bland annat innehålla en beskrivning av fältets avsedda användningsfall, standardvärden, mönster, format, oavsett om fältet är obligatoriskt eller inte.

![](../images/tutorials/explore/field-properties.png)

Om fältet som du inspekterar är ett uppräkningsfält, visar den högra listen även de värden som fältet förväntar sig att ta emot.

![](../images/tutorials/explore/enum-field.png)

### Identitetsfält {#identity}

När du undersöker scheman som innehåller identitetsfält markeras dessa fält på arbetsytan med en fingeravtrycksikon (![Fingeravtrycksikonbild](../images/tutorials/explore/identity-symbol.png)). Om du väljer identitetsfältets namn kan du visa ytterligare information, till exempel [identitetsnamnutrymmet](../../identity-service/namespaces.md) och om fältet är den primära identiteten för schemat eller inte.

![](../images/tutorials/explore/identity-field.png)

### Relationsfält {#relationship}

Relationsfält markeras också unikt på arbetsytan och visar namnet på målschemat som fältet refererar till. Om du väljer relationsfältets namn kan du visa identitetsnamnområdet för målschemats primära identitet.

![](../images/tutorials/explore/relationship-field.png)

>[!NOTE]
>
>Mer information om hur du använder relationer i XDM-scheman finns i självstudiekursen [om hur du skapar en relation i användargränssnittet](./create-schema-ui.md) .

## Nästa steg

I det här dokumentet beskrivs hur du utforskar befintliga XDM-resurser i användargränssnittet i Experience Platform. Mer information om de olika funktionerna på [!UICONTROL Schemas] arbetsytan och [!DNL Schema Editor]finns i självstudiekursen [för att skapa](./create-schema-ui.md)scheman.