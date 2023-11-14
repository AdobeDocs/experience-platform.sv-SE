---
solution: Experience Platform
title: Schemafältgrupp för information om segmentmedlemskap
description: Det här dokumentet innehåller en översikt över schemafältgruppen för segmentmedlemsdetaljer.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# [!UICONTROL Segment Membership Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Segment Membership Details] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Fältgruppen innehåller ett enda kartfält som samlar in information om segmentmedlemskap, inklusive vilka segment den enskilda personen tillhör, senaste kvalificeringstid och när medlemskapet är giltigt till.

>[!WARNING]
>
>Med `segmentMembership` fältet måste läggas till manuellt i profilschemat med den här fältgruppen. Du bör inte försöka fylla i eller uppdatera det här fältet manuellt. Systemet uppdaterar automatiskt `segmentMembership` mappning för varje profil när segmenteringsjobb utförs.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `segmentMembership` | Mappa | Ett kartobjekt som beskriver personens segmentmedlemskap. Objektets struktur beskrivs i detalj nedan. |

{style="table-layout:auto"}

Följande är ett exempel `segmentMembership` mappning som systemet har fyllt i för en viss profil. Segmentmedlemskap sorteras efter namnutrymme, vilket anges av objektets rotnivånycklar. De enskilda nycklarna under varje namnutrymme representerar i sin tur ID:n för de segment som profilen är medlem i. Varje segmentobjekt innehåller flera underfält med mer information om medlemskapet:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
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
| `xdm:version` | Den version av segmentet som den här profilen är kvalificerad för. |
| `xdm:lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `xdm:validUntil` | En tidsstämpel som anger när segmentmedlemskapet inte längre ska antas vara giltigt. Om det här fältet inte är inställt för externa målgrupper behålls segmentmedlemskapet endast i 30 dagar från `lastQualificationTime`. |
| `xdm:status` | Ett strängfält som anger om segmentmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`realized`: Profilen kvalificerar för segmentet.</li><li>`exited`: Profilen avslutar segmentet som en del av den aktuella begäran.</li></ul> |
| `xdm:payload` | Vissa segmentmedlemskap innehåller en nyttolast som beskriver ytterligare värden som är direkt relaterade till medlemskapet. Endast en nyttolast av en viss typ kan anges för varje medlemskap. `xdm:payloadType` anger typ av nyttolast (`boolean`, `number`, `propensity`, eller `string`), medan dess jämställda egenskap tillhandahåller värdet för nyttolasttypen. |

{style="table-layout:auto"}

>[!NOTE]
>
>Alla segmentmedlemskap som finns i `exited` status i mer än 30 dagar, baserat på `lastQualificationTime`, kan tas bort.

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
