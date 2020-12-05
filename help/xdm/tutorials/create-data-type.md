---
keywords: Experience Platform;home;popular topics;ui;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create;data type;data types;
solution: Experience Platform
title: Skapa och redigera datatyper med hjälp av användargränssnittet i schemaregistret
topic: tutorial
type: Tutorial
description: I den här självstudien används användargränssnittet för Experience Platform för att vägleda dig genom stegen för att skapa en anpassad datatyp.
translation-type: tm+mt
source-git-commit: 9008b49e1eb5e32b0f4cda7049bf873c689f6442
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---


# Skapa och redigera datatyper med användargränssnittet i Experience Platform

I Experience Data Model (XDM) används datatyper som referenstypfält i klasser eller blandningar på samma sätt som grundläggande litteralfält, med den största skillnaden är att datatyper kan definiera flera delfält. Även om de liknar blandningar i genom att de medger konsekvent användning av en struktur med flera fält, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan mixar bara kan läggas till på rotnivån.

Adobe Experience Platform har många standarddatatyper som kan användas för ett stort antal vanliga användningsfall för upplevelsehantering. Men du kan också definiera egna anpassade datatyper för att tillgodose dina unika affärsbehov.

I den här självstudiekursen beskrivs stegen för att skapa och redigera anpassade datatyper i användargränssnittet för plattformen.

## Förutsättningar

Den här självstudiekursen kräver en fungerande förståelse för XDM System. Se översikten över [](../home.md) XDM för en introduktion till XDM:s roll i ekosystemet Experience Platform och [grunderna i schemakomposition](../schema/composition.md) för hur datatyper bidrar till XDM-scheman.

