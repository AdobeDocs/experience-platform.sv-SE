---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datauppsättningar jämfört med tabeller och scheman
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# Datauppsättningar jämfört med tabeller och scheman

Granska listan över tillgängliga datauppsättningar i användargränssnittet [för](https://platform.adobe.com/datasets)Adobe Experience Platform och observera datauppsättningsnamnen.
>[!NOTE]
>
>Vissa datauppsättningsnamn har blanksteg och kan i annat fall vara SQL-säkra.

![](../images/queries/datasets-and-tables/dataset-names.png)


Granska dataschemats hierarkiska struktur i användargränssnittet genom att klicka på ett schemanamn i datamängdstabellen.

![](../images/queries/datasets-and-tables/schema-information.png)

Öppna PSQL-kommandoraden och använd anslutningsinformationen här: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Om du vill visa de tillgängliga tabellerna i [!DNL Platform] med SQL kan du antingen använda `\d` eller `SHOW TABLES;`.


`\d` visar PostgreSQL-standardvyn

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` är ett anpassat kommando som ger en mer detaljerad vy och visar tabellen samt namnet på datauppsättningen i [!DNL Platform] användargränssnittet.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Om du vill visa rotschemat för en tabell använder du `\d table_name` kommandot.

>[!NOTE]
>
>I det angivna schemat visas rotfälten, som i de flesta fall är komplexa, och som refereras till en objekttyp i dataschemats användargränssnitt.

`\d luma_midvalues`

```
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

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
