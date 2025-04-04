---
title: Sorterings- och filtreringssvar i API:t för Flow Service
description: Den här självstudiekursen beskriver syntaxen för sortering och filtrering med hjälp av frågeparametrar i API:t för Flow Service, inklusive vissa avancerade användningsfall.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Sortera och filtrera svar i API:t för Flow Service

När du utför listförfrågningar (GET) i [Flow Service API](https://www.adobe.io/experience-platform-apis/references/flow-service/) kan du använda frågeparametrar för att sortera och filtrera svar. Den här handboken innehåller en referens för hur du använder de här parametrarna för olika användningsområden.

## Sortering

Du kan sortera svar med hjälp av en `orderby`-frågeparam. Följande resurser kan sorteras i API:

* [Anslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Source-anslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Målanslutningar](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flöden](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Kör](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Om du vill använda parametern måste du ange dess värde för den specifika egenskap som du vill sortera efter (till exempel `?orderby=name`). Du kan lägga till ett plustecken (`+`) för stigande ordning eller minustecken (`-`) för fallande ordning. Om inget ordningsprefix anges sorteras listan som standard i stigande ordning.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Du kan också kombinera en sorteringsparameter med en filterparameter genom att använda en&quot;och&quot;-symbol (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtrering

Du kan filtrera svar med en `property`-parameter med ett nyckelvärdesuttryck. `?property=id==12345` returnerar till exempel bara resurser vars `id`-egenskap är exakt `12345`.

Filtrering kan tillämpas generellt på alla egenskaper i en entitet så länge som den giltiga sökvägen till den egenskapen är känd.

>[!NOTE]
>
>Om en egenskap är kapslad i ett arrayobjekt måste du lägga till hakparenteser (`[]`) till arrayen i sökvägen. Se avsnittet [filtrera arrayegenskaper](#arrays) för exempel.

**Returnera alla källanslutningar där källtabellens namn är `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Returnera alla flöden för ett specifikt segment-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Kombinera filter

Flera `property` filter kan inkluderas i en fråga förutsatt att de avgränsas med&quot;och&quot;-tecken (`&`). En AND-relation antas när filter kombineras, vilket innebär att en enhet måste uppfylla alla filter för att den ska kunna inkluderas i svaret.

**Returnera alla aktiverade flöden för ett segment-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrera på arrayegenskaper {#arrays}

Du kan filtrera baserat på egenskaperna för objekt i arrayer genom att lägga till `[]` i arrayegenskapens namn.

**Returflöden som är associerade med specifika källanslutningar:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Returflöden som har en omformning som innehåller ett specifikt väljarvärde-ID:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Returnera källanslutningar som har en kolumn med ett specifikt `name`-värde:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Slå upp flödeskörnings-ID för ett mål genom att filtrera på segment-ID:**

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

{style="table-layout:auto"}

**`flowSpec`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

**`run`**

| Egenskap | Exempel |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

I det här avsnittet finns några specifika exempel på hur du kan använda filtrering och sortering för att returnera information om vissa anslutningar eller för att hjälpa dig med felsökningsfrågor. Om det finns fler användningsfall som du vill att Adobe ska lägga till använder du **[!UICONTROL Detailed feedback options]** på sidan för att skicka en begäran.

**Filtrera bara för att returnera anslutningar till ett visst mål**

Du kan bara använda filter för att returnera anslutningar till vissa mål. Fråga först `connectionSpecs`-slutpunkten enligt nedan:

```http
GET /connectionSpecs
```

Sök sedan efter önskad `connectionSpec` genom att undersöka parametern `name`. Du kan till exempel söka efter Amazon Ads, Pega eller SFTP och så vidare i parametern `name`. Motsvarande `id` är den `connectionSpec` som du kan söka efter i nästa API-anrop.

Du kan till exempel filtrera destinationerna så att endast befintliga anslutningar till Amazon S3-anslutningar returneras:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrera så att dataflöden endast returneras till mål**

När du skickar en fråga till slutpunkten `/flows` kan du, i stället för att returnera alla källor och destinationsdataflöden, använda ett filter för att endast returnera dataflöden till destinationer. Använd `isDestinationFlow` som frågeparameter så här:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filtrera bara för att returnera dataflöden till en viss källa eller mål**

Du kan filtrera dataflöden om du bara vill returnera dataflöden till ett visst mål eller från en viss källa. Du kan till exempel filtrera destinationerna så att endast befintliga anslutningar till Amazon S3-anslutningar returneras:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtrera för att hämta alla körningar av ett dataflöde för en viss tidsperiod**

Du kan filtrera dataflödeskörningar av ett dataflöde så att du bara tittar på körningar under ett visst tidsintervall, som nedan:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filter som endast returnerar felaktiga dataflöden**

I felsökningssyfte kan du filtrera och se alla misslyckade dataflöden för ett visst käll- eller måldataflöde, som nedan:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Nästa steg

I den här guiden beskrivs hur du använder frågeparametrarna `orderby` och `property` för att sortera och filtrera svar i API:t för Flow Service. Stegvisa guider om hur du använder API:t för vanliga arbetsflöden i Experience Platform finns i API-självstudiekurserna som finns i dokumentationen för [sources](../../sources/home.md) och [destination](../../destinations/home.md) .
