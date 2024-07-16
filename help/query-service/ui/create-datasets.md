---
keywords: Experience Platform;home;populära topics;query service;Query service;generate datasets;generate dataset;create dataset;
solution: Experience Platform
title: Generera utdatauppsättningar från frågeresultat
type: Tutorial
description: Med Adobe Experience Platform Query Service kan du skapa datauppsättningar från användargränssnittet. När en datauppsättning har skapats kan den nås som vilken annan datauppsättning som helst i datasjön och användas för en mängd olika användningsfall.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Generera utdata från frågeresultat

Med [!DNL Query Service] kan du använda frågor för att generera datauppsättningar i [!DNL Data Lake]. Dessa datauppsättningar kan sedan användas som indata för fler frågor eller i andra tjänster som [!DNL Data Science Workspace], kundprofil i realtid eller [!DNL Analysis Workspace].

## Generera datauppsättningar från Adobe Experience Platform användargränssnitt

Så här skapar du datauppsättningar från Adobe Experience Platform användargränssnitt:

1. Skapa en fråga med en ansluten klient och validera utdata. Läs [!DNL Query Editor] UI-guiden [ om hur du skriver frågor ](./user-guide.md#writing-queries) om du vill lära dig hur du skriver frågor med [!DNL Query Editor].

2. I plattformsgränssnittet går du till **[!UICONTROL Queries]** följt av fliken **[!UICONTROL Templates]** och väljer den fråga du har skapat. Mer information om hur du visar frågor som har skapats och sparats för din organisation i plattformsgränssnittet finns i [[!DNL Query Service] översikten](./overview.md#browse).

3. Välj **[!UICONTROL Run as CTAS]** på panelen Frågeinformation.

   ![Fliken [!UICONTROL Templates] i arbetsytan Frågor med Markera [!UICONTROL Run as CTAS] markerad.](../images/ui/create-datasets/run-as-ctas.png)

4. I dialogrutan som visas anger du ett datauppsättningsnamn som föregås av ditt LDAP-ID. Datauppsättningsnamnet behöver inte vara unikt eller SQL-säkert. Observera att tabellnamnet för datauppsättningen genereras baserat på det datauppsättningsnamn som du skapar här.

5. Ange sedan en beskrivning av datauppsättningen i fältet [!UICONTROL Description] och välj **[!UICONTROL Run as CTAS]**.

   ![Dialogrutan för utdata med datauppsättningsinformation och [!UICONTROL Run as CTAS] markerad](../images/ui/create-datasets/run-query.png)

6. När frågekörningen är klar går du till **[!UICONTROL Datasets]** för att visa den datauppsättning du har skapat. Mer information om hur du utför vanliga åtgärder när du arbetar med datauppsättningar i plattformsgränssnittet finns i [användargränssnittsguiden för datauppsättningar](../../catalog/datasets/user-guide.md).

När en datauppsättning har skapats kan den nås på samma sätt som andra datauppsättningar i [!DNL Data Lake] och användas för olika användningsområden.

>[!NOTE]
>
>I en aktiv implementering måste du använda datastyrningsetiketter när datauppsättningen har skapats. Mer information om hur du använder dataanvändningsetiketter på datauppsättningar finns i [Översikt över dataanvändningsetiketter](../../data-governance/labels/overview.md).

## Generera datauppsättningar med ett fördefinierat [!DNL Experience Data Model]-schema

Använd SQL-syntaxen för att generera en datauppsättning med ett fördefinierat [!DNL Experience Data Model]-schema (XDM). Mer information om syntaxen som stöds av [!DNL Query Service] finns i [SQL-syntaxguiden](../sql/syntax.md#create-table-as-select).

## Utdatauppsättningar

Datauppsättningar som skapas med den här funktionen genereras med ett ad hoc-schema som matchar strukturen för utdata enligt SQL-satsen. Vissa tjänster i senare led kräver datauppsättningar med särskilda XDM-scheman. Kontrollera dataformateringskraven för tjänster längre fram i kedjan innan du skriver frågorna.

## Nästa steg

När du har läst det här dokumentet bör du nu förstå hur du använder [!DNL Query Service] för att generera datauppsättningar från plattformsgränssnittet. Mer information om hur du får åtkomst till, skriver och kör frågor i plattformsgränssnittet finns i [[!DNL Query Service] användargränssnittsöversikt](./overview.md).
