---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Generera datauppsättningar från frågeresultat
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Generera datauppsättningar från frågeresultat

Den verkliga styrkan hos Query Service visas när frågor används för att generera datauppsättningar i datasjön som kan användas som indata i fler frågor eller i andra tjänster som Data Science Workspace, Real-time Customer Profile eller Analysis Workspace.

Med frågetjänsten kan du skapa datauppsättningar från användargränssnittet. Följ de här stegen:

1. Skriv frågan med en ansluten klient och validera utdata.
2. Logga in på Platform användargränssnitt och gå till Frågor.
3. Leta reda på frågan i listan och hovra över raden.
4. Klicka på **Skapa datauppsättning**. ![Bild](../images/queries/create-datasets/click-create-dataset.png)
5. Ange ett datauppsättningsnamn som föregås av ditt LDAP-ID (behöver inte vara unikt eller SQL-säkert). systemet genererar ett&quot;tabellnamn&quot; baserat på det namn som anges här).
6. Ange en datauppsättningsbeskrivning och klicka på **Kör fråga**.![Bild](../images/queries/create-datasets/run-query.png)
7. Se frågan färdig och gå sedan till listsidan för datauppsättningar för att se den datauppsättning du just skapade.

När en datauppsättning har skapats kan den nås på samma sätt som andra datauppsättningar i datasjön och användas för olika användningsområden.

>[!NOTE]
>
>I en aktiv implementering måste du använda datastyrningsetiketter när datauppsättningen har skapats.

## Generera datauppsättningar med ett fördefinierat Experience Data Model-schema

Om du vill generera en datauppsättning med ett fördefinierat XDM-schema (Experience Data Model) måste du använda SQL-syntaxen. Mer information om vilken syntax du måste använda finns i [SQL Syntax Guide](../sql/syntax.md#create-table-as-select).

## Utdatauppsättningar

Datauppsättningar som skapas med den här funktionen genereras med ett ad hoc-schema som matchar strukturen för utdata enligt SQL-satsen. Vissa tjänster i senare led kräver datauppsättningar med särskilda XDM-scheman (Experience Data Model). Kontrollera dataformateringskraven för tjänster längre fram i kedjan innan du skriver frågorna.