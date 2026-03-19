---
description: Experience Platform Destination SDK använder mallar för att konvertera data som exporteras från Experience Platform till det format som krävs för målplatsen.
title: Omformningsfunktioner som stöds i Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Omformningsfunktioner som stöds i Destination SDK

Experience Platform Destination SDK använder [[!DNL Pebble] mallar](https://pebbletemplates.io/), vilket gör att du kan omvandla data som exporteras från Experience Platform till det format som krävs för målplatsen.

Implementeringen av Experience Platform [!DNL Pebble] har vissa ändringar jämfört med den körklara versionen som tillhandahålls av [!DNL Pebble]. Utöver de färdiga funktionerna som tillhandahålls av [!DNL Pebble] har Adobe även skapat ytterligare funktioner som du kan använda med Destination SDK.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Används {#where-to-use}

Använd de funktioner som stöds nedan på den här sidan när du [skapar en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md) för data som exporteras från Experience Platform till ditt mål.

Meddelandetransformeringsmallen används i [målserverkonfigurationen](templating-specs.md) för direktuppspelningsmål.

## Förutsättningar {#prerequisites}

Om du vill förstå begreppen och funktionerna på den här referenssidan läser du först dokumentet [meddelandeformat](message-format.md). Du måste förstå [strukturen för en profil](message-format.md#profile-structure) i Experience Platform innan du kan använda [!DNL Pebble]-mallar för att omforma exporterade data.

Innan du går vidare till de funktioner som beskrivs nedan bör du granska mallexemplen i avsnittet [Använda ett mallspråk för identitet, attribut och konverteringar av målgruppsmedlemskap](message-format.md#using-templating). Exemplen där börjar mycket enkelt och blir mer komplicerade.

## [!DNL Pebble] funktioner som stöds {#supported-functions}

I taggavsnittet [!DNL Pebble] stöder Destination SDK endast:

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [om](https://pebbletemplates.io/wiki/tag/if/)
* [uppsättning](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Användningen av `for` skiljer sig åt när du itererar genom elementen *array* eller *map* i en mall. När du itererar genom en array kan du hämta elementet direkt. När du itererar genom en karta får du varje mappningspost, som har ett nyckelvärdepar.
>
> * Ett exempel på ett arrayelement kan vara om du tänker på identiteterna i ett [identityMap](message-format.md#identities) -namnutrymme, där du kan iterera genom element som `identityMap.gaid`, `identityMap.email` eller liknande.
> * Ett exempel på ett kartelement kan vara [segmentMembership](message-format.md#segment-membership).

I filteravsnittet [!DNL Pebble] stöder Destination SDK alla funktioner. Ett exempel nedan visar hur funktionen `date` kan användas i Destination SDK.

I avsnittet [!DNL Pebble]-funktioner har Adobe *inte* stöd för funktionen [range](https://pebbletemplates.io/wiki/function/range/) .

## Exempel på hur funktionen `date` används {#date-function}

Om du vill se exempel på hur [!DNL Pebble]-funktioner används i Destination SDK kan du läsa nedan om hur datumfunktionen ([link in Pebble documentation](https://pebbletemplates.io/wiki/filter/date/)) används för att omforma formatet för en tidsstämpel.

### Användningsfall {#date-use-case}

Du vill ändra tidsstämpeln `lastQualificationTime` från standardvärdet för [ ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) som Experience Platform exporterar till ett annat värde som du föredrar.

### Exempel {#date-example}

#### Indata {#date-input}

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Format {#date-format}

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Utdata {#date-output}

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funktioner som lagts till av Adobe {#functions-added-by-adobe}

Förutom de användningsklara funktionerna från [!DNL Pebble], se nedan de extrafunktioner som skapas av Adobe och som du kan använda för dataexporter.

### Funktionerna `addedSegments` och `removedSegments` {#addedsegments-removedsegments-functions}

#### Användningsfall {#segments-use-case}

Dessa funktioner kan användas för att få en lista över målgrupper som har lagts till eller tagits bort från en profil.

#### Exempel {#segments-example}

##### Indata {#segments-input}

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

##### Format {#segments-format}

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Utdata {#segments-output}

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

Du vet nu vilka [!DNL Pebble]-funktioner som stöds i Destination SDK och hur du använder dem för att justera formatet för exporterade data efter dina behov. Därefter ska du granska följande sidor:

* [Skapa och testa en meddelandeomformningsmall](../../testing-api/streaming-destinations/create-template.md)
* [API-åtgärder för återgivningsmall](../../testing-api/streaming-destinations/render-template-api.md)
