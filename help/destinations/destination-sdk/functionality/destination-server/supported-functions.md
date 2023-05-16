---
description: I Experience Platform Destination SDK används mallar för att skapa bläddring, vilket gör att du kan omforma de data som exporteras från Experience Platform till det format som krävs för destinationen.
title: Omformningsfunktioner som stöds i Destinationen SDK
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---


# Omformningsfunktioner som stöds i Destinationen SDK

Experience Platform Destination SDK använder [[!DNL Pebble] mallar](https://pebbletemplates.io/)så att du kan omforma de data som exporteras från Experience Platform till det format som krävs för destinationen.

Experience Platform [!DNL Pebble] implementeringen har vissa ändringar jämfört med den färdiga versionen som tillhandahålls av [!DNL Pebble]. Förutom funktionerna som finns i [!DNL Pebble]har Adobe skapat ytterligare funktioner som du kan använda med Destination SDK.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Används {#where-to-use}

Använd funktionerna som stöds längre ned på den här sidan när [skapa en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md) för data som exporteras från Experience Platform till destinationen.

Meddelandetransformeringsmallen används i [målserverkonfiguration](templating-specs.md) för direktuppspelningsmål.

## Förutsättningar {#prerequisites}

Om du vill veta mer om begrepp och funktioner på den här referenssidan läser du [meddelandeformat](message-format.md) dokument först. Du måste förstå [struktur för en profil](message-format.md#profile-structure) i Experience Platform innan du kan använda [!DNL Pebble] -mallar för att omforma och exportera data.

Granska mallexemplen i avsnittet innan du går vidare till funktionerna som beskrivs nedan [Använda ett mallspråk för identitet, attribut och segmentmedlemskapsomvandlingar](message-format.md#using-templating). Exemplen där börjar mycket enkelt och blir mer komplicerade.

## Stöds [!DNL Pebble] funktioner {#supported-functions}

Från [!DNL Pebble] taggsektion, Destinationen SDK stöder endast:

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Använda `for` är annorlunda när du itererar igenom *array* eller *map* -element i en mall. När du itererar genom en array kan du hämta elementet direkt. När du itererar genom en karta får du varje mappningspost, som har ett nyckelvärdepar.
>
> * Ett exempel på ett arrayelement är om du tänker på identiteterna i ett [identityMap](message-format.md#identities) namnutrymme, där du kan iterera genom element som `identityMap.gaid`, `identityMap.email`eller liknande.
> * Ett exempel på ett kartelement kan vara att tänka på [segmentMembership](message-format.md#segment-membership).


Från [!DNL Pebble] filtersektion, Destination SDK stöder alla funktioner. Ett exempel nedan visar hur `date` -funktionen kan användas i Destinationen SDK.

Från [!DNL Pebble] funktionsavsnittet, Adobe gör *not* stöder [omfång](https://pebbletemplates.io/wiki/function/range/) funktion.

## Exempel på hur `date` funktionen används {#date-function}

Så här visar du hur [!DNL Pebble] funktioner som används i Destination SDK, se nedan hur datumfunktionen ([link in Pebble documentation](https://pebbletemplates.io/wiki/filter/date/)) används för att omforma formatet för en tidsstämpel.

### Användningsfall

Du vill ändra `lastQualificationTime` tidsstämpel från standard [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) det värde som Experience Platform exporterar till ett annat värde som du föredrar.

### Exempel

#### Indata

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Format

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Utdata

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funktioner som lagts till av Adobe {#functions-added-by-adobe}

Förutom funktionerna som finns i [!DNL Pebble]finns nedan de ytterligare funktioner som skapas av Adobe som du kan använda för dataexport.

### `addedSegments` och `removedSegments` funktioner {#addedsegments-removedsegments-functions}

#### Användningsfall

Dessa funktioner kan användas för att få en lista över segment som har lagts till eller tagits bort från en profil.

#### Exempel

##### Indata

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Utdata

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Nästa steg {#next-steps}

Du vet nu [!DNL Pebble] -funktioner stöds i Destination SDK och hur du använder dem för att justera formatet för exporterade data efter dina behov. Därefter ska du granska följande sidor:

* [Skapa och testa en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md)
* [API-åtgärder för återgivningsmall](../../testing-api/streaming-destinations/render-template-api.md)
