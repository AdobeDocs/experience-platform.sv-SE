---
title: Fuzzy Match in Query Service
description: Lär dig hur du utför en matchning av plattformsdata som kombinerar resultat från flera datauppsättningar genom att i princip matcha en valfri sträng.
source-git-commit: a3a4ca4179610348eba73cf1239861265d2bf887
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---

# Fuzzy match

Använd en &#39;luddig&#39; matchning på plattformsdata för att returnera de mest troliga, ungefärliga matchningarna utan att behöva söka efter strängar med identiska tecken. Detta gör att du kan söka efter data på ett mycket flexiblare sätt och gör dina data mer tillgängliga genom att spara tid och arbete.

I stället för att försöka formatera om söksträngarna för att matcha dem analyserar den oskarpa matchningen förhållandet mellan två sekvenser och returnerar procentandelen likhet. [!DNL FuzzyWuzzy] rekommenderas för den här processen eftersom dess funktioner passar bättre för att matcha strängar i mer komplexa situationer jämfört med [!DNL regex] eller [!DNL difflib].

Exemplet i det här fallet fokuserar på matchning av liknande attribut från en hotellrumssökning mellan två olika data från resebyråer. Dokumentet visar hur strängar ska matchas genom deras likhet från stora separata datakällor. I det här exemplet jämförs sökresultaten med ett rum från resebyråerna Luma och Acme.

## Komma igång {#getting-started}

Som en del av den här processen kräver att du utbildar en maskininlärningsmodell, vilket krävs i det här dokumentet för att du ska kunna lära dig en eller flera maskininlärningsmiljöer.

Det här exemplet använder [!DNL Python] och [!DNL Jupyter Notebook] utvecklingsmiljö. Det finns många alternativ, men [!DNL Jupyter Notebook] rekommenderas eftersom det är ett webbprogram med öppen källkod som har låga datorkrav. Det kan vara [hämtat från den officiella Jupyter-webbplatsen](https://jupyter.org/).

Innan du börjar måste du importera de nödvändiga biblioteken. [!DNL FuzzyWuzzy] är en öppen källkod [!DNL Python] bibliotek som är byggt ovanpå [!DNL difflib] bibliotek och används för att matcha strängar. Den använder [!DNL Levenshtein Distance] för att beräkna skillnaderna mellan sekvenser och mönster. [!DNL FuzzyWuzzy] har följande krav:

- [!DNL Python] 2.4 (eller senare)
- [!DNL Python-Levenshtein]

Använd följande kommando från kommandoraden för att installera [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Eller använd följande kommando för att installera [!DNL Python-Levenshtein] samt

```console
pip install fuzzywuzzy[speedup]
```

Mer teknisk information om [!DNL Fuzzywuzzy] finns i deras [officiell dokumentation](https://pypi.org/project/fuzzywuzzy/).

### Anslut till frågetjänst

Du måste ansluta din maskininlärningsmodell till frågetjänsten genom att ange dina anslutningsreferenser. Du kan ange både utgångsdatum och icke-utgångsdatum. Se [inloggningsguide](../ui/credentials.md) om du vill ha mer information om hur du hämtar nödvändiga inloggningsuppgifter. Om du använder [!DNL Jupyter Notebook], se hela guiden för [hur du ansluter till frågetjänsten](../clients/jupyter-notebook.md).

Se även till att importera [!DNL numpy] i [!DNL Python] miljö för linjär algebra.

```python
import numpy as np
```

Nedanstående kommandon krävs för att ansluta till frågetjänsten från [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Dina [!DNL Jupyter Notebook] -instansen är nu ansluten till frågetjänsten. Om anslutningen lyckas visas inget meddelande. Om anslutningen misslyckas visas ett fel.

### Rita data från Luma-datauppsättningen {#luma-dataset}

Analysdata hämtas från den första datauppsättningen med följande kommandon. I korthet har exemplen begränsats till de första 10 resultaten i kolumnen.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Välj **Utdata** för att visa den returnerade arrayen.

+++Utdata

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Rita data från Acme-datauppsättningen {#acme-dataset}

Analysdata hämtas nu från den andra datauppsättningen med följande kommandon. Som en fortsättning har exemplen begränsats till de första 10 resultaten i kolumnen.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Välj **Utdata** för att visa den returnerade arrayen.

+++Utdata

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Skapa en otydlig poängfunktion {#fuzzy-scoring}

Sedan måste du importera `fuzz` från FuzzyWuzzy-biblioteket och utför en partiell jämförelse av strängarna. Med funktionen för partiell proportion kan du utföra delsträngsmatchning. Detta tar den kortaste strängen och matchar den med alla delsträngar som har samma längd. Funktionen returnerar ett procentvärde för likhet på upp till 100 %. Funktionen för partiella proportioner skulle till exempel jämföra följande strängar &#39;Deluxe Room&#39;, &#39;1 King Bed&#39; och &#39;Deluxe King Room&#39; och returnera en likhetspoäng på 69 %.

I hotell-rummet används följande kommandon:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Nästa, importera `cdist` från [!DNL SciPy] bibliotek för att beräkna avståndet mellan varje par i de två indatamängderna. Detta beräknar poängen för alla par hotellrum som tillhandahålls av var och en av resebyråerna.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Skapa mappningar mellan de två kolumnerna med hjälp av det oskarpa hörnet

Nu när kolumnerna har bedömts utifrån avstånd kan du indexera paren och bara behålla matchningar som har poängsatts högre än en viss procentandel. I det här exemplet behålls endast par som matchar med en poäng på 70 % eller högre.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Resultatet kan visas med följande kommando. Resultatet är begränsat till tio rader.

```python
matched_pairs[:10]
```

Välj **Utdata** för att se resultaten.

+++Utdata

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

Resultatet matchas sedan med SQL med följande kommando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Använda mappningarna för att göra oskarp koppling i frågetjänsten {#mappings-for-query-service}

Därefter förenas matchningspar med hög poäng med hjälp av SQL för att skapa en ny datauppsättning.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Välj **Utdata** om du vill se resultatet av det här sammanfogningen.

+++Utdata

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Spara oskarpa matchningsresultat till plattformen {#save-to-platform}

Slutligen kan resultatet av den oskarpa matchningen sparas som en datauppsättning som kan användas i Adobe Experience Platform med hjälp av SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```


