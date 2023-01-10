---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Skapa och redigera klasser i användargränssnittet
description: Lär dig hur du skapar och redigerar klasser i användargränssnittet i Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# Skapa och redigera klasser i användargränssnittet

I Adobe Experience Platform definierar en schemaklass beteendeaspekterna för de data som schemat ska innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för Experience Data Model (XDM), inklusive [!DNL XDM Individual Profile] och [!DNL XDM ExperienceEvent]. Förutom dessa huvudklasser kan du även skapa egna anpassade klasser som beskriver mer specifika användningsfall för organisationen.

Det här dokumentet innehåller en översikt över hur du skapar, redigerar och hanterar anpassade klasser i användargränssnittet i Experience Platform.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) om du vill veta hur klasser bidrar till XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen på [skapa ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Skapa en ny klass {#create}

I **[!UICONTROL Schemas]** arbetsyta, välja **[!UICONTROL Create schema]** väljer **[!UICONTROL Browse]** i listrutan.

![](../../images/ui/resources/classes/browse-classes.png)

En dialogruta visas där du kan välja från en lista med tillgängliga klasser. Välj **[!UICONTROL Create new class]**. Du kan sedan ge den nya klassen ett visningsnamn (ett kort, beskrivande, unikt och användarvänligt namn för klassen), en beskrivning och ett beteende för de data som schemat ska definiera (**[!UICONTROL Record]** eller **[!UICONTROL Time-series]**).

När du är klar väljer du **[!UICONTROL Assign class]**.

![](../../images/ui/resources/classes/class-details.png)

The [!DNL Schema Editor] visas, med ett nytt schema på arbetsytan som är baserat på den klass du just skapade. Eftersom inga fält har lagts till i klassen ännu innehåller schemat bara ett `_id` -fält, som representerar den systemgenererade unika identifieraren som automatiskt tillämpas på alla resurser i [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>När du skapar ett schema som implementerar en klass som definierats av din organisation, måste du komma ihåg att schemafältgrupper endast är tillgängliga för användning med kompatibla klasser. Eftersom klassen du definierade är ny finns det inga kompatibla fältgrupper i listan **[!UICONTROL Add field group]** -dialogrutan. Istället måste du [skapa nya fältgrupper](./field-groups.md#create) för användning med den klassen. Nästa gång du skapar ett schema som implementerar den nya klassen visas de fältgrupper som du har definierat och är tillgängliga för användning.

Nu kan du börja [lägga till fält i klassen](#add-fields), som delas av alla scheman som använder klassen.

## Redigera en befintlig klass {#edit}

>[!NOTE]
>
>Endast anpassade klasser som definierats av din organisation kan redigeras och anpassas helt. För huvudklasser som definieras av Adobe kan bara visningsnamnen för deras fält redigeras inom kontexten för enskilda scheman. Se avsnittet om [redigera visningsnamn för schemafält](./schemas.md#display-names) för mer information.
>
>När en anpassad klass har sparats och använts vid dataanvändningen kan endast additiva ändringar göras i den därefter. Se [regler för schemautveckling](../../schema/composition.md#evolution) för mer information.

Om du vill redigera en befintlig klass väljer du **[!UICONTROL Browse]** och markera sedan namnet på ett schema som innehåller den klass som du vill redigera.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Du kan använda arbetsytans sök- och filtreringsfunktioner för att enklare hitta schemat. Se guiden [utforska XDM-resurser](../explore.md) för mer information.

The [!DNL Schema Editor] visas med schemats struktur på arbetsytan. Nu kan du börja [lägga till fält i klassen](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Lägga till fält i en klass {#add-fields}

När du har ett schema som använder en anpassad klass öppen i [!UICONTROL Schema Editor]kan du börja lägga till fält i klassen. Om du vill lägga till ett nytt fält väljer du **plus (+)** -ikon bredvid schemats namn.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Kom ihåg att alla fält som du lägger till i en klass används i alla scheman som använder den klassen. Du bör därför noga tänka på vilka fält som är användbara i alla schemaanvändningsfall. Om du funderar på att lägga till ett fält som bara kan se användning i vissa scheman under den här klassen, kanske du vill lägga till det i dessa scheman genom att [skapa en fältgrupp](./field-groups.md#create) i stället.

A **[!UICONTROL New field]** visas på arbetsytan och den högra listen uppdateras för att visa kontroller för att konfigurera fältets egenskaper. Under **[!UICONTROL Assign to]** väljer du **[!UICONTROL Class]**.

![](../../images/ui/resources/classes/assign-to-class.png)

Se guiden [definiera fält i användargränssnittet](../fields/overview.md#define) för specifika steg om hur du konfigurerar och lägger till fältet i klassen. Fortsätt att lägga till så många fält som behövs för klassen. När du är klar väljer du **[!UICONTROL Save]** för att spara både schemat och klassen.

![](../../images/ui/resources/classes/save.png)

Om du tidigare har skapat scheman som använder den här klassen visas de nya fälten automatiskt i dessa scheman.

## Ändra klassen för ett schema {#schema}

Du kan ändra schemaklassen när som helst under den inledande skapandeprocessen innan det har sparats. Se guiden [skapa och redigera scheman](./schemas.md#change-class) för mer information.

## Nästa steg

I det här dokumentet beskrivs hur du skapar och redigerar klasser med hjälp av användargränssnittet för plattformen. Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).

Så här hanterar du klasser med [!DNL Schema Registry] API, se [klassers slutpunktshandbok](../../api/classes.md).
