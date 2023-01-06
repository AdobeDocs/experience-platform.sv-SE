---
keywords: Experience Platform;hem;mappare;mappningsuppsättning;mappning;
solution: Experience Platform
title: Översikt över mappningsuppsättningar
description: Lär dig hur du använder mappningsuppsättningar med Adobe Experience Platform Data Prep.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Översikt över mappningsuppsättningar

En mappningsuppsättning är en uppsättning mappningar som transformerar data från ett schema till ett annat. Det här dokumentet innehåller information om hur mappningsuppsättningar är sammansatta, inklusive indataram, utdataram och mappningar.

## Komma igång

Den här översikten kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataprep](./home.md): Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).
- [Dataflöden](../dataflows/home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras över olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar till [!DNL Identity] och [!DNL Profile]och till [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Metoderna som data kan skickas till [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.

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
| `sourceType` | För varje mappning i listan används `sourceType` -attribut anger vilken typ av källa som ska mappas. Kan vara en av `ATTRIBUTE`, `STATIC`, eller `EXPRESSION`: <ul><li> `ATTRIBUTE` används för alla värden som finns i källsökvägen. </li><li>`STATIC` används för värden som matas in i målsökvägen. Detta värde förblir konstant och påverkas inte av källschemat.</li><li> `EXPRESSION` används för ett uttryck som kommer att tolkas under körning. En lista med tillgängliga uttryck finns i [guide för mappningsfunktioner](./functions.md).</li> </ul> |
| `source` | För varje mappning i listan visas `source` -attribut anger det fält som du vill mappa. Mer information om hur du konfigurerar källan finns i [källsektion](#sources). |
| `destination` | För varje mappning i listan visas `destination` -attributet anger fältet eller sökvägen till fältet, där värdet som extraheras från `source` fältet placeras. Mer information om hur du konfigurerar dina mål finns i [målavsnitt](#destination). |
| `mappings.name` | (*Valfritt*) Ett namn för mappningen. |
| `mappings.description` | (*Valfritt*) En beskrivning av mappningen. |

## Konfigurera mappningskällor

I en mappning visas `source` kan vara ett fält, uttryck eller ett statiskt värde. Baserat på den angivna källtypen kan värdet extraheras på olika sätt.

### Fält i kolumndata

När du mappar ett fält i kolumndata, t.ex. en CSV-fil, använder du `ATTRIBUTE` källtyp. Om fältet innehåller `.` inom sitt namn, använd `\` för att undvika värdet. Ett exempel på den här mappningen finns nedan:

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

När du mappar ett fält i kapslade data, till exempel en JSON-fil, ska du använda `ATTRIBUTE` källtyp. Om fältet innehåller `.` inom sitt namn, använd `\` för att undvika värdet. Ett exempel på den här mappningen finns nedan:

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

När du mappar ett fält inom en array kan du hämta ett specifikt värde med hjälp av ett index. Om du vill göra det använder du `ATTRIBUTE` källtyp och index för det värde som du vill mappa. Ett exempel på den här mappningen finns nedan:

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

Använda `ATTRIBUTE` källtyp kan du också mappa en array direkt till en array eller ett objekt till ett objekt. Ett exempel på den här mappningen finns nedan:

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

Använda `ATTRIBUTE` källtyp kan du iterativt slinga igenom arrayer och mappa dem till ett målschema med hjälp av ett jokertecken (`[*]`). Ett exempel på den här mappningen finns nedan:

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

Om du vill mappa en konstant, eller ett statiskt värde, använder du `STATIC` källtyp.  När du använder `STATIC` källtyp, `source` representerar det hårdkodade värdet som du vill tilldela `destination`. Ett exempel på den här mappningen finns nedan:

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

Om du vill mappa ett uttryck använder du `EXPRESSION` källtyp. En lista över godkända funktioner finns i [guide för mappningsfunktioner](./functions.md). När du använder `EXPRESSION` källtyp, `source` representerar den funktion som du vill matcha. Ett exempel på den här mappningen finns nedan:

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

I en mappning visas `destination` är platsen där värdet extraheras från `source` infogas.

### Fält på rotnivå

När du vill mappa `source` till rotnivån för dina omformade data, följ exemplet nedan:

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

När du vill mappa `source` till ett kapslat fält i dina omformade data, följ exemplet nedan:

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

När du vill mappa `source` värde till ett specifikt index i en array i dina omformade data, följ exemplet nedan:

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

Genom att läsa det här dokumentet bör du nu förstå hur mappningsuppsättningar är uppbyggda, inklusive hur du konfigurerar enskilda mappningar i en mappningsuppsättning. Mer information om andra dataförberedelsefunktioner finns i [Översikt över datapreflight](./home.md). Läs mer om hur du använder mappningsuppsättningar i API:t för dataförberedelser i [Utvecklarhandbok för dataprep](./api/overview.md).
