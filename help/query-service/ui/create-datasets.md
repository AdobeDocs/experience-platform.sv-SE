---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;generera datauppsättningar;generera datauppsättning;skapa datauppsättning;
solution: Experience Platform
title: Generera datauppsättningar från resultat i frågetjänsten
topic-legacy: queries
type: Tutorial
description: Med Adobe Experience Platform Query Service kan du skapa datauppsättningar från användargränssnittet. När en datauppsättning har skapats kan den nås som vilken annan datauppsättning som helst i datasjön och användas för en mängd olika användningsfall.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Generera datauppsättningar från resultat i frågetjänsten

Den verkliga kraften hos [!DNL Query Service] visas när frågor används för att generera datauppsättningar i [!DNL Data Lake] som används som indata i fler frågor eller i andra tjänster som [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], eller [!DNL Analysis Workspace].

[!DNL Query Service] gör det möjligt att skapa datauppsättningar från användargränssnittet. Följ de här stegen:

1. Skriv frågan med en ansluten klient och validera utdata.
2. Logga in på [!DNL Platform] Användargränssnitt och gå till Frågor.
3. Leta reda på frågan i listan och hovra över raden.
4. Välj **[!UICONTROL Create Dataset]**. ![Bild](../images/ui/create-datasets/output-dataset.png)
5. Ange ett datauppsättningsnamn som föregås av ditt LDAP-ID (behöver inte vara unikt eller SQL-säkert). systemet genererar ett&quot;tabellnamn&quot; baserat på det namn som anges här).
6. Ange en datauppsättningsbeskrivning och välj **[!UICONTROL Run Query]**.![Bild](../images/ui/create-datasets/run-query.png)
7. Se frågan färdig och gå sedan till listsidan för datauppsättningar för att se den datauppsättning du just skapade.

När en datauppsättning har skapats kan den nås på samma sätt som andra datauppsättningar i [!DNL Data Lake] och används för en mängd olika användningsområden.

>[!NOTE]
>
>I en aktiv implementering måste du använda datastyrningsetiketter när datauppsättningen har skapats.

## Generera datauppsättningar med en fördefinierad [!DNL Experience Data Model] schema

För att generera en datauppsättning med en fördefinierad [!DNL Experience Data Model] (XDM) måste du använda SQL-syntaxen. Mer information om vilken syntax du ska använda finns i [SQL Syntax Guide](../sql/syntax.md#create-table-as-select).

## Utdatauppsättningar

Datauppsättningar som skapas med den här funktionen genereras med ett ad hoc-schema som matchar strukturen för utdata enligt SQL-satsen. Vissa tjänster i senare led kräver datauppsättningar med särskild [!DNL Experience Data Model] (XDM) scheman. Kontrollera dataformateringskraven för tjänster längre fram i kedjan innan du skriver frågorna.
