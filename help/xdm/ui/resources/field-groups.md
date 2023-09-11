---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Skapa och redigera schemafältgrupper i användargränssnittet
description: Lär dig hur du skapar och redigerar schemafältgrupper i användargränssnittet i Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 51ef116ad125b0d699bf4808e3d26d3b00b743e2
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# Skapa och redigera schemafältgrupper i användargränssnittet {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Standardfilter eller filter för anpassad fältgrupp"
>abstract="Listan med tillgängliga fältgrupper filtreras i förväg baserat på hur de skapades. Välj alternativknappen för att välja mellan alternativen Standard och Egen. Alternativet Standard visar entiteter som skapats av Adobe och alternativet Anpassad visar entiteter som skapats i din organisation. Mer information om hur du skapar och redigerar fältgrupper finns i dokumentationen."

I Experience Data Model (XDM) är schemafältgrupper återanvändbara komponenter som definierar ett eller flera fält som implementerar vissa funktioner, till exempel personuppgifter, hotellinställningar eller adress. Fältgrupper är avsedda att ingå i ett schema som implementerar en kompatibel klass.

En fältgrupp definierar vilka klasser den är kompatibel med, baserat på beteendet för de data som fältgruppen representerar (post- eller tidsserie). Det innebär att inte alla fältgrupper är tillgängliga för användning med alla klasser.

Adobe Experience Platform erbjuder många standardfältgrupper som täcker ett brett urval av användningsområden för marknadsföring. Men du kan också skapa och redigera egna fältgrupper för att definiera ytterligare koncept som är relaterade till din verksamhet i dina XDM-scheman. Den här guiden ger en översikt över hur du skapar, redigerar och hanterar anpassade fältgrupper för din organisation i plattformsgränssnittet.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) för hur fältgrupper bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen på [skapa ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Skapa en ny fältgrupp {#create}

Om du vill skapa en ny fältgrupp måste du först välja ett schema som fältgruppen ska läggas till i. Du kan [skapa ett nytt schema](./schemas.md#create) eller [välj ett befintligt schema att redigera](./schemas.md#edit).

När du har öppnat schemat i [!DNL Schema Editor], markera **[!UICONTROL Add]** bredvid [!UICONTROL Field groups] till vänster.

![](../../images/ui/resources/field-groups/add-field-group.png)

I den dialogruta som visas väljer du **[!UICONTROL Create new field group]**. Här kan du ange en **[!UICONTROL Display name]** och **[!UICONTROL Description]** för fältgruppen. När du är klar väljer du **[!UICONTROL Add field groups]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

The [!DNL Schema Editor] visas igen med den nya fältgruppen i den vänstra listen. Eftersom det här är en helt ny fältgrupp innehåller den för närvarande inga fält till schemat och arbetsytan ändras därför inte. Nu kan du börja [lägga till fält i fältgruppen](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Redigera en befintlig fältgrupp {#edit}

>[!NOTE]
>
>Endast anpassade fältgrupper som definierats av din organisation kan redigeras och anpassas helt. För huvudfältgrupper som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom ramen för enskilda scheman. Se avsnittet om [redigera visningsnamn för schemafält](./schemas.md#display-names) för mer information.
>
>När en anpassad fältgrupp har sparats och använts i ett schema för datainmatning kan endast additiva ändringar göras i fältgruppen därefter. Se [regler för schemautveckling](../../schema/composition.md#evolution) för mer information.

Om du vill redigera en befintlig fältgrupp måste du först öppna ett schema som använder fältgruppen i [!DNL Schema Editor]. Du kan [välj ett befintligt schema att redigera](./schemas.md#edit)eller så kan du [skapa ett nytt schema](./schemas.md#create) och lägg till fältgruppen i fråga.

När du har öppnat schemat i redigeraren kan du börja [lägga till fält i fältgruppen](#add-fields).

## Lägga till fält i en fältgrupp {#add-fields}

>[!NOTE]
>
>Det här avsnittet fokuserar på att lägga till fält i anpassade fältgrupper. Mer information om hur du lägger till anpassade fält i standardfältgrupper finns i [gränssnittshandbok för scheman](./schemas.md#custom-fields-for-standard-groups).

Om du vill lägga till fält i en anpassad fältgrupp börjar du med att välja **plus (+)** -ikonen bredvid schemats namn på arbetsytan.

![](../../images/ui/resources/field-groups/add-field.png)

An **[!UICONTROL Untitled Field]** platshållaren visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. Se guiden på [definiera fält i användargränssnittet](../fields/overview.md#define) för specifika steg om hur du konfigurerar olika fälttyper.

Under **[!UICONTROL Assign to]** väljer du **[!UICONTROL Field Group]** väljer du sedan den önskade fältgruppen i listan. Du kan börja skriva in namnet på fältgruppen för att begränsa resultatet.

![](../../images/ui/resources/field-groups/select-field-group.png)

Under **[!UICONTROL Assign to]** väljer du **[!UICONTROL Field Group]** väljer du sedan den önskade fältgruppen i listan. Du kan börja skriva in namnet på fältgruppen för att begränsa resultatet.

![](../../images/ui/resources/field-groups/select-field-group.png)

När fältet har lagts till i schemat tilldelas det till den valda fältgruppen. Fortsätt att lägga till så många fält som behövs i fältgruppen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och fältgruppen.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Om samma fältgrupp redan används i andra scheman visas de nya fälten automatiskt i dessa scheman.

## Nästa steg

I den här handboken beskrivs hur du skapar och redigerar fältgrupper med hjälp av användargränssnittet för plattformen. Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).

Så här hanterar du fältgrupper med [!DNL Schema Registry] API, se [slutpunktsguide för fältgrupper](../../api/field-groups.md).
