---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: Blandning av profilsegmentering
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# [!UICONTROL Profile segmentation] blanda

[!UICONTROL Profile segmentation] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Kombinationen innehåller ett enda kartfält som samlar in information om segmentmedlemskap, inklusive vilka segment personen tillhör, senaste kvalificeringstid och när medlemskapet gäller till.

>[!WARNING]
>
>Även om `segmentMembership` fältet måste läggas till manuellt i ditt profilschema med den här blandningen bör du inte försöka fylla i eller uppdatera det här fältet manuellt. Systemet uppdaterar automatiskt kartan `segmentMembership` för varje profil när segmenteringsjobb utförs.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `segmentMembership` | Mappa | Ett kartobjekt som beskriver personens segmentmedlemskap. Objektets struktur beskrivs närmare nedan. |

Följande är ett exempel på en `segmentMembership` karta som systemet har fyllt i för en viss profil. Segmentmedlemskap sorteras efter namnutrymme, vilket anges av objektets rotnivånycklar. De enskilda nycklarna under varje namnutrymme representerar i sin tur ID:n för de segment som profilen är medlem i. Varje segmentobjekt innehåller flera underfält med mer information om medlemskapet:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:version` | Den version av segmentet som profilen är kvalificerad för. |
| `xdm:lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `xdm:validUntil` | En tidsstämpel som anger när segmentmedlemskapet inte längre ska antas vara giltigt. |
| `xdm:status` | Anger om segmentmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`existing`: Profilen var redan en del av segmentet innan begäran gjordes och fortsätter att behålla medlemskapet.</li><li>`realized`: Profilen går in i segmentet som en del av den aktuella begäran.</li><li>`exited`: Profilen avslutar segmentet som en del av den aktuella begäran.</li></ul> |
| `xdm:payload` | Vissa segmentmedlemskap innehåller en nyttolast som beskriver ytterligare värden som är direkt relaterade till medlemskapet. Endast en nyttolast av en viss typ kan anges för varje medlemskap. `xdm:payloadType` anger nyttolastens typ (`boolean`, `number`, `propensity`eller `string`), medan dess jämställda egenskap anger värdet för nyttolasttypen. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
