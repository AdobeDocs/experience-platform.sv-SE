---
keywords: Experience Platform;hem;populära ämnen;ui;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;schema;schema;scheman;scheman;scheman;scheman;create;data type;data types;
solution: Experience Platform
title: Skapa och redigera datatyper med användargränssnittet
type: Tutorial
description: Lär dig hur du skapar och redigerar datatyper i användargränssnittet i Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Skapa och redigera datatyper med användargränssnittet

I Experience Data Model (XDM) är datatyper återanvändbara fält som innehåller flera underfält. Även om datatyperna liknar schemafältgrupper på så sätt att de medger konsekvent användning av en flerfältsstruktur, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan fältgrupper bara kan läggas till på rotnivån.

Adobe Experience Platform har många standarddatatyper som kan användas för ett stort antal vanliga användningsfall för upplevelsehantering. Men du kan också definiera egna anpassade datatyper för att tillgodose dina unika affärsbehov.

I den här självstudiekursen beskrivs stegen för att skapa och redigera anpassade datatyper i användargränssnittet för plattformen.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) för hur datatyper bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen på [skapa ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Öppna [!DNL Schema Editor] för en datatyp

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna [!UICONTROL Schemas] väljer du **[!UICONTROL Data types]** -fliken. En lista över tillgängliga datatyper visas, inklusive de som definieras av Adobe och de som skapats av din organisation.

![](../../images/ui/resources/data-types/data-types-tab.png)

Här finns två alternativ:

- [Skapa en ny datatyp](#create)
- [Välj en befintlig datatyp att redigera](#edit)

### Skapa en ny datatyp {#create}

På fliken **[!UICONTROL Data types]** väljer du **[!UICONTROL Create data type]**.

![](../../images/ui/resources/data-types/create.png)

The [!DNL Schema Editor] visas med den aktuella strukturen för den nya datatypen på arbetsytan. Till höger om redigeraren kan du ange ett visningsnamn och en valfri beskrivning av datatypen. Se till att du anger ett unikt och koncist namn för din datatyp, eftersom det är så det identifieras när du lägger till den i ett schema.

I den här självstudien skapas en datatyp som beskriver en restaurangegenskap, så datatypen får visningsnamnet &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Härifrån kan du hoppa fram till [nästa avsnitt](#add-fields) för att börja lägga till fält till den nya datatypen.

### Redigera en befintlig datatyp

>[!NOTE]
>
>När en befintlig datatyp används i ett schema som har aktiverats för användning i kundprofilen i realtid, kan endast icke-förstörande ändringar göras i den datatypen därefter. Se [regler för schemautveckling](../../schema/composition.md#evolution) för mer information.

Endast anpassade datatyper som definieras av din organisation kan redigeras. Om du vill begränsa den visade listan väljer du filterikonen (![Filterikon](../../images/ui/resources/data-types/filter.png)) för att visa kontroller för filtrering baserat på [!UICONTROL Owner]. Välj **[!UICONTROL Customer]** om du bara vill visa anpassade datatyper som ägs av din organisation.

Välj den datatyp som du vill redigera i listan för att öppna den högra listen och visa information om datatypen. Markera namnet på datatypen i den högra listen för att öppna strukturen i [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Lägg till fält i datatypen {#add-fields}

Om du vill börja lägga till fält i datatypen väljer du **plus (+)** -ikonen bredvid rotnivåfältet på arbetsytan. Ett nytt fält visas nedan och den högra listen uppdateras för att visa kontroller för det nya fältet.

![](../../images/ui/resources/data-types/new-field.png)

Använd kontrollerna i den högra listen för att konfigurera information om det nya fältet. Se guiden [definiera fält i användargränssnittet](../fields/overview.md#define) för specifika steg om hur du konfigurerar och lägger till fältet i datatypen.

Datatypen Restaurant kräver ett strängfält som representerar restaurangens namn. Därför är [!UICONTROL Field name] anges som &quot;name&quot; och [!UICONTROL Type] anges som &quot;[!UICONTROL String]&quot;. Välj **[!UICONTROL Apply]** för att tillämpa ändringarna på fältet.

![](../../images/ui/resources/data-types/name-field.png)

Fortsätt lägga till fler fält till datatypen efter behov. Datatypen Restaurant har nu ytterligare fält för märke, sittplatskapacitet och golvutrymme.

![](../../images/ui/resources/data-types/more-fields.png)

Förutom grundläggande fält kan du även kapsla in ytterligare datatyper i din anpassade datatyp. Datatypen Restaurant kräver till exempel ett fält som representerar egenskapens fysiska adress. I det här fallet kan du lägga till ett nytt adressfält som tilldelas standarddatatypen &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Detta visar hur flexibla datatyper kan vara när det gäller att beskriva dina data: datatyper kan använda fält som också är datatyper, som i sin tur kan innehålla fler datatyper, osv. På så sätt kan du abstrahera och återanvända vanliga datamönster i hela XDM-scheman, vilket gör det enklare att representera komplexa datastrukturer.

När du är klar med att lägga till fält till datatypen väljer du **[!UICONTROL Save]** för att spara ändringarna och lägga till datatypen i [!DNL Schema Library].

## Lägg till datatypen i ett schema

När du har skapat en datatyp kan du börja använda den i dina scheman. Eftersom XDM-scheman består av en klass och noll eller flera fältgrupper, kan fält som tillhandahålls av en datatyp inte läggas till direkt i ett schema. De måste i stället inkluderas i en klass eller en fältgrupp.

Börja med att följa de steg som ingår i [lägga till ett fält i en klass](./classes.md#add-fields) eller [lägga till ett fält i en fältgrupp](./field-groups.md#add-fields). Du kan också börja [lägga till ett fält direkt i ett schema](./schemas.md#add-individual-fields) och välj den överordnade klassen eller fältgruppen där. När du väljer **[!UICONTROL Type]** för det nya fältet väljer du namnet på datatypen i listrutan.

## Konvertera ett flerfältsobjekt till en datatyp {#convert}

När du skapar ett objekttypsfält med flera delfält i [!DNL Schema Editor]kan du konvertera det fältet till en datatyp så att du kan använda samma fältstruktur i en annan klass eller fältgrupp.

Om du vill konvertera ett fält av objekttyp till en datatyp, markerar du fältet på arbetsytan. Innan du konverterar fältet bör du kontrollera att **[!UICONTROL Display name]** är en beskrivning av de data som objektet kommer att innehålla, eftersom detta blir namnet på datatypen. När du är redo att konvertera fältet väljer du **[!UICONTROL Convert to new data type]** i rätt spår.

![](../../images/ui/resources/data-types/convert-object.png)

Arbetsytan uppdaterar fältets datatyp från[!UICONTROL Object]till den nya datatypen. Den här strukturen kan nu återanvändas i andra klasser och fältgrupper genom att välja den här datatypen i **[!UICONTROL Type]** när du definierar ett nytt fält.

![](../../images/ui/resources/data-types/converted.png)

## Nästa steg

I den här handboken beskrivs hur du skapar och redigerar datatyper med hjälp av användargränssnittet för plattformen. Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).

Så här hanterar du datatyper med [!DNL Schema Registry] API, se [slutpunktsguide för datatyper](../../api/data-types.md).
