---
keywords: Experience Platform;hem;mappare;mappningsuppsättning;mappning;
solution: Experience Platform
title: Översikt över mappningsuppsättningar
description: Lär dig använda mappningsuppsättningar med Adobe Experience Platform Data Prep.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 660948b7a43ed3c18feb74cccf8f9c607470759c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Översikt över mappningsuppsättningar

En mappningsuppsättning är en uppsättning mappningar som transformerar data från ett schema till ett annat. Det här dokumentet innehåller information om hur mappningsuppsättningar är sammansatta, inklusive indataram, utdataram och mappningar.

## Komma igång

Den här översikten kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Data Prep](./home.md): Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).
- [Dataflöden](../dataflows/home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] samt till [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Metoderna som data kan skickas till [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

## Syntax för mappningsuppsättning

En mappningsuppsättning består av ett ID, ett namn, ett indatabchema, ett utdatabchema och en lista med associerade mappningar.

Följande JSON är ett exempel på en typisk mappningsuppsättning:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En unik identifierare för mappningsuppsättningen. |
| `name` | Mappningsuppsättningens namn. |
| `inputSchema` | XDM-schemat för inkommande data. |
| `outputSchema` | Det XDM-schema som indata har transformeras för att anpassas till. |
| `mappings` | En array med fält-till-fält-mappningar från källschemat till målschemat. |
| `sourceType` | För varje mappning i listan anger dess `sourceType`-attribut vilken typ av källa som ska mappas. Kan vara en av `ATTRIBUTE`, `STATIC` eller `EXPRESSION`: <ul><li> `ATTRIBUTE` används för alla värden som hittas i källsökvägen. </li><li>`STATIC` används för värden som matats in i målsökvägen. Detta värde förblir konstant och påverkas inte av källschemat.</li><li> `EXPRESSION` används för ett uttryck som kommer att matchas under körning. En lista med tillgängliga uttryck finns i [guiden för mappningsfunktioner](./functions.md).</li> </ul> |
| `source` | För varje mappning i listan anger attributet `source` vilket fält du vill mappa. Mer information om hur du konfigurerar källan finns i [Källöversikten](../sources/home.md). |
| `destination` | För varje mappning i listan anger attributet `destination` fältet, eller sökvägen till fältet, där värdet som extraherats från fältet `source` placeras. Mer information om hur du konfigurerar dina mål finns i [målöversikten](../destinations/home.md). |
| `mappings.name` | (*Valfritt*) Ett namn för mappningen. |
| `mappings.description` | (*Valfritt*) En beskrivning av mappningen. |

## Konfigurera mappningskällor

I en mappning kan `source` vara ett fält, uttryck eller ett statiskt värde. Baserat på den angivna källtypen kan värdet extraheras på olika sätt.

### Fält i kolumndata

Använd källtypen `ATTRIBUTE` när du mappar ett fält i kolumndata, t.ex. en CSV-fil. Om fältet innehåller `.` i namnet använder du `\` för att undvika värdet. Ett exempel på den här mappningen finns nedan:

**CSV-exempelfil:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Exempelmappning**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Fält i kapslade data

Använd källtypen `ATTRIBUTE` när du mappar ett fält i kapslade data, t.ex. en JSON-fil. Om fältet innehåller `.` i namnet använder du `\` för att undvika värdet. Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Fält i en array

När du mappar ett fält inom en array kan du hämta ett specifikt värde med hjälp av ett index. Det gör du genom att använda källtypen `ATTRIBUTE` och indexvärdet för det värde som du vill mappa. Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Array till array eller objekt till objekt

Med källtypen `ATTRIBUTE` kan du även mappa en array direkt till en array eller ett objekt till ett objekt. Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Iterativa åtgärder för arrayer

Med hjälp av källtypen `ATTRIBUTE` kan du iterativt slinga igenom arrayer och mappa dem till ett målschema med hjälp av ett jokertecken (`[*]`). Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Konstantvärde

Om du vill mappa en konstant, eller ett statiskt värde, använder du källtypen `STATIC`.  När du använder källtypen `STATIC` representerar `source` det hårdkodade värdet som du vill tilldela `destination`. Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exempelmappning**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Omformade data**

```json
{
    "userType:": "CUSTOMER"
}
```

### Uttryck

Om du vill mappa ett uttryck använder du källtypen `EXPRESSION`. En lista över godkända funktioner finns i [guiden för mappningsfunktioner](./functions.md). När du använder källtypen `EXPRESSION` representerar `source` funktionen som du vill matcha. Ett exempel på den här mappningen finns nedan:

**JSON-exempelfil**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Exempelmappning**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Omformade data**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Konfigurerar mappningsmål

I en mappning är `destination` platsen där värdet som extraherats från `source` infogas.

### Fält på rotnivå

När du vill mappa värdet `source` till rotnivån för dina omformade data följer du exemplet nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "name": "John Smith"
}
```

### Kapslat fält

När du vill mappa värdet `source` till ett kapslat fält i dina omformade data följer du exemplet nedan:

**JSON-exempelfil**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exempelmappning**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Fält vid ett specifikt arrayindex

När du vill mappa värdet `source` till ett specifikt index i en array i dina omformade data följer du exemplet nedan:

**JSON-exempelfil**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "piList": ["John Smith"]
}
```

### Interaktiv matrisåtgärd

När du iterativt vill göra en slinga genom arrayer och mappa värdena till målet, kan du använda ett jokertecken (`[*]`). Ett exempel på detta visas nedan:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exempelmappning**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Omformade data**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur mappningsuppsättningar är uppbyggda, inklusive hur du konfigurerar enskilda mappningar i en mappningsuppsättning. Mer information om andra dataförberedelsefunktioner finns i [översikten för dataförberedelser](./home.md). Läs [Utvecklarhandboken för dataprep](./api/overview.md) om du vill lära dig hur du använder mappningsuppsättningar i API:t för dataprep.
