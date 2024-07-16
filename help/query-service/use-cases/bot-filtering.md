---
title: Rotfiltrering i frågetjänsten med maskininlärning
description: Det här dokumentet innehåller en översikt över hur du använder frågetjänst och maskininlärning för att fastställa robotaktivitet och filtrera deras åtgärder från äkta besökstrafik på webben.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# Bot-filtrering i [!DNL Query Service] med maskininlärning

Bitaktivitet kan påverka analysstatistik och skada dataintegriteten. Adobe Experience Platform [!DNL Query Service] kan användas för att upprätthålla din datakvalitet genom robotfiltrering.

Med punktfiltrering kan ni behålla er datakvalitet genom att i stort sett ta bort datakontaminering som är ett resultat av icke-mänsklig interaktion med er webbplats. Den här processen uppnås genom en kombination av SQL-frågor och maskininlärning.

Rotaktiviteten kan identifieras på flera olika sätt. Den metod som används i det här dokumentet fokuserar på aktivitetsökning, i det här fallet antalet åtgärder som en användare vidtagit under en viss tidsperiod. Till att börja med anger en SQL-fråga godtyckligt ett tröskelvärde för antalet åtgärder som har tagits under en tidsperiod för att kvalificera sig som båda aktiviteterna. Tröskelvärdet förfinas sedan dynamiskt med hjälp av en maskininlärningsmodell för att förbättra noggrannheten för dessa proportioner.

Det här dokumentet innehåller en översikt och detaljerade exempel på SQL Root-filtreringsfrågor och de maskininlärningsmodeller som behövs för att du ska kunna konfigurera processen i din miljö.

## Komma igång

Som en del av den här processen kräver att du utbildar en maskininlärningsmodell, vilket krävs i det här dokumentet för att du ska kunna lära dig en eller flera maskininlärningsmiljöer.

I det här exemplet används [!DNL Jupyter Notebook] som en utvecklingsmiljö. Det finns många alternativ, men [!DNL Jupyter Notebook] rekommenderas eftersom det är ett webbprogram med öppen källkod som har låga datorkrav. Den kan [hämtas från den officiella webbplatsen](https://jupyter.org/).

## Använd [!DNL Query Service] för att definiera ett tröskelvärde för robotaktivitet

De två attributen som används för att extrahera data för att identifiera robotar är:

* Experience Cloud Visitor ID (ECID, även kallat MCID): Detta ger ett universellt, beständigt ID som identifierar besökarna i alla Adobe-lösningar.
* Tidsstämpel: Här anges tid och datum i UTC-format när en aktivitet inträffade på webbplatsen.

>[!NOTE]
>
>Det går fortfarande att använda `mcid` i namnområdesreferenser till Experience Cloud Visitor-ID:t, vilket visas i exemplet nedan.

Följande SQL-sats ger ett inledande exempel för att identifiera robotaktivitet. Programsatsen förutsätter att om en besökare utför 50 klick inom en minut är användaren en robot.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

Uttrycket filtrerar ECID:n (`mcid`) för alla besökare som uppfyller tröskelvärdet, men som inte åtgärdar trafiktoppar från andra intervall.

## Förbättra robotidentifiering med maskininlärning

Den inledande SQL-satsen kan förfinas så att den blir en funktionsextraheringsfråga för maskininlärning. Den förbättrade frågan bör ge fler funktioner för olika intervaller för utbildning av maskininlärningsmodeller med hög precision.

Exemplet är expanderat från en minut med upp till 60 klick, och innehåller 5- och 30-minutersperioder med antalet klick på 300 respektive 1 800.

Exemplet samlar in det maximala antalet klick för varje ECID (`mcid`) under de olika varaktigheterna. Den inledande programsatsen har utökats så att den omfattar en minut (60 sekunder), 5 minuter (300 sekunder) och en timme (1 800 sekunder).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

Resultatet av det här uttrycket kan se ut ungefär som tabellen nedan.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identifiera nya tröskelvärden för spike med maskininlärning

Exportera sedan den resulterande frågedatauppsättningen till CSV-format och importera den sedan till [!DNL Jupyter Notebook]. Från den miljön kan du utbilda en maskininlärningsmodell med hjälp av aktuella maskininlärningsbibliotek. Se felsökningsguiden för mer information om [hur du exporterar data från [!DNL Query Service] i CSV-format](../troubleshooting-guide.md#export-csv)

De tillfälliga topptröskelvärden som ursprungligen fastställdes är inte datadrivna och saknar därför precision. Maskininlärningsmodeller kan användas för att utbilda parametrar som trösklar. Det innebär att du kan öka frågans effektivitet genom att minska antalet `GROUP BY`-nyckelord genom att ta bort onödiga funktioner.

I det här exemplet används datorutbildningsbiblioteket Scikit-Learn, som är installerat som standard med [!DNL Jupyter Notebook]. Pandafotobiblioteket importeras också för användning här. Följande kommandon matas in i [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Därefter måste du utbilda en klassificerare för beslutsträd i datauppsättningen och följa logiken som följer av modellen.

Biblioteket Matplotlib används för att visualisera klassificeraren för beslutsträdet i exemplet nedan.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

De värden som returneras från [!DNL Jupyter Notebook] för det här exemplet är följande.

```text
Model Accuracy: 0.99935
```

![Statistiska utdata från [!DNL Jupyter Notebook] maskininlärningsmodell.](../images/use-cases/jupiter-notebook-output.png)

Resultaten för modellen som visas i exemplet ovan är mer än 99 % exakta.

Eftersom klassificeraren för beslutsträd kan tränas med data från [!DNL Query Service] på ett regelbundet slut med hjälp av schemalagda frågor, kan du säkerställa dataintegriteten genom att filtrera robotaktiviteten med hög noggrannhet. Genom att använda de parametrar som härletts från maskininlärningsmodellen kan de ursprungliga frågorna uppdateras med de exakta parametrar som skapas av modellen.

Exemplmodellen avgör med stor noggrannhet att alla besökare som har mer än 130 interaktioner på fem minuter är upptagna. Den här informationen kan nu användas för att förfina robotfiltreringen av SQL-frågor.

## Nästa steg

Genom att läsa det här dokumentet får du en bättre förståelse för hur du använder [!DNL Query Service] och maskininlärning för att fastställa och filtrera startaktiviteten.

Andra dokument som demonstrerar fördelarna med [!DNL Query Service] för din organisations strategiska affärsinsikter är [det övergivna exemplet på bläddringsanvändning](./abandoned-browse.md).
