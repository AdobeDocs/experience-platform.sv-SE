---
title: Filtrera svar i reaktors-API
description: Lär dig hur du filtrerar resultat när du visar resurser i Reactor API.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# Filtrera svar i reaktors-API

När du använder listslutpunkter (GET) i Reaktors-API:t kan det vara nödvändigt att begränsa de returnerade resultaten till en delmängd av poster. För att uppnå detta har många av API:ns listslutpunkter stöd för möjligheten att filtrera efter specifika attribut. Om du vill göra strukturerade frågor till API:t i stället, se guiden [söka](./search.md).

## Filtreringssyntax

I följande exempel förklaras hur du implementerar filter för dina GETTER.

**API-format**

Om du vill filtrera svaret för en viss listslutpunkt måste du ange en `filter` frågeparametern i sökvägen för begäran.

>[!NOTE]
>
>I mallen nedan används hakparentes (`[]`) och blankstegstecken för läsbarhet. I praktiken måste de här tecknen vara URI-kodade enligt instruktionerna i [RFC 3986](https://tools.ietf.org/html/rfc3986). Ett exempel på en korrekt kodad sökväg visas senare i den här handboken.
>
>Observera att om filterstrukturen är felaktig tillämpas inga filter och den fullständiga resultatmängden returneras.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Egenskap | Beskrivning |
| --- | --- |
| `{ENDPOINT}` | En listslutpunkt i Reactor API som stöder filterparametrar. |
| `{ATTRIBUTE_NAME}` | Namnet på ett specifikt attribut att filtrera resultat efter. Tänk på att olika slutpunkter har stöd för olika attribut för filtrering. I referenshandboken för slutpunkten som du arbetar med finns en lista med tillgängliga filterattribut. |
| `{OPERATOR}` | Operatorn som bestämmer hur resultaten utvärderas mot den angivna `{VALUE}`. Operatorer som stöds listas i [appendix-avsnitt](#supported-operators). |
| `{VALUE}` | Värdet som returnerade resultat ska jämföras med. Vid jämförelse av likhet med `EQ` måste värdet vara en exakt, skiftlägeskänslig matchning för att kunna inkluderas i svaret. |

{style="table-layout:auto"}

**Begäran**

Exempelbegäran nedan hämtar en lista med publicerade bibliotek genom att använda ett filter som kräver bibliotekets `state` attribute to equal `published`.

Före URI-kodning skulle syntaxen för det här filtret i sökvägen för begäran se ut ungefär så här:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

När sökväg- och frågeparametrarna har URI-kodats kan de användas i API-begäranden som den nedan:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## Filtrera på flera värden {#multiple-values}

Om du vill filtrera efter flera värden för ett enskilt attribut anger du värdena som en kommaavgränsad lista.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Använda flera filter

Om du vill använda filter för flera attribut anger du en `filter` parameter för varje attribut. Parametrar måste avgränsas med et-tecken (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Om du anger samma attribut i flera filter på samma begäran tillämpas bara det senast angivna filtret för det attributet.

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med filter i Reaktors-API:t.

### Filteroperatorer som stöds {#operators}

I följande tabell visas vilka operatorvärden som stöds för filterparametrar. Tänk på att beroende på vilket attribut du filtrerar efter kommer inte alla tillgängliga filteroperatorer att användas, till exempel operatorerna &quot;mindre än&quot; och &quot;större än&quot; för strängattribut.

| Operatör | Beskrivning |
| --- | --- |
| `EQ` | Attributet måste vara lika med det angivna värdet. |
| `NOT` | Attributet får inte vara lika med det angivna värdet. |
| `LT` | Attributet måste vara mindre än det angivna värdet. |
| `GT` | Attributet måste vara större än det angivna värdet. |
| `BETWEEN` | Attributet måste ligga inom ett angivet värdeintervall. När du använder den här operatorn [två värden](#multiple-values) måste anges för att ange minimi- och maximivärden för det önskade intervallet. |
| `CONTAINS` | Attributet måste innehålla det angivna värdet, till exempel en teckenuppsättning i ett strängattribut. |
