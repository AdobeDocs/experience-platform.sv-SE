---
keywords: Experience Platform;hem;populära ämnen;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience data model;data model;data model;explore;class;field group;data type;schema;
solution: Experience Platform
title: Utforska schemaresurser i användargränssnittet
description: Lär dig utforska befintliga scheman, klasser, schemafältgrupper och datatyper i användargränssnittet i Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Utforska schemaresurser i användargränssnittet

I Adobe Experience Platform lagras alla XDM-schemaresurser (Experience Data Model) i [!DNL Schema Library], inklusive standardresurser från Adobe och anpassade resurser som definierats av din organisation. I användargränssnittet i Experience Platform kan du visa strukturen och fälten för befintliga scheman, klasser, fältgrupper eller datatyper i [!DNL Schema Library]. Detta är särskilt användbart när du planerar och förbereder för dataöverföring, eftersom användargränssnittet ger information om de förväntade datatyperna och användningsexemplen för varje fält som tillhandahålls av dessa XDM-resurser.

Den här självstudiekursen beskriver stegen för att utforska befintliga scheman, klasser, fältgrupper och datatyper i användargränssnittet för Experience Platform.

## Söka efter en schemaresurs {#lookup}

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen. The [!UICONTROL Schemas] arbetsytan innehåller **[!UICONTROL Browse]** för att utforska alla scheman i organisationen, tillsammans med ytterligare dedikerade flikar för att utforska **[!UICONTROL Classes]**, **[!UICONTROL Field groups]** och **[!UICONTROL Data types]** respektive.

![](../images/ui/explore/tabs.png)

Filterikonen (![Filterikonbild](../images/ui/explore/icon.png)) visar kontroller i den vänstra listen för att begränsa listade resultat. Vilka kontroller som visas varierar beroende på vilken typ av resurs som visas.

Om du till exempel vill filtrera listan så att endast standarddatatyper som tillhandahålls av Adobe visas väljer du **[!UICONTROL Datatype]** och **[!UICONTROL Adobe]** under **[!UICONTROL Type]** och **[!UICONTROL Owner]** -avsnitt.

The **[!UICONTROL Included in Profile]** kan du filtrera resultaten så att endast resurser som används i scheman som har aktiverats för användning i [Kundprofil i realtid](../../profile/home.md).

![](../images/ui/explore/filter.png)

När resurser listas på **[!UICONTROL Classes]**, **[!UICONTROL Field groups]**, eller **[!UICONTROL Data types]** -flikar kan du välja **[!UICONTROL Adobe]** för att endast visa standardresurser eller **[!UICONTROL Customer]** om du bara vill visa resurser som har skapats av din organisation.

![](../images/ui/explore/filter-data-type.png)

Du kan även använda sökfältet för att begränsa resultaten ytterligare.

![](../images/ui/explore/search.png)

Resurserna som visas i sökresultaten ordnas först efter matchningar av titel och sedan efter matchningar av beskrivning. Ju fler ord som matchar i någon av dessa kategorier, desto högre visas resursen i listan.

När du har hittat resursen som du vill utforska väljer du resursens namn i listan för att visa dess struktur på arbetsytan.

## Utforska en XDM-resurs på arbetsytan {#explore}

När du har valt en resurs öppnas dess struktur på arbetsytan.

![](../images/ui/explore/canvas.png)

Alla objekttypsfält som innehåller underegenskaper komprimeras som standard när de först visas på arbetsytan. Om du vill visa underegenskaperna för ett fält markerar du ikonen bredvid namnet.

![](../images/ui/explore/field-expand.png)

### Systemgenererade fält {#system-fields}

Vissa fältnamn har ett understreck, till exempel `_repo` och `_id`. Dessa representerar platshållare för fält som systemet automatiskt genererar och tilldelar när data hämtas.

Därför bör de flesta av dessa fält uteslutas från datastrukturen när de hämtas till Platform. Det huvudsakliga undantaget för den här regeln är [`_{TENANT_ID}` fält](../api/getting-started.md#know-your-tenant_id), som alla XDM-fält som skapas under din organisation måste namnges under.

### Datatyper {#data-types}

För varje fält som visas på arbetsytan visas dess motsvarande datatyp bredvid namnet, vilket i en snabbtitt anger vilken typ av data som fältet förväntar sig för inmatning.

![](../images/ui/explore/data-types.png)

Alla datatyper som läggs till med hakparenteser (`[]`) representerar en array med den aktuella datatypen. En datatyp med **[!UICONTROL String]\[]** anger att fältet förväntar sig en array med strängvärden. En datatyp för **[!UICONTROL Payment Item]\[]** anger en array med objekt som följer [!UICONTROL Payment Item] datatyp.

Om ett matrisfält baseras på en objekttyp kan du markera dess ikon på arbetsytan för att visa de förväntade attributen för varje matrisobjekt.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

När du markerar namnet på ett fält på arbetsytan uppdateras den högra listen så att information om fältet visas under **[!UICONTROL Field properties]**. Detta kan bland annat innehålla en beskrivning av fältets avsedda användningsfall, standardvärden, mönster, format, oavsett om fältet är obligatoriskt eller inte.

![](../images/ui/explore/field-properties.png)

Om fältet som du inspekterar är ett uppräkningsfält, visar den högra listen även de värden som fältet förväntar sig att ta emot.

![](../images/ui/explore/enum-field.png)

### Identitetsfält {#identity}

När du inspekterar scheman som innehåller identitetsfält visas dessa fält i den vänstra listen under den klass eller fältgrupp som tillhandahåller dem till schemat. Markera namnet på identitetsfältet i den vänstra listen för att visa fältet på arbetsytan, oavsett hur djupt det är kapslat.

Identitetsfält markeras på arbetsytan med en fingeravtrycksikon (![Fingeravtrycksikonbild](../images/ui/explore/identity-symbol.png)). Om du väljer identitetsfältets namn kan du visa ytterligare information, till exempel [identity namespace](../../identity-service/namespaces.md) och om fältet är den primära identiteten för schemat eller inte.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Se guiden [definiera identitetsfält](./fields/identity.md) om du vill ha mer information om identitetsfält och deras relation med plattformstjänster längre fram i kedjan.

### Relationsfält {#relationship}

Om du inspekterar ett schema som innehåller ett relationsfält visas fältet i den vänstra listen under **[!UICONTROL Relationships]**. Markera relationsfältets namn i den vänstra listen för att visa fältet på arbetsytan, oavsett hur djupt det är kapslat.

Relationsfält markeras också unikt på arbetsytan och visar namnet på målschemat som fältet refererar till. Om du väljer relationsfältets namn kan du visa identitetsnamnområdet för målschemats primära identitet i den högra listen.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Se självstudiekursen om [skapa en relation i användargränssnittet](../tutorials/relationship-ui.md) för mer information om hur relationer används i XDM-scheman.

## Nästa steg

I det här dokumentet beskrivs hur du utforskar befintliga XDM-resurser i användargränssnittet i Experience Platform. Mer information om de olika funktionerna i [!UICONTROL Schemas] arbetsyta och [!DNL Schema Editor], se [[!UICONTROL Schemas] arbetsyta - översikt](./overview.md).
