---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Skriver frågor
topic: queries
type: Tutorial
description: Det här dokumentet innehåller viktig information som du bör känna till när du skriver frågor i Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Allmän vägledning för frågekörning i [!DNL Query Service]

Det här dokumentet innehåller viktig information som du bör känna till när du skriver frågor i Adobe Experience Platform [!DNL Query Service].

Mer information om SQL-syntaxen som används i [!DNL Query Service]finns i [SQL-syntaxdokumentationen](../sql/syntax.md).

## Frågekörningsmodeller

Adobe Experience Platform [!DNL Query Service] har två modeller för frågekörning: interaktiva och icke-interaktiva. Interaktiv körning används för frågeutveckling och rapportgenerering i verktyg för affärsinformation, medan icke-interaktiv används för större jobb och operativa frågor som en del av ett arbetsflöde för databearbetning.

### Interaktiv frågekörning

Frågor kan utföras interaktivt genom att de skickas via [!DNL Query Service] användargränssnittet eller [via en ansluten klient](../clients/overview.md). När du kör [!DNL Query Service] via en ansluten klient körs en aktiv session mellan klienten och [!DNL Query Service] tills den skickade frågan returneras eller timeout inträffar.

Interaktiv frågekörning har följande begränsningar:

| Parameter | Begränsning |
| --------- | ---------- |
| Timeout för fråga | 30 minuter |
| Maximalt antal rader har returnerats | 50,000 |
| Maximalt antal samtidiga frågor | 5 |

>[!NOTE]
>
>Ta med `LIMIT 0` i frågan om du vill åsidosätta den maximala radbegränsningen. Frågetidsgränsen på 10 minuter gäller fortfarande.

Som standard returneras resultatet av interaktiva frågor till klienten och de bevaras **inte** . Om du vill behålla resultaten som en datauppsättning i [!DNL Experience Platform]måste frågan använda `CREATE TABLE AS SELECT` syntaxen.

### Icke-interaktiv frågekörning

Frågor som skickas via [!DNL Query Service] API körs icke-interaktivt. Icke-interaktiv körning innebär att [!DNL Query Service] tar emot API-anropet och kör frågan i den ordning den tas emot. Icke-interaktiva frågor leder alltid till att en ny datauppsättning skapas i [!DNL Experience Platform] för att ta emot resultaten, eller att nya rader infogas i en befintlig datauppsättning.

## Åtkomst till ett specifikt fält i ett objekt

Om du vill komma åt ett fält i ett objekt i frågan kan du antingen använda punktnotation (`.`) eller hakparenteser (`[]`). Följande SQL-sats använder punktnotation för att gå igenom `endUserIds` objektet ned till `mcid` objektet.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Namnet på analystabellen. |

Följande SQL-sats använder hakparenteser för att gå igenom `endUserIds` objektet ned till `mcid` objektet.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Namnet på analystabellen. |

>[!NOTE]
>
>Eftersom varje notationstyp returnerar samma resultat, beror det på vad du föredrar.

Båda exempelfrågorna ovan returnerar ett förenklat objekt i stället för ett enda värde:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Det returnerade `endUserIds._experience.mcid` objektet innehåller motsvarande värden för följande parametrar:

- `id`
- `namespace`
- `primary`

När kolumnen bara deklareras ned till objektet returneras hela objektet som en sträng. Om du bara vill visa ID:t använder du:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## När enkla citattecken, dubbla citattecken och bakåtcitattecken ska användas

I det här avsnittet beskrivs när enkla citattecken, dubbla citattecken och bakåtcitattecken ska användas i frågor.

### Enkla citattecken

Det enkla citattecknet (`'`) används för att skapa textsträngar. Den kan till exempel användas i programsatsen `SELECT` för att returnera ett statiskt textvärde i resultatet och i `WHERE` -satsen för att utvärdera innehållet i en kolumn.

Följande fråga deklarerar ett statiskt textvärde (`'datasetA'`) för en kolumn:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

I följande fråga används en sträng med bara citattecken (`'homepage'`) i WHERE-satsen för att returnera händelser för en viss sida.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Citattecken

Det dubbla citattecknet (`"`) används för att deklarera en identifierare med blanksteg.

I följande fråga används dubbla citattecken för att returnera värden från angivna kolumner när en kolumn innehåller ett blanksteg i sin identifierare:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Dubbla citattecken **kan inte** användas med åtkomst till punktnotationsfält.

### Bakåtcitat

Det bakre citattecknet `` ` `` används **bara** för att undvika reserverade kolumnnamn när punktnotationssyntax används. Eftersom `order` är ett reserverat ord i SQL måste du använda citattecken för att komma åt fältet `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Bakåtcitattecken används också för att komma åt ett fält som börjar med en siffra. Om du till exempel vill komma åt fältet `30_day_value`måste du använda citattecken.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Bakåtcitattecken behövs **inte** om du använder hakparenteser.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Nästa steg

När du läser det här dokumentet har du fått en del viktiga synpunkter när du skriver frågor med [!DNL Query Service]. Mer information om hur du använder SQL-syntaxen för att skriva egna frågor finns i [SQL-syntaxdokumentationen](../sql/syntax.md).