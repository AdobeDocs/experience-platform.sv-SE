---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Skapa och redigera schemafältgrupper i användargränssnittet
description: Lär dig hur du skapar och redigerar schemafältgrupper i användargränssnittet i Experience Platform.
topic-legacy: user guide
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Skapa och redigera schemafältgrupper i användargränssnittet

I Experience Data Model (XDM) är schemafältgrupper återanvändbara komponenter som definierar ett eller flera fält som implementerar vissa funktioner, till exempel personuppgifter, hotellinställningar eller adress. Fältgrupper är avsedda att ingå i ett schema som implementerar en kompatibel klass.

En fältgrupp definierar vilka klasser den är kompatibel med, baserat på beteendet för de data som fältgruppen representerar (post- eller tidsserie). Det innebär att inte alla fältgrupper är tillgängliga för användning med alla klasser.

Adobe Experience Platform erbjuder många standardfältgrupper som täcker ett brett urval av användningsområden för marknadsföring. Men du kan också skapa och redigera egna fältgrupper för att definiera ytterligare koncept som är relaterade till din verksamhet i dina XDM-scheman. Den här guiden ger en översikt över hur du skapar, redigerar och hanterar anpassade fältgrupper för din organisation i plattformsgränssnittet.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i ekosystemet Experience Platform och [grunderna i schemakomposition](../../schema/composition.md) för hur fältgrupper bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen om [disposition av ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Skapa en ny fältgrupp {#create}

Om du vill skapa en ny fältgrupp måste du först välja ett schema som fältgruppen ska läggas till i. Du kan välja att [skapa ett nytt schema](./schemas.md#create) eller [välja ett befintligt schema att redigera](./schemas.md#edit).

När du har schemat öppet i [!DNL Schema Editor] väljer du **[!UICONTROL Add]** bredvid avsnittet [!UICONTROL Field groups] i den vänstra listen.

![](../../images/ui/resources/field-groups/add-field-group.png)

En dialogruta visas med en lista över fältgrupper som finns för din organisation. Välj **[!UICONTROL Create new field group]** längst upp i dialogrutan. Här kan du ange en **[!UICONTROL Display name]** och **[!UICONTROL Description]** för fältgruppen. När du är klar väljer du **[!UICONTROL Add field group]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor] visas igen, med den nya fältgruppen i den vänstra listen. Eftersom det här är en helt ny fältgrupp innehåller den för närvarande inga fält till schemat och arbetsytan ändras därför inte. Nu kan du börja [lägga till fält i fältgruppen](#add-fields).

## Redigera en befintlig fältgrupp {#edit}

>[!NOTE]
>
>Endast anpassade fältgrupper som definierats av din organisation kan redigeras och anpassas helt. För huvudfältgrupper som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom ramen för enskilda scheman. Mer information finns i avsnittet [redigera visningsnamn för schemafält](./schemas.md#display-names).
>
>När en anpassad fältgrupp har sparats och använts i ett schema för datainmatning kan endast additiva ändringar göras i fältgruppen därefter. Mer information finns i [reglerna för schemautveckling](../../schema/composition.md#evolution).

Om du vill redigera en befintlig fältgrupp måste du först öppna ett schema som använder fältgruppen i [!DNL Schema Editor]. Du kan [välja ett befintligt schema att redigera](./schemas.md#edit), eller [skapa ett nytt schema](./schemas.md#create) och lägga till fältgruppen i fråga.

När du har öppnat schemat i redigeraren kan du börja [lägga till fält i fältgruppen](#add-fields).

## Lägga till fält i en fältgrupp {#add-fields}

Om du vill lägga till fält i en fältgrupp i [!DNL Schema Editor] börjar du med att markera fältgruppens namn i den vänstra listen och sedan väljer du ikonen **plus (+)** bredvid schemats namn på arbetsytan.

![](../../images/ui/resources/field-groups/add-field.png)

En **[!UICONTROL New field]** visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. Se guiden [definiera fält i användargränssnittet](../fields/overview.md#define) för specifika steg om hur du konfigurerar och lägger till fältet i fältgruppen.

Fortsätt att lägga till så många fält som behövs i fältgruppen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och fältgruppen.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Om samma fältgrupp redan används i andra scheman visas de nya fälten automatiskt i dessa scheman.

## Nästa steg

I den här handboken beskrivs hur du skapar och redigerar fältgrupper med hjälp av användargränssnittet för plattformen. Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas]](../overview.md).

Mer information om hur du hanterar fältgrupper med hjälp av API:t [!DNL Schema Registry] finns i [handboken om fältgruppsslutpunkter](../../api/field-groups.md).