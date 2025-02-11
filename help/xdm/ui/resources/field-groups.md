---
keywords: Experience Platform;home;populära topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Skapa och redigera schemafältgrupper i användargränssnittet
description: Lär dig hur du skapar och redigerar schemafältgrupper i Experience Platform användargränssnitt.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Skapa och redigera schemafältgrupper i användargränssnittet {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Standardfilter för anpassad fältgrupp"
>abstract="Listan med tillgängliga fältgrupper filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen Standard och Egen. Alternativet Standard visar entiteter som skapats av Adobe och alternativet Egen visar entiteter som skapats i din organisation. Mer information om hur du skapar och redigerar fältgrupper finns i dokumentationen."

I Experience Data Model (XDM) är schemafältgrupper återanvändbara komponenter som definierar ett eller flera fält som implementerar vissa funktioner, till exempel personuppgifter, hotellinställningar eller adress. Fältgrupper är avsedda att ingå i ett schema som implementerar en kompatibel klass.

En fältgrupp definierar vilka klasser den är kompatibel med, baserat på beteendet för de data som fältgruppen representerar (post- eller tidsserie). Det innebär att inte alla fältgrupper är tillgängliga för användning med alla klasser.

Adobe Experience Platform erbjuder många standardfältgrupper som täcker ett brett urval av användningsområden för marknadsföring. Men du kan också skapa och redigera egna fältgrupper för att definiera ytterligare koncept som är relaterade till din verksamhet i dina XDM-scheman. Den här guiden ger en översikt över hur du skapar, redigerar och hanterar anpassade fältgrupper för din organisation i plattformsgränssnittet.

## Förhandskrav {#prerequisites}

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i Experience Platform-ekosystemet och [grunderna i schemakomposition](../../schema/composition.md) för hur fältgrupper bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen om att [komponera ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Skapa en ny fältgrupp {#create}

Om du vill skapa en ny fältgrupp måste du först välja ett schema som fältgruppen ska läggas till i. Du kan välja att [skapa ett nytt schema](./schemas.md#create) eller [välja ett befintligt schema att redigera](./schemas.md#edit).

När du har öppnat schemat i [!DNL Schema Editor] väljer du **[!UICONTROL Add]** bredvid avsnittet [!UICONTROL Field groups] i den vänstra listen.

![](../../images/ui/resources/field-groups/add-field-group.png)

Välj **[!UICONTROL Create new field group]** i den dialogruta som visas. Här kan du ange **[!UICONTROL Display name]** och **[!UICONTROL Description]** för fältgruppen. När du är klar väljer du **[!UICONTROL Add field groups]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor] visas igen, med den nya fältgruppen i den vänstra listen. Eftersom det här är en helt ny fältgrupp innehåller den för närvarande inga fält till schemat och arbetsytan ändras därför inte. Nu kan du börja [lägga till fält i fältgruppen](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Filtrera fältgrupper {#filter}

Listan med tillgängliga fältgrupper filtreras i förväg baserat på hur de skapades. Standardinställningen visar de fältgrupper som definieras av Adobe. Du kan även filtrera listan så att den visar de som har skapats av din organisation. Välj alternativknappen för att välja mellan alternativen [!UICONTROL Standard] och [!UICONTROL Custom]. Alternativet [!UICONTROL Standard] visar entiteter som skapats av Adobe och alternativet [!UICONTROL Custom] visar entiteter som skapats i din organisation.

![Fliken [!UICONTROL Field groups] i arbetsytan [!UICONTROL Schemas] med [!UICONTROL Standard] och [!UICONTROL Custom] markerade.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Redigera en befintlig fältgrupp {#edit}

>[!NOTE]
>
>Endast anpassade fältgrupper som definierats av din organisation kan redigeras och anpassas helt. För huvudfältgrupper som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom ramen för enskilda scheman. De indikeras i Schemaredigeraren av en hänglåsikon (![En hänglåsikon.](/help/images/icons/lock-closed.png)). Mer information finns i avsnittet [Redigera visningsnamn för schemafält](./schemas.md#display-names).
>
>När en anpassad fältgrupp har sparats och använts i ett schema för datainmatning kan endast additiva ändringar göras i fältgruppen därefter. Mer information finns i [reglerna för schemautveckling](../../schema/composition.md#evolution).

Om du vill redigera en befintlig fältgrupp måste du först öppna ett schema som använder fältgruppen i [!DNL Schema Editor]. Du kan [välja ett befintligt schema att redigera](./schemas.md#edit) eller [skapa ett nytt schema](./schemas.md#create) och lägga till fältgruppen i fråga.

När du har öppnat schemat i redigeraren kan du börja [lägga till fält i fältgruppen](#add-fields).

## Lägga till fält i en fältgrupp {#add-fields}

>[!NOTE]
>
>Det här avsnittet fokuserar på att lägga till fält i anpassade fältgrupper. Mer information om hur du lägger till anpassade fält i standardfältgrupper finns i [schemas användargränssnittsguide](./schemas.md#custom-fields-for-standard-groups).

Om du vill lägga till fält i en anpassad fältgrupp börjar du med att markera ikonen **plus (+)** bredvid schemats namn på arbetsytan.

![](../../images/ui/resources/field-groups/add-field.png)

En **[!UICONTROL Untitled Field]**-platshållare visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. I guiden om att [definiera fält i användargränssnittet](../fields/overview.md#define) finns mer information om hur du konfigurerar olika fälttyper.

Välj alternativet **[!UICONTROL Field Group]** under **[!UICONTROL Assign to]** och använd sedan listrutan för att välja önskad fältgrupp från listan. Du kan börja skriva in namnet på fältgruppen för att begränsa resultatet.

![](../../images/ui/resources/field-groups/select-field-group.png)

Välj alternativet **[!UICONTROL Field Group]** under **[!UICONTROL Assign to]** och använd sedan listrutan för att välja önskad fältgrupp från listan. Du kan börja skriva in namnet på fältgruppen för att begränsa resultatet.

![](../../images/ui/resources/field-groups/select-field-group.png)

När fältet har lagts till i schemat tilldelas det till den valda fältgruppen. Fortsätt att lägga till så många fält som behövs i fältgruppen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och fältgruppen.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Om samma fältgrupp redan används i andra scheman visas de nya fälten automatiskt i dessa scheman.

## Nästa steg {#next-steps}

I den här handboken beskrivs hur du skapar och redigerar fältgrupper med hjälp av användargränssnittet för plattformen. Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).

Mer information om hur du hanterar fältgrupper med API:t [!DNL Schema Registry] finns i [handboken om fältgruppers slutpunkter](../../api/field-groups.md).
