---
keywords: Experience Platform;hem;populära ämnen;ui;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;schema;schema;scheman;scheman;scheman;scheman;create;data type;data types;
solution: Experience Platform
title: Skapa och redigera datatyper med användargränssnittet
type: Tutorial
description: Lär dig hur du skapar och redigerar datatyper i användargränssnittet i Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# Skapa och redigera datatyper med användargränssnittet {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Standarddatatypsfilter eller -filter"
>abstract="Listan med tillgängliga datatyper filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen Standard och Egen. Alternativet Standard visar entiteter som skapats av Adobe och alternativet Anpassad visar entiteter som skapats i din organisation. Mer information om hur du skapar och redigerar datatyper finns i dokumentationen."

I Experience Data Model (XDM) är datatyper återanvändbara fält som innehåller flera underfält. Även om datatyperna liknar schemafältgrupper på så sätt att de medger konsekvent användning av en flerfältsstruktur, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan fältgrupper bara kan läggas till på rotnivån.

Adobe Experience Platform har många standarddatatyper som kan användas för ett stort antal vanliga användningsfall för upplevelsehantering. Men du kan också definiera egna anpassade datatyper för att tillgodose dina unika affärsbehov.

>[!NOTE]
>
>Om ett fält definieras som en viss datatyp kan du inte skapa samma fält med en annan datatyp i ett annat schema. Begränsningen gäller för hela organisationens klientorganisation.

I den här självstudiekursen beskrivs stegen för att skapa och redigera anpassade datatyper i användargränssnittet för plattformen.

