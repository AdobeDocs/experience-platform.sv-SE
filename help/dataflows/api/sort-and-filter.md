---
title: Sorterings- och filtreringssvar i API:t för Flow Service
description: Den här självstudiekursen beskriver syntaxen för sortering och filtrering med hjälp av frågeparametrar i API:t för Flow Service, inklusive vissa avancerade användningsfall.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Sortera och filtrera svar i API:t för Flow Service

När du utför listförfrågningar (GET) i [API:t för flödestjänst](https://www.adobe.io/experience-platform-apis/references/flow-service/) kan du använda frågeparametrar för att sortera och filtrera svar. Den här handboken innehåller en referens för hur du använder de här parametrarna för olika användningsområden.

## Sortering

Du kan sortera svar med en `orderby`-frågeparameter. Följande resurser kan sorteras i API:

* [Anslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Källanslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Målanslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flöden](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Körningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Om du vill använda parametern måste du ange dess värde till den specifika egenskap som du vill sortera efter (till exempel `?orderby=name`). Du kan lägga till ett plustecken (`+`) som inledande ordning eller ett minustecken (`-`) för fallande ordning. Om inget ordningsprefix anges sorteras listan som standard i stigande ordning.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Du kan också kombinera en sorteringsparameter med en filterparameter genom att använda symbolen &quot;and&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtrering

Du kan filtrera svar genom att använda en `property`-parameter med ett nyckelvärdesuttryck. Till exempel returnerar `?property=id==12345` bara resurser vars `id`-egenskap är exakt `12345`.

Filtrering kan tillämpas generellt på alla egenskaper i en entitet så länge som den giltiga sökvägen till den egenskapen är känd.

>[!NOTE]
>
>Om en egenskap är kapslad i ett arrayobjekt måste du lägga till hakparenteser (`[]`) till arrayen i sökvägen. Se avsnittet [filtrering på arrayegenskaper](#arrays) för exempel.

**Returnera alla källanslutningar där källtabellens namn är  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Returnera alla flöden för ett specifikt segment-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Kombinera filter

Flera `property`-filter kan inkluderas i en fråga förutsatt att de avgränsas med&quot;och&quot;-tecken (`&`). En AND-relation antas när filter kombineras, vilket innebär att en enhet måste uppfylla alla filter för att den ska kunna inkluderas i svaret.

**Returnera alla aktiverade flöden för ett segment-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrera på arrayegenskaper {#arrays}

Du kan filtrera baserat på egenskaperna för objekt i arrayer genom att lägga till `[]` till arrayegenskapens namn.

**Returflöden som är associerade med specifika källanslutningar:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Returflöden som har en omformning som innehåller ett specifikt väljarvärde-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Returnera källanslutningar som har en kolumn med ett specifikt  `name` värde:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Söka efter flödeskörnings-ID för ett mål genom att filtrera på segment-ID:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Alla filtreringsfrågor kan läggas till med frågeparametern `count` med värdet `true` för att returnera antalet resultat. API-svaret innehåller en `count`-egenskap vars värde representerar antalet filtrerade objekt. De filtrerade objekten returneras inte i det här anropet.

**Returnera antalet aktiverade flöden i systemet:**

```http
GET /flows?property=state==enabled&count=true
```

Svaret på frågan ovan ser ut så här:

```json
{
  "count": 95
}
```

### Filterbara egenskaper efter resurs

Beroende på vilken Flow Service-enhet du hämtar kan olika egenskaper användas för filtrering. Tabellerna nedan delar upp rotnivåfälten för varje resurs som vanligtvis används vid filtrering.

**`connectionSpec`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`flow`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style=&quot;table-layout:auto&quot;}

**`run`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

I den här guiden beskrivs hur du använder frågeparametrarna `orderby` och `property` för att sortera och filtrera svar i API:t för Flow Service. Stegvisa guider om hur du använder API:t för vanliga arbetsflöden i Platform finns i API-självstudiekurserna i dokumentationen för [source](../../sources/home.md) och [mål](../../destinations/home.md).
