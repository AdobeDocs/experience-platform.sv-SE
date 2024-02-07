---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Skapa och redigera klasser i användargränssnittet
description: Lär dig hur du skapar och redigerar klasser i användargränssnittet i Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 640d3ca0d3c227306436f2e653ef66fdc8ebd31c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Skapa och redigera klasser i användargränssnittet {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standardklassfilter eller -filter"
>abstract="Listan med tillgängliga klasser filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen Standard och Egen. Alternativet Standard visar enheter som skapats av Adobe och innehåller både XDM-klasserna Individual Profile och XDM Experience Event. Alternativet Egen visar enheter som skapats i din organisation. Mer information om hur du skapar och redigerar klasser finns i dokumentationen."

I Adobe Experience Platform definierar en schemaklass beteendeaspekterna för de data som schemat ska innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för Experience Data Model (XDM), inklusive XDM Individual Profile och XDM ExperienceEvent. Förutom dessa huvudklasser kan du även skapa egna anpassade klasser som beskriver mer specifika användningsfall för organisationen.

Det här dokumentet innehåller en översikt över hur du skapar, redigerar och hanterar anpassade klasser i användargränssnittet i Experience Platform.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) om du vill veta hur klasser bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen på [skapa ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i Schemaredigeraren.

## Komma igång

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna [!UICONTROL Schemas] väljer du **[!UICONTROL Classes]** -fliken. En lista över tillgängliga klasser visas.

## Filterklasser {#filter}

Listan med klasser filtreras automatiskt baserat på hur de skapades. Standardinställningen visar de klasser som definieras av Adobe. Du kan även filtrera listan så att den visar de som har skapats av din organisation. Välj alternativknappen för att välja mellan [!UICONTROL Standard] och [!UICONTROL Custom] alternativ. The [!UICONTROL Standard] alternativet visar enheter som skapats av Adobe och [!UICONTROL Custom] visas enheter som har skapats i din organisation.

![The [!UICONTROL Classes] -fliken i [!UICONTROL Schemas] arbetsyta med [!UICONTROL Standard] och [!UICONTROL Custom] markerad.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Använd sökfunktionerna för att filtrera eller hitta en klass baserat på dess namn. Se guiden på [utforska XDM-resurser](../explore.md) för mer information.

## Skapa en ny klass {#create}

Det finns två metoder för att skapa en klass i plattformsgränssnittet. Från en flik i [!UICONTROL Schemas] arbetsyta, välja **[!UICONTROL Create schema]** eller från [!UICONTROL Classes] tabbmarkera **[!UICONTROL Create class]**.

![The [!UICONTROL Classes] -fliken i [!UICONTROL Schemas] arbetsyta med [!UICONTROL Create schema] och [!UICONTROL Create class] markerad](../../images/ui/resources/classes/create-class-methods.png)

Om du väljer **[!UICONTROL Create class]**, [!UICONTROL Create class] visas. Ange en [!UICONTROL Display name] och [!UICONTROL Description] för klassen och välj önskat beteende för klassen med alternativknapparna. Klasser kan vara av typen, postserier eller tidsserier. Välj **[!UICONTROL Create]** för att bekräfta dina val och gå tillbaka till [!UICONTROL Classes] -fliken.

![The [!UICONTROL Create class] dialogruta med [!UICONTROL Create] markerad.](../../images/ui/resources/classes/create-class-dialog.png)

Klassen som du har skapat är tillgänglig och visas i [!UICONTROL Classes] vy.

![The [!UICONTROL Classes] -fliken i [!UICONTROL Schemas] arbetsyta med den nyligen skapade klassen markerad.](../../images/ui/resources/classes/new-class-listing.png)

### Skapa eller redigera en klass {#create-or-edit}

Om du väljer **[!UICONTROL Create schema]**, [!UICONTROL Create schema] arbetsflödet visas. I [!UICONTROL Schema details] avsnitt, markera **[!UICONTROL Other]**. En lista över tillgängliga klasser visas. Härifrån kan du bläddra bland och filtrera befintliga klasser som den nya klassen ska baseras på.

>[!NOTE]
>
>Endast anpassade klasser som definierats av din organisation kan redigeras och anpassas helt. För huvudklasser som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom kontexten för enskilda scheman. Se avsnittet om [redigera visningsnamn för schemafält](./schemas.md#display-names) för mer information.
>
>När en anpassad klass har sparats och använts vid dataanvändningen kan endast additiva ändringar göras i den därefter. Se [regler för schemautveckling](../../schema/composition.md#evolution) för mer information.

![The [!UICONTROL Create schema] arbetsflöde med [!UICONTROL Other] markerat i [!UICONTROL Schema details] -avsnitt.](../../images/ui/resources/classes/other-schema-details.png)

Markera en alternativknapp om du vill filtrera klasserna baserat på om de är anpassade eller standardklasser. Du kan även filtrera tillgängliga resultat baserat på bransch eller söka efter en viss klass med hjälp av sökfältet.

![The [!UICONTROL Create schema] arbetsflöde med sökfältet, [!UICONTROL Custom]och [!UICONTROL Industries] markerad.](../../images/ui/resources/classes/filter-and-search.png)

Det finns info (![En informationsikon.](../../images/ui/resources/classes/info.png)) och förhandsgranska (![En förhandsgranskningsikon.](../../images/ui/resources/classes/preview.png)) för varje klass. Informationsikonen öppnar en dialogruta med en beskrivning av klassen och den bransch som den är kopplad till. Förhandsgranskningsikonen öppnar en förhandsvisningsdialogruta för den klass som innehåller ett schemadiagram och dess egenskaper.

![En förhandsvisning av den valda klassen med schemat och klassegenskaperna markerade.](../../images/ui/resources/classes/class-preview.png)

Markera en rad för att välja en klass och markera sedan **[!UICONTROL Next]** för att bekräfta ditt val.

![The [!UICONTROL Create schema] arbetsflöde med en klass vald från tabellen med tillgängliga klasser och [!UICONTROL Next] markerad.](../../images/ui/resources/classes/select-class.png)

The [!UICONTROL Name and review] -avsnittet i arbetsflödet visas. I det här avsnittet anger du ett namn och en beskrivning som identifierar ditt schema. &#x200B;Schemats grundstruktur (tillhandahålls av klassen) visas på arbetsytan så att du kan granska och verifiera den valda klassen och schemastrukturen.

Ange ett kort, beskrivande, unikt och användarvänligt namn för klassen i [!UICONTROL Schema display name] textfält. Ange sedan en lämplig beskrivning för att identifiera beteendet för de data som definieras i schemat. När du har granskat schemastrukturen och är nöjd med dina inställningar väljer du **[!UICONTROL Finish]** för att skapa ditt schema.

![The [!UICONTROL Name and review] i [!UICONTROL Create schema] arbetsflöde med [!UICONTROL Schema display name], [!UICONTROL Description]och [!UICONTROL Finish] markerad.](../../images/ui/resources/classes/name-and-review-class.png)

Schemaredigeraren visas med schemats struktur på arbetsytan. Nu kan du börja [lägga till fält i klassen](#add-fields).

![Schemaredigeraren med schemats struktur på arbetsytan.](../../images/ui/resources/classes/edit.png)

## Lägga till fält i en klass {#add-fields}

När du har ett schema som använder en anpassad klass öppen i [!UICONTROL Schema Editor]kan du börja lägga till fält i klassen. Om du vill lägga till ett nytt fält väljer du **plus (+)** -ikon bredvid schemats namn.

>[!IMPORTANT]
>
>När du skapar ett schema som implementerar en klass som definierats av din organisation, måste du komma ihåg att schemafältgrupper endast är tillgängliga för användning med kompatibla klasser. Eftersom klassen du definierade är ny finns det inga kompatibla fältgrupper i listan **[!UICONTROL Add field group]** -dialogrutan. Istället måste du [skapa nya fältgrupper](./field-groups.md#create) för användning med den klassen. Nästa gång du skapar ett schema som implementerar den nya klassen visas de fältgrupper som du har definierat och är tillgängliga för användning.

![Schemaredigeraren med knappen Lägg till markerad.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Kom ihåg att alla fält som du lägger till i en klass används i alla scheman som använder den klassen. Du bör därför noga tänka på vilka fält som är användbara i alla schemaanvändningsfall. Om du funderar på att lägga till ett fält som bara kan se användning i vissa scheman under den här klassen, kanske du vill lägga till det i dessa scheman genom att [skapa en fältgrupp](./field-groups.md#create) i stället.

An **[!UICONTROL Untitled Field]** platshållaren visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. Under **[!UICONTROL Assign to]**, markera **[!UICONTROL Class]**.

![Ett namnlöst fält på arbetsytan i schemaredigeraren med fältegenskapen Tilldela till klass markerad och markerad.](../../images/ui/resources/classes/assign-to-class.png)

Se guiden på [definiera fält i användargränssnittet](../fields/overview.md#define) för specifika steg om hur du konfigurerar och lägger till fältet i klassen. Fortsätt att lägga till så många fält som behövs för klassen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och klassen.

![Det nyligen skapade schemat på arbetsytan i Schemaredigeraren, med [!UICONTROL Save] markerad.](../../images/ui/resources/classes/save.png)

Om du tidigare har skapat scheman som använder den här klassen visas de nya fälten automatiskt i dessa scheman.

## Ändra klassen för ett schema {#schema}

Du kan ändra schemaklassen när som helst under den inledande skapandeprocessen innan det har sparats. Detta bör dock göras med försiktighet, eftersom fältgrupper bara är kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält som du har lagt till.
Se guiden på [skapa och redigera scheman](./schemas.md#change-class) för mer information.

## Nästa steg

I det här dokumentet beskrivs hur du skapar och redigerar klasser med hjälp av användargränssnittet för plattformen. Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).

Om du vill lära dig hur du hanterar klasser med API:t för schemaregister läser du i [stödlinje för klassers slutpunkt](../../api/classes.md).