Även om det inte krävs för den här självstudiekursen rekommenderar vi att du också följer självstudiekursen om hur du [komponerar ett schema i användargränssnittet](./-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Öppna [!DNL Schema Editor] för en datatyp

I plattformsgränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna [!UICONTROL Schemas] arbetsytan och sedan **[!UICONTROL Data types]** fliken. En lista över tillgängliga datatyper visas, inklusive de som definieras av Adobe samt de som skapats av din organisation.

![](../images/tutorials/create-datatype/data-types-tab.png)

Här finns två alternativ:

* [Skapa en ny datatyp](#create)
* [Välj en befintlig datatyp att redigera](#edit)

### Skapa en ny datatyp {#create}

From the **[!UICONTROL Data types]** tab, select **[!UICONTROL Create data type]**.

![](../images/tutorials/create-datatype/create.png)

Den [!DNL Schema Editor] visas med den aktuella strukturen för den nya datatypen på arbetsytan. Till höger om redigeraren kan du ange ett visningsnamn och en valfri beskrivning av datatypen. Se till att du anger ett unikt och koncist namn för din datatyp, eftersom det är så det identifieras när du lägger till den i ett schema.

I den här självstudien skapas en datatyp som beskriver en restaurangegenskap, så datatypen får visningsnamnet &quot;Restaurant&quot;.

![](../images/tutorials/create-datatype/data-type-properties.png)

Gå vidare till [nästa avsnitt](#add-fields) för att börja lägga till fält i datatypen.

### Redigera en befintlig datatyp

Endast anpassade datatyper som definieras av din organisation kan redigeras. Om du vill begränsa den visade listan väljer du filterikonen (![Filterikon](../images/tutorials/create-datatype/filter.png)) för att visa kontroller för filtrering baserat på [!UICONTROL Owner]. Välj **[!UICONTROL Customer]** om du bara vill visa anpassade datatyper som ägs av din organisation.

Välj den datatyp som du vill redigera i listan för att öppna den högra listen och visa information om datatypen. Markera namnet på datatypen i den högra listen för att öppna dess struktur i [!DNL Schema Editor].

![](../images/tutorials/create-datatype/edit.png)

## Lägg till fält i datatypen {#add-fields}

Om du vill börja lägga till fält i datatypen väljer du **plusikonen (+)** bredvid rotnivåfältet på arbetsytan. Ett nytt fält visas nedan och den högra listen uppdateras för att visa kontroller för det nya fältet.

![](../images/tutorials/create-datatype/new-field.png)

Använd kontrollerna för höger spår för att ange en **[!UICONTROL Field name]**, **[!UICONTROL Display name]** och **[!UICONTROL Type]** för fältet. Observera att ett fälts typ kan vara en grundläggande skalär typ (till exempel en sträng, ett heltal eller ett booleskt värde), eller kan representera en annan datatyp med flera fält som definieras av Adobe eller din organisation.

Datatypen Restaurant kräver ett strängfält som representerar restaurangens namn. Därför [!UICONTROL Field name] anges &quot;name&quot; och [!UICONTROL Type] anges som [!UICONTROL String]. Välj **[!UICONTROL Apply]** om du vill använda ändringarna i fältet.

![](../images/tutorials/create-datatype/name-field.png)

Fortsätt med samma process när du lägger till ytterligare fält, och börja med att välja **plusikonen (+)** bredvid rotnivåfältet och ange konfigurationsinformationen i den högra listen.

Datatypen Restaurant har nu ytterligare fält för märke, sittplatskapacitet och golvutrymme.

![](../images/tutorials/create-datatype/more-fields.png)

Förutom grundläggande fält kan du även kapsla in ytterligare datatyper i din anpassade datatyp. Datatypen Restaurant kräver till exempel ett fält som representerar egenskapens fysiska adress. I det här fallet kan du lägga till ett nytt adressfält som tilldelas standarddatatypen &quot;[!UICONTROL Postal address]&quot;.

![](../images/tutorials/create-datatype/address-field.png)

Detta visar hur flexibla datatyper kan vara när det gäller att beskriva dina data: datatyper kan använda fält som också är datatyper, som i sin tur kan innehålla fler datatyper, osv. På så sätt kan du abstrahera och återanvända vanliga datamönster i hela XDM-scheman, vilket gör det enklare att representera komplexa datastrukturer.

När du är klar med att lägga till fält till datatypen väljer du **[!UICONTROL Save]** att spara ändringarna och lägga till datatypen i [!DNL Schema Library].

## Lägg till datatypen i en blandning

När du har skapat en datatyp kan du börja använda den i dina scheman. Eftersom XDM-scheman består av en klass och noll eller flera blandningar, kan fält som tillhandahålls av en datatyp inte läggas till direkt i ett schema. De måste i stället ingå i en klass eller en blandning.

>[!NOTE]
>
>I det här avsnittet fokuseras på att lägga till en datatyp i en blandning, eftersom detta är det vanligaste mönstret för anpassade datatyper. Du kan i stället använda samma steg för att lägga till datatypen i en klass.

Du kan lägga till datatypen i en befintlig blandning eller skapa en ny blandning helt och hållet. I båda fallen måste du öppna [!DNL Schema Editor] för ett schema som du tänker lägga till den nya datatypen i, antingen genom att välja ett befintligt schema på **[!UICONTROL Browse]** fliken eller genom att skapa ett helt nytt schema.

När du har schemat öppet i [!DNL Schema Editor]markerar du den blandning du vill lägga till datatypen i i den vänstra listen. Om schemat inte har någon lämplig blandning följer du stegen för att [skapa en ny blandning](./create-schema-ui.md#define-mixin) som ska läggas till i schemat i stället och kontrollerar att mixinen är markerad i den vänstra listen.

![](../images/tutorials/create-datatype/mixin-selected.png)

Välj **plusikonen (+)** bredvid schemats namn för att lägga till ett nytt fält i den valda mixen. När du väljer egenskapen **[!UICONTROL Type]** för fältet är namnet på datatypen som du skapade tidigare nu tillgängligt i listrutan. Du kan börja skriva namnet på datatypen för att enklare hitta den.

![](../images/tutorials/create-datatype/add-data-type.png)

Välj datatyp i listan och välj sedan **[!UICONTROL Apply]**. Schemafältet uppdateras på arbetsytan för att visa de strukturerade underfälten som datatypen ger. Om du sparar schemat genom att markera **[!UICONTROL Save]** det sparas även mixinen så att du kan återanvända den i ytterligare scheman som tillhör samma klass.

![](../images/tutorials/create-datatype/data-type-added.png)

>[!NOTE]
>
>Blandningar är bara kompatibla med en klass. Om du vill använda din datatyp i ytterligare scheman som baseras på olika klasser, måste du följa stegen ovan för att lägga till datatypen i ytterligare blandningar som är avsedda att utöka dessa klasser.

## Nästa steg

I den här självstudien beskrivs hur du skapar och redigerar datatyper och hur du lägger till dem i blandningar med hjälp av [!DNL Schema Editor]. Mer information om hur du arbetar med datatyper i användargränssnittet, inklusive hur du konverterar ett flerfältsobjekt till en datatyp finns i självstudiekursen [för att skapa](./create-schema-ui.md#datatype)scheman.

Mer information om hur du skapar en datatyp med API:t för schemaregister finns i [datatypens slutpunktshandbok](../api/data-types.md#create).