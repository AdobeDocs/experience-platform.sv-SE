---
keywords: Experience Platform;hem;populära ämnen;dataförberedelse;api guide;scheman;
title: API-slutpunkt för funktioner
description: Du kan använda slutpunkten "/functions" i API:t för dataförberedelser för att validera mappningsuttrycken och visa tillgängliga mappningsuppsättningsfunktioner.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Funktionsslutpunkter

Med mappningsfunktionerna kan du omforma data mellan käll- och målscheman. Du kan använda `/languages/el` slutpunkt för att validera dina uttryck och få en lista över alla tillgängliga mappningsfunktioner.

## Validera uttryck

Du kan validera om det aktuella uttrycket är giltigt genom att göra en POST-förfrågan till `/languages/el/validate` slutpunkt.

**API-format**

```
POST /languages/el/validate
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med uttryckets valideringsstatus.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Funktioner för listmappningsuppsättning

Du kan hämta en lista över alla mappningsfunktioner som är tillgängliga genom att göra en GET-förfrågan till `/languages/el/functions` slutpunkt.

**API-format**

```
GET /languages/el/functions
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över alla tillgängliga mappningsfunktioner.

>[!NOTE]
>
>Svaret har trunkerats för utrymme.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Operatorer för listmappningsuppsättning

Du kan hämta en lista över alla mappningsoperatorer som är tillgängliga för dig genom att göra en GET-förfrågan till `/languages/el/operators` slutpunkt.

**API-format**

```
GET /languages/el/operators
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över alla tillgängliga mappningsoperatorer.

>[!NOTE]
>
>Svaret har trunkerats för utrymme.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