## Förhandskrav {#prerequisites}

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i ekosystemet Experience Platform och [grunderna i schemakomposition](../../schema/composition.md) för hur datatyper bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen om att [komponera ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Öppna [!DNL Schema Editor] för en datatyp {#data-type}

I plattformsgränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna arbetsytan i [!UICONTROL Schemas] och sedan fliken **[!UICONTROL Data types]**. En lista över tillgängliga datatyper visas. Listan med datatyper filtreras automatiskt baserat på hur de skapades. Standardinställningen visar de datatyper som definieras av Adobe. Du kan även filtrera listan så att den visar de som har skapats av din organisation.

![Arbetsytan [!UICONTROL Schemas] med [!UICONTROL Schemas] i den vänstra navigeringen och [!UICONTROL Data types] markerad.](../../images/ui/resources/data-types/data-types-tab.png)

Här har du följande alternativ:

- [Skapa en ny datatyp](#create)
- [Filtrera datatyper](#filter)
- [Välj en befintlig datatyp att redigera](#edit)

### Skapa en ny datatyp {#create}

På fliken **[!UICONTROL Data types]** väljer du **[!UICONTROL Create data type]**.

![Fliken [!UICONTROL Schemas] arbetsyta [!UICONTROL Data types] med [!UICONTROL Create data type] markerad.](../../images/ui/resources/data-types/create.png)

[!DNL Schema Editor] visas med den aktuella strukturen för den nya datatypen på arbetsytan. Till höger om redigeraren kan du ange ett visningsnamn och en valfri beskrivning av datatypen. Se till att du anger ett unikt och koncist namn för din datatyp, eftersom det är så det identifieras när du lägger till den i ett schema.

I den här självstudien skapas en datatyp som beskriver en restaurangegenskap, så datatypen får visningsnamnet &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Härifrån kan du hoppa fram till [nästa avsnitt](#add-fields) för att börja lägga till fält i den nya datatypen.

### Filtrera datatyper {#filter}

Listan med tillgängliga datatyper filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen [!UICONTROL Standard] och [!UICONTROL Custom]. Alternativet [!UICONTROL Standard] visar entiteter som skapats av Adobe och alternativet [!UICONTROL Custom] visar entiteter som skapats i din organisation.

![Fliken [!UICONTROL Data types] i arbetsytan [!UICONTROL Schemas] med [!UICONTROL Standard] och [!UICONTROL Custom] markerade.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Redigera en befintlig datatyp {#edit}

>[!NOTE]
>
>När en befintlig datatyp används i ett schema som har aktiverats för användning i kundprofilen i realtid, kan endast icke-förstörande ändringar göras i den datatypen därefter. Mer information finns i [reglerna för schemautveckling](../../schema/composition.md#evolution).

Endast anpassade datatyper som definieras av din organisation kan redigeras. Välj **[!UICONTROL Custom]** om du bara vill visa anpassade datatyper som ägs av din organisation.

Välj den datatyp som du vill redigera i listan för att öppna den högra listen och visa information om datatypen. På informationspanelen kan du även hämta en exempelfil, kopiera JSON-strukturen eller lägga till datatypen i ett paket.

Markera namnet på datatypen i den högra listen för att öppna dess struktur i [!DNL Schema Editor].

![Fliken [!UICONTROL Data types] på arbetsytan [!UICONTROL Schemas], med en datatyp, [!UICONTROL Custom] och datatypen [!UICONTROL Name] markerade.](../../images/ui/resources/data-types/edit.png)

## Lägg till fält i datatypen {#add-fields}

Om du vill börja lägga till fält i datatypen väljer du ikonen **plus (+)** bredvid rotnivåfältet på arbetsytan. Ett nytt fält visas nedan och den högra listen uppdateras för att visa kontroller för det nya fältet.

![](../../images/ui/resources/data-types/new-field.png)

Använd kontrollerna i den högra listen för att konfigurera information om det nya fältet. I guiden om att [definiera fält i användargränssnittet](../fields/overview.md#define) finns mer information om hur du konfigurerar och lägger till fältet i datatypen.

Datatypen Restaurant kräver ett strängfält som representerar restaurangens namn. Därför anges [!UICONTROL Field name] som&quot;name&quot; och [!UICONTROL Type] som [!UICONTROL String]. Välj **[!UICONTROL Apply]** om du vill använda ändringarna i fältet.

![](../../images/ui/resources/data-types/name-field.png)

Fortsätt lägga till fler fält till datatypen efter behov. Datatypen Restaurant har nu ytterligare fält för märke, sittplatskapacitet och golvutrymme.

![](../../images/ui/resources/data-types/more-fields.png)

Förutom grundläggande fält kan du även kapsla in ytterligare datatyper i din anpassade datatyp. Datatypen Restaurant kräver till exempel ett fält som representerar egenskapens fysiska adress. I det här scenariot kan du lägga till ett nytt adressfält som har tilldelats standarddatatypen [!UICONTROL Postal address].

![](../../images/ui/resources/data-types/address-field.png)

Detta visar hur flexibla datatyper kan vara när det gäller att beskriva dina data: datatyperna kan använda fält som också är datatyper, som i sin tur kan innehålla fler datatyper, och så vidare. På så sätt kan du abstrahera och återanvända vanliga datamönster i hela XDM-scheman, vilket gör det enklare att representera komplexa datastrukturer.

När du har lagt till fält till datatypen väljer du **[!UICONTROL Save]** för att spara ändringarna och lägga till datatypen i [!DNL Schema Library].

## Lägg till datatypen i ett schema {#add-data-type}

När du har skapat en datatyp kan du börja använda den i dina scheman. Eftersom XDM-scheman består av en klass och noll eller flera fältgrupper, kan fält som tillhandahålls av en datatyp inte läggas till direkt i ett schema. De måste i stället inkluderas i en klass eller en fältgrupp.

Börja med att följa stegen som ingår i [att lägga till ett fält i en klass](./classes.md#add-fields) eller [lägga till ett fält i en fältgrupp](./field-groups.md#add-fields). Du kan också börja med att [lägga till ett fält direkt i ett schema](./schemas.md#add-individual-fields) och välja den överordnade klassen eller fältgruppen därifrån. När du väljer **[!UICONTROL Type]** för det nya fältet väljer du namnet på datatypen i listrutan.

## Konvertera ett flerfältsobjekt till en datatyp {#convert}

När du skapar ett fält av objekttyp med flera delfält i [!DNL Schema Editor] kan du konvertera det fältet till en datatyp så att du kan använda samma fältstruktur i en annan klass eller fältgrupp.

Om du vill konvertera ett fält av objekttyp till en datatyp, markerar du fältet på arbetsytan. Innan du konverterar fältet måste du se till att **[!UICONTROL Display name]** är beskrivande av de data som objektet kommer att innehålla, eftersom detta blir namnet på datatypen. När du är redo att konvertera fältet väljer du **[!UICONTROL Convert to new data type]** i den högra listen.

![](../../images/ui/resources/data-types/convert-object.png)

Arbetsytan uppdaterar datatypen för fältet från [!UICONTROL Object] till den nya datatypen. Den här strukturen kan nu återanvändas i andra klasser och fältgrupper genom att välja den här datatypen i listrutan **[!UICONTROL Type]** när du definierar ett nytt fält.

![](../../images/ui/resources/data-types/converted.png)

## Nästa steg {#next-steps}

I den här handboken beskrivs hur du skapar och redigerar datatyper med hjälp av användargränssnittet för plattformen. Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).

Mer information om hur du hanterar datatyper med [!DNL Schema Registry]-API:t finns i [slutpunktshandboken för datatyper](../../api/data-types.md).
