---
keywords: Experience Platform;home;popular topics;query service;Query service;datasets;tables;schemas;
solution: Experience Platform
title: Datauppsättningar jämfört med tabeller och scheman
topic: queries
type: Tutorial
description: Det här dokumentet innehåller information om hur du visar datauppsättningar i datasetens schemastruktur och använder PostgreSQL-kommandon.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 1%

---


# Datauppsättningar jämfört med tabeller och scheman

Granska listan över tillgängliga datauppsättningar i [Adobe Experience Platform-gränssnittet](https://platform.adobe.com/datasets)och observera datauppsättningsnamnen.
>[!NOTE]
>
>Vissa datauppsättningsnamn har blanksteg och kan annars vara SQL-säkra.

![](../images/queries/datasets-and-tables/dataset-names.png)


Granska dataschemats hierarkiska struktur i användargränssnittet genom att klicka på ett schemanamn i datamängdstabellen.

![](../images/queries/datasets-and-tables/schema-information.png)

Öppna PSQL-kommandoraden och använd anslutningsinformationen här: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Om du vill visa de tillgängliga tabellerna i [!DNL Platform] med SQL kan du antingen använda `\d` eller `SHOW TABLES;`.


`\d` visar PostgreSQL-standardvyn

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` är ett anpassat kommando som ger en mer detaljerad vy och visar tabellen samt namnet på datauppsättningen i [!DNL Platform] användargränssnittet.

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Om du vill visa rotschemat för en tabell använder du `\d table_name` kommandot.

>[!NOTE]
>
>I schemat visas rotfälten, som oftast är komplexa, som refereras till en objekttyp i dataschemats användargränssnitt.

`\d luma_midvalues`

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Om du vill gå längre in i schemat använder du understreck (`_`) för att deklarera kolumnen i tabellen som du vill beskriva. Exempel: `\d table_name_column`

`\d luma_midvalues_web`

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
