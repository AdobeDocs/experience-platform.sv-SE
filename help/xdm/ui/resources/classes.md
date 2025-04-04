---
keywords: Experience Platform;home;populära topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Skapa och redigera klasser i användargränssnittet
description: Lär dig skapa och redigera klasser i Experience Platform användargränssnitt.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# Skapa och redigera klasser i användargränssnittet {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standardklassfilter eller -filter"
>abstract="Listan med tillgängliga klasser filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen Standard och Egen. Alternativet Standard visar enheter som skapats av Adobe och innehåller både XDM-klasserna Individual Profile och XDM Experience Event. Alternativet Egen visar enheter som skapats i din organisation. Mer information om hur du skapar och redigerar klasser finns i dokumentationen."

I Adobe Experience Platform definierar en schemaklass beteendeaspekterna för de data som schemat ska innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för Experience Data Model (XDM), inklusive [XDM Individual Profile](../../classes/individual-profile.md) och [XDM ExperienceEvent](../../classes/experienceevent.md). Förutom dessa huvudklasser kan du även skapa egna anpassade klasser som beskriver mer specifika användningsfall för organisationen.

Det här dokumentet innehåller en översikt över hur du skapar, redigerar och hanterar anpassade klasser i Experience Platform-gränssnittet.

## Förhandskrav {#prerequisites}

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i Experience Platform-ekosystemet och [grunderna i schemakomposition](../../schema/composition.md) för att lära dig hur klasser bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen om att [komponera ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i Schemaredigeraren.

## Komma igång {#getting-started}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna arbetsytan i [!UICONTROL Schemas] och sedan fliken **[!UICONTROL Classes]**. En lista över tillgängliga klasser visas.

![Antalet klasser på fliken [!UICONTROL Classes] i arbetsytan [!UICONTROL Schemas] [!UICONTROL Classes] och [!UICONTROL Schemas] är markerade.](../../images/ui/resources/classes/available-classes.png)

## Filterklasser {#filter}

Listan med klasser filtreras automatiskt baserat på hur de skapades. Standardinställningen visar de klasser som definieras av Adobe. Du kan även filtrera listan så att den visar de som har skapats av din organisation. Välj alternativknappen för att välja mellan alternativen [!UICONTROL Standard] och [!UICONTROL Custom]. Alternativet [!UICONTROL Standard] visar entiteter som skapats av Adobe och alternativet [!UICONTROL Custom] visar entiteter som skapats i din organisation.

![Fliken [!UICONTROL Classes] i arbetsytan [!UICONTROL Schemas] med [!UICONTROL Standard] och [!UICONTROL Custom] markerade.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Använd sökfunktionerna för att filtrera eller hitta en klass baserat på dess namn. Mer information finns i guiden [Utforska XDM-resurser](../explore.md).

## Skapa en ny klass {#create}

Det finns två metoder för att skapa en klass i Experience Platform-gränssnittet, till och med **[!UICONTROL Create class]** eller **[!UICONTROL Create schema]**.

### Skapa klass

Välj **[!UICONTROL Create class]** på fliken [!UICONTROL Classes] på arbetsytan [!UICONTROL Schemas].

![Fliken [!UICONTROL Classes] på arbetsytan [!UICONTROL Schemas] med [!UICONTROL Create class] markerat](../../images/ui/resources/classes/create-class.png)

Dialogrutan [!UICONTROL Create class] visas. Ange [!UICONTROL Display name] och [!UICONTROL Description] som klass och välj önskat beteende för klassen med alternativknapparna. Klasser kan vara av typen [!UICONTROL Record] eller [!UICONTROL Time-series]. Välj **[!UICONTROL Create]** för att bekräfta dina val och återgå till fliken [!UICONTROL Classes].

![Dialogrutan [!UICONTROL Create class] med [!UICONTROL Create] markerad.](../../images/ui/resources/classes/create-class-dialog.png)

Klassen som du har skapat är tillgänglig och visas i vyn [!UICONTROL Classes].

![Fliken [!UICONTROL Classes] på arbetsytan [!UICONTROL Schemas] med den nyligen skapade klassen markerad.](../../images/ui/resources/classes/new-class-listing.png)

### Skapa schema

Du kan också skapa en klass genom att skapa ett schema manuellt. Välj **[!UICONTROL Create schema]** på fliken [!UICONTROL Classes] på arbetsytan [!UICONTROL Schemas].

![Fliken [!UICONTROL Classes] på arbetsytan [!UICONTROL Schemas] med [!UICONTROL Create schema] markerat](../../images/ui/resources/classes/create-schema.png)

Välj **[!UICONTROL Manual]** i dialogrutan [!UICONTROL Create a schema] som visas.

>[!NOTE]
>
>Om du använder arbetsflödet för att skapa XML-stödda scheman kan du överföra en fil och använda ML-algoritmer för att generera ett rekommenderat schema. I arbetsflödet där du skapar scheman behöver du inte ange basklassen för ditt schema. Mer information om hur ML kan rekommendera en schemastruktur baserad på en csv-fil finns i guiden [Maskinininlärningsassisterade schemaskapare](../ml-assisted-schema-creation.md).

![Dialogrutan Skapa ett schema med arbetsflödesalternativen och välj markerad.](../../images/ui/resources/classes/manually-create-a-schema.png)

Arbetsflödet för att skapa scheman visas. Välj **[!UICONTROL Other]** i avsnittet [!UICONTROL Schema details]. En lista över tillgängliga klasser visas. Välj **[!UICONTROL Create class]**.

![Arbetsflödet [!UICONTROL Create schema] med [!UICONTROL Other] markerat i avsnittet [!UICONTROL Schema details].](../../images/ui/resources/classes/other-schema-details.png)

Dialogrutan [!UICONTROL Create class] visas. Ange [!UICONTROL Display name] och [!UICONTROL Description] som klass och välj önskat beteende för klassen med alternativknapparna. Klasser kan vara av typen [!UICONTROL Record] eller [!UICONTROL Time-series]. Välj **[!UICONTROL Create]** för att bekräfta dina val och återgå till fliken [!UICONTROL Classes].

![Dialogrutan [!UICONTROL Create class] med [!UICONTROL Create] markerad.](../../images/ui/resources/classes/create-class-from-schema.png)

Klasslistan uppdateras i avsnittet [!UICONTROL Schema details] och den klass du nyss skapade markeras automatiskt. Välj **[!UICONTROL Next]** om du vill fortsätta skapa ditt schema.

![Avsnittet [!UICONTROL Schema details] med den nya klassen markerad och [!UICONTROL Next] markerad.](../../images/ui/resources/classes/select-new-class.png)

När du har valt en klass visas avsnittet [!UICONTROL Name and review]. I det här avsnittet anger du ett namn och en beskrivning som identifierar ditt schema. &#x200B;Schemats grundstruktur (tillhandahålls av klassen) visas på arbetsytan så att du kan granska och verifiera den valda klassen och schemastrukturen.

Ange en [!UICONTROL Schema display name] som är användarvänlig i textfältet. Ange sedan en lämplig beskrivning för att identifiera schemat. När du har granskat din schemastruktur och är nöjd med dina inställningar väljer du **[!UICONTROL Finish]** för att skapa ditt schema.

![Avsnittet [!UICONTROL Name and review] i arbetsflödet [!UICONTROL Create schema] med [!UICONTROL Schema display name], [!UICONTROL Description] och [!UICONTROL Finish] markerade.](../../images/ui/resources/classes/schema-details.png)

## Lägga till fält i en klass {#add-fields}

När du har ett schema som använder en anpassad klass som är öppen i Schemaredigeraren kan du börja lägga till fält i klassen. Om du vill lägga till ett nytt fält väljer du ikonen **plus (+)** bredvid schemats namn.

>[!IMPORTANT]
>
>När du skapar ett schema som implementerar en klass som definierats av din organisation, måste du komma ihåg att schemafältgrupper endast är tillgängliga för användning med kompatibla klasser. Eftersom klassen som du definierade är ny finns det inga kompatibla fältgrupper i listan i dialogrutan **[!UICONTROL Add field group]**. I stället måste du [skapa nya fältgrupper](./field-groups.md#create) som kan användas med den klassen. Nästa gång du skapar ett schema som implementerar den nya klassen visas de fältgrupper som du har definierat och är tillgängliga för användning.

![Schemaredigeraren med knappen Lägg till markerad.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Kom ihåg att alla fält som du lägger till i en klass används i alla scheman som använder den klassen. Du bör därför noga tänka på vilka fält som är användbara i alla schemaanvändningsfall. Om du funderar på att lägga till ett fält som bara kan visa användning i vissa scheman under den här klassen, kanske du vill lägga till det i dessa scheman genom att [skapa en fältgrupp](./field-groups.md#create) i stället.

En **[!UICONTROL Untitled Field]**-platshållare visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. Välj **[!UICONTROL Class]** under **[!UICONTROL Assign to]**.

![Ett namnlöst fält på arbetsytan i Schemaredigeraren med fältegenskapen Tilldela till [!UICONTROL Class] markerad och markerad.](../../images/ui/resources/classes/assign-to-class.png)

I guiden om att [definiera fält i användargränssnittet](../fields/overview.md#define) finns mer information om hur du konfigurerar och lägger till fältet i klassen. Fortsätt att lägga till så många fält som behövs för klassen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och klassen.

![Det nyligen skapade schemat på arbetsytan i Schemaredigeraren, med [!UICONTROL Save] markerat.](../../images/ui/resources/classes/save.png)

Om du tidigare har skapat scheman som använder den här klassen visas de nya fälten automatiskt i dessa scheman.

## Redigera en klass (#edit-a-class)

>[!NOTE]
>
>Endast anpassade klasser som definierats av din organisation kan redigeras och anpassas helt. För huvudklasser som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom ramen för enskilda scheman. Mer information finns i avsnittet [Redigera visningsnamn för schemafält](./schemas.md#display-names).
>
>När en anpassad klass har sparats och använts vid dataanvändningen kan endast additiva ändringar göras i den därefter. Mer information finns i [reglerna för schemautveckling](../../schema/composition.md#evolution).

Du kan redigera en klass via schemaarbetsflödet genom att redigera ett befintligt schema som utökar klassen eller genom att skapa ett schema manuellt. Det går inte att redigera en klass direkt. Välj en befintlig klass eller **[!UICONTROL Create a schema]** på fliken [!UICONTROL Browse] på arbetsytan [!UICONTROL Schemas].

![Schemaredigeraren med en befintlig klass och [!UICONTROL Create a schema] markerat.](../../images/ui/resources/classes/edit-class-options.png)

Om du väljer att skapa ett nytt schema finns mer information i avsnittet [Skapa ett schema](#create-schema). När du har skapat schemat (eller efter att du har valt ett befintligt schema) visas schemaredigeraren. Om du vill uppdatera ett befintligt klassfält markerar du fältet i schemastrukturen. Fältets information visas i den högra listen. Kontrollera [!UICONTROL Assign to]
**[!UICONTROL Class]** är valt, annars kommer uppdateringarna inte att påverka klassen.

![Schemaredigeraren med ett fält markerat och markerat, och den högra listen visas. [!UICONTROL Assign to] markeras.](../../images/ui/resources/classes/edit-existing-field.png)

Gör önskade ändringar i fältet och rulla nedåt i den högra listen för att välja **[!UICONTROL Apply]** för att spara ändringarna.

>[!IMPORTANT]
>
> Alla uppdateringar du gör av fält kommer att tillämpas i alla scheman som använder den klassen, enligt [reglerna för schemautveckling](../../schema/composition.md#evolution).

![Schemaredigeraren med ett fält markerat och den högra listen markerad. [!UICONTROL Apply] markeras.](../../images/ui/resources/classes/save-changes.png)

Om du vill lägga till nya fält följer du guiden [Lägg till fält i en klass](#add-fields-to-a-class). När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och klassen.

![Schemaredigeraren med [!UICONTROL Save] markerat.](../../images/ui/resources/classes/save-schema.png)

## Ändra klassen för ett schema {#schema}

Du kan ändra schemaklassen när som helst under den inledande skapandeprocessen innan det har sparats. Detta bör dock göras med försiktighet, eftersom fältgrupper bara är kompatibla med vissa klasser. Om du ändrar klassen återställs arbetsytan och alla fält som du har lagt till.
Mer information finns i guiden om [att skapa och redigera scheman](./schemas.md#change-class).

## Nästa steg {#next-steps}

I det här dokumentet beskrivs hur du skapar och redigerar klasser med hjälp av användargränssnittet i Experience Platform. Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).

Om du vill lära dig hur du hanterar klasser med API:t för schemaregister läser du [klassernas slutpunktshandbok](../../api/classes.md).
