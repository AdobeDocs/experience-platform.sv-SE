---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visa resurser
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---


# Visa resurser

Du kan visa en lista över alla resurser i schemaregistret av en viss typ (klasser, mixins, scheman, datatyper eller beskrivningar) i en behållare genom att utföra en GET-begäran.

>[!NOTE]
>
>När resurser listas begränsas resultatmängden till 300 objekt. Om du vill returnera resurser som överskrider den här gränsen måste du använda [sidindelningsparametrar](#paging). Vi rekommenderar också att du använder frågeparametrar för att [filtrera resultaten](#filtering) och minska antalet returnerade resurser.

**API-format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren där resurserna finns (&quot;global&quot; eller&quot;tenant&quot;). |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska hämtas från schemabiblioteket. Giltiga typer är `classes`, `mixins`, `schemas`, `datatypes`och `descriptors`. |
| `{QUERY_PARAMS`} | Valfria frågeparametrar för att filtrera resultat efter. Mer information finns i avsnittet om [frågeparametrar](#query) . |

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på vilket Acceptera-huvud som skickas i begäran. Följande Accept headers är tillgängliga för att visa resurser:

| Acceptera rubrik | Beskrivning |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| application/vnd.adobe.xed+json | Returnerar det fullständiga JSON-schemat för varje resurs, med ursprungligt `$ref` och `allOf` inkluderat. (Gräns: 300) |
| application/vnd.adobe.xdm-v2+json | När du använder `/descriptors` slutpunkten måste du använda denna Accept-rubrik för att kunna använda sidindelningsfunktionerna. |

**Svar**

I begäran ovan användes rubriken `application/vnd.adobe.xed-id+json` Godkänn. Svaret innehåller därför bara attributen `title`, `$id`, `meta:altId`och `version` för varje resurs. Om du ersätter `full` rubriken Acceptera returneras alla attribut för varje resurs. Välj lämpligt sidhuvud för Acceptera beroende på vilken information du behöver i ditt svar.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Använda frågeparametrar {#query}

Schemaregistret har stöd för användning av frågeparametrar för att filtrera resultat och sidor när resurser listas.

>[!NOTE]
>
>När du kombinerar flera frågeparametrar måste de avgränsas med et-tecken (`&`).

### Sidindelning {#paging}

De vanligaste frågeparametrarna för sidindelning är:

| Parameter | Beskrivning |
| --- | --- |
| `start` | Ange var de listade resultaten ska börja. Det här värdet kan hämtas från attributet för ett listsvar och användas för att komma åt nästa resultatsida. `_page.next` Om `_page.next` värdet är null finns ingen ytterligare sida tillgänglig. |
| `limit` | Begränsa antalet returnerade resurser. Exempel: `limit=5` kommer att returnera en lista med fem resurser. |
| `orderby` | Sortera resultaten efter en specifik egenskap. Exempel: `orderby=title` sorterar resultaten efter rubrik i stigande ordning (A-Z). Om du lägger till en `-` före-rubrik (`orderby=-title`) sorteras objekt efter rubrik i fallande ordning (Z-A). |

### Filtrering {#filtering}

Du kan filtrera resultat med hjälp av `property` parametern, som används för att tillämpa en viss operator på en viss JSON-egenskap i de hämtade resurserna. Operatorer som stöds är:

| Operator | Beskrivning | Exempel |
| --- | --- | --- |
| `==` | Filtrerar efter om egenskapen är lika med det angivna värdet. | `property=title==test` |
| `!=` | Filtrerar efter om egenskapen inte är lika med det angivna värdet. | `property=title!=test` |
| `<` | Filtrerar efter om egenskapen är mindre än det angivna värdet. | `property=version<5` |
| `>` | Filtrerar efter om egenskapen är större än det angivna värdet. | `property=version>5` |
| `<=` | Filtrerar efter om egenskapen är mindre än eller lika med det angivna värdet. | `property=version<=5` |
| `>=` | Filtrerar efter om egenskapen är större än eller lika med det angivna värdet. | `property=version>=5` |
| `~` | Filtrerar efter om egenskapen matchar ett angivet reguljärt uttryck. | `property=title~test$` |
| (Ingen) | Om du bara anger egenskapsnamnet returneras bara poster där egenskapen finns. | `property=title` |

>[!TIP]
>
>Du kan använda parametern `property` för att filtrera blandningar efter deras kompatibla klass. Returnerar till exempel bara blandningar som är kompatibla med klassen XDM Individual Profile. `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`
